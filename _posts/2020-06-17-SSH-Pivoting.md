---
layout: posts
title: "Pivoting with SSH"
---

Today I was trouble shooting a machine at work. I did not have access via RDP or VNC, so I used SSH to forward my traffic to the host so I could access a URL.

This is to serve as a cheat sheet for what I did, in case I need to do it again.

Side Note:
* A handy trick for lateral movement / pentesting.


# Dynamically forwarding traffic via SSH
```bash
ssh -D 8080 user@192.x.x.x
```
This will dynamically forward any traffic through that host. Need to set a tool or browser for send traffic through local host on port 8080.

Key point: This will forward traffic through the host to any ip and port

Using Foxy Proxy:
* remember to set SOCKS5

![](/images/ssh_forwarding/ssh_1.png)



# Statically forwarding traffic via SSH
```bash
ssh   -L 127.0.0.1:8080:192.168.1.1:80 hacker@192.168.1.2
```
This will forward local port 8080 traffic to 192.168.1.1 port 80 VIA (goes through 192.168.1.2)



```bash
ssh  -L 127.0.0.1:8080:192.168.1.1:80 hacker@192.168.1.1
```
This will forward local port 8080 to the remote host and send the traffic to the remote hosts (192.168.1.1) port 80
