---
title: Mac OSX Mountain Lion下尝试蓝牙SPP server
author: fluke
layout: post
permalink: /2012/12/mac-osx-mountain-lion%e4%b8%8b%e5%b0%9d%e8%af%95%e8%93%9d%e7%89%99spp-server/
categories:
  - Mac OS X
---

因为想搭建一个调试环境，在mountain lion上面通过蓝牙做一个SPP串口服务，用于和android手机的程序（譬如BluetoothChat）进行程序调试，所以就进行了一番尝试，结果是暂时失败的，记录一下。

一、Java的方案

根据文章《[JSR-82 : Java Bluetooth][1]》提示，可以通过java来使用系统蓝牙服务，能够达到跨平台的效果（当然不同平台有不同的实现或者适配），并且找到了mac下面的一个开源实现–[BlueCove][2]。测试的代码在《JSR-82: Java Bluetooth》以及《[Java and Bluetooth][3]》这篇文章都有，编译的时候注意包含jar路径即可。由于是32位的库，所以运行的时候需要加上-d32参数。编译和运行的命令行如下：

 [1]: http://www.jsr82.com/jsr-82-sample-spp-server-and-client/
 [2]: http://bluecove.org/
 [3]: http://homepages.ius.edu/RWISMAN/C490/html/JavaandBluetooth.htm

	javac -classpath bluecove-2.1.0-10dot6.jar SampleSPPServer.java
	
	java -d32 -classpath ".:bluecove-2.1.0-10dot6.jar" SampleSPPServer

可惜还是有错：

	dyld: lazy symbol binding failed: Symbol not found: _IOBluetoothLocalDeviceReadSupportedFeatures
	
	  Referenced from: /private/var/folders/rv/scdm9d6x6vn\_56s7ftzxj\_wm0000gn/T/bluecove\_laoyongchao\_	libbluecove.jnilib
	
	  Expected in: /System/Library/Frameworks/IOBluetooth.framework/Versions/A/IOBluetooth
	
	 
	
	dyld: Symbol not found: _IOBluetoothLocalDeviceReadSupportedFeatures
	
	  Referenced from: /private/var/folders/rv/scdm9d6x6vn\_56s7ftzxj\_wm0000gn/T/bluecove\_laoyongchao\_	libbluecove.jnilib
	
	  Expected in: /System/Library/Frameworks/IOBluetooth.framework/Versions/A/IOBluetooth
	
	 
	
	Trace/BPT trap: 5


看起来有符号已经变化了，下载了BlueCove来编译，发现原工程用的是OS X 10.6的SDK，而Mountain Lion已经是10.8了，有部分蓝牙相关的函数已经找不到符号，在苹果的页面已经找到了[删除掉接口的说明][4]……

 [4]: https://developer.apple.com/library/mac/#releasenotes/General/APIDiffsMacOSX10_8/IOBluetooth.html

没办法，这需要深入到蓝牙的API，所以暂时不研究。

二、 python的方案

找到一个python的方案叫[lightblue][5]，也是一个跨平台的封装，其中还包含了一个naive库叫做LightAquaBlue，只可惜这个方案也不支持mountain lion。

 [5]: http://lightblue.sourceforge.net/

所以目前打算两个方案：

1. 用虚拟机（破解vmware fusion）  
2. 自己编译BlueCove（要修改）