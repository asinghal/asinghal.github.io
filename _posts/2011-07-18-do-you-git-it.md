---
author: Aishwarya Singhal
comments: true
date: 2011-07-18 06:58:07+00:00
layout: post
slug: do-you-git-it
title: Do you Git it ?
wordpress_id: 69
tags:
- Git
- Rails
---

Another new experience - Git. I looked at it because it looks like github is a cool thing these days, and well I have to admit that it does look a bit cool :-)

I thought I would play with Git and see for what its worth. Having worked with various version control systems - VSS then CVS and for many years later SVN, I don't really see a need for a new one, but then I didn't see the need for subversion when it first came in. Now IMHO, Github is cool simply because somebody else on the web is managing it for you and it integrates version control with wikis.

Anyways, I created a github profile and followed the instruction to the letter to set up my repository. Nice and easy - took me a total of 15 mins from getting an intent to having a repository online. Then I editted the README file on the github website to put in more detail and started building a basic application on rails on my laptop. When I tried to commit, it didn't work - said there was nothing to commit but there were unversioned files. Ofcourse, I needed to add the new files!

	git add .

	git commit -m "my basic app"

The above worked! So the code was committed now. Oh wait, it still didn't show up on github. Hmm... what was I doing wrong? Read a few articles to realise I needed to "push" my changes!

	git push

Didn't work ... it complained that I was trying a non-fast-forward ... whatever that means :worried: Reading a few articles again I realised that my editting README on github directly caused the issue - I need to pull the changes before I could commit (much like svn update before committing).

	git pull

	git status

	git push

This worked and now I have my code on github!
