---
layout: post
title: "IPhone Development Guide"
date: 2010-03-02
categories: blog
---

Just a collection of information and useful advice that I have collected. Hope this helps you get started.

Start [where I started](http://icodeblog.com/2008/07/26/iphone-programming-tutorial-hello-world/) doing something simple _hello world_ type examples. All of the [icodeblog](http://icodeblog.com/) tutorials are worth doing if you are starting out (though watch out for the SQLite ones as Core Data replaces that now). Try this [one](http://icodeblog.com/2008/07/29/iphone-programming-tutorial-beginner-interface-builder-hello-world/) to get a feel for interface builder and this [one](http://icodeblog.com/2008/07/30/iphone-programming-tutorial-connecting-code-to-an-interface-builder-view/) next for tying the code into IB. It can take a little while to learn the name of the different controls you will be using. This [tutorial](http://icodeblog.com/2008/10/13/iphone-programming-tutorial-using-tabbarview-to-switch-between-views/) is on one of the navigation controls, the **[UITabBarController](http://devworld.apple.com/iphone/library/documentation/UIKit/Reference/UITabBarController_Class/Reference/Reference.html)**, which visually rests on the bottom of the window and will be one of your staples.

Cocoa has a learning curve of its own, get up to speed on [Key-Value Coding](http://theocacao.com/document.page/161) (further [reading](http://cocoawithlove.com/2010/01/5-key-value-coding-approaches-in-cocoa.html?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed:+CocoaWithLove+(Cocoa+with+Love)&amp;utm_content=Google+Reader)), the framework makes use of many dictionaries. There is also a good post (with even more links) on the [MVC Model](http://www.bit-101.com/blog/?p=1969) used on the iPhone. It differs slightly from other representations of the Model View Controller pattern.

![Model-View-Controller design pattern](http://developer.apple.com/mac/library/documentation/General/Conceptual/DevPedia-CocoaCore/Art/model_view_controller.jpg)[_source_](http://developer.apple.com/mac/library/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)

The primary difference is in the behavior between the different flows back to the view. On the iPhone, only your controller should be interacting with the [UIView](http://developer.apple.com/iphone/library/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html) where as traditionally it is acceptable for the Model to have some interactions (Notifications or checking state).

[](http://www.bit-101.com/blog/?p=1969)
 Matt Gallagher’s [blog](http://cocoawithlove.com/) is probably something that you want to [subscribe to](http://feeds.feedburner.com/CocoaWithLove). A few of my favorites:

*   [The design of an iPhone application](http://cocoawithlove.com/2009/12/design-of-iphone-application.html?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed:+CocoaWithLove+(Cocoa+with+Love)&amp;utm_content=Google+Reader)*   [Quality control without unit tests](http://cocoawithlove.com/2010/01/high-quality-in-software-development.html?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed:+CocoaWithLove+(Cocoa+with+Love)&amp;utm_content=Google+Reader)*   [Application with unit tests](http://cocoawithlove.com/2009/12/sample-iphone-application-with-complete.html?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed:+CocoaWithLove+(Cocoa+with+Love)&amp;utm_content=Google+Reader)*   [Objective-C’s niche](http://cocoawithlove.com/2009/10/objective-c-niche-why-it-survives-in.html?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed:+CocoaWithLove+(Cocoa+with+Love)&amp;utm_content=Google+Reader)
