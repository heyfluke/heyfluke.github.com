---
layout: post
title: "jekyll的时间处理问题"
description: ""
category: 网站维护
tags: [jekyll, timezone, ruby]
date: 2013-02-13 15:09:20 +0800
---
{% include JB/setup %}

jekyll的时间处理看起来比较复杂，简单描述一下：

1. 默认字符串输出的时候时区为本地时间。譬如在我的机子上面输出完整的时间字符串形如“2013-02-13 14:30:00 +0800”，而在github则形如“2013-02-13 14:30:00 -0800”（这里仅仅就时间格式来举例说明，不代表两个时间是同一个）。

2. date对象（对ruby不熟悉，忘了是Time还是DateTime对象）默认带有时区信息，如果输入文字信息供parse的话，也需要从里面读取时区信息，一个完整的信息形如“2013-02-13 14:30:00 +0800”表示2012年2月13日下午2点30分，时区为东8区。如果读入的时间字符串为“2013-02-12 00:00:00 +0800”则表示在东8区的2月12日凌晨0点；如果去掉了时区来读的话（“2013-02-12 00:00:00”）则默认表示0时区的2月12日凌晨，如果我在-1时区输出对应的时间信息则为“2013-02-11 23:00:00 -0100”；如果去掉了时间只写日期的话（"2013-02-12"）则时间似乎为“本地时间”的0点，这个时候，我在x时区输出的时间就是“2013-02-12 00:00:00 x”，不但丢掉了时间信息，还造成了不确定时区的问题。
对于这两个问题，我的解决办法暂时就是在写文章的时候，尽量用完整的时间字符串，然后输出时间的时候，保留时区信息，虽然对于中国的读者来说显示出来的可能还是-8时间，但起码时间是对的。

在考虑以后切换jekyll到本地生成（那可能换更加熟悉的python写的框架譬如[pelican][1]，在本地编写插件的时候也更加方便。但目前考虑到github直接支持上传markdown文件到服务器上面使用jekyll来生成页面，所以还是先留着。这样在ipad等客户端写的时候，就不需要在本地生成了。

另外，jekyll在发布的时候并没有在文章里面写名时间导致时间为默认的文件名时间，所以只能显示为当日，并且不确定时区，为此，我修改了Rakefile，在发布的时候默认获取当前时间，或者解析时间（其中从命令行参数解析时间似乎原来就有bug），两次改动在：

[https://github.com/heyfluke/heyfluke.github.com/commit/3ef10272c141a23a49e2531e675e5bb919420b0b#Rakefile][2]

和

[https://github.com/heyfluke/heyfluke.github.com/commit/9372152e3c3cc16e4d84c599f0aea1762da6d5f1#Rakefile][3]

最后，为了时间显示得稍微友好一些，我使用strftime的方式来格式化字符串，使得+0800这样的时区至少显示为CST，虽然时区简写有歧义但是体验稍微好了一点。

	<span class="date">{ { post.date | date: "%Y-%m-%d %H:%M:%S %Z" } } <!-- ({ { post.date }}) --> </span>

[1]: http://pelican.notmyidea.org
[2]: https://github.com/heyfluke/heyfluke.github.com/commit/3ef10272c141a23a49e2531e675e5bb919420b0b#Rakefile
[3]: https://github.com/heyfluke/heyfluke.github.com/commit/9372152e3c3cc16e4d84c599f0aea1762da6d5f1#Rakefile

