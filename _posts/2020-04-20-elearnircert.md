---
layout: posts
title: "Incident Handling Certification"
---

Since I blogged about my experience at OpenSoc I wanted to expand on the value I found in my eLearnSecuirty incident response course. What you will find below is a bit of a review of the course itself and the exam.

# What to expect:
A review based on my specific circumstances and the value I myself gained from the certification.

A serious alternative to training that is triple the cost.

# What course?
The course I signed up for was [Incident Handling & Response Professional](https://www.elearnsecurity.com/course/incident_handling_response_professional/)

It was released last year in January.

## Who is it by?
[elearnSecurity](https://www.elearnsecurity.com/company/about_us)
This company is based in Italy and the US as you can see in the about us section.
![](/images/ihrp/elearn4.png)
## Why Did I choose this course?
The security training space is very wide both in cost and quality.
You don't always get what you pay for. I am quite skeptical of training providers and associated costs. I work as security a manager with analyst/pentest responsibilities. So the training I needed had to be applicable to my day job.

I don't work at a company where security itself is a revenue generator, for example it does not do penetration testing as a consultancy. It is also not very large. These 2 things mean I have a certain sized training budget that will not cover premium well known (or should I say highly marketed) training providers.

So my criteria was:  
* Good quality training
* Not sink me into debt
* Tie into my job (hands-on exam)

After going through the course and exam I personally feel it met my 3 criteria superbly. This was mostly due to the fact that my day job for incident response is focused heavily in Splunk.


# What does the course cover?
The standard syllabus is here:
> Start from the very basics, all the way to advanced incident response activities
Professionally analyze, handle, and respond to security incidents on heterogeneous networks and assets
Understand the mechanics of modern cyber-attacks and how to detect them
Effectively use and fine-tune open source IDS (Bro, Snort, Suricata)
Make the best of open source SIEM solutions (ELK stack, Splunk, etc.)
Effectively utilize regexes and log management solutions to detect intrusions
Detect and even (proactively) hunt for intrusions by analyzing traffic, flows and endpoints, as well as utilizing analytics and tactical threat intelligence
Gives you access to dedicated forums
Makes you a proficient professional incident responder
After obtaining the eCIRv1 certification qualifies you for 40 CPE

# The Exam Format  
First off, the interest will probably be with the "What is the certification exam like" or "what do I get out of the exam"

I have done a practical hands on exam on offensive security and a multiple choice exam for offensive security. I learned, applied and retained much more in a practical exam.

The exam is all hands-on. There are zero multiple choice questions. It is scenario based (2) requiring not just technical knowledge of Splunk and ELK but understanding the business and its critical assets.


## What I learned from the course
This is NOT an exhaustive description

### Flowing through Splunk & Elk
By flowing, I mean the opposite of staring at a search bar in Splunk or ELK and going 'where do I even start'

Unfortunately there is a load of theory to cover to be able to do this. I found I am able to look through different logs and sources within the 2 platforms much more efficiently. I still have to google things now and again for exact syntax or something, but in general I 'understand' possible locations for where information related to an incident could be.

There is never a straight forward investigation to an attack. There is no answer like "machine dropped malware then moved to machine B". Especially when there is legitimate traffic flowing around. 

I have many notes now on ELK and Splunk queries to help me jump start an investigation.

As an example I have notes on LM/NTML
![notes](/images/ihrp/elearn2.png)

A Splunk search for pvileges that can be abused:  
![](/images/ihrp/elearn3.png)


#### Job Applicability
I imagine it would be beneficial if I went for a job related to a SOC or IR, being able to say I have a cheatsheet, or like a playbook guide to my investigations. This shows even though I may not do IR every day, I think about what I am doing, what works and what does not, instead of starting from scratch each time.

The benefit for me, is that it keeps my options open. I am still fine tuning my career and want to be able to change career paths.


### Hands on with a variety of tools
Full transparency, the exam does not cover the tools. The exam covers Splunk, ELK and PCAP analysis.

The labs do a fine job of getting you acquainted with the tools and providing varying levels of depth. Sometimes going beyond the tool.

The tools covered include:  
Incident Response Platforms
 * Velociraptor
 * GRR (Google Rapid Response)


IDS/IPS:
* Zeek/Bro
* Snort
* Suricata

SIEM Platforms:  
* Splunk
* ELK

#### IR platforms
These were good just to be able to understand the benefits of having a centralized platform for IR, including being able to pull information such as a list of files in a suspect directory.

I did not have to set these up myself, the labs had it all installed.


#### IPS/IDS
Not having to rely on one tool will be beneficial. Especially if consulting at different clients.

The value I found in here, was being able to evaluate the pros and cons of the tools. Such as skill required, effort to maintain or tune and or cost of deployment (purchase price, time & effort).

Obviously at a company, we use an IDS/IPS and it was beneficial to be able to make sure that at my job we could get the most out of the platform, such as tuning it a bit better or understanding its limitations better.

Because it is not my day to day role, I wrote a blog post based on some of the learning on zeek  [here](https://thehackerwhorolls.home.blog/2019/11/05/zeek-bro-cheat-sheet/). it is very short but will help me quickly be able to read a PCAP and or write a rule if needed.




#### Job Applicability
For someone junior, being exposed to the tools and having a go at writing your own rules would be invaluable.

For someone like myself, the value is also in being able to run the tool and tune rules, but also understanding how it gets deployed, the effort to maintain it, where the sensors should be. How to justify the value of the tool (via understanding what it does and what it does not do) to upper management.

### Attacker Methodology - From the Blue side


#### Job Applicability





# Quality / Size of the Theory
There is a lot. It is extremely important to learn and it is a lot. Try to drink from the fire hose and you will burn out.

Reading standard text is never fun, but critical. For example, if you don't know which windows event log and type shows a remote login, how will you know to search for it in Splunk? The answer is [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624) with a logon type 3 for Network.

Which is part of the cheat sheets I created:
![](/images/ihrp/elearn5.png)


For transparency: Yes there are some grammatical mistakes. The author is from Italy originally so it is understandable. His expertise is within IR not English "_"

