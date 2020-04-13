---
layout: posts
title: "OpenSoc Experience  & ElearnSecurity IR Course"
---
# Intro

So Thursday (April 9th) I participated in an online blue team defense simulation event, known as OpenSOC.

What follows is:
* What the event is
* How I found out about the event
* The Event and my Experience
* Things I learned
* how the event was run
* How an IR course I took in December helped



# What is OpenSOC?
According to their website found here: https://opensoc.io/
> OpenSOC is a blue team defense simulation that is as close to "the real thing" as it gets. This isn’t just another CTF. We’ve built this platform to train real-world responders to handle real-world situations. Our environment is a highly portable, fully functional replication of an enterprise environment, complete with all the trimmings - Active Directory, Exchange, distributed networks, various sensors, log aggregation, end-user simulation, and more.
>
> OpenSOC is comprised of over a dozen open source projects, including the below.

The tools they list are what you would think of:  
* Metasploit
* Osquery
* Snort
* pfsense
* Graylog
* Suricata

\+ others
![Tools](/images/opensoc_1.png)
screenshot from the  OpenSoc website.

# How I found out about the event?
Twitter... Seriously twitter!

A post came across my feed asking for interested. I responded and apparently so did enough people that we had 700 people during the event.

## REminder to add Tweet here ##


# The Event And My Experience

## My preparation
I had once participated in ProsvJoes CTF at BsidesLV. As such I expected a hands on 'defense' event. 

The 3 main tools to be used were Graylog, molo-ch and OSquery. For my team, I focused on OSquery.  
  
There is a great course from "Applied Network Defense" that I had started but never finished. So I quickly ran through the usage videos to get a handle on that. The course can be found here networkdefense.io/library/osquery-for-security-analysis.

![OSquery](/images/opensoc_2.png)
 
I had completed the eLearnSecurity Incident Responder certification exam in December (course found here: [Course](https://www.elearnsecurity.com/course/incident_handling_response_professional/_. So I had a large list of investigating queries to use. For my exam I had them in Splunk and ELK search formats) )(not all of them), so I thought it would be easy enough to convert them to Graylog. Or at least use as a reference sheet.

![Query](/images/opensoc_3.png)


