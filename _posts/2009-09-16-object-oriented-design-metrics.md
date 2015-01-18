---
layout: post
title: "Object-Oriented Design Metrics"
date: 2009-09-16
categories: blog
---

I have had many discussions with colleagues and friends about the different things we value in software. Why we favor one thing over another, why we implement something a particular way, etc… However, I have also had numerous discussions with developers whose values differed drastically to my own. Arguably, many of these values can be subjective, and when we both reached that conclusion the argument became simply an expression of what we favor and why.

For example, how can you argue the value of something like the [single responsibility principle [pdf]](http://www.objectmentor.com/resources/articles/srp.pdf)? Ask them if they agree and call them an idiot if they say no? Ad hominem has hardly proven to be an effective argument technique. So what do you do to effectively introduce new ideas and argue their value when the other party just keeps asking why that has value?

The technique that has worked for me, in discovering why someone feels a certain way about a principle, is to break everything down to very basic parts that are nearly universally true and introduce your idea under those truths, explaining how it affects them positively. These pieces must be so small that to challenge them would signal the warning signs that the individual is ignorant of the subject matter or intentionally breaking it. In the case of the later, this gives you an ideal platform to challenge why the decision was made and why it is or is not valid. This is more than saying SRP is good because it improves code quality. You must get to the heart of everything, including code quality. And this is where I wish to begin, with OOD metrics that I feel are universally true.

The measure of quality software is more than simply achieving the list of requirements on a specification document. The design of the software itself is equally, if not more so, paramount to the overall quality of the software. In order to properly design complex systems we must have metrics by which to judge that design. These metrics should be so fundamental that they appear to be common sense.

**Robustness**

Every good programmer wants to produce software that is correct, which means that the program produces the right output for all the anticipated inputs in the program’s application. In addition, we want software to be _robust_, that is, capable of handling unexpected inputs that are not explicitly defined for its application. For example, if a program is expecting a positive integer and instead is given a negative integer, then the program should be able to recover gracefully from this error. A program that does not gracefully handle such unexpected-input errors is not robust and can be embarrassing for the programmer.

**Adaptability**

Modern software projects will typically involve large programs that are expected to last for years. Software, therefore, needs to be able to evolve over time in response to changing conditions in its environment. These changes can be expected, such as gradual hardware improvements, or they can be unexpected, such as new requirements. Software should be able to adapt to unexpected events that, in hindsight, really should have been expected. Thus, another important goal of quality software is that it achieves adaptability.

**Reusability**

Going hand in hand with adaptability is the desire that software be reusable, that code should be usable as a component of different systems in various applications. Developing quality software can be an expensive enterprise, and its cost can be offset somewhat if the software is designed in a way that makes it easily reusable in future applications. Such reuse should be done with care, however, for one of the major sources of software errors can come from inappropriate reuse of software. This means software must also be clear about what it does and does not do. From this clarity, however, software reuse can be a significant cost-saving and time-saving technique.
