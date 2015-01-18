---
layout: post
title: "Gzip Issue"
date: 2009-09-01
categories: blog
---

A co-worker was facing down a problem with one of his asp.net portals last week and asked for some help. The full details about what this portal does are not important, but suffice to say that it would zip up some files on the server and allow users to download them.

The problem was that on one of the two servers where this portal was hosted, files were coming down smaller than the other and failing to unzip. It almost appeared that the last 5-8KB of the files was just being truncated. I spent a fair amount of time with this person checking the versions were consistent, that the configuration files were consistent and that basically nothing was wrong on the developers end.

At this point we were ready to point the finger at IIS, but we needed to be sure.

I logged onto the failing server (this is in dev), ran _inetmgr_ and compared the IIS settings to the working server. Aside from a few false leads, everything is more or less that same. The particular site is running as a virtual directory, all the usual settings look like carbon copies of one another (security, permissions, thread pool, .net version, etc…) and nothing appears to be out of place.

At this point we are starting to think it must be in some part of IIS we were not familiar with and decide to give [fiddler](http://www.fiddler2.com/fiddler2/) a try on the user’s end instead. For those that are unfamiliar with fiddler, it is a lot like [wireshark](http://www.wireshark.org/) except it plugs directly into internet explorer and captures all the network traffic in a much more friendly and active way. I ran into this tool a couple of years ago and it has remained in my toolbox since.

Request header for the working server.

[![fiddler_workingserver_request](http://lh3.ggpht.com/_VrsVJGFhz4c/SpvyhrEFWZI/AAAAAAAABrI/RKG5oPA-1TU/fiddler_workingserver_request_thumb%5B7%5D.jpg?imgmax=800 "fiddler_workingserver_request")](http://lh3.ggpht.com/_VrsVJGFhz4c/SpvyhVvqAhI/AAAAAAAABrE/qzKAp6coQk0/s1600-h/fiddler_workingserver_request%5B11%5D.jpg)

Request header for the failing server.

[![fiddler_failingserver_request](http://lh6.ggpht.com/_VrsVJGFhz4c/SpvyinAYolI/AAAAAAAABrQ/nwSXFi9WjuE/fiddler_failingserver_request_thumb%5B6%5D.jpg?imgmax=800 "fiddler_failingserver_request")](http://lh4.ggpht.com/_VrsVJGFhz4c/Spvyh9FFWcI/AAAAAAAABrM/EjmvrI-ymak/s1600-h/fiddler_failingserver_request%5B8%5D.jpg)

Other than different session ids, they are identical.

This was the response header from the working server.

[![fiddler_workingserver_response](http://lh6.ggpht.com/_VrsVJGFhz4c/SpvykEHu6OI/AAAAAAAABrY/u7X9ZYGVuW0/fiddler_workingserver_response_thumb%5B8%5D.jpg?imgmax=800 "fiddler_workingserver_response")](http://lh5.ggpht.com/_VrsVJGFhz4c/SpvyiztCjVI/AAAAAAAABrU/d_Ah7vjXEGU/s1600-h/fiddler_workingserver_response%5B10%5D.jpg)

This was the response header from the failing server.

[![fiddler_failingserver_response](http://lh5.ggpht.com/_VrsVJGFhz4c/Spvyk0E-_2I/AAAAAAAABrg/sQ7f1enNkGo/fiddler_failingserver_response_thumb%5B7%5D.jpg?imgmax=800 "fiddler_failingserver_response")](http://lh4.ggpht.com/_VrsVJGFhz4c/SpvykcAfgrI/AAAAAAAABrc/_Li7HVLmGm0/s1600-h/fiddler_failingserver_response%5B9%5D.jpg)

Notice the difference? If somehow you missed it, the transport mechanism from the server to the client is using gzip on the failing server. I decided to disable it for that server to see if it would fix the issue as a proof that the issue was with gzip compressing the zip files.

A quick way to disable something for gzip compression is to check if the file extension you don’t want compressed is included in the MetaBase (IIS configuration file).

[![metabase_location](http://lh4.ggpht.com/_VrsVJGFhz4c/SpvymB3w04I/AAAAAAAABro/OjXoEwoQjHU/metabase_location_thumb%5B1%5D.png?imgmax=800 "metabase_location")](http://lh5.ggpht.com/_VrsVJGFhz4c/SpvyldtQvoI/AAAAAAAABrk/rZe6M-6v-S8/s1600-h/metabase_location%5B1%5D.png)

The tag you want to look for is **IISCompressionScheme**

[![metabase_iiscompressionscheme](http://lh3.ggpht.com/_VrsVJGFhz4c/SpvymxUcFBI/AAAAAAAABrw/0LYSWQBxsog/metabase_iiscompressionscheme_thumb%5B1%5D.png?imgmax=800 "metabase_iiscompressionscheme")](http://lh6.ggpht.com/_VrsVJGFhz4c/SpvymYsZNzI/AAAAAAAABrs/dvzCmvr6xF8/s1600-h/metabase_iiscompressionscheme%5B1%5D.png)

There is a decent step by step guide on enabling gzip compression [here](http://dev1.wordpress.com/2008/12/30/step-by-step-setting-up-gzip-on-iis-6-compressing-servers-output-stream/). The biggest tip is that you need to shut down IIS before editing the MetaBase file. There is an option to do this in the restart procedure.

That all said and done, it was indeed gzip that was causing the issue. It really shouldn’t matter if the content is compressed between the server and the browser, but for some reason none of the major browsers would uncompress the file. Another issue for another day I suppose.
