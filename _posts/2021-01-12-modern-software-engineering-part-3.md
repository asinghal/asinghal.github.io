---
author: Aishwarya Singhal
comments: true
layout: post
title: Modern Software Engineering - Part 3 - Designing the organization
tags:
---

Typical IT organizations have evolved into having multiple layers of managers. Some of that is because organizations try to reduce their risk by having more managers reviewing the work being done. Some is because the growth model only supports growth as managers, and hence everybody grows into a managerial role sooner or later, leading to a pyramid of people that are primarily in supervisory roles. Many organizations have as much as 50% staff in supervisory/ managerial roles. Simply speaking, only 50% of the staff is involved in actual production of software. Basic economics implies that typical overheads (or SG&A) in an organization should be about 20-25%. Shouldn't the same logic apply to IT teams too? 

Another aspect here is that complex organization structures lead to a lot of meetings that wastes productive time.

At the same time, there is the question of quality being delivered and the trust between different teams. Often, we see a "handover" mindset in most teams - they deliver their part, and then any issues found are to be fixed by the team that comes next in the chain. More often than not, the end-user's perspective is ignored and forgotten, and teams focus more on covering their backs than on doing the right thing for the user.

Let's look at all these aspects through various enabling mechanisms.

1. **Aligned goals and metrics**

    A key aspect of ensuring quality in deliverables is that there is a common definition of quality across the organization. Most teams fail to recognize this, and we see different metrics being used by them. So, while a sales team might be tracking revenue, or customer service team might use Average Handling Time (AHT), the IT team enabling that might still be measuring the number of code releases, or bugs. Now clearly, there is much more than goes into enabling high revenue or low AHT than the software, and there are a lot of IT specific aspects developers need to care for, but that does not mean that the software developers do not have a view on these business metrics.

    It is vital that everybody uses one language and common metrics across the organization. My most impactful stories have been from situations when my teams took the end-user view and partnered with the stakeholders to ensure that the end result was beautiful. Magic happens when developers and business teams collaborate on achieving common goals.

    One simple example - we had a feature request to enable printing of VAT invoices for customers, and the developer on my team had already implemented it. However, he did not look happy. I walked up to him to find out why, and I saw him with a printout of an invoice and an envelope. He was upset that the printed customer's address did not fit in the center of the address cut-out on the envelop. He did not have to do that test, but he went out of his way, fetched an envelope, printed and folded the invoice, and checked if it will work.

    On the other hand, I was in a team for a large company whose main business was through online sales. Their website crashed, and it had been down for 2-3 days. We were parachuted in as external experts to rescue and fix. At 5 pm, the developers picked their bags and were leaving. We asked the lead developer if he could help debug the issue and he refused - it is the job of the support team and they need to manage it. Now it was late, so I get his point-of-view. However, in such a situation, I would expect an all-hands-on-the-deck type mindset.

    The disconnect between software developers and business goals is sometimes shocking.

        Most successful set ups are where all software teams have a business leader who is committed to enabling success and is not just a stakeholder. These business leaders also have sufficient say in the system, typically a direct line to company's leadership. And in such cases every software team is directly responsible for their impact on the business metrics.

    There will be IT specific metrics that the developers need to track, but they also need to have a keen view on the business goals.

    I recommend having large screen monitors (that show both business and IT metrics) next to where the developers sit, and I recommend that the teams include the business metrics in their performance reports at least once a month.

    *However, you do not need to over-engineer this. You do not need to track business value or cost per feature. A meta level view is just fine. The goal here is to establish better quality via ownership and awareness, and not to bring in an accounting overhead.*

