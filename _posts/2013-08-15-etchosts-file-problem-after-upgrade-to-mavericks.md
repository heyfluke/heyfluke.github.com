---
layout: post
title: "升级Mac OS X到Mavericks以后/etc/hosts文件失效"
description: ""
category: 
tags: [/etc/hosts, dns, OS X 10.9, Mavericks]
date: 2013-08-15 19:04:31 +0800
---
{% include JB/setup %}

最近正式升级到Mavericks了，虽然比DP1版本刚出来的时候稳定了，但感觉内存方面好像还不够优化。不过不管怎么说，还是接受这种风格的变化的。

这次升级以后的一个比较严重的问题是不能通过/etc/hosts文件来配置本地域名记录了，起初怀疑是解析顺序的问题，甚至还安装了dnsmasq来试图解决问题，但是dnsmasq也不行，才想到配置它的记录文件到另外一个文件，配置的办法是“addn-hosts=/etc/addion_hosts”。

配置之前我开始怀疑是文件权限的问题，ls看一下，原来文件权限是700，并且用户是属于我很久以前重装过一次之前的用户名，看来OS X在重新安装的时候还是有残留的……

这个时候只需要修改文件属性为644，用户组wheel，用户root即可，一切恢复如初。只是想不通的是为什么升级到Mavericks会导致文件的属性变成隔了一次重装系统之前的用户名。

附上修改的办法：

```
	sudo chown root /etc/hosts
	sudo chgrp wheel /etc/hosts
	sudo chmod 644 /etc/hosts
```
