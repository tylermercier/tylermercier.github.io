---
layout: post
title: "Method Exit Points"
date: 2009-02-02
comments: false
categories: blog
---

Method exit points are important in many ways. Under the assumption that multiple entry (goto) is not even worth talking about, the focus is on where you exit your method.

When going with a Single Entry, Single Exit you get a few advantages. First, you know that the full length of the method will always be followed. In older languages, this is a good thing. With newer languages, not as much of an issue. Regardless, closing out or handling things the exact same way each time can be quite useful. This can make things safer as you won't be exiting at midway through a method when a file was not closed properly or exception handled. It also allows you to follow the return value through the full scope of the method which can give you a better idea of what each point is returning.

Single Entry, Multiple Exit can lead to more clear and readable code. The best practice is to assume failure and prove otherwise. This leads towards building guard statements with immediate returns, rather than building an onion backwards with condition statements. It also doesn't carry any unnecessary baggage. The check failed? Then why continue?
