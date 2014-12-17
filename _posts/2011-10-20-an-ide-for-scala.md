---
author: Aishwarya Singhal
comments: true
date: 2011-10-20 06:01:35+00:00
layout: post
slug: an-ide-for-scala
title: An IDE for Scala
wordpress_id: 86
tags:
- scala
---

I have been working on Scala in my spare time for the past ~3 months now and I absolutely love it! It is extremely powerful, the syntax is sleek and it has an API for almost every basic operation!

My choice of IDE so far has been Eclipse which I am a big fan of while working in Java. Unfortunately, when it comes to Scala coding, the Scala plugin hangs up every now and then, the code assist does not like certain permitted formats so kind of enforces you to write code the way it understands it, the compiler blocks the user when code is saved (so I can't type more code until the time it has completed compilation) and the code assist (ctrl + space) gives some very useless suggestions at times. It just didn't work for me. So I tried other options - JEdit, Vim, and read about Netbeans and IDEA, all of them seem to have Scala support as a huge afterthought and hence is very insufficient.



So I started writing an IDE for Scala that I now call Slate. The intent is to have a simple tool that developers can code Scala  on without the IDE being too intrusive. It should be light and quick - we don't need a memory hog and neither do we need something that will be slow and start influencing the developer's coding speed. At the same time, it should have all the basics that make coding easy and fast.

I am still actively developing Slate but you can check it out at [github](https://github.com/asinghal/SlateIDE). As always, I would love to hear of some feedback and criticism. Also, I need some partners from the Scala community to contribute and make this the "right" IDE for Scala. Let me know if you are interested!


