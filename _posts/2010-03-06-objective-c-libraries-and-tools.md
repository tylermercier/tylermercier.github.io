---
layout: post
title: "Objective-C Libraries and Tools"
date: 2010-03-06
categories: blog
---

There are quite a few open source cocoa touch libraries and frameworks.

[OCMock](http://www.mulle-kybernetik.com/software/OCMock/), the winner by default when it comes to mocking in objective-c. It is actually a really decent mocking framework with all the elements you would come to expect (mocks, stubs and partial mocks). Setting it up can be a bit of a pain, fortunately Colin Barret has [figured that out for us](http://iamthewalr.us/blog/2008/11/ocmock-and-the-iphone/) already.

[Google Toolbox](http://code.google.com/p/google-toolbox-for-mac/), augments the SenTestingKit (OCUnit) providing more assertions, log tracking, binding testing and [more](http://code.google.com/p/google-toolbox-for-mac/wiki/CodeVerificationAndUnitTesting). A very [visual tutorial](http://www.luisdelarosa.com/2009/02/19/how-to-create-an-iphone-project-in-xcode-that-can-run-unit-tests/) on setting up Google Toolbox.

[GHUnit](http://github.com/gabriel/gh-unit), I am still spending time with this one. Seems promising so far. Key features are running individual tests, running tests from the command line (easier) and testing macros.

[UISpec](http://code.google.com/p/uispec/) is a test automation tool. It’s key feature is that it can run automation tests within the simulator (OCUnit must deploy to the iPhone). Documentation is pretty sparse.

[ASIHTTPRequest](http://allseeing-i.com/ASIHTTPRequest/) is a library that wraps the CFNetwork API, handling quite a bit of the grunt work for you. Great for working with RESTful services.

[json-framework](http://code.google.com/p/json-framework/), another key element of working with RESTful services. JSON is lighter weight and uses key-value pairs to represent data. This plays very nicely with the KVC techniques you should be using in Cocoa.

[SpeedLimit](http://osxdaily.com/2009/08/19/limit-connection-bandwidth-with-speedlimit/), this is a great utility for simulating the network speeds you are likely to have on the iPhone.
