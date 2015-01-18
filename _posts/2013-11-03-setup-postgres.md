---
layout: post
title: "Setup Postgres"
date: 2013-11-03
categories: blog
---

Setup postgres with an application user.

```bash
sudo -u postgres psql -c "drop database #{postgresql_database}"
sudo -u postgres psql -c "drop user #{postgresql_user}"
sudo -u postgres psql -c "create user #{postgresql_user} with password '#{postgresql_password}';"
sudo -u postgres psql -c "create database #{postgresql_database} owner #{postgresql_user};"
```
