---
layout: post
title: "Mocha with blocks"
date: 2014-11-26 19:26
comments: true
categories: blog
---

The popular ruby mocking library, [mocha](https://github.com/freerange/mocha), has a handy feature for testing incovations. The `with` method can take a block. This is useful for assert params that you are calling the object with.

```bash
  # common usage
  User.expects(:save).with(user)

  # use a block to verify parameters
  User.expects(:save).with do |user|
    assert_equal 'tyler', user.first_name
    assert_equal 'mercier', user.last_name
    assert_equal 'active', user.status
    ...
  end
```
