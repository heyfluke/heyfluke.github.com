---
layout: post
title: "Django实践：用south来迁移数据库/模型"
description: ""
category: 其他技术
tags: [Django, south, migrate]
date: 2013-05-28 22:45:02 +0800
---
{% include JB/setup %}

开发了一段时间Django以后，应该多多少少会遇到Model需要修改的情况。这在以前是一个比较麻烦的事情，手工升级的话，容易出现遗漏和错误，如果编写脚本的话，又麻烦。而Django引入了一个叫south的模块（目前甚至已经替换了./manager.py syncdb的默认实现），专门用于处理Model变更的情况。

south一般使用场景有两种：

1. 软件一开始就使用south来维护

* 编写好model，假设app为helloworld，写好helloworld/models.py以后，通过以下命令来生成一个迁移记录文件。

```./manage.py schemamigration helloworld --initial```

这会生成一个以0001_开头的文件，譬如：

./helloworld/migrations/0001_initial.py

文件内容是当前model的scheme。

这个时候如果数据库还没有同步的话，可以通过以下命令来同步到数据库：

```./manage.py migrate helloworld```

* 然后遇到需求变更，需要增加某个字段的话，先修改helloworld/models.py，增加fieldx。再运行以下south命令生成当前版本的升级脚本：

```./manage.py schemamigration helloworld --auto```

这时，生成的文件大概会是：

./helloworld/migrations/0002_auto__add_field_helloworld_fieldx.py

这时，如果当前数据库是0001版本的话，那直接运行以下命令就可以进行迁移了：

```./manage.py migrate helloworld```

2. 另外一个场景是，如果你在软件上线以后，突然想对现有的系统进行改造，但原来没有用south管理过，则需要有一点点小几条。

在了解这个小技巧之前，先了解一下south升级的时候会干什么事情。对于mysql，south会先检查一下当前的migration文件和当前的升级日志，从升级日志中了解当前数据库的结构是哪个版本的，然后才开始执行下一个版本的升级。

这个时候如果直接生成migration文件，然后执行的话，会报下面的错误：

	The error was: (1050, "Table 'helloworld_mytable' already exists")
	 ! Error found during real run of migration! Aborting.

	 ! Since you have a database that does not support running
	 ! schema-altering statements in transactions, we have had 
	 ! to leave it in an interim state between migrations.

	! You *might* be able to recover with:   = DROP TABLE `helloworld_mytable` CASCADE; []

	 ! The South developers regret this has happened, and would
	 ! like to gently persuade you to consider a slightly
	 ! easier-to-deal-with DBMS (one that supports DDL transactions)
	 ! NOTE: The error which caused the migration to fail is further up.

这是因为south发现数据库中没有升级记录，是未知的版本，但升级0001版本的话，又和数据库原有的表冲突。而既然场景1可以完成升级，这个场景里面，也是可以的，只要骗骗south，告诉它我们已经在0001版本即可。而south刚好提供了--fake参数，在这个参数下，迁移并不会进行，但又会写上迁移的日志。

* 所以，可以在数据库同一个版本的model下，先创建一个版本的migration，即上面的：

```./manage.py schemamigration helloworld --initial```

* 然后“骗骗”south：

```./manage.py migrate helloworld --fake```

这时发现数据表south_migrationhistory会多一条记录:

helloworld	0001_initial

* 然后修改helloworld/models.py，再运行:

```./manage.py schemamigration helloworld --auto```

* 然后就和场景1一样了。