2. **Product and platform, not project teams**

    Many organizations work in an outsourcing model even with their internal IT teams. The business team creates a project, gives it to the IT team, and then the IT team has the responsibility to deliver. As expected, this helps optimize the costs (*maybe*) but erodes quality and trust.

    The issue here is that most organizations have one model for day-to-day functioning and for mentoring and reporting. This does not have to be. 

    It is important that organizations drop the notion of projects and move towards products. Now "product" has a specific connotation in most organizations - however, we are not talking about the product that you sell to your customer. We are talking about the *"software product"* that will enable that sale. Although you may sometimes align software product teams with actual products that will be sold to the customer.
    
        The difference between a product and a project is that the latter has an end date. It is important that there are product teams that take an end-to-end view on a product, and not a tactical view on enabling a feature/ few features. This enables an improved view on quality and ownership in the teams. This also enables an easier way to align KPIs/ OKRs with the business teams.

    An easy way to create product teams hence is to follow the business metrics and their responsible business leaders. So, sales may warrant a developer team, customer service might warrant another, and logistics might need yet another. All of them may warrant multiple teams, depending on the number of metrics and business leaders.

    Another interesting tactic is to allow each business area to have a budget for software development and let them allocate it to each product team based on the latter's performance in their QBR presentations. This drives collaboration between the business sponsors and the product teams.

    When you have multiple product teams for a common business area (e.g., sales), you just need all product owners to collaborate with the same business responsible person.

3. **Your organization structure does not need to reflect your IT architecture**

    Many IT teams adopt a n-tier architecture, which is composed of different layers. Many of them model their organizations to align with the architecture too - there is a frontend team, a middleware team, a backend team, etc. etc. This leads to a large number of dependencies (and bottlenecks) across teams, and also a lack of end-to-end ownership.

    In my experience, the most effective model is when organization structure does not replicate the IT architecture. In such cases, there are product teams with *end-to-end* responsibilities, and platform teams that enable the product teams with tools and frameworks.

    The platform teams, or as we alternatively call them - IT-for-IT, are deeply technical teams that develop tools and frameworks. Think of these teams as R&D or enabling teams, whose customers are the product teams, and whose primary responsibility is to bring in efficiency and innovation. These are extremely important, and the product owners for these teams need to directly report into the IT leaders.

    Although we call these platform teams, they should not be centered around specific technical tools, e.g., a Salesforce team, or a SAP team. Salesforce experts, or SAP experts, should be embedded in the right product team.

    In some cases, the work required is too much to be handled within one "full stack" team. In such cases, there are 2 options, viz., a) take thinner slices of work so a lean team with end-to-end responsibility can still work, or b) divide the teams based on 1-2 layers such that they still have a business significance (e.g., one team does everything until API-enablement, and other prepares frontend and integrates the APIs). The second option is less preferred, and as much as possible, end-to-end ownership should be ensured.

