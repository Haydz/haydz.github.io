---
layout: posts
title: "Security Architecture 1"
---

I wanted to blog about security Architecture.

I have been reading and watching a lot of material. I have been taking notes, and it seems to just want to sit in my short term memory. There are CTFs for pentesting and incident response, or hands on network analysis challenges. Nothing as easy for security architecture.

Perhaps I can build up my home lab as much as possible. However this is just so much.

So lets start with a high level view of Security Architecture and domains.

# Material

I have been going through a Pluralsight course called:
* Architecture and Design for CompTia Security+
[Found here](https://app.pluralsight.com/library/courses/comptia-security-plus-architecture-design/table-of-contents)
As well as other pluralsight courses.

There are  also frameworks:
* ISO 27001 (not specifically architecture)
* [SABSA](https://sabsa.org/)


## High Level
Security Architecture according to SABSA has multiple concepts or as it names it 'views'. Due to the over-arching size of Enterprise Security Architecture it makes sense.

You can read in detail [here](https://medium.com/@marioplatt/what-is-sabsa-enterprise-security-architecture-and-why-should-you-care-a649418b2742)

SABSA ensures all different stakeholders are included, as shown in the below image:


![](/images/SecArch/image_1.png)

This lays out the main areas to consider within Enterprise Security Architecture.

### In simple terms:
The Business view:
* Ensure you consider the business drivers, business risk assessment, supply chain management.

> This is the view seen from the viewpoint of the business owner or executive business manager.

*W101 Architecting a Secure Digital World An Overview*

### The Architects View: 
* This is the overall concept of the business attributes profile and risk objectives. 

> It defines principles and fundamental concepts that guide the selection and organisation of the logical and physical elements at the lower layers of abstraction.
*W101 Architecting a Secure Digital World An Overview*


### The Designers view
* This is also known as the logical security architecture part. This is where context of information, services, and applications functions are considered.


The difference I see in between the Architects view and the Designers view is that the Architect is looking at it from the organization side of things and the designer is about what services and applications need to be part of that organization. In an analogy, it seems the Architecture view would be the organization (design) of an office space (the lay out) and the designer understanding what there needs to be in that office space to make it work.

### The Builders view
* Takes the logical descriptions and network diagrams and makes it come to life. They "build" it, they choose the technology models and stacks that will work with the 'requirements'

### The Technicians View

