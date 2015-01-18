---
layout: post
title: "30 Days of iPhone Development"
date: 2010-02-23
categories: blog
---

Having programmed professionally in C# for the last four years, something new was certainly welcome. I decided to give objective-c a month before really expressing my opinions of the language, so it doesn’t come off as, “I hate it, it isn’t what I am familiar with”. Since I have done objective-c almost exclusively for the last month, so give me some credit.

**The IDE**

[Xcode](http://developer.apple.com/tools/xcode/) described in one word would be, _sufficient_. It gets the job done and if you are running Snow Leapord version 3.2 is a bit better than 3.1.2 (Leapord) that I am running. The differences are minimal though. My major gripes are that xcode uses something called “groups” which look like folders, but are not. You can “group” your code into actual files and they will look the same, but you have to do that on the command line (or Finder), which is a bit unexpected. So assuming you didn’t know that and had been working on a project for a while it could look something like this.

[![Picture 1](http://lh6.ggpht.com/_VrsVJGFhz4c/S4TCpqBDzoI/AAAAAAAABvY/5CFPqRvNMjE/Picture%201_thumb%5B10%5D.png?imgmax=800 "Picture 1")](http://lh6.ggpht.com/_VrsVJGFhz4c/S4TCpMJNpxI/AAAAAAAABvU/-qMlZuFl_-M/s1600-h/Picture%201%5B14%5D.png) [![Picture 2](http://lh4.ggpht.com/_VrsVJGFhz4c/S4TCtdda0wI/AAAAAAAABvg/J9c0y8Oca5A/Picture%202_thumb%5B6%5D.png?imgmax=800 "Picture 2")](http://lh4.ggpht.com/_VrsVJGFhz4c/S4TCrPo3vNI/AAAAAAAABvc/jUhicZg0iGM/s1600-h/Picture%202%5B10%5D.png)

Bit disappointing to see that mess when you assumed you had created some sort of order in all the chaos. Also, files are not listed alphabetically. You can have .m files listed before the .h or after. Whatever strikes your fancy.

**The Debugger**

I don’t really mind the debugger and it can be really helpful for… well… debugging. It’s good, honest. However, Xcode loves putting everything into its own window, so the debugger is not on the same page as your coding window (akin to eclipse). This is done so things like console output, stack trace and variables in scope can be displayed, but it still feels vastly inferior to the Visual Studio debugging experience where that kind of information is pulled in during debugging, but context remains the same.

Also, whoever decided the break points needed more than one state needs to be shot. Seriously, why would I want a breakpoint that the debugger won’t enter? There is undoubtedly some way to change this, as the forcing save alert before running and undo alerts can be done away with, but I have not found it yet. In the meantime, it means I need to add breakpoints and re-click them if I start coding and need to debug the same piece of code again. You know, try something, debug, it fails, try something else, debug the new solution.

Note: Undo trick is in user defaults.

_defaults write com.apple.Xcode XCShowUndoPastSaveWarning NO_

**Header Files**

Having little real experience with C/C++, header files are not something I have ever really had to worry about. All I can say is they are huge waste of time. People complain about unit testing, but these are worse and with none of the benefits. I understand why they have to be written in C/C++, but the thing is you don’t even need them in objective-c. They are there to prevent warnings and give guidance on how to use your code. Essentially nothing is private, so you have to be careful what you show (hence header files). Below is an example of a “public” method called **logMySimpleString.**

```
#import <UIKit/UIKit.h>

@interface MyClass : NSObject {
	NSString *aSimpleString;
}

- (void) logMySimpleString;

@property(nonatomic, retain) NSString *aSimpleString;

@end

@implementation MyClass
@synthensize aSimpleString

- (void) logMySimpleString {
	NSLog(@"%@", aSimpleString);
}

@end
```

Objective-c 2.0 includes support for auto properties, you can see one declared above. Aside from how obviously useless the header file is, look at the **three** places I have to reference aSimpleString to have an autoproperty. While nicer than writing the getters and setters by hand, it still introduces a lot of repeat code that offers very little value.

**Templates and Customization**

Finally, more of the positive! Templates for files and projects in xcode are pretty easy to accomplish. This [post](http://blog.highorderbit.com/2009/03/15/customizing-xcode-cocoa-touch-file-templates/) covers it pretty well, but if you are familiar with ReSharper templates, they are almost as easy and certainly the same fashion. You have to put them into an Xcode/user directory which is unique for iPhone SDK elements (see below).

/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/File Templates

To its credit, most of Xcode is pretty customizable with really good short-cuts. You can define your own in preferences.

[![Picture 3](http://lh4.ggpht.com/_VrsVJGFhz4c/S4TCvBAD4dI/AAAAAAAABvo/ac2dhucen-E/Picture%203_thumb%5B1%5D.png?imgmax=800 "Picture 3")](http://lh6.ggpht.com/_VrsVJGFhz4c/S4TCt7_asTI/AAAAAAAABvk/qp9RZpVZ-Ek/s1600-h/Picture%203%5B3%5D.png)

**Objective-c!**

Objective-c is a superset of the C language, so you can both include and use C/C++ code along with your objc code. Yea… that wouldn’t sell me on it either… Sometimes this means you can include useful libraries, but mostly it just means some of your code will go off into some foreign and scary land.

Fortunately, this new language comes with a completely different framework. Coming from ASP.NET/WinForms background, I am very pleased to be working in an MVC pattern which is really well implemented for the iPhone. I also love the observer pattern via [NSNotifications](http://developer.apple.com/iphone/library/documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html). I’ll probably do a post on that next as they are pretty slick.

There is a good document on the apple site on other [patterns common to cocoa](http://developer.apple.com/iphone/library/documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaDesignPatterns/CocoaDesignPatterns.html#//apple_ref/doc/uid/TP40002974-CH6-SW6). There is also a good one on [implementing a singleton](http://developer.apple.com/mac/library/documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaObjects/CocoaObjects.html#//apple_ref/doc/uid/TP40002974-CH4-SW32), which you’ll need if you don’t want to create [Big Ball of Mud](http://en.wikipedia.org/wiki/Big_ball_of_mud) in your AppDelegate.

I’ll probably continue this later with an observer example using NSNotifications and talk more about how some of the Small Talk elements work within Objective-c.
