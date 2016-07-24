---
published: true
title: Don't turn your unit tests into integration tests
layout: post
---
It's a common issue to use tools that aren't very mock/stub friendly. In these cases it's easy to fall in the trap of abandoning unit tests for integration ones. This post will analyze the impact and how to overcome this problem.  

## Rapid feepback loop
 TDD and BDD require a rapid feedback loop, you need a suit of tests that will provide you information in a timely manner about the correctness of your code. When an external service is required or even a service running in a docker process, the net latency is introduced into every remote call which will cause a noticeable impact on your suite performance wasting precious time.  

## Line ruid
 The worst con you'll see is unexpected behavior. In fact this is so bad it may entirely defeat the purpose of testing. Calling a a hot service will make your test suite subject to network outage, dns failures and a myriad of other problems.

## Help Mock-wan, you're my only hope
 The interference of external variables on the test suite should be minimal and mocking is the best way to insulate your application. When dealing with tools that don't support it as first-class citizen, build wrappers to allow mocking and stubbing to take place.

