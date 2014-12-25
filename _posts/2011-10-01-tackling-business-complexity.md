---
layout: post
title: "Tackling Business Complexity"
date: 2011-10-01
comments: false
categories: blog
---

This week at a client site, one of our stories came back from the dead because some condition wasn't handled. As we were implementing the story, our understanding increased and along with understanding came new questions. After asking these new questions, it became clear that there was a lack of holistic understanding for the both the developers and the business. The developers wanted a rationalized set of conditions, the business wanted things to be displayed in different ways when certain conditions were met. Basically, we wanted the same thing, but could not meet on a common language.

The thing we could agree on was what parts were important, so I came up with the idea of producing a truth table to hash out the different combinations. It looked a lot like the image below.

override | mapped | mappedByParent | mappable
- | - | - | -
T | T | T | T
T | T | T | F
T | T | F | T
T | T | F | F
T | F | T | T
T | F | T | F
T | F | F | T
T | F | F | F
F | T | T | T
F | T | T | F
F | T | F | T
F | T | F | F
F | T | T | T
F | T | T | F
F | T | F | T
F | T | F | F

After creating the table, it was a matter of going through each combination and recording what expected result should be displayed. This produced five potential outcomes that turned out to be relatively simple to handle.

```
if (overriden) {
  // override condition
}
if (mapped) {
  // mapped condition
}
if (mappedByParent) {
  // mapped by parent condition
}
if (mappable) {
  // mappable condition
}
// default condition
```

Looks almost too easy right? I'll assure you that the vernacular of the story did not cover the problem in such logical terms. The distillation of these guard statements (each condition returned) was a direct result of the truth table. Had we gone with a more classical approach, it would have likely resulted in a fair bit of cyclomatic complexity or the introduction of more classes to tackle this problem through polymorphism.

As it turned out, we wrote some tests, wired everything up and it worked just like the BA wanted, but could not logically define.
