---
author: Aishwarya Singhal
comments: true
date: 2010-12-13 05:45:25+00:00
layout: post
slug: unit-testing-with-hsql
title: Unit Testing with HSQL
wordpress_id: 12
categories:
- J2EE
- Quality
- Unit Testing
tags:
- HSQL
- Junits
- Unit Testing
---

Ever wondered how you could increase the speed of execution of test cases that run against a database? Or how you could unit test without impacting the data in your database? The obvious answer to the latter is to use a seperate database schema, but speed? How about an in-memory database? See, now we are talking!

HSQL provides a means of running an in-memory all Java RDBMS, so everything runs in the heap. All you need to do is to include the JARs from HSQL website (no I wont give a link here, please use internet search :-) ) into the JUnit execution classpath, configure the datasource as jdbc:hsqldb:mem:mydatabase?shutdown=true. If you use Hibernate in your application, you can use the SchemaExport feature (with Spring over Hibernate, use session factory bean to create database schema) to create the tables et al in the database as well. Bingo, you have a new and shinny blank database schema in the Java heap to run tests against.

I had to write my own Oracle specific functions and register them with HSQL because people had used them in HQLs :-(. Anyways, its not difficult and all you need to do is to have a class with static methods that implement the required feature and run "CREATE ALIAS" SQL queries against the database. That's it, easy peasy!

Using HSQL, I was able to bring down test execution time from 1.5 hrs to 20 mins.
