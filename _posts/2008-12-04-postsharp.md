---
layout: post
title: "Postsharp"
date: 2008-12-04
categories: blog
---

[Postsharp](http://www.postsharp.org/) is an AOP centric logging library. The creator, Gael Fraiteur, provides a demo walkthrough. In it, he explains that you need to start with adding a reference to PostSharp.Laos and PostSharp.Public. The sections for logging are flagged by a [Trace] attribute above each method or just at the class level, which I thought was pretty convienent. Finally you need to define the Method Boundary logging behavior, which seems where the most tinkering would be spent. I will certainly be playing with this more in the future.

Here is a link to the open source user samples.
[http://code.google.com/p/postsharp-user-samples/](http://code.google.com/p/postsharp-user-samples/)
