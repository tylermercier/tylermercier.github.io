---
layout: post
title: "Install PhantomJS on Ubuntu"
date: 2013-01-30
categories: blog
---

For those that know me, [PhantomJS](http://phantomjs.org/), is something that I have a soft spot for. It is fantastic for [testing your JavaScript](http://codecuriosity.com/blog/2012/09/25/testing-javascript-in-rails/). Lately, I have been trying to use it to test my application [features](http://en.wikipedia.org/wiki/Acceptance_testing) with [Poltergeist](https://github.com/jonleighton/poltergeist), but have run into some version issues. For whatever reason, apt-get is installing a very old version (1.4). In order to install the current version you need to pull it down from the PhantomJS site. Below should help you out.

```bash
cd /usr/local/share/
sudo wget http://phantomjs.googlecode.com/files/phantomjs-1.8.1-linux-x86_64.tar.bz2
sudo tar jxvf phantomjs-1.8.1-linux-x86_64.tar.bz2
sudo ln -s /usr/local/share/phantomjs-1.8.1-linux-x86_64/ /usr/local/share/phantomjs
sudo ln -s /usr/local/share/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
```

The steps are straight forward, but let me explain them anyways. Hop into the share folder. Download the latest at the time of this post (1.8.1) into the share. Unzip the file. Symlink the unzipped directory to phatomjs. Symlink the phatomjs executable (though the previous symlink) into the /usr/local/bin. If everything worked, then you should see it when running the following.

```bash
which phantomjs
```
