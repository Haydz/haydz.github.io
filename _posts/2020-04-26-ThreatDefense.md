---
layout: posts
title: "Threat Defense Workshop"
---

On April 25th I was fortunate enough to participate in the Trend Micro Threat Defense workshop. 

You'll find a quick explanation of this event and some screenshots.

# What is a Threat Defense Workshop?

[Workshop](https://www.eventbrite.com/e/dc416-x-trend-micro-virtual-threat-defense-workshop-hybrid-cloud-edition-tickets-94851686949)
![](/images/threatdefense/image_9.png)

> At this workshop you will be working in teams with a scenario - a company is currently under attack. You are in charge of its protection. Live the adrenaline by defending the company from different attacks in real time whose objective is to steal the most important part of your business: Information. Be part of this experience and strengthen your security strategy, with the expert help. The aim is to win the Threat Defense Challenge, by gaining the most points through a series of discovery and attack challenges. Are you ready for the challenge?

The workshop had three phases based on hybrid data centre use cases:
* Forensic - to find out what happened – to discover/obtain information
* Defense – to define the protection strategy
* Proactive – to set the security needed to avoid being compromised again 

## Organized by whom?
The workshop was created by Trend Micro and organized in conjunction with the [DC416](https://dc416.com/) crew.

![](/images/threatdefense/image_10.png)


## How long was the event?
It was on a Saturday from 9am to 3:30pm.
6 and a half hours



# What was Involved

## Systems
The network was accessed via the cloud.  
  
Systems within the game:
* A Jump host to RDP into others
* Docker Host
* IIS Webserver
* Database Server (MySQL)

## Tools
This was a Trend Micro event, meaning it was all designed and created by their team. As such the only tool given was [Deep Security](https://www.trendmicro.com/en_us/business/products/hybrid-cloud/deep-security.html) 

Deep Security example:
![](/images/threatdefense/image_4.png)

However there were other tools that were required:
* John The Ripper
* OpenSSL
* Windows Event logs itself
* Command line - for both Linux and Windows

We did not finish all the challenges, so there was much more to explore.

## Challenges
Varied from basic to hard.

Basic examples:  
* what account is being brute forced
* What is the name of <xyz> malware on <xyz host>

To more thinking outside the box:  
* Need to find a password to open a file or gain access to something. Would you brute-force, or look on a server for the password?
* Enabling features within Deep Security tool to give more visibility, or fine tuning


Example finding malware:
![](/images/threatdefense/image_1.png)

Example using hexdump, which was NOT the way to solve the challenge:
![](/images/threatdefense/image_3.png)

Example viewing Windows events through Deep Security:
![](/images/threatdefense/image_5.png)



# What Did The Scoreboard Look Like?
This was a unique take on scoreboards.  
  
Instead of just having a ladder and challenges. The idea was that you were 'hacking around the world'. Each country had its own challenge. Obviously it started off in Canada!
![](/images/threatdefense/image_8.png)
![](/images/threatdefense/image_7.png)



Example Challenges:
![](/images/threatdefense/image_6.png)



# How Did We Place
5th! Which I feel is pretty awesome.
It was great to try a new tool and continue challenging myself.


![](/images/threatdefense/image_2.png)


