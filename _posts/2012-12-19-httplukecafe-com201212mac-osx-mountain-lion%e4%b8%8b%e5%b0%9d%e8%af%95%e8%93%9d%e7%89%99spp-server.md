---
title: 续Mac OSX Mountain Lion下尝试蓝牙SPP server
author: fluke
layout: post
permalink: /2012/12/httplukecafe-com201212mac-osx-mountain-lion%e4%b8%8b%e5%b0%9d%e8%af%95%e8%93%9d%e7%89%99spp-server/
categories:
  - Mac OS X
---
# 

之前写了《[Mac OSX Mountain Lion下尝试蓝牙SPP server][1]》，说明在 Mountain Lion下面由于蓝牙API的变化已经不容易编写串口程序，但是突然想起一个很简单的方法，原来一定是大脑短路了没想到。

 [1]: http://lukecafe.com/2012/12/mac-osx-mountain-lion下尝试蓝牙spp-server/

蓝牙SPP服务无非就是一种串口通信，而在\*INX下面，会把串口写成/dev/tty\*设备，并且是字符串设备，可以直接与这个设备进行读写的通信。

基于这个事实，想要做到测试最简单的方式就是编写脚本，用python的serial模块很方便就能够做到了。

示例：

> #!/usr/bin/env python
> 
>  
> 
> import serial
> 
>  
> 
> def main():
> 
> print '===== Test Serial Communication ====='
> 
> ser = serial.Serial('/dev/tty.Bluetooth-PDA-Sync', 9600, timeout=10)
> 
> recvbuf = ''
> 
> while True:
> 
> char = ser.read(1)
> 
> if not len(char): continue
> 
> recvbuf = char
> 
> # TODO: parse proto
> 
> ser.write(char)
> 
>  
> 
> ser.close()
> 
>  
> 
> if \_\_name\_\_ == '\_\_main\_\_':
> 
> main()