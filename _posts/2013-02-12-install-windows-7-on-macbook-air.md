---
layout: post
title: "通过U盘在Macbook Air 2010上安装windows 7"
description: ""
category: "Mac OS X"
tags: [windows 7 on Macbook Air, window install, Macbook Air]
date: 2013-02-12 19:30:00 +0800
---
{% include JB/setup %}

续[用U盘为2010年版MacbookAir重装系统][1]，现在要在Macbook Air上面安装windows 7。方法还算比较简单，但有一个地方需要注意。

Macbook Air默认只有一个硬盘，一个分区，大小大约为60GB。使用Boot Camp助手分区，默认情况下，如果只有Mac分区的话，Boot Camp助手会默认提示下载windows支持文件，大约有600M大小，然后提示创建windows分区，默认的标签是BOOTCAMP，还可以调整大小，分区为FAT格式，但注意分区的标识可能无法用别的分区软件来识别。最后一步会提示开始安装windows，因为没有光驱，所以选择以后再安装。

与此同时，用另外一个u盘在用[windows 7 usb dvd download tool][2]来制作win7的安装盘，大约需要10分钟。

现在开始有2个可做的方法，如果第一种不行就选第二种：

1. 重启，按住option直到从win7安装盘启动。
2. 如果上面方法不可以的话，就去安装一个[rEFIt-0.14][3]，然后执行enable-always.sh脚本（用spotlight搜索）。然后重启，会默认有启动菜单，选择从u盘启动（盘符标识是黄色的盘，有时候会出现两个，可以试一下）。

安装过程就开始了，*重点*需要注意，要安装的windows分区会提示不是激活分区或者格式不对等等，需要先选择驱动器选项，格式化（默认是NTFS），然后重启再选择U盘进入安装过程，这里如果不重启的话，那一直都会提示错误。

安装完成以后安装BootCamp下载的WindowsSupport文件夹下面的软件就好了。

[1]: /2013/02/reinstall-system-for-macbook-air-late-2010
[2]: http://www.microsoftstore.com/store/msstore/html/pbPage.Help_Win7_usbdvd_dwnTool
[3]: http://refit.sourceforge.net/
