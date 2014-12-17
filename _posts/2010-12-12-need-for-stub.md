---
author: Aishwarya Singhal
comments: true
date: 2010-12-12 17:57:18+00:00
layout: post
slug: need-for-stub
title: Need for Stub!
wordpress_id: 6
tags:
- ESB
- J2EE
- Quality
- ESB
- Mule
- Stubs
- Testing
---

Do you have many external system interactions? Too many third parties? Do they provide easy interfaces for testing different scenarios in your application? Do I hear a resounding no? :-)

We have an application that depends on 30+ external systems that either do not provide test interfaces, or the ones that are provided, are quite primitive. That's quite bad because we can not effectively test our application and most of the logic goes untested to production. Take a guess... yes we have a large number of issues on production :-(

When we started writing the application, we decided we needed stubs, i.e. programs that will block our actual interaction with the third party and give us some response back. The problem with this approach is that you never look at the request! So we scratched our heads and we thought the following were the options:

1. Dumb stubs: Any request, you get a fixed response. No good unless you don't have any logic around the response that comes back.

2. Wise stubs: Based on the request coming in, validate it, point out errors, and prepare a response. The response could be different for different requests so can enable a wider scale of testing.

3. Simulators: Enhance the wise stubs so that they maintain a state of requests as well (may be across stubs if required). So if you have a stub for withdraw money and another to deposit, both should update a "balance" which should be visible to both.

In all of these cases, another dimension is that you could have stubs that sit in the same layer of application as the end point connectors, or you could have them available as services over protocols similar to how it will be on live.

I suggest building wise stubs that are available as services. Simulators are too much of a pain to write so unless you need them desperately, avoid them.

This is what we did recently: we used Mule. How does Mule help me ? Greatly!

1. Mule provides me with a central way of interacting with all different stubs.

2. We now have a common framework for designing and implementing stubs.

3. Most of the protocols are supported out of the box (we had to write a custom handler for Telnet though) so its kind of plug-and-play.

4. It can be easily run on a seperate JVM and can be deployed anywhere in the system.

5. I can easily build delays in the responses so that performance testing can see real life type responses.

6. And its easy!


