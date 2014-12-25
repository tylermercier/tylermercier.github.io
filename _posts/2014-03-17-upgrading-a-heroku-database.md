---
layout: post
title: "Upgrading a Heroku Database"
date: 2014-03-17 20:20
comments: true
categories: blog
---

Migrating database instances on heroku is surprisingly easy.

```bash
# disable your application to prevent DB writes
heroku maintenance:on -a source-app

# capture a backup
heroku pgbackups:capture -a source-app --expire

# restore the backup to the new location
heroku pgbackups:restore HEROKU_DATABASE_URL -a target-app `heroku pgbackups:url -a source-app`

# change over to the new database
heroku config:set DATABASE_URL=<correct url>

# enable your application
heroku maintenance:off -a source-app
```
