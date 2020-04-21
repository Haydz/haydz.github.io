---
layout: posts
title: "Incident Handling Certification"
---

Since I blogged about my experience at OpenSoc I wanted to expand on the value I found in my eLearnSecuirty incident response course. What you will find below is a bit of a review of the course itself and the exam.

# What to expect:
A review based on my specific circumstances and the value I myself gained from the certification

# What course?
The course I signed up for was [Incident Handling & Response Professional](https://www.elearnsecurity.com/course/incident_handling_response_professional/)

It was released last year in January.

## Who is it by?
[elearnSecrutiy](https://www.elearnsecurity.com/company/about_us)
This company is based in Italy and the US as you can see in the about us section.
![Logo](/images/ihrp/elearn1.png)
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


### 





# Quality of the Theory

