---
layout: post
title: "Objective-c Inheritance & Message Passing"
date: 2010-03-29
comments: false
categories: blog
---

Came across an interesting result while overriding a base class last week. Assume we have a class with two methods, one overloading the other as follows.

```
- (void)create:(int)id {
  // implementation
}

- (void)create {
  [self create:12];
}
```

Assume both methods are defined within the interface (intentionally public). Now when we&nbsp;inherit&nbsp;from this class and override the first method (create:id), where does the "create:int" message in the second method get passed too? It is calling "self" from the context of the parent, but we just overrode the method in the child.

```
Child *childInstance = [[Child alloc]init];
[childInstance create];
```

Given the above, where does the message go? Will it call create:id on the child or the parent?

Turns out, it is all in what you declare within your interface for the child. Define

```
- (void)create:(int)id;
```

in the child interface and it will pass the message to the child (using your override). Don't and the message will instead go to the parent. Thought it was very curious behavior as a C# guy.</div>
