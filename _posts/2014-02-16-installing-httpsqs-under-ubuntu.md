---
layout: post
title: "在Ubuntu下安装HTTPSQS"
description: ""
category: 其他技术
tags: [HTTPSQS, ubuntu]
date: 2014-02-16 21:29:40 +0800
---
{% include JB/setup %}

[HTTPSQS][1]是个好项目，在其[项目官网][1]和[作者博客][2]都介绍了安装和使用办法，估计是以centos为例。在ubuntu下面建议直接从仓库安装对应的依赖项，只单独编译安装主程序。

	sudo aptitude install libevent-dev tokyocabinet-bin libtokyocabinet-dev
	wget http://httpsqs.googlecode.com/files/httpsqs-1.7.tar.gz
	tar zxvf httpsqs-1.7.tar.gz
	cd httpsqs-1.7/
	make
	sudo make install
	cd ../

[1]: https://code.google.com/p/httpsqs/
[2]: http://blog.s135.com/httpsqs/