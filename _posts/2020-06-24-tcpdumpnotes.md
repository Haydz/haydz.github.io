---
layout: posts
title: "Tcpdump Notes"
---


I have been using tcpdump recently and wanted to note down some of the commands I have been using. For future reference.

# Cheat Sheet:
### To monitor certain ports:  
* In this case, monitoring for the existence of NETBIOS traffic

```bash
sudo tcpdump -n -i eth0 '(port 137 or 138 or 139)'
```

-n is to stop IP name resolution
-i is for the interface


### Record traffic looking for a specific host:

```bash
sudo tcpdump -i eth0 -n 'host 192.168.1.2 and (port 137 or 138 or 139)'
```

### To write to a file:
```bash
 sudo tcpdump -n -i eth0 ip6 -w ipv6.pcap
```
![](/images/tcpdump/image_1.png)


### To select hosts from a Pcap file:
```bash
 sudo tcpdump -n -r llmnr.pcap | cut -d " " -f3 | cut -d "." -f 1-4  | sort -u  
```

This assumes the ip and port are together such as:
```bash
192.168.2.1.80
```