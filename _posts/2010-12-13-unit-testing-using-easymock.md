---
author: Aishwarya Singhal
comments: true
date: 2010-12-13 05:42:33+00:00
layout: post
slug: unit-testing-using-easymock
title: Unit Testing Using EasyMock
wordpress_id: 8
tags:
- J2EE
- Quality
- Unit Testing
- EasyMock
- Junits
- Unit Testing
---

One of the most frustrating problems I have faced over years is around how to test just the unit of code I am interested in. The problem is aggravated by the fact that many a times my unit tests actually depend on the environment (data/ system settings). So my unit tests don't actually test units, do they?

I came across something called MockObjects way back in 2004, but even though we used it extensively then, I always found it a bit troublesome to use, one of the reasons why I did not use it much in the following years. I had heard about EasyMock over the years, but did not quite use it until recently. And hey, its the most amazing thing i have used in years! After Hibernate of course :-)

So whats so cool about EasyMock? One, you don't have to write a separate class called MockBlah to mock up Blah. EasyMock uses CGLIB proxies to create mocks on the fly! By default, you can only do it for interfaces, but with its class extensions, it can be done for classes as well.

Secondly, you don't need to tell EasyMock exactly what parameter value to expect going into a method, just give it the class type (`EasyMock.isA(...)` or `EasyMock.anyInt(...)`) and it will work for any object of the given type.

Thirdly, you can simulate exceptions by expecting method calls to throw exceptions. So you don't need a database dead lock or insertion failure to see how your code will behave in a case like that, just throw a SQLException from the interacting method's expectation.

Plus, you can stub method behaviours using the `Answer` functionality. Grab a hold of the parameters passed into a method and play with them - return whatever you expect, or set values in the passed objects. Brilliant, isn't it ?

What this means for me is that the JUnits are no longer data/ environment dependent, so there's no real set up and tear down needed. The test cases are now fantastically fast as well -I don't interact with the system and worry only about my Java code now. I also don't need to test on large and useless data sets, I create different types of data in my test cases so as to cover my code execution paths. Data independence, fast execution times and an ability to achieve a higher code coverage.

Read more about EasyMock at [http://www.easymock.org/](http://www.easymock.org/)
