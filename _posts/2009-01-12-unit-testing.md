---
layout: post
title: "Unit Testing"
date: 2009-01-12
comments: false
categories: blog
---

The primary goal of [unit testing](http://msdn.microsoft.com/en-us/library/aa292197(VS.71).aspx) is to take the smallest piece of testable software in the application, isolate it from the remainder of the code, and determine whether it behaves exactly as you expect. Each unit is tested separately before integrating them into modules to test the interfaces between modules. Unit testing has proven its value in that a large percentage of defects are identified during its use.

[Michael Feathers](http://www.michaelfeathers.com/), says that good unit tests should run quickly and help point out problems. He also defines what isn't a unit test.
  > Any test that talks to a database
> Any test that communicates across a network
> Any test that interacts with the file system
> Any test that you must do special configurations to your environment to run

Other important aspects of unit tests are ensuring that you get consistent test results. Running the same test repeatedly should return the same results consistently.

The tests should not require configuration. Though mentioned above, it should be more explicitly stated that unit tests need to be as simple as possible or else you will likely introduce bugs within your unit tests.

Testing order should not matter. This means partial test runs can work correctly. Also, if you keep this design philosophy in mind, it will likely aid in your test creation.

Remember that any testing is better than no testing. The difficulty can be found in writing good clean unit tests that promote ease of creation and maintenance. The more difficult the testing framework, the more opposition there will be to employing it. Testing is your friend.
