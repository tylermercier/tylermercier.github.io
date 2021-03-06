---
layout: post
title: "Tell, Don't Ask"
date: 2012-08-07 15:15
categories: blog
---

I have been *asking* quite a few of my colleagues to *tell* me what "Tell, Don't Ask" means to them. Mostly we agreed on a definition similar to what is below, but there was enough discrepancy to warrant a blog post. My definition is as follows:

>TELL things what you need, don't ASK them for information

In more detail, this means is that you should not be interrogating the state of other objects to make decisions. It is better to tell a module what you need and let the module sort out the logic. This helps to keep the module encapsulated and reduce the amount of coupling your code will have to the module. A real example drives home the point much better than any description. Below is a violation of Tell, Don't Ask.

```coffeescript
class Car
  constructor: (@doors) ->

car = new Car(4)

if car.doors > 2
  alert('Higher insurance!');
```

## The Problem

Most of us have written code like this and will continue to do so. In a small example, such as this, the problems introduced are relatively minimal. However, there are problems and primary among them is coupling. Simply put, coupling is the degree to which each part of the code relies on another part. High coupling becomes a problem when we want to change the structure of the code.

What does this look like when we remove the violation?

```coffeescript
class Car
  constructor: (@doors) ->
  isSporty: -> @doors > 2

car = new Car(4)

if car.isSporty()
  alert('Higher insurance!');

```

## The Solution

Coupling has now been reduced. Make no mistake, our change does not remove the reliance entirely, as a change in the **car** would still impact our code. What we have done is manage that coupling through a better separation of concerns.

In the violated example, the code that is coupled is deciding on state it does not control. Because the class does not control the state, we should push the decision making into the class that does. This helps to separate the concern (state logic) from the class we are working in and prevents it from being duplicated in the future.
