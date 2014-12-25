---
layout: post
title: "Object Store"
date: 2009-03-27
comments: false
categories: blog
---

A few weeks back I was having a discussion with a couple co-workers about how large scale web applications handle their database needs. Eventually, object store came up. I have certainly heard about object orientated databases before and their associated trade-offs. This almost made me write-off object storing as just a fresh buzz word built on old idea.

The structure is really trivial and requires the following columns:

Primary Indentifier (Object Key)
Search String (To aid in finding the key)
SystemType (The object type that the data serializes to)
Data (Use an image type)
CreatedOn (Date created
ModifiedOn (Date changed)

This is by no means something you should be using for just any field. It is, however, a very convenient solution to handling web config entries or other xml configurations. I would not recommend the creation of a god object housing everything and anything your site needs to know, but the creation of a site object, derived through this database table, could be very useful. Break it into components as needs and it really would shine. Especially with the destruction of all those painful web config entries.

The beauty of this is that your table can store any object and doesn't need to be updated if that object changes. One consideration would be in your code and that would be handling of missing xml nodes since you could be pulling in an older version.
