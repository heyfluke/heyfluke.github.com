---
layout: post
title: "iPhone资源图片中的PNG格式"
description: ""
category: iOS开发
tags: [png, CgBI, cocos2d-x]
date: 2013-03-04 16:27:24 +0800
---
{% include JB/setup %}

在用cocos2d-x做一个跨平台产品的时候，发现到了android下面，明明也能读取到图片，但读出的png数据缓冲就有问题，最终也会导致程序崩溃（调试的时候没有记录下来，凭印象png文件头应该是\x89开始的，而读取出来的是\211）。

后来怀疑图片有问题的时候使用imagemagick里面的convert一看，就报图片格式不认识，通过二进制对比，发现多了一个CgIB的chunk(png文件格式是由一个一个chunk块组成的)。后经过查证，是苹果为了png在设备上面的处理效率（敬业啊），特别修改了一下，使得格式不标准。后来试过gimp,photoshop都不支持这种格式。

由于我的图片是从别人的程序里面扣出来用的，所以就存在这个问题，需要解决也很简单，可以自己根据资料解析这个CgBI（github也有项目叫pngcrush）也可以直接在一个网站（[Extract and convert iPhone PNG files online!][1]）上面在线转换，两个方向都可以，这个网站支持多文件拖拽操作，做的还比较现代。

[1]: http://convert-iphone-png-online.protonail.com/
