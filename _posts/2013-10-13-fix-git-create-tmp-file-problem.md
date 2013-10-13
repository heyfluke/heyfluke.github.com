---
layout: post
title: "修复git远程创建临时文件失败的问题"
description: ""
category: 
tags: []
date: 2013-10-13 12:44:03 +0800
---
{% include JB/setup %}

今天提交遇到这个问题：

	remote: error: unable to create temporary file: Invalid argument
	remote: fatal: failed to write object
	error: unpack failed: unpack-objects abnormal exit

网上讨论可能是权限出问题了： http://stackoverflow.com/questions/685319/git-pull-error-unable-to-create-temporary-sha1-filename

先试下最保险的解决办法，用git gc。

到/home/git/repositories/username/project.git目录下，运行：

	$ sudo -u git -H git gc

