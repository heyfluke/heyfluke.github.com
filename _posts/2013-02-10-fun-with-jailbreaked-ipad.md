---
layout: post
title: "iPad越狱后的好玩法"
description: ""
category: 玩设备
tags: [iPad, jail break, 越狱, ssh, Cydia, apt-get, jekyll]
---
{% include JB/setup %}

先对自己和朋友说声蛇年新年快乐！

最近把iPad升级到了iOS6.1并且越狱了，继续探索越狱仓库，顺便把写一些越狱以后的好玩法。

1. 可以通过ssh上iPad去进行bash shell的操作。需要在Cydia仓库安装SSH Connect软件，然后在设置界面吧ssh访问打开。在wifi状态下，可以看设备的ip，在局域网内可以登陆。root用户默认密码为alpine。如果没有网络的话可以用vSSH Lite之类的软件在iPad登陆localhost来获取shell。

2. 可以开启网络共享功能，在Cydia仓库里面以Tether为关键字搜索即可。

3. 可以用apt-get工具，在Cydia仓库安装APT 0.6 Transition即可，如果习惯用aptitude的也可以再装这个。

4. 在尝试安装编译器和编译git。如果成功的话，可以在iPad上面用markdown来编写基于Jekyll的blog，通过git提交。
