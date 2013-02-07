---
layout: post
title: "为blog应用新的主题"
description: ""
category: 网站维护
tags: [jekyll theme, jekyll, jekyll-bootstrap, github pages]
---
{% include JB/setup %}

根据[jekyll-bootstrap][1]上面的说明，切换theme是一件很简单的事情。

* 安装：

	$ rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.gi

或者
	
	$ rake theme:install name="the-program"

* 应用:

	$ rake theme:switch name="the-program"

我选用了[the-minimum][2]这个主题，看起来小清新，编写的也符合（没验证过）html5规范，还是非常不错的，目前唯一的遗憾就是标题栏（logo）和内容不是左对其，感觉总是不舒服，有时间的时候打算调整一下。

[1]: http://jekyllbootstrap.com/
[2]: https://github.com/jekyllbootstrap/theme-the-minimum