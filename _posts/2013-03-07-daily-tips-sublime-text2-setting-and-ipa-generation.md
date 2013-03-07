---
layout: post
title: "今日技巧：Sublime Text 2语法缩进配置和ipa文件生成"
description: ""
category: 其他技术
tags: [daily tips, 今日技巧, Sublime Text 2, ipa]
date: 2013-03-07 21:01:36 +0800
---
{% include JB/setup %}

## 在Sublime Text 2中配置python的tab缩进为空格

[Tublime text 2][1]是一个很灵活的编辑器，不过所有的设置都通过配置文件来完成，感觉体验有点不好。不过不管这么说，熟悉了以后还是很方便的。今天修改一下针对python的缩进设置，一般在python的代码中，都是4格缩进（google内部好像是2格），很少用tab的，而Sublime Text 2默认对所有文件的tab都不进行转换，进行设置以后，自己输入和自动补全的tab都会自动被转换成空格。

这里在Mac OS X下操作，其他平台应该没什么区别。设置的方法是Sublime Text 2菜单 -> Preference -> Settings - More -> Syntax Specific - User，点击以后默认会打开当前文件对应的格式的配置文件，所以在点击之前，应该确认自己正在编辑python脚本或者先在View菜单里面设置当前的语言为python。

这里打开的是python.sumlime-settings文件，默认可能是空的，加入如下内容：

```
{
    "tab_size": 4,
    "translate_tabs_to_spaces": true
}
```

配置文件的格式为json，虽然还不算很友好，但是书写起来已经比XML舒服很多了。其中第一行表示tab占用的位置，第二行表示把占用位置都替换成空格。

关于Sumlime Text 2的配置，本次是参考了官方的手册[Indentation Settings][2]。

## Xcode中打包iOS程序为ipa包的步骤和注意事项

在Xcode中打包程序出来测试是常见的工作，方便小范围测试。这里测试的版本是Xcode4.6+iOS5.0，打包的步骤如下：

* 确保在$程序名-Info.plist中的Application Requires iPhone env.. 的值为No。后面有附图表明这点。
* 在Xcode中选择Product -> Build For -> Archiving。
* 在Xcode左侧的Product文件夹会有一个程序名.app的应用，可能没有app后缀，只有app图标。右击它，点击Show in finder。
* 在Finder里面把这个程序（其实是一个有隐藏.app后缀的文件夹，苹果惯用的Bundle方式）拷贝到外面。
* 建立一个Payload文件夹，把程序放进去，然后把Payload压缩成Payload.zip，然后更名为你的程序.ipa即可

这个时候就可以到91助手或者iTunes里面去测试了。

![][3]

[1]: http://www.sublimetext.com/
[2]: http://www.sublimetext.com/docs/2/indentation.html
[3]: /images/upload/2013-03-07-info.plist.png

