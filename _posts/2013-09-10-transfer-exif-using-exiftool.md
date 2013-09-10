---
layout: post
title: "查看和转移exif信息"
description: ""
category: 其他技术
tags: [exif, exiftool, exif on OS X]
date: 2013-09-10 13:49:38 +0800
---
{% include JB/setup %}

[EXIF][1]用于存放附加的信息在照片中，最广泛的使用可以算是数码相机了。基本上所有的相机、手机拍摄的照片都会留下这样的信息，就好像MP3有[ID3][2]信息一样。

EXIF信息包含但不限于以下信息：

* 制造商和相机型号
* 相片方向
* 相片分辨率和像素密度
* YCbCr排列
* 感光信息
* 拍照时间
* 地理位置信息
* 缩略图

EXIF的版本也在更新以适用于更多的信息存放。

通过EXIF信息，虽然可以看到照片在被创建时的各种参数，但可惜还不能作为版权保护、证据判断的依据，因为EXIF是开放可修改的信息，并且通常来说，一旦被修改，信息就会被更新。例如使用[PhotoShop][3]修改照片以后，原始的信息就没有了。

在Mac OS X下，查看EXIF信息很简单，只要在Finder中按Command+I即可查看到完整的信息。如果要修改、解压出缩略图的话，可以在macports下安装exif命令，也可以通过macports安装py-exif。

如果只是想简单地转移EXIF到另外一个图片上，则推荐使用[exiftool][4]，这是一个非常强大的命令，支持读写众多文件格式，现在只介绍转移一个文件的EXIF信息到另外一个文件。

* 如果要保留重复的信息，就使用这样的命令：

exiftool -wm cg -tagsfromfile "origin.jpg" -all:all "target.jpg"

* 其中 "-wm cg" 就是保留重复，如果不需要则直接用下面的命令即可：

exiftool -tagsfromfile "origin.jpg" -all:all "target.jpg"

[1]: http://zh.wikipedia.org/wiki/EXIF
[2]: http://en.wikipedia.org/wiki/ID3
[3]: http://zh.wikipedia.org/wiki/Photoshop
[4]: http://www.sno.phy.queensu.ca/~phil/exiftool/index.html

