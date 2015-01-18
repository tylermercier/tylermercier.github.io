---
layout: post
title: "What is NuGet"
date: 2011-03-28
categories: blog
---

After spending some time with Ruby on Rails and the wonderful package management tool [RubyGems](http://rubygems.org/), I was very excited to hear about NuGet, a .NET package manager that comes bundled with [ASP.NET MVC 3](http://www.asp.net/mvc/mvc3). Finally, the .NET community gets a Microsoft supported package manager. The NuGet page has a pretty good description of what it is and why you should care...

> NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.
>
> When you use NuGet to install a package, it copies the library files  to your solution and automatically updates your project (add references,  change config files, etc). If you remove a package, NuGet reverses  whatever changes it made so that no clutter is left.You can think of it as a much more convenient way to include third party libraries if you haven't used something like ruby gems before. As a [package manager](http://en.wikipedia.org/wiki/Package_management_system), NuGet will do many things for you to make your life easier.

First, it makes it simple to find and include a library. You don't have to google for the library, find the project page, find the download page, find the right version, etc... You can easily install the package the way you would a local library (almost).

It will pull in dependencies for that library. Want to use Fluent-NHibernate? Just grab the NuGet package and it will include NHibernate, along with NHibernates own dependencies.

It can also allow the injection of useful template code into your project to help get you started. [MVCMailer](http://www.hanselman.com/blog/NuGetPackageOfTheWeek2MvcMailerSendsMailsWithASPNETMVCRazorViewsAndScaffolding.aspx) does just this to help get you started with sample views and mailers.

If this sounds worthwhile, head over to Justin Etheredge's [blog](http://www.codethinked.com/you-really-should-be-using-nuget) and follow his tutorial, which is really good.

Also be sure to check out some of the available packages in the [NuGet Gallery](http://nuget.org/List/Packages).
