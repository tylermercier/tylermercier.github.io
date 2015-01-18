---
layout: post
title: "ReSharper"
date: 2009-04-04
categories: blog
---

Figured I would put a serious effort behind learning how to use more of the ReSharper features and gain a better familiarity with it. I am also using the latest 4.1 build and the first thing I noticed was recommendation to use implicitly typed local variables everywhere. I like having access to implicit variables and truely enjoy programming in python because of duck typing. However, I in no way condone switching any variable in an explicitly typed language over to implictly typed just because it has support for it. Use interfaces and proper structured code, don't cheat with passing var's or using var's just because you don't have to go back and rename a variable. That is what ReSharper is for.

Fortunately, this is quickly turned off by selection Resharper Options and under the Code Inspection section select Inspection Severity. Under Code Redundancies go down to the bottom where it says, Use 'var' keyword when initializer explicitly declares type and toggle it to off.
