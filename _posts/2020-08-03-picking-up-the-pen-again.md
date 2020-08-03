---
author: Aishwarya Singhal
comments: true
layout: post
title: Picking up the pen again
tags:
---

I haven't written much in recent years, at least not publicly, and I decided now would be a good time to start again. 

I also haven't written much code in recent years, so I decided to re-write [Factile](www.factile.net) in a more popular tech stack. It has been a great experience for various reasons:

1. I could resurrect Factile which has been sitting on a broken server for past 3 years with me having no time to fix it
2. I could experience first hand some of the techs my colleagues have been talking about - its been extremely fulfilling
3. ... and it gives me confidence that I can still write a fair quality of code

It took me about 4 weeks of few hours a day to completely rewrite it, and I followed the engineering practices I have been coaching my teams on.
 
Factile has been re-written in [Node JS](https://nodejs.org/) and [React JS](https://reactjs.org/), something that has been a trend for a few years now, and I believe represents a robust developer community. I discarded Scala as a the language for Factile primarily because the frequent churn in the language made it extremely difficult to keep the stack up-to-date and stable in the past, not to mention the fact that it still has a niche in developer community as compared to the ultra vibrant JS community.

I chose [Cypress](https://www.cypress.io/) for browser testing because a) I wanted to see what the fuss was about, and b) I absolutely love the idea that you can [stub API calls inside of tests](https://docs.cypress.io/guides/guides/network-requests.html#Stubbing)

Finally, I use [UptimeRobot](https://uptimerobot.com/) for monitoring, [CircleCI](https://circleci.com/) for continuous integration and [APIDoc](https://apidocjs.com/) for, well, API documentation. Of these, APIDoc suprised me the most - it is just amazingly simple to use, and simple to extend (which I did in a way because I did not like the default template/ color schemes).

I have been using CircleCI since 2015 and I think recently, it has become incredibly complex with poor documentation. I could have used TravisCI I guess, but I'll stay with Circle for now.

Oh yes, I didn't use Typescript. Why? I personally don't like my JS code to have a need to compile, and I feel that instead of writing types for JS, I would rather write code in Scala (or Java, or Kotlin) ;-)