4. **More [pigs than chicken](https://en.wikipedia.org/wiki/The_Chicken_and_the_Pig)**

    You need more people that have their skin in the game than those that are just supervisors or advisors. My typical assessment works on the following lines:

    * Anybody who is not actively building or maintaining a product, nor takes an active part in defining the requirements, is an overhead. This includes all advisory roles - security, privacy, architecture, coaches, etc. etc.
    * Anybody spending more that 50% of their time in meetings is an overhead
    * The total number of **overhead roles should be less than 25% of the total organization**. So, if the IT team is 100 people, at least 75 of them must be actively building the product

        A simple way to start is to de-layer the organization. A product owner should have a direct reporting to the business leader responsible for that area, and all developers work directly with the product owner and the tech lead, and all tech leads work directly with the IT leader (CIO/ CTO/ VP/ ...). Cut down on all other managerial layers, and clearly define roles and responsibilities for every role

    Ensure that the Product Owner comes from business team's perspective and is responsible for writing clear requirements, and for verifying the implementation, and the Tech Lead is a senior developer with >80% time dedicated to coding, and remaining time for mentoring the team.

    Automate all non-value adding tasks, and simplify what cannot be automated, e.g., coordinator functions, where someone is only responsible to raise a ticket or act as a SPOC for communication. Another example is replacement of manual QA work with automated tests as much as possible.

    As an example, all advisory roles could be staffed on product teams as needed and would be expected to have an acceptable utilization rate.

    Typically, such an exercise frees up between 15-20% of capacity that can then be reallocated to value adding roles. The freed-up people are also very talented people in wrong roles, and normally >95% of them can be reallocated (and will be interested) for further value creation. Some might need a bit of training and investing into them brings out magic. Congratulations, you just created a significant productivity boost (through saving and reallocating).

    At the same time, as a word of caution, do not go overboard with this idea. Many of the advisory teams are often understaffed and underappreciated. In some cases, having SPOCs helps product owners and business leaders to maintain their sanity, especially when it comes to managing vendor relationships. You may still need some manual QA. Similarly, all organizations do require managers, so trying to move towards a near zero managerial capacity will be an absolute disaster. While it is important to chart out an ideal picture, it is also important to then apply a prudent lens and ensure that the model will work in your context.

    [A study at Google](https://rework.withgoogle.com/print/guides/5721312655835136/) indicated that the most effective teams are the ones where team members feel psychological safety and have structure and clarity. I recommend keeping this as the underlying thought when designing the organization.

5. **2 pizza box teams**

    This concept came from Amazon and is almost an industry standard now. The idea is that the team is small enough to have a healthy collaboration and can work together as a SWAT team to deliver towards a common goal. My recipe for typical teams is: 1 Product Owner, 1 Designer, 1 Tech Lead, 4-5 Developers, 1 QA, and 1 Advisor. The designer and advisor role may be fulfilled by different people at different points in time of a product release, based on the need. E.g., there may be a UI designer at 50% and UX designer at 50%, or 50% of architect, 20% of security, and 30% of Subject Matter Experts/ coaches. Some of these may be shared across different teams. So, there are 7-8 dedicated team members, and 2 that are floating. The reason why I would count the floating also into the team is because these need to be in the stand-ups and need to be accountable for the quality of delivery (i.e., they need to be pigs, and not chicken).

    In special cases, depending on the complexity and (lack of) maturity of the organization, some teams may also have a Business Analyst/ Junior Product Owner, someone that helps the product owner by taking up some of their responsibilities.

6. **Functional vs Reporting structures**

    One important clarification to be made here. Everything above talks about how the teams should operate, and not where they should report. The IT team members should continue to report into the IT leaders, so that their career growth, learning and mentoring can be shaped by leaders that understand the field.

    The product teams should have a dotted line reporting to the business leaders, and the feedback on their performance should be evaluated based on their performance in that context.

    Another thing to note here is that **this does not mean that the IT leaders report into their business counterparts.** Both IT and business leaders need to have a top level reporting into the company leadership. This is necessary to ensure that the organization does not always prioritize tactical goals over technical excellence and innovation.

    This model ensures that the business leaders do not need to worry about the mentorship of technical teams, and the teams get guidance and support from leaders that understand the space. At the same time, the technical teams are focused on generating business value for the organization.

7. **Chapters, or communities of practice**

    A final missing piece here is knowledge sharing. It is important that teams share their work for 3 reasons:

    * It enables consistency of implementation across the organization. People have an ability to challenge each other every time they spot an inconsistency. This in turn helps with cost optimizations via prevention of fragmentation and avoidance of duplicate costs
    * It enables learning within a community of similarly skilled colleagues
    * It helps identify training needs for specific skills

    Spotify has [Guilds and Chapters](https://blog.crisp.se/wp-content/uploads/2012/11/SpotifyScaling.pdf); many other organizations have [communities of practice](https://en.wikipedia.org/wiki/Community_of_practice). It is vital to encourage creation of similar *virtual* structures and ensure that they are exchanging knowledge on a regular basis. So, the community needs to appoint a leader, and that leader should regularly share their observations with the IT leaders. Note that this is not a dedicated role, but an additional responsibility for an existing team member.

    This has an interesting side-effect: it enables a different growth model in IT compared to traditional ones. Developers *can remain* developers and still grow (in responsibilities and financial sense) without taking up managerial roles.

```
As always, there is not just one answer for organization structures. Different models work for different set ups, and it is important to understand the context you operate in, and what works in that context. Similarly, the size of an organization can play an important role in defining the feasibility of some of these measures. What works for a 50-member team may not work for a 5000-member organization. Finally, culture and team maturity play an important part in defining the model. At the same time, the principles remain broadly the same, and as long as one can define an execution model that works in their context, it will enable a significant productivity and quality boost in the output.
```

So how do we solve for large organizations? Well, for one, there are a number of standard frameworks and methodologies. I hear [SAFe](https://www.scaledagileframework.com/) is the most famous. I am personally uncomfortable with any "one-size-fits-all" solutions, so I would recommend evaluating the options based on your context and devising an execution mechanic that works for your organization.

Finally, at the heart of all these tips is the intent to simplify (reduce complexity). Anything that increases overheads or complexity *in the long term* must be challenged and re-evaluated for fit in your context.
