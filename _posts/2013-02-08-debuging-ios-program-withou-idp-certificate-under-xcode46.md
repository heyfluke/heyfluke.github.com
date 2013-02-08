---
layout: post
title: "在Xcode4.6下无证书调试iOS程序（iOS6.1）"
description: ""
category: 
tags: []
---
{% include JB/setup %}

苹果今日推出了Xcode4.6，相隔几天iOS6.1也出了完美越狱，在这种情况下，应该很多人会升级到Xcode4.6了，首先需要解决的往往就是真机免证书调试问题。我已经测试过可以完成，下面分两个步骤描述。

### 打补丁

对Xcode4.6打补丁的办法类似于原来网上比较流行的一个教程《[Xcode 4.1/4.2/4.3/4.4/4.5 + iOS 5.1.1免证书(iDP)开发+真机调试+生成IPA全攻略][1]》所描述的步骤，其中有一些不一样的，我在下面写出来。

如果之前已经进行过老版本的破解，证书就不需要重新创建了。

修改Xcode的配置文件和二进制文件
旧:（Xcode4.5请执行）cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.0.sdk
新：（Xcode4.6请执行）cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.1.sdk
sudo cp SDKSettings.plist SDKSettings.plist.orig


sudo vim SDKSettings.plist  (旧的4.5不是文本，而4.6是文本，可以直接编辑)
将以下两段中的YES改为NO
	<key>CODE_SIGNING_REQUIRED</key>
	<string>YES</string>
	和
	<key>ENTITLEMENTS_REQUIRED</key>
	<string>YES</string>

	cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform

备份
	sudo cp Info.plist Info.plist.orig

编辑文件
（Xcode4.1/4.2/4.3/4.4请执行）sudo vim Info.plist
将全部的XCiPhoneOSCodeSignContext 修改成 XCCodeSignContext，网上的大部分文章说有2处，但我找到了3处，可能是Xcode 4.1要多一处？（Xcode 4.2/4.3/4.3.2也有三处）总之都改掉了。提示：在在vim中输入/要搜索的内容来搜索，按n键是搜索下一处。

（Xcode 4.5/4.6)编辑命令如下
	sudo /Applications/Xcode.app/Contents/MacOS/Xcode /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Info.plist
Xcode 4.5/4.6也有三处，分别在DefaultProperties分支下、RuntimeRequirements分支下和OverrideProperties分支下。


	#(Xcode 4.3/4.4/4.5/4.6执行) (记得权限不够要sudo)
	mkdir /Applications/Xcode.app/Contents/Developer/iphoneentitlements
	cd /Applications/Xcode.app/Contents/Developer/iphoneentitlements
	curl -O http://www.alexwhittemore.com/iphone/gen_entitlements.txt
	mv gen_entitlements.txt gen_entitlements.py
	chmod 777 gen_entitlements.py

### 添加AppSync
AppSync适用于校验盗版签名的一个程序，安装了才能安装第三方盗版软件。我这里紧用作调试。
安装办法是在Cydia的源里面添加一个源，地址是：http://smolk.myrepospace.com
然后搜索AppSync就能找到AppSync for iOS 6.x。安装就好了。


[1]: http://kqwd.blog.163.com/blog/static/4122344820117191351263/

