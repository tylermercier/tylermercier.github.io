---
layout: post
title: "Object-Oriented Design Basics"
date: 2009-10-22
categories: blog
---

In order to achieve each of the metrics defined [previously](http://www.codecuriosity.com/2009/09/object-oriented-design-metrics.html) we can employ some very fundamental techniques. Techniques that should appear to be common sense, hopefully. Though broad in scope and concept, they are the basis for much of what we currently try to achieve in programming.

**Abstraction**

The notion of abstraction is to distill a complicated system down to its most fundamental parts and describe these parts in a simple, precise language. Typically, describing the parts of a system involves naming them and describing their functionality. For instance, take a design pattern such as the [Abstract Factory](http://sourcemaking.com/design_patterns/abstract_factory). When I use this pattern, declaring its name in the class definition, I am telling the next programmer what this class is supposed to do without documentation and without comments. When I declare some class called, CarFactory, a programmer should know that an instance of this class with provide instances of Car objects.

**Encapsulation**

Another important principle of object-oriented design is the concept of encapsulation or information hiding. Encapsulation means that different components of a software system should not reveal the internal details of their respective implementations.&#160; In general terms, the principle of encapsulation states that all the different components of a large software system should operate on a strictly need-to-know basis. There is a common saying surrounding this, “TELL, DON’T ASK”.

One of the main advantages of encapsulation is that it gives the programmer freedom in implementing the details of a system. The only constraint on the programmer is to maintain the abstract interface that is visible. Encapsulation aids in adaptability because it allows the how to change without altering the expected outcome.

**Modularity**

In addition to abstraction and encapsulation, a principle fundamental to object-oriented design is modularity. Software systems typically consist of several different components that must interact correctly in order for the entire system to work properly. Keeping these interactions straight requires that these different components be well organized. In the object-oriented approach, this structure centers around the concept of modularity, which refers to an organizing structure in which different components of a software system are divided into separate functional units.

The structure imposed by modularity helps to enable software reusability. If software modules are written in an abstract way to solve general problems, then modules can be reused when instance of these same general problems may arise under a different context.
