---
layout: post
title: "God Objects"
date: 2008-12-15
categories: blog
---

If Only I Was Agnostic Towards God... Objects.

One thing that has always been a thorn in my side while programming is difficult code. I know each of us is guilty at one point or another. Certainly, we have all written a hack or rushed something out the door. Today I faced down a problem from the realm of the Anti-Pattern, the God Object. How they come about is a whole different discussion, what I am more interested in is ways of dealing with them.

**Test Cases**

 Test cases are going to be your best friend here. Reading the code will give you only a slight idea of what it does, the real value is in the test cases. You will want to have a look at all the tests you can find, as they will give you a very good idea of what exactly is going on. Everyone is going to want to refactor the class into the ground, but without proper tests, you will never know if it is going to ever work again.

**Improve Readability**

We need to make whatever improvements we can to the code without changing the functionality. We should be moving similar methods together if they are strewn haphazardly all over the place. Replacing useless variable names with something more meaningful. Enhancing or creating documentation in the code as you discover the functionality. Lastly, you may want to look at code folding or regions (.NET). I detest them because they are a solution that promotes a problem. However, they are still a solution.

Now we are ready for the next step and the real work. We want to understand what this god object does and how it does it. Know your enemy so to speak. Code tracing and document enhancing can be beneficial, but I want to recommend another technique all together.

**Take the code offline and break it**

Too often we get tied into the source repository and the idea that everything we write is valuable. Simply playing around with the code may not get you the new methods you need or help to clean up the class directly, but what it will give you is a better understanding of what the object is doing. Once again, the primary concern is learning as much as we can about the object so that we can break it apart properly.

**Incremental Improvement**

The goal should not be to fix everything immediately, the goal should be to fix everything while drastically improving upon it and maintaining existing functionality. If there are no tests, create them. If there are tests, add more. Cover as much as you can with test cases and understand what is going into those test cases. Then you can start dismantling the large class into more appropriately sized chunks. The easier the class becomes to work with, the easier it will be to refactor and work with in the future.

If that doesn't work.&#160; Then there is always [Conway's Law](http://en.wikipedia.org/wiki/Conway).
&quot;Organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations.&quot;
