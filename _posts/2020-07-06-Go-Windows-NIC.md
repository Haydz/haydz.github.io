---
layout: posts
title: "Golang and Windows Network Interfaces"
---

I have been working on Windows and needed to connect to a Network Interface (NIC). I ran into problems, here is what I learned and hope it saves the same trouble I had in troubleshooting.


TL;DR: Do not use friendly names (Ethernet/eth0) for Windows NICs.  Prepend `"\Device\NPF_` to the interface GUID found from `getmac`.


# Why Connect to a Windows NIC?
Creating TCP sockets or web sockets does not involve connecting to a network interface specifically. It involves listening or dialing with an IP address and a port. Such as:


{%highlight go linenos %}
	CONNECT := "192.168.1.1:9999"
	c, err := net.Dial("tcp", CONNECT)
	if err != nil {
		fmt.Println(err)
		return
	}

{% endhighlight %}


But if you wanted to use the [Gopacket](https://github.com/google/gopacket) package and create your own packets, or read packets from the network, connecting to a Windows NIC is needed. This is where some code connecting to a NIC is needed:

{%highlight go linenos %}
 device       string = "eth0"
 handle, err = pcap.OpenLive(device, snapshot_len, promiscuous, timeout)
{% endhighlight %}


A great breakdown of the gopacket package can be found [here](https://www.devdungeon.com/content/packet-capture-injection-and-analysis-gopacket)
It covers:  
* Finding devices
* Opening devices (Does not work on Windows, hence this post)
* Writing a Pcap File
* Reading and Writing packets
* and more
 
# The Issue with a Windows NIC
In Linux as shown above, the name `eth0` or equivalent can be used to connect to the NIC.
 
In short:
* The `ifconfig` output in Linux is also the name
    * This is not the case in Windows
![](/images/Win_NIC.png)
 
The `ipconfig` output on Windows is not the name to be used within Gopacket.

![](/images/WIN_NIC/image1.png)
 
 
If you add the Windows NIC name from that output, you will receive the following error:
* No such device exists

 ![](/images/WIN_NIC/image2.png)
 
This is a known issue:
* [net: get npcap usable windows network device names](https://github.com/golang/go/issues/35095#issuecomment-545528366> )
* [Gopacket/pcap and Windows Device Names](https://forum.golangbridge.org/t/soved-gopacket-pcap-and-windows-device-names/15856/2)
 
 
# Fixing the issue
Running `getmac` in the Windows command-line  will show the name that can be appended:
 
 ![](/images/WIN_NIC/image3.png)
 
So the full line would become:
 * `\\Device\\NPF_{6DXXX78X-2267-4XX9-938F-1243F92XXX64}`
    * X's for redaction
    * Double back slash for escaping in Go
    
    
In Go format it would look like:
{%highlight go linenos %}
var (
	device       string = "\\Device\\NPF_{6DXXX78X-2267-4XX9-938F-1243F92XXX64}"
	snapshot_len int32  = 1024
	promiscuous  bool   = false
	err          error
	timeout      time.Duration = 30 * time.Second
	handle       *pcap.Handle
	buffer       gopacket.SerializeBuffer
	// options      gopacket.SerializeOptions
)
{% endhighlight %}
    
Once  fixed the code should use the Windows NIC:

![](/images/WIN_NIC/image7.png)
![](/images/WIN_NIC/image8.png)


# Getting The Correct NIC Name in Go
Within Gopacket the `pcap.FindalDevs()` Will get the correct name.

So Go code such as the below, will print out the correct names needed:
{%highlight go linenos %}
package main

import (
	"fmt"
	"log"

	"github.com/google/gopacket/pcap"
)

func main() {
	// Find all devices
	devices, err := pcap.FindAllDevs()
	if err != nil {
		log.Fatal(err)
	}

	// Print device information
	fmt.Println(devices)
	fmt.Println("Devices found:")
	for _, device := range devices {
		fmt.Println("\nName: ", device.Name)
	}

}
{% endhighlight %}

![](/images/WIN_NIC/image4.png)

Adding `device.Description` and printing the IP address will help in better identification:

{%highlight go linenos %}

	fmt.Println("Devices found:")
	for _, device := range devices {
		fmt.Println("\nName: ", device.Name)
		fmt.Println("Description: ", device.Description)
		for _, address := range device.Addresses {
			fmt.Println("- IP address: ", address.IP)
		}
{% endhighlight %}


Where as using `net.Interfaces()` will get the 'friendly name'. This is NOT usable for connecting to a Windows NIC with gopacket.

Which will look like:

![](/images/WIN_NIC/image5.png)

{%highlight go linenos %}
func main() {

	infs, _ := net.Interfaces()
	for _, f := range infs {
		fmt.Println(f.Name)
	}
}
{% endhighlight %}

This will print the friendly names:
![](/images/WIN_NIC/image6.png)

 
# Reasoning For The Issue:
Reading the links that I had found had identified the issue and that a correct interface name was in the format of `\Device\NPF_{GUID}`

GUID stands for a globally unique identifier which is used by system drives and other components for identification.

`\Device\NPF_` is the device volume name. Windows uses its own underlying non-username, indicating the devices PCI bus address.
 
This [article](https://daveurrutiablog.wordpress.com/2016/05/03/tshark-network-interface-names-mystery-guid/) explains that the GUID can be found in the registry such as `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Network\{4D36E972-E325-11CE-BFC1-08002BE10318}`.
* Please note: Looking in my registry my interface GUIDs from `getmac` didn't match what was in the registry.
 
The article also explains that "NPF is a driver which stands for NetGroup Packet Filter Driver. It turns out NPF is a vital part of the Windows Packet Capture (WinPcap) process".

This helps explain why simply using `ipconfig` to grab a Windows NIC name will not work.

