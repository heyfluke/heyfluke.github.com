---
layout: post
title: "migrate django database from mysql to sqlite"
description: ""
category: 其他技术
tags: [django]
date: Sun Jul 07 19:28:56 +0800 2013
---
{% include JB/setup %}

* ./manage.py dumpdata --exclude=contenttypes > dump.json

* edit setting.py change to sqlite

* ./manage.py syncdb   # and choose not to create auth info here

* ./manage.py migrate

* ./manage.py loaddata dump.json
