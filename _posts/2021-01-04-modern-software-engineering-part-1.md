---
author: Aishwarya Singhal
comments: true
layout: post
title: Modern Software Engineering - Part 1. Defining a strategy for success
prev_link: /2021/01/03/modern-software-engineering-intro.html
next_link: /2021/01/08/modern-software-engineering-part-2.html
tags:
---

As leaders, we are often faced with challenges in balancing the needs of the business, and the constraints in delivering to those expectations. It is a complex problem, and one that requires multiple considerations.

Over the years, I have developed a list of 5 "principles" I found useful in defining a winning tech strategy.

1. **Speed trumps quality, but not always**

    The speed to deliver a software, or a feature, the time to market, is extremely important. At the same time, it is important to focus on the quality. However, these two do not go hand-in-hand. Quality needs time, and that slows down delivery. And nobody likes something that lacks quality even if it is delivered ultra-quick.

    The definition of *acceptable* quality changes based on the context. A throw-away software that enables a quick test of a business concept does not need to be perfect. However, a software that is related to hardware which can result in expensive losses due to bugs ([like a space shuttle](https://www.bugsnag.com/blog/bug-day-ariane-5-disaster)), needs to have a much higher quality level. It is important to know the minimum acceptable levels for both speed and quality. How quickly do you need a feature, and how perfect does it have to be?

    Usually, in a "Build vs Buy" discussion, "Buy" is more preferable. If you can find an opensource library that already solves a problem, it is better to use it instead of building from scratch. Similarly, a commercial off-the-shelf product may also provide a good foundation and jump start. However, ensure that sufficient due diligence (including a short proof of concept) has been done before adopting/ buying a software. There are a number of horror stories around off-the-shelf products. The marketing material always looks cooler than the actual fit of a software in your ecosystem.

    In general, an 80-20 rule helps. Ensuring that 80% of scope is delivered with >95% quality is much better than having 100% scope delivered with <80% quality, or only ~20% scope delivered with 100% quality.

    It is far more important to be able to fix defects quickly, than to avoid them altogether. There will always be unforeseen issues once the software is released to consumers, but if you can fix that in minutes instead of days, nobody notices, and the impact is negligible.

    An investment into technology - automated delivery (continuous delivery pipelines), monitoring, and processes that enable an on-demand deployment in minutes - will provide a much better risk management ability compared to any review processes that try to foresee and prevent risk.

2. **When in doubt, prioritize customer centricity** 

    In the B2C world, customer trumps everything else. Even if you are not in B2C, any software you produce needs to be optimized for the consumer. It is extremely important to define metrics and goals with the customers point of view. There are often conflicting priorities, and the engineers would always like to invest into ensuring a robust and maintainable system. As an engineer, I often find myself at the center of this conflict myself. However, as a principle, customer always takes a priority. It is *always* an unpleasant discussion, but a necessary one.

    I read a quote from Steve Jobs somewhere: 
    
    > When you're a carpenter making a beautiful chest of drawers, you're not going to use a piece of plywood on the back, even though it faces the wall, and nobody will ever see it. You'll know it's there, so you're going to use a beautiful piece of wood on the back.

    This is a cool quote, and I immensely respect Mr. Jobs, but perhaps this is something that **does not** apply to most modern software projects. For me, that plywood in the back may be perfectly ok as a way to get started. That does not mean that it should remain there forever. It should be replaced with beautiful wood as soon as possible. But we do not need to wait for the final quality until the software is released, as long as the chest of drawers is usable by the consumer.

    Does that mean we let poor quality software to be developed? Absolutely not. Optimize for the customer and ensure that only the best quality is presented to them. At the same time, it is important to keep track of "technical debt" - compromises that have been made to urgently ship software to address a business or customer need. And it is important to have a *real* plan to fix that. Typically, a "technical budget" of 15-20% development capacity is a good way to ensure that the debt does not mount beyond unmanageable levels.

3. **Shipping software is far more important than perfecting it**

    A few thoughts to keep in mind here

    * Software sitting on a development or test machine is worthless until it is made available to the consumers
    * The best way to perfect a software is to put it in front of customers and get feedback on it. There is no way one can perfect a software without the customers providing inputs to it
    * The longer you wait to release software, chances are that the quality will be lower. Counter-intuitive? That's because the longer you wait, the needs of business are likely to evolve. Plus, it will be more complicated to merge all on-going changes being produced by the larger team, and it is more difficult to isolate and fix problems since there is too much change deployed at once

    I remember working with a colleague who had previously worked in electronics industry - he was stunned that we could modify software and deploy "so quickly". In hardware world, they had to plan every change, implement the change on a breadboard, send the design to a factory for circuit printing, send the circuits over to the QA department, and work on the feedback. It took them weeks. That's not how software engineering works though, and it is important to recognize the difference. In today's world, if a software takes months or years to deliver, somebody's heart sinks.

    There are various stories from leading technology companies. Amazon deploys every 11.7 seconds [[1]](https://techbeacon.com/devops/10-companies-killing-it-devops), and Google plans for 4 million builds a day [[2]](https://thenewstack.io/google-reveals-the-secrets-of-devops/).

    How about the risk of errors due to frequent deployments? Risk management is often misunderstood. In my experience in software engineering, risk mitigation is far more effective than risk avoidance. As long as issues are immediately identified and quickly addressed on production. So, while all change managers will tell you otherwise, set an aspiration for your tech team to deploy multiple times a day, to production. OK - for a greenfield product, you need to first establish a minimum viable product (MVP) on production, before you have multiple deployments a day, but in that case, you only have a production environment once the MVP is ready. It is extremely important to have processes and technology that support multiple daily deployments.

    I read somewhere: if you are not failing, you are not trying hard enough. Failure is not a problem, not being able to learn or come out of a failure is a problem.

    Technically,

    * Use Cloud for all deployments - ideally public cloud
    * Automate everything - DevOps, Continuous Delivery, etc. Support zero-touch processes. Anything that requires a human interaction will slow you down
    * Push for an MVP mindset across the board and rationalize the scope for software delivery

    Shipping software is probably second only to customer centricity in terms of a tech organization's priorities.

4. **Quality is directly proportional to the investment into talent and culture**

    To start with, I am not talking about the financial investment only. I am also talking about time that you invest as a leader. 

    Now, of course, getting quality developers will cost a bit more than the cheapest available in the market. But you do not need the most expensive ones either. Having an all-star team does not guarantee quality. However, a team that sticks together, challenges each other, and believes in the goals of the organization goes a long way in establishing quality.

    Similarly, the importance of culture cannot be overstated. My key considerations here:

    * Hire quality developers and enable them for success. Let them take decisions. Collective brain power is always better than ivory towers
    * Have a performance centric culture. Celebrate successes and capture learning from failures. However, ensure that people are not scapegoated for failures. The only failures that need to be discussed are where people were comfortable with their status-quo and failed to try or innovate
    * Ensure alignment of common language and goals across the organization. As long as there is a separate "business" and "IT team", quality will suffer. Ensure that the same goals are used for both, and that they are working as collaborators. **Software needs to be business led, and not IT led** (although the tech team needs to have a sufficient degree of freedom to bring in tech innovation). Encourage everyone to think of the customer. It is not just the designer's problem, or the customer service department's. Spend time with the teams, so they feel connected
    * Invest into the best tooling for the developers. High quality tooling improves productivity, encourages creativity and innovation, and improves people retention. E.g., buying good laptops for developers is a one-time cost, and not a great cost, but significantly improves the quality of their output. Good tooling can also improve collaboration and cut down on unnecessary meetings, which further improves the productivity
    * Ensure that everyone is learning from external community (outside of your company) via meet ups, conferences, or talks delivered by external experts. This needs to happen frequently, and the experts need to be real experts, even if they do not speak the local language

    *Getting quality delivered to customers is hard and it will only happen when the whole organization collaborates, instead of throwing it over the wall to the "IT team".*

5. **Be bold: there is no replacement for testing and learning**

        The road to wisdom? — Well, it's plain
        and simple to express:
        Err
        and err
        and err again
        but less
        and less
        and less.
        - Piet Hein

    There is no shortcut to testing.

    Before the teams start building a product, test the business case. Conduct user tests on cheap prototypes. Not every fancy idea is worth developing, and what may work for another company in another set up, may not always work for you. As a leader, you can (and should) help the teams rationalize their requirements.

    Once built, measure everything, and capture as much customer feedback as possible. Invest into analytics and capture every customer interaction. Analyze the data for any trends, and feed that back to the technical teams' "backlog" to be prioritized and implemented.

    Also, that means that approaches like [Mechanical Turk](https://en.wikipedia.org/wiki/The_Turk) which involves setting up "fake" solutions until "proper" solutions are available, can be fantastic in getting customer insights.

    The cycle should be: Build -> Measure -> Learn -> Repeat [[1]](http://www.startuplessonslearned.com/2010/09/good-enough-never-is-or-is-it.html). Shorter this cycle, the better it is.

    However, a balance is important as always - avoid rabbit holes and know when to pivot. A VC-like mindset is often helpful. So be a coach for the team, encourage testing, but also encourage learning from others and to let go when tests *consistently* reveal negative results.

    At the same time, encourage the teams to be bold and bring in innovation from around the world, and not just constrain themselves to a specific sector. Every idea is worth testing.


In the end, there is no silver bullet solution, and you will need to review all of these in the context of your organizations. But I certainly hope that these may warrant a discussion within your leadership circles and help define a strategy that works for you.
