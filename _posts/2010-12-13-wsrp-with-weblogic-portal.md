---
author: Aishwarya Singhal
comments: true
date: 2010-12-13 05:43:41+00:00
layout: post
slug: wsrp-with-weblogic-portal
title: WSRP with Weblogic Portal
wordpress_id: 10
tags:
- J2EE
- Remote Portlets
- Weblogic
- WSRP
---

**Introduction
**We have recently implemented WSRP using Oracle’s Weblogic Portal technology for our selfcare customer experiene for a client. This application had been in production for over 4 years and we had started to face severe challenges around its scalability and maintainability. The application had grown huge, was packaged in a single enterprise archive (EAR) and testing the smallest changes required a full regression test to be conducted. This meant that the system could not scale well in future, and also that we could not propagate changes to production swiftly and without impacting the whole website.
Once we read about WSRP, we knew it was the way to go!

**Enter WSRP!**
Webservices for Remote Portlets (WSRP) specification provides means for integrating remote applications and content into a website (portal) via pluggable and interactive webservices. These webservices have a well defined interface and protocol for processing user interactions and fragments that can be brought together to render web pages. This also means that all of your remote applications now integrate with each other using one single mechanism and one single adaptor, removing the need for having different adaptors for different applications.
An example of where WSRP shows its true might is where you have to show device information, price plan information, billing information, stock feeds and weather feeds on the same web page – say a customer’s home page. You may have device information coming from a different data source, plans and bills from yet another, stock and weather feeds may be third party. In a classical web application, you would have different parts of the application working sequentially sourcing all the necessary data and once done, would dump it all on the screen. If any one breaks, the page may entirely break. This is not very different to the way a regular portlet based application would behave either. However, in a WSRP based application, you have the option of executing these in parallel through minor configuration, and also, the impact is limited to a part of the page rather than the entire webpage. So you may have weather and stock information on the page even if your database is down! This also means you can pull information from completely independent sources without any code changes to your application.

The integrating part of the application (that puts everything together) is called a consumer, and all applications supplying the fragments are called producers. There can obviously be many consumers (different web sites) using a number of producers. So you could have different websites, say a public one, a customer service one, an intranet, an administration application etc all using different fragments coming from a set of producers. These websites may have a different look and feel and an entirely different purpose.

Typically, the interaction between producers and consumers happens in form of SOAP (over HTTP) and hence these producers could well be located in separate geographies. This enables horizontal scalability in the same application – we can now have parts of our application running on one server and other parts on other servers (of course, managing response times could be a challenge!).
**Advantages of Using WSRP
**We see the following benefits with the use of WSRP:



	
  * There are smaller and more manageable applications now which can be developed and deployed in isolation.

	
  * The development and testing effort now goes down as the impacts of changes are contained to smaller applications.

	
  * A smaller regression test effort is required which implies a shorter test phase.

	
  * Project lifecycle is shortened with the impact being contained and hence there is more agility in delivery.

	
  * There is a larger possibility of code reuse in the application with individual deployable components.

	
  * Applications can be deployed onto production without a full outage on the currently running website.

	
  * With the use of shared libraries/ optional packages, it is possible to share code between different applications as well.


**Performance Considerations**

While WSRP provides many advantages in terms of maintainability, there is some obvious performance overhead associated with the same:



	
  * The number of applications now increase which means there will be a default static load on the system (each application will come with its own overhead). In our case, there was a 60M overhead with each EAR.

	
  * There is a CPU overhead because of the increase in number of interactions (each producer-consumer interaction is a new request).

	
  * The memory utilization goes up as well as there are more sessions created (one per producer) and more caches created.

	
  * Weblogic recommends using local proxy portlets rather than using remote proxy.
We saw the response timings jump up as well. For static pages, the jump was significant (almost double).

	
  * We saw the heap memory jump up from 2 GB to 2.5 GB and the CPU jump up from 20% utilization to 30%-35%.

	
  * The startup memory jumped up from 200 MB to 600 MB.

	
  * The size of LDAP files grows rapidly with WSRP as it is used for securing all communication between producers and consumers. The impact of LDAP is significant as Weblogic caches the entire LDAP in heap and having a large LDAP means high memory utilization, leaving small space for application to run. There are ways to limit the size of LDAP so they must be leveraged.


