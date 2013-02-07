---
title: 遇到Mountain Lion的两个bug
author: fluke
layout: post
permalink: /2013/01/%e9%81%87%e5%88%b0mountain-lion%e7%9a%84%e4%b8%a4%e4%b8%aabug/
categories:
  - Mac OS X
tags:
  - bug
  - Mountain Lion
  - OS X
  - Show in Finder
---

才开始转用mac不久，就遇上了两个Mountain Lion的bug，其中第一个应该是系统级别的bug，希望近期能够修复。

1. 应用程序中的“show in Finder”或者“在Finder中显示”功能失效。这个很诡异，我一开始还以为是金山快盘修改了Finder里面的icon功能导致的，后来到stackoverflow看了一下，发现是消息队列的bug，看来还有潜在的别的问题，譬如拖拽等。解决办法是kill掉appleeventsd（不需要重启了？不清楚）：

	sudo killall -KILL appleeventsd

2. 系统自带的备忘录丢失。

机器从来没关过，从来都是休眠，昨天打开盖子的时候曾发现登陆背景花瓶，进入以后没感觉什么异样，今天早上开机打开备忘录发现少了一条，过了大约1分钟，突然显示出那条记录的早期状态（估计是从icloud同步下来的）。难道是临界状态ssd写入的问题？