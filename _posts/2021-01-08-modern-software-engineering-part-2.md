---
author: Aishwarya Singhal
comments: true
layout: post
title: Modern Software Engineering - Part 2 - Maximizing developer experience and writing high quality software
tags:
---

Is the practice of developing software a science (Computer Science), an engineering (software engineering), or an art (software craftsmanship) ? When I was in university, we always viewed software as science. We experimented, we learned, and we treated it as mathematics - driven by pure logic. When I started working, it became more of an engineering - applying known techniques, searching for ways how others have solved a problem before, and looking for efficiencies. In recent years, I was introduced to the idea of it being a craft - i.e. focus on quality, and believe in the fact that it can always be improved. I can't say I fully practice craftsmanship, however I have moved from engineering more towards it. In my personal view, most projects unfortunately do not quite allow for (or warrant) the time needed for the craft. In any case, we can *always* do a few things:

1. Ensure a certain level of quality the first time we publish the software through automated checks and thorough code reviews, but avoid over-engineering
2. Make time for refactoring
3. Work smart, not hard - get as many open source libraries as possible to solve your problems, and only write code for things that are truly specific to your problem and can not be found on the net

Based on these 3 ideas, I have a few practical tips.

1. **Build on best-in-class programming techniques**

    My favourite here is the [UNIX philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) that was published in 1978 (yes, over 40 years ago!):

        * Make each program do one thing well. To do a new job, build afresh rather than complicate old programs by adding new "features".

        * Expect the output of every program to become the input to another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input.

        * Design and build software, even operating systems, to be tried early, ideally within weeks. Don't hesitate to throw away the clumsy parts and rebuild them.

        * Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tools and expect to throw some of them out after you've finished using them.

    Why do I love these? These have stayed solid (as has UNIX) over the past 40 years. I derive my coding principles from these, and the following are my most commonly used ones at the moment

    * Write short methods that do one thing only and do it well. This in turn helps to keep a low cyclomatic complexity as well as less number of lines of code per method. I love the Unix pipes and filters, and if you can build that idea into your methods (e.g. using Strategy pattern), a fantastic code quality emerges
    * Use [microservices](https://martinfowler.com/articles/microservices.html) (small pieces of functionality that are independently deployed) where possible
    * Go minimalistic in your design of interfaces, following the [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) and [Convention over configuration](https://en.wikipedia.org/wiki/Convention_over_configuration) principles. Try to follow the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle as much as possible (without making the code too unreadable)
    * Insist on modularity so that pieces of code can be thrown away when not needed. Caution: avoid over-engineering. This is not the most important aspect if you are following the other principles
    * Refactor, refactor, refactor: Do not shy away from refactoring. The principle is, `Whenever you look at a piece of code, aspire to leave it in a better state than you found it in`

    A technique I find useful in writing modular code is:

        Every time you feel the need to write a comment in the code, see if you can make a new method/ service. Comments usually indicate that the code is doing more than what can be easily understood.

    You can use any programming language, and any style - my personal favourite at the moment is Functional programming in whichever language I use, because it helps me implement the above mentioned goals easily.

    A technique not mentioned here and one I am a big fan of is [Event Driven Architecture](https://en.wikipedia.org/wiki/Event-driven_architecture), (or alternatively, Reactive Programming). It helps reduce dependencies, and provides an easier way to guarantee performance and reliability of a system.

2. **Align on quality goals and then automate them**

    I have seen situations where the team discussed at length, and kept discussing, the choice of technology. I have also seen similar debates around quality. The only way to avoid an endless debate is to propose and align a set of technologies and quality measures *democratically* with the team, and then adhere to them for at least a few months. And the best way for that to happen is to automate the agreed principles. 

        Do not define a quality goal that can not be *(at least partially)* automated, because it is unlikely that it will be implemented.
    
    * Be real about your Definion of Done (or equivalent) and hold your team accountable to it during code reviews
    * Timebox all decisions
    * Try to leverage industry standards where possible - e.g. AirBnB style for Javascript linting is often used by teams, or like back in the day Sun's Java conventions were pretty standard guideline for Java code
    * Call a meeting at the start of the project and agree on quality goals (and publish them)
    * Anybody joining the team afterwards can give suggestions on these goals, but they should only be accepted if they do not disrupt the rest of the team. Alternatively, they can be accepted in the next review of the quality goals (after at least 6-8 weeks)

    As I mentioned earlier, bugs are any deviation from a user's expectations. That includes functional defects, and also performance, usability, reliability, etc. Ensure that your quality goals take a complete view.

    Typical techniques like TDD, Code Reviews, Code Style checks (static code analysis), etc are usually good measures. When writing automated tests, it is more important to have real quality tests than writing for the sake of getting a 100% test coverage (e.g. you must get a 100% coverage on code containing logic, and it is ok to skip tests for simple Value Objects).

    Some aspects can be only partially tested - e.g. in case of web accessibility, or security, a manual review may still be required. However, there are many tools available to get you a 80% correct view (if not more) and I would highly encourage using them.

    Similarly, take your code reviews seriously. Github and similar tools simplify the review process significantly, and can integrate all feedback that automated tools can generate to help you review code.

    Technology evolves fast, and I would always recommend checking for the best ways to achieve automation of quality goals before starting any project, and every couple of months even after starting a project.

    A manual review by the product owner or quality engineer may still be required, but by the time it goes to them, all other checks would have ensured a decent quality level.

3. **Be truly agile: ship the software as soon as possible**

    As I said in the [previous blog](http://asinghal.github.io/2021/01/04/modern-software-engineering-part-1.html), shipping software is far more important than perfecting it. As long as the code meets all quality goals, it should be good to deploy.

    I always reflect back on my days in the school, when I first started to code. This was what SDLC looked like to me then:
    1. Get a problem (requirements) from the teacher (product owner/ user)
    2. Implement them on my computer
    3. Copy the working code into a floppy drive (deploy)
    4. Show it to the teacher

    It did not take me weeks or months to do that. It was often done from one day to the next, and in some cases even during a class.

    Even when we had a project where multiple teammates were working on it, the cycle only had one more step between 3 and 4: Integrate your code with a friend on their computer (aka production set up)

    There was no 3 or 5 environment set up, no change management, no design aprovals, etc etc.

        We have made software development overly complex over the years, and it is important to simplify it. The longer you take to ship software, the worse quality you can expect.

    Now of course, you need to have processes and checks to ensure quality of delivery. However, as long as you have defined sound quality goals and the code meets them all, your code should be good to ship. Put it in front of the customer, and address any learnings that come out of that. If you can fix issues quickly, it is perfectly ok to have a few bugs that pop up once you deploy.

    Some ideas:

    * Use feature branches and feature flags for software development, and have a process to clean up stale feature flags once a feature has been stabilized
    * Ideally, you should push your code to production at least once a day. Worst case (for complex and large problems), push it within a week. For sub-projects (like a redesign) that takes longer, create a pipeline to deploy the feature branch on the test environment for that sub-project - thats your production environment for the sub-project. In no case, keep the feature branch alive for more than a week
    * Fully automated deployments: Use continuous delivery pipelines and allow developers to build their own infrastructure through scripts/ bots (infrastructure as code). Achieve a full automation on deployment, ideally including the production environment. In highly controlled settings, implement a fully automatic deployment pipleline at least until pre-production/ staging environment, and then a 1-click deployment for production
    * Ensure sufficient monitoring and logging in the code to observe and learn from user behaviour. That will ensure a much higher level of quality than what can be predicted during the development phase, and is absolutely needed for a continuous delivery system. [CNCF](https://www.cncf.io/projects/) is a great place to start for such topics.
    * Optimize the delivery pipeline to take less than 30 minutes (faster is better) including test execution. This will ensure that developers get feedback on broken builds and issues ASAP, and are able to quickly fix the issues on production.

    One last tip here - be honest to yourself. Everytime you have to do a less than perfect job, note down a technical debt item in your product backlog so it is tracked and never forgotten.

4. **Reduce the number of meetings you attend**

    One the main time drains for developers is the number of meetings that happen. Avoid them. Put a limit of a total of 30 minutes per day for meetings that need more than 5 people (e.g. the morning standup) for at least 4 days a week. The exception will be some days when you have a architecture/ design session with whole team, planning meeting, or a retrospective, etc. These longer meetings should be on the fifth day of the week.

    Try to move as much communication online as possible. Use tools like Slack to have effective integrations with various tools, and have chats with your team. An online discussion has various advantages - you only dedicate time that you absolutely have to. Also, it helps any other team member to pitch in or learn if they see value in the topic - that makes it much more productive.

    It is vital to understand the true meaning of agile and I recommend re-reading the [Manifesto](https://agilemanifesto.org/) and listening to the talk [Agile is Dead](https://www.youtube.com/watch?v=a-BOSpxYJ9M) every few months. More often than not, teams claim to work in agile manner but still have numerous complex processes and constraints built around them. Whenever you get an invitation for a meeting, ask yourself - can I avoid this meeting? Try to skip as many meetings as possible. At the same time, pair programming sessions can be awesome. Take a pragmatic view and do those whenever it makes sense.

    One of the reasons for meetings is dependencies and integrations. Can you reduce them? Try to design your coding responsibilities so you can own end-to-end slices and have minimum dependencies on other teams/ team members. Use [interface contracts](https://saucelabs.com/blog/intro-to-contract-testing-getting-started-with-postman#:~:text=Contract%20testing%20is%20a%20way,the%20data%20the%20client%20needs) ) along with techniques like Mechanical Turk, stubs and mocks, to be able to independently develop your code. When done well, this can be done completely independently, and results in significantly reducing integration efforts.

    Lastly, when I talk about meetings, I am excluding the ones that help you learn (e.g. conferences, meet ups, knowledge exchange sessions). Try to carve out time for them so you do not disrupt your productivity too much, and yet have reasonable time available to learn and share knowledge.

    As a thumb rule, you should be able to get 6-7 hours a day for focussed coding.

5. **Leverage and contribute to Open Source Software, and Internal Open Source**

    A key aspect to optimising your time *and* imporving the quality of your code is to leverage open source libraries as much as possible. Everytime you have a problem to solve, check if there is a library that already does that. Ask your team. There is a library for most of the commonly encountered problems - somebody somewhere solved it, stabilized it, and published it. Beware that there are also a number of bad libraries out there, so make sure that a) there is sufficient community behind it, and b) you have tested and seen it working. 

    Open source is awesome because people contribute to it. See what you can publish too. If you solved a generic problem, publish a sanitized library (check for your organization's policy first). It helps the community of developers, but it also builds a brand for you and your company, and attracts good developers to work with you.

    Similarly, see if you can build an "internal open source". If a colleague needs to re-use a piece of code, or if you are re-using code written by someone else, see if it can be a library to be shared internally (or if it generic enough, externally too). Do not greedily create libraries, but instead let that be done on demand. This ensures that a good ecosystem exists for all software in your organization, and everybody benefits from your learnings. 
    
    At the same time, allow anyone in the organization to submit a pull request, or make changes to the library and help evolve it. That's the true nature of open source software and helps with its adoption. Failing this, it just becomes a framework component that will always be your responsibility to maintain and fix, and will also see scepticism from your colleagues on its adoption.

Finally, find time to learn. Time spent on learning yields exponential results in your productivity (and happiness). Keep measuring quality of your code (through different tools), and you will master it. 

Happy coding!
