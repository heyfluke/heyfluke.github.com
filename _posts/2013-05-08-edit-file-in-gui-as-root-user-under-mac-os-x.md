---
layout: post
title: "Mac OS X下以Root身份用图形界面编辑文件"
description: ""
category: 其他技术
tags: [Max OS X, edit as root]
date: 2013-05-08 12:04:12 +0800
---
{% include JB/setup %}

在Mac OS X下面，如果需要以root身份来编辑某个文件，通常都是在Terminal下用sudo vim/nano来完成，如果想用GUI方式，有点麻烦，有以下集中方法供选择：

* 安装Gedit，可以在命令行启动Gedit。安装方式为sudo port install gedit。这种方式的弊端在于gtk2程序的复制、粘贴快捷键是control+c/v，而不是OS X程序常用的Command+c/v。
* sudo操作文本编辑器
* sudo使用open命令，例如sudo open -e /path/to/myfile。这种方式可能在老一些的版本里面没有问题，但是在Mountain Lion下面测试，直接这样打开，这样会以“当前普通用户的身份打开”文本编辑器的一个实例，打开编辑的时候会提示“您不是文件“myfile”的所有者，因此没有权限写到该文件。”

然而，对于sudo使用open命令的问题，是有办法解决的，那就是先用root用户强行开一个文本编辑器的实例，然后再用open命令来编辑，最后用完了才退出文本编辑器。操作方式如下：

* 第一次打开文本编辑器的话，在Terminal输入：sudo -b /Applications/TextEdit.app/Contents/MacOS/TextEdit，其中b表示在后台运行，不会阻塞Terminal。
* 然后直接在弹出的窗口中选择打开文件，或者：
* 也可以继续在Terminal输入：sudo open -e /opt/local/etc/nginx/vhost/localdjango.conf，但这种方法要求先退出普通用户可能已经打开的默认文本编辑器，否则会使用先打开的程序来打开。
