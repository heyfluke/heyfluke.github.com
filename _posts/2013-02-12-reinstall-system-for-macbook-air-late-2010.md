---
layout: post
title: "用U盘为2010年版MacbookAir重装系统"
description: ""
category: "Mac OS X"
tags: [Mac OS X, Lion, reinstall, Macbook Air]
---
{% include JB/setup %}

今天拿到一台2010年版本的Macbook Air，并且要为它安装win7，但由于没有安装过，所以把系统给弄坏了（先是安装rEFIt的情况下也无法从win7安装U盘启动，然后用bootcamp助手划分分区的时候遇到了系统功能锁死，所以终止掉了这个过程，造成了系统损坏），因而需要把系统先恢复成Mac OS X（恢复了以后再考虑用BootCamp来安装windows）。

查了网上的资料，也不算复杂，从2010年开始，苹果给Macbook Air默认就配了恢复系统的U盘，从理论上说，后期的零售版系统都支持烧录到U盘上面进行安装。而对于Macbook Air2010来说，最好用的应该是Mac OS X Lion，所以就下载了这个，并且配合[Lion DiskMaker 2][1]来进行镜像文件的写入，它会自动检测安装app内的DMG镜像文件，也可以手工选择这个镜像文件的路径，很方便，顺利的制作好。

安装的时候我故意在开机的时候按着option，希望进入启动菜单，但是直接就识别到U盘进行安装了。

[1]: http://liondiskmaker.com
