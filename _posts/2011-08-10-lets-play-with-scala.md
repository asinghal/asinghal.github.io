---
author: Aishwarya Singhal
comments: true
date: 2011-08-10 06:36:17+00:00
layout: post
slug: lets-play-with-scala
title: Lets Play with Scala
wordpress_id: 82
tags:
- PlayFramework
- scala
---

Sometime earlier this year, I read a [blog ](http://ikaisays.com/2009/04/02/twitter-ruby-on-rails-scala-and-people-who-dont-rtfa/) and an [article](http://www.theregister.co.uk/2009/04/01/twitter_on_scala/). These are interesting thoughts and coming from the Java space of enterprise applications, I know exactly how bad performance and unmaintainable the code can get.

Scala's [claim](http://www.scala-lang.org/) of reducing the code by a factor of 2 or 3 is extremely tempting! Add to that a lot of goodies like closures, functional programming, immutable types combined with the power of running on JVM and having an ability to reuse Java frameworks and libraries make it a very irresistible option.

So, I started exploring it. The first thing that struck me was that it wasn't easy to learn! I spent weeks reading through a book and forgetting what I was reading - not good at all. Then I decided to build an application - what's more convincing that to build a web application, something we build in real lives? The power of Scala is not in web applications, they are not its forte, but then it would be a good start.

Looking for web frameworks, and I didn't want to use Spring or Struts to avoid getting into the trap of writing a lot of Java, I came across Lift. It looks good, but is again fairly complex. And then I came across [Play](http://www.playframework.org/) and there's been no looking back. Its a nice web framework and is highly productive for a developer. Code changes do not warrant a restart of server and user libraries (called modules, similar to gems in Rails) can be easily built and integrated. The test framework, code coverage et al comes out of the box too!

I do like Rails for all the productivity boosts it gives, especially in the form of code generation. And I missed it in Play. So I have started writing something similar for the Play + Scala combination. If you are interested, it is hosted on github at [https://github.com/asinghal/Play-ScalaGen](https://github.com/asinghal/Play-ScalaGen)

With this module, you can now generate Rails like scaffolds and have a CRUD application running in less than 5 mins! Oh, did I say that it generates unit and Selenium test cases too?

It is in a pretty nascent stage right now and I would love to hear of some feedback on it.






