---
author: Aishwarya Singhal
comments: true
layout: post
title: Decomposing Complexity
tags:
---

Over the years, I have come across various software engineering projects that were deemed complex. When you are faced with complexity, the question we are inevitably faced with is if its worth pursuing the solution (will it yield the expected ROI), or should the idea be dropped and alternatives explored.

To start with, lets differentiate between complex and impossible. Complexity can be solved, given time and investment. If something is impossible, its because it depends on severe technical limitations that are not easy to solve in forseeable future. Technology evolves, and the impossible of today can move to being easy or complex in future. But, in this article, we will only look at problems that are complex - i.e., they can be solved with available means and technologies. 

> “The definition of genius is taking the complex and making it simple.” - Albert Einstein

As a word of caution, I do not aspire to provide any silver bullet answers here, but rather provide an understanding that enables you to ask the right questions *in your context* and come up with appropriate solutions. 

So what makes something complex? I believe that complexity has 3 main dimensions.

1. **It involves a lot of effort or investments**: These are problems we know how to solve, but its just a *lot* of work or you can buy the solution but at a very high price. It is also context specific. What may be a lot of work for a start-up may be perfectly acceptable for a larger team.

    In any case, this can be tackled with appropriate prioritization and scope management. It is much easier said than done though, and a lot of teams struggle to define that they *really* need in a Minimum Viable Product (MVP). In a recent example, I witnessed a MVP being built for 5 years (and its not ready yet). It is painful nevertheless vital to define the right scope of work.

    In some cases, it may not be easy to prioritize, specially if it involves rewriting or replacing an existing system. In such cases, a side car approach may work better. Build a fake or parallel system, and start migrating topics one by one.

    Obviously, a large effort can also be handled by adding more people to the team. However, larger teams need more processes than smaller teams and can sometimes be slower, so there is a fine balance to the maximum team size that will be effective in a certain context.

2. **There is a huge risk of quality**: This is a wider topic. Some things are easy to implement, but are too risk prone. The best way to work with such cases is to break down the problem into smaller components that reduce the risks as much as possible.

    But doesn't everything have a quality risk? Perhaps. It is important to understand what is acceptable risk in your context and educate your team on it. You do not need to safeguard against every possible risk, especially if the probability of it materializing in your context is small.

    To understand this topic better, lets break it down further into 3 situations that lead to such risks.

    a) **There are a lot of unknowns**: The solution requires components or technologies that the team is not fully familiar with, or some of the requirements can not be completely defined yet. 

    It is extremely important to map out all the unknowns and actively work towards reducing the ambiguity. It is also important to avoid the unknowns as much as possible and find reasonable solutions using unknown techniques. In most cases, if a requirement is unclear, it is unlikely to create a significant value for the overall solution.

    Also, many times people try to solve problems by themselves and do not ask for help. It is important that teams discuss bottlenecks and complexities together, and try to find relevant expertise to help with the solution.

    b) **There are associated business risks**: and the tolerance for errors is extremely small. Most of the times, the risks are overstated. It is important to understand the risks, and add metrics and measures to know when they materialize. These may require more than normal diligence and validations, and build mechanisms to mitigate these risks when they do materialize.

    c) **It is difficult to validate a solution**: perhaps because it involves a lot of permutations of test data that is not easy to generate, or it addresses very special cases that are not easy to create on a test environment. 

    This type of complexity is the hardest to address, and requires a judgement based on the context. It is not impossible, it just needs the team to use pragmatic workarounds to generate confidence in the solution.

    > It is perfectly OK if the solution that comes out is not the most elegant one from a software engineering point of view, as long as it is easy to understand and maintain.

3. **There are dependencies beyond our control**: Many problems can not be solved by individual teams, but rather require a cooperation between many. 

    > The key to success here is a clear mandate from the leadership team.

    These can be of few types.

    a) **There are skills needed from different teams**: This is primarily a staffing challenge as you need to assemble a team of individuals that have the right skills to deliver a solution. Co-located team members with a common guidance around the project's objectives are most effective in such a setting.

    b) **There is a dependency on other teams/ providers to implement parts of the solution**: This is more complex. Each team needs to prioritize the change according to the needs of the overall project, and requires a great degree of transparent and clear communication. Complexity increases many fold as the quantum of change required of each team increases. There are unfortunately no good answers in such a situation, but teams can work with defining interface contracts between their components, and building solutions against temporary stubs until the dependency is resolved.

    c) **There are process complexities**: Many a times, the complexity in a project comes from process complexity. It is key to identify such complexities upfront and discuss relevance/ workarounds on a case-to-case basis. Many processes are a hangover of past issues, and should be re-evaluated from time to time.


To summarize, when you come across something complex, you can look at the following questions:

1. Can I break down the problem into smaller more manageable problems and still get some value?
2. Can I simplify the ask?
3. Can the complexity be significantly reduced by a mandate from the leadership team?

I am curious to hear how you resolve complexities in your organization. Please share your thoughts in the comments below.