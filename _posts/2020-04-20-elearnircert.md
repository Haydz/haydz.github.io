---
layout: posts
title: "Incident Handling Certification"
---

Since I blogged about my experience at OpenSoc I wanted to expand on the value I found in my eLearnSecuirty Incident Response course. What you will find below is a bit of a review of the course itself and the exam.

This post not only is intended to help others identify other training options but also to serve as a refresh of content I learned.

# What to Expect:
A review based on my specific circumstances and the value I myself gained from the certification.

eLearnSecurity is a serious alternative to other training providers that can cost up to 3 times more.

Full Transparency:
* I had this reviewed by eLearnSecurity so that I didn't run into any copyright issues
* I also did not mean to write so much but I got into a 'flow'
* I plan on taking the web application penetration testing course to supplement my web app role in my day to day job

# What Course?
The course I signed up for was [Incident Handling & Response Professional](https://www.elearnsecurity.com/course/incident_handling_response_professional/). It was released last year in January.

## Who Is It By?
[eLearnSecurity](https://www.elearnsecurity.com/company/about_us)
This company is based in Italy and the US as you can see in the about us section.

![](/images/ihrp/elearn9.png)

## Why Did I Choose This Course?
The security training space is very wide, both in cost and quality.
You don't always get what you pay for. I'm quite skeptical of training providers, associated costs and 'certifications' in general. I'm certainly not an expert. I use certifications as a guideline for my learning path, not the end all be all.

I work as a security manager looking after the overall program, in addition to analyst/pentest responsibilities. So the training I needed had to be applicable to my day job.

I don't work at a company where security itself is a revenue generator nor at a company that is large. These 2 things mean I have a certain sized training budget that will not cover premium well known training providers.

So my criteria was:  
* Good quality training
* Not sink me into debt
* Tie into my job (hands-on exam)

After going through the course and exam I personally feel it met my 3 criteria superbly. This was mostly due to the fact that my day job for incident response is focused heavily in Splunk and the IHRP course covers this indepth.


# What Does The Course Cover?
The course at a glance section:
> Start from the very basics, all the way to advanced incident response activities

> Professionally analyze, handle, and respond to security incidents on heterogeneous networks and assets

> Understand the mechanics of modern cyber-attacks and how to detect them

> Effectively use and fine-tune open source IDS (Bro, Snort, Suricata)

> Make the best of open source SIEM solutions (ELK stack, Splunk, etc.)

> Effectively utilize regexes and log management solutions to detect intrusions``

> Detect and even (proactively) hunt for intrusions by analyzing traffic, flows and endpoints, as well as utilizing analytics and tactical threat intelligence

> Gives you access to dedicated forums

> Makes you a proficient professional incident responder

> After obtaining the eCIRv1 certification qualifies you for 40 CPE




# The Exam Format  
First off, the interest will probably be with the "What is the certification exam like" or "what do I get out of the exam".

I have done a practical hands on exam in offensive security and a multiple choice exam for offensive security. I learned, applied and retained much more in a practical exam setting.

The exam is all hands-on. There are zero multiple choice questions. It is scenario based (2) requiring not just technical knowledge of Splunk and ELK but understanding the business and its critical assets. There is a component of network traffic analysis to mix it up and give another way  to gain visibility on the attack.

The practical portion is 2 full days. This is the investigation portion.

There is also an additional 2 days for report writing. That is, take all the notes from the practical portion and reporting on the what the attacker 'did'. That could be anything from the Cyber Kill Chain, such as initial infection, moving to different systems, persistence and or something related to "acting on objectives". 

More can be read [Here](https://www.elearnsecurity.com/certification/ecir/)

## Difficulty of exam
Investigation is contextual, based on critical assets, initial infection and the network etc.

The exam is difficult in that identifying each technique used and each stage on the kill chain is not a point and click exercise, nor is it to the extreme difficulty where you need years of experience in the field. 

The exam for me at least seemed balanced between requiring most of the investigation techniques taught in the course and requiring use of the "process of investigation" taught in the course. By process of investigation I mean following the indicators that you have found instead of copy pasting pre-made queries (like my cheat sheet). In saying that, it did push me and my skills up a notch.

The exam also requires friendly intelligence such as understanding which host is owned by which user etc (skills that pentesters use as well).

Side note: The sources in the exam platforms are not the same as in the lab. So copy and paste will not work.

**What you get out of the exam**

* A 'real world' (I say that loosely) scenario to apply Incident Response skills.
* The ability to confirm you have learned and can apply the content. Humans tend to over estimate how well they have learned a topic. ([reference](https://sites.williams.edu/nk2/files/2011/08/Kornell.Bjork_.2009.pdf)) and thus practical application / testing that knowledge is proof it is more than a memory cue from a multiple choice exam.
* A certification exam aligned with a NIST role.


### Preparing For The Exam
For all intents and purposes, the course teaches you what you need to pass the exam.

However in saying that, if all you do is the course the exam might be much more difficult than need be.  
  
It is a good idea to spend extra time in the platforms either by building your own home lab or finding something online. Try to become more 'fluent' and comfortable with Splunk and ELK. During the exam you will feel the pressure and you don't want to be googling basic syntax command prior to considering what to look for.

Another thing I found that helped, was reading on the same topics outside of the course. This helped understand other ways tools could be used, other thought processes for investigation.



# What I learned From The Course
This is NOT an exhaustive description, but the most valuable knowledge I gained.

## Flowing Through Splunk & Elk
By flowing, I mean the opposite of staring at a search bar in Splunk or ELK and going 'where do I even start'. The ability to change queries to get different information as needed.

Unfortunately there is a load of theory to cover to be able to do this. I've since found I am able to look through different logs and sources within the 2 platforms much more efficiently. I still have to google things now and again for exact syntax or something, but in general I 'understand' possible locations for where information related to an incident could be.

There is never a straight forward investigation to an attack. There is no answer like "machine dropped malware then moved to machine B". Especially when there is legitimate traffic flowing around. 

I have many notes now on ELK and Splunk queries to help me jump start an investigation.

As an example I have notes on LM/NTML
![notes](/images/ihrp/elearn2.png)

A Splunk search for privileges that can be abused:  
![more notes](/images/ihrp/elearn3.png)


### Job Applicability
I imagine it would be beneficial if I went for a job related to a SOC or  for an IR position to be to say I have a cheatsheet. A playbook to guide to my investigations. This would show that even though I may not do IR every day, I think about what I am doing, what works and what does not, instead of starting from scratch each time.

The benefit for me, is that it keeps my options open. I am still fine tuning my career and want to be able to change career paths if needed.

## LABS - Hands on with a variety of tools
Full transparency, the exam does not cover the IDS/IPS tools. The exam covers Splunk, ELK and PCAP analysis.

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


For transparency:
* The lab learning curve can be quite steep. They do provide a document with the questions and solutions so you can follow along. It felt like a 'big' jump in learning was expected at times.
* My approach was to attempt to answer the lab questions as much as possible prior to looking at the solution. It was at times frustrating to see a huge 'gap' in what i was doing and where I was expected to get to. The gap being the knowledge I had not obtained. 

#### IR Platforms
These were good just to be able to understand the benefits of having a centralized platform for IR, including being able to pull information such as a list of files in a suspect directory.

I did not have to set these up myself, the labs had it all installed.


#### IPS/IDS
Not having to rely on one tool will be beneficial. Especially if consulting at different clients.

The value I found in here, was being able to evaluate the pros and cons of the tools. Such as skill required, effort to maintain or tune and or cost of deployment (purchase price, time & effort).

Obviously at a company, we use an IDS/IPS and it was beneficial to be able to make sure that at my job we could get the most out of the platform, such as tuning it a bit better or understanding its limitations better.

Because it is not my day to day role, I wrote a blog post based on some of the learning on zeek  [here](https://thehackerwhorolls.home.blog/2019/11/05/zeek-bro-cheat-sheet/). it is very short but will help me quickly be able to read a PCAP and or write a rule if needed. - It is also on my old blog site (horrible and ugly to edit and look at).


I have a Suricata Cheat Sheet post as well. It includes basic references for writing rules. Find it[here](https://thehackerwhorolls.home.blog/2019/11/03/suricata-cheat-sheet-2/)

Example:
![](/images/ihrp/elearn10.png)


### Job Applicability
For someone junior, being exposed to the tools and having a go at writing your own rules would be invaluable.

For someone like myself, the value is not only in being able to run the tool and tune rules, but also understanding how it gets deployed, the effort to maintain it, and where the sensors should be. How to justify the value of the tool (via understanding what it does and what it does not do) to upper management is also a plus.

## Attacker Methodology - From The Blue Side
My initial experience and interest within infosec was penetration testing. I would research online how to fix or defend against the techniques used. But I hadn't experienced it from a true Enterprise defender side before. Sure I had installed Splunk and a home lab, but it isn't the same.

Attacks look very different from a blue team side, again with a lot of friendly traffic it is almost impossible to detect. Add in false-positives and it is extremely difficult.

The value here for me is the high level actions that can be taken and how those filter down into a log or combination of logs.

For example, in an active directory environment, the Domain Controllers hold some logs and the clients hold other logs, requiring both to put the full piece together. Or in case of the exam, comparing logs with network traffic analysis.

### Job Applicability
* Understanding that there is no big red alert saying "attacker".
* Being able to identify potential other sources to look to get a full picture of an incident. 
* Having both perspectives from an attacker and defender.

### US Job Applicability
Not so much of importance for myself. However:

The courses such as this one are design around the NIST [NICE Cybersecurity Workforce framework](https://www.nist.gov/itl/applied-cybersecurity/nice/nice-cybersecurity-workforce-framework-resource-center)

[PDF HERE](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-181.pdf)

From their website
> The NICE Framework, NIST Special Publication 800-181, is a national-focused resource that categorizes and describes cybersecurity work.

and 
> Current and future cybersecurity workers, to help explore Tasks and Work Roles and assist with understanding the KSAs that are being valued by employers for in-demand cybersecurity jobs and positions.

IHRP/eCIR is developed towards the following NIST roles:
* Cyber Defense Incident Responder
* Law Enforcement/Counterintelligence Forensics Analyst
* Cyber Defense Forensics Analyst

Upon looking at the PDF, the description of Cyber Incident Responder and Cyber Defense Incident Response appear to match with the content of the course.

![](/images/ihrp/elearn6.png)

![](/images/ihrp/elearn7.png)

# Quality / Size of the Theory
There is a lot. It is extremely important to learn and can be overwhelming. Try to drink from the fire hose and you will burn out. I see this as a necessary evil due to the complexities of what attackers can do on a machine, on both Linux and Windows.

Reading standard text is never fun, but critical. For example, if you don't know which windows event log and login type shows a remote login, how will you know to search for it in Splunk? The answer is [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624) with a logon type 3 for Network.

Which is part of the cheat sheets I created:
![](/images/ihrp/elearn5.png)

For transparency: Yes there are some grammatical errors. The author is from Greece originally so it is understandable. His expertise is within IR not English.


# Summary - To Finish Up
* Overall a great course for its price range
* The practical exam really makes this shine forcing you to be able to apply the skills learned
* A differentiator from multiple choice exams
* Prepares you to do the job not just teach a bunch of theory and tools