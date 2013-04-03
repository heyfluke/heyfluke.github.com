---
layout: post
title: "亚马逊ec2微实例的benchmark"
description: ""
category: 服务器维护
tags: [unixbench, ubuntu, ec2, amazon ec2]
date: 2013-04-03 11:56:32 +0800
---
{% include JB/setup %}

今天对我开在美国西海岸的一个[Ec2][1]的实例进行了benchmark，使用的是[unixbench][2]，为了方便对比，我还在自己的macbook上安装的ubuntu虚拟机进行了benchmark。两个系统都是[ubuntu server 12.0][3]。

ec2的配置了2GHz的E5-2650 CPU以及600MB的RAM，而虚拟机的ubuntu则配置了2.3GHz的i7-3615QM CPU以及1G RAM。通过测试发现ec2落后了几倍，尤其是浮点运算以及文件拷贝速度比较让人担忧，原始分数甚至相差8-9倍。不过具体使用起来是否能够满足需求，等我下半年再总结一下数据。

完整的benchmark结果参考[这个文件][4]。

[1]: http://aws.amazon.com/ec2/
[2]: https://code.google.com/p/byte-unixbench/
[3]: http://releases.ubuntu.com/precise/
[4]: /files/upload/20130403-ec2-benchmark.txt
