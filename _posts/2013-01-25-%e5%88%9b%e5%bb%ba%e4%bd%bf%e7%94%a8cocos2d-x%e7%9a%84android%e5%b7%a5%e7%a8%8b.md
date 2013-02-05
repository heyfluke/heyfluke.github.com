---
title: 创建使用cocos2d-x的Android工程
author: fluke
layout: post
permalink: >
  /2013/01/%e5%88%9b%e5%bb%ba%e4%bd%bf%e7%94%a8cocos2d-x%e7%9a%84android%e5%b7%a5%e7%a8%8b/
categories:
  - Android
tags:
  - android
  - cocos2d-x
---
# 

本文基于cocos2d-x 2.0稳定版，主机操作系统为Mac OSX。对于linux和windows应该是类似的（win下的脚本为bat）。

 

cocos2d是一个为ios编写的游戏开发库，流行起来以后创建了跨平台的cocos2d-x库，也可以支持android(主要基于c 开发)。

 

创建Android工程的方式为通过cocos2d-x目录下面的create-android-project.sh来创建。因为依赖Android的NDK以及SDK，所以需要先把它们都安装好，并且设置好NDK\_ROOT以及ANDROID\_SDK_ROOT这两个环境变量指向它们所在目录。如果不想添加这两个变量，也可以在脚本里面修改以下两行：

 

> # set environment paramters
> 
> NDK\_ROOT\_LOCAL="/home/laschweinski/android/android-ndk-r5"
> 
> ANDROID\_SDK\_ROOT\_LOCAL="/home/laschweinski/android/android-sdk-linux\_86"

 

我把环境变量添加到~/.bash_profile里面。然后运行./create-android-project.sh。整个交互过程需要输入包名、API id、项目名等，参考：

 

> agspc98:cocos2d-2.0-x-2.0.4 laoyongchao$ ./create-android-project.sh 
> 
> use global definition of NDK_ROOT: /Users/laoyongchao/Applications/android-ndk-r6-crystax-2
> 
> use global definition of ANDROID\_SDK\_ROOT: /Users/laoyongchao/Applications/adt-bundle-mac/sdk
> 
> Input package path. For example: org.cocos2dx.example
> 
> fluke.play.testcocos2dx
> 
> Now cocos2d-x supports Android 2.2 or upper version
> 
> Available Android targets:
> 
> ———-
> 
> id: 1 or "android-8"
> 
>      Name: Android 2.2
> 
>      Type: Platform
> 
>      API level: 8
> 
>      Revision: 3
> 
>      Skins: HVGA, QVGA, WQVGA400, WQVGA432, WVGA800 (default), WVGA854
> 
>      ABIs : armeabi
> 
> ———-
> 
> id: 2 or "android-17"
> 
>      Name: Android 4.2
> 
>      Type: Platform
> 
>      API level: 17
> 
>      Revision: 1
> 
>      Skins: HVGA, QVGA, WQVGA400, WQVGA432, WSVGA, WVGA800 (default), WVGA854, WXGA720, WXGA800, WXGA800-7in
> 
>      ABIs : armeabi-v7a
> 
> input target id:
> 
> 1
> 
> input your project name:
> 
> TestCocos2dx
> 
> Created project directory: /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/src/fluke/play/testcocos2dx
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/src/fluke/play/testcocos2dx/TestCocos2dx.java
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/res
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/bin
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/libs
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/res/values
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/res/values/strings.xml
> 
> Created directory /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/res/layout
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/res/layout/main.xml
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/AndroidManifest.xml
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/build.xml
> 
> Added file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/proguard-project.txt
> 
> Resolved location of library project to: /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/cocos2dx/platform/android/java
> 
> Updated project.properties
> 
> Updated local.properties
> 
> Updated file /Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android/proguard-project.txt
> 
> agspc98:cocos2d-2.0-x-2.0.4 laoyongchao$ 

 

然后是编译的过程，到TestCocos2dx目录去，发现工程文件都被整理在proj.android目录里面了（每个平台都统一这样的目录结构，比如ios的在proj.ios），到proj.android目录下运行./build_native.sh，结果发现很多错误，怀疑是对ndk的版本有要求，就换成ndk-r8c，结果成功：

 

> ….
> 
> Prebuilt       : curl.a  
> StaticLibrary  : libextension.a
> 
> SharedLibrary  : libgame.so
> 
> Install        : libgame.so => libs/armeabi/libgame.so
> 
> make: Leaving directory `/Users/laoyongchao/Documents/projects/os/cocos2d-2.0-x-2.0.4/TestCocos2dx/proj.android'
> 
> agspc98:proj.android laoyongchao$ 

 

然后编译apk，如果是第一次运行，还需要更新以下环境：

 

> agspc98:proj.android laoyongchao$ android update project –path .
> 
> Updated local.properties
> 
> Updated file ./proguard-project.txt

 

另外也可以通过ANDROID_HOME变量指向sdk路径的方式来使得编译时候能找到SDK。

 

我很悲催，上面两种方式都不可行，暂时不想花时间去检查ant的问题，就用第三种方式，直接在ant命令行用-D来插入定义：

 

> ant debug -Dsdk.dir=/Users/laoyongchao/Applications/adt-bundle-mac/sdk

 

然后安装：

 

> agspc98:proj.android laoyongchao$ adb install bin/TestCocos2dx-debug.apk 
> 
> * daemon not running. starting it now on port 5037 *
> 
> * daemon started successfully *
> 
> 3458 KB/s (1624090 bytes in 0.458s)
> 
> pkg: /data/local/tmp/TestCocos2dx-debug.apk
> 
> Success

 

 

 