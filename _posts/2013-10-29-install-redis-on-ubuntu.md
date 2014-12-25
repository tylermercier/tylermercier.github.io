---
layout: post
title: "Install Redis on Ubuntu"
date: 2013-10-29 20:26
comments: true
categories: blog
---

Setting up [Sidekiq](http://sidekiq.org/) recently forced me to install [redis](http://redis.io/).Sidekiq requires a pretty [recent version](https://groups.google.com/forum/#!topic/gitlabhq/2Nn5Wc6PQCU) of redis. One more recent than the package manger on Ubuntu provides. You can use the following script to install a more recent version. It's also useful for other packages you might need more up to date versions of ([nginx](http://wiki.nginx.org/Main), [postgres](http://www.postgresql.org/), etc...)

```bash
sudo apt-get -y update
sudo apt-get -y install python-software-properties
sudo add-apt-repository -y ppa:rwky/redis
sudo apt-get -y update
sudo apt-get -y install redis-server
```

**python-software-properties** adds the add-apt-repository command. **add-apt-repository** is  a  script  which  adds an external APT repository to either /etc/apt/sources.list or a file in /etc/apt/sources.list.d/ or removes an already existing repository. Basically, it allows us to reference and use the PPA (Personal Package Archives) and install a more recent version of redis.

```bash
root@test:~# redis-server -v
Redis server v=2.6.16 sha=00000000:0 malloc=jemalloc-3.2.0 bits=64
```

Some other useful commands to test redis is running correctly.


```bash
netstat -nlpt | grep 6379
```

```bash
redis-cli -h xxx.xxx.xxx.xxx ping
```

You could also do this from your application

```ruby
r = Redis.new(host: 'xxx.xxx.xxx.xxx', port: 6379)
r.ping
```
