---
layout: post
title: "苹果iPad/iPhone越狱并访问facebook"
description: ""
category: 其他技术
tags: [越狱, jailbreak, iPad/iPhone, 翻墙]
date: 2013-04-03 12:41:40 +0800
---
{% include JB/setup %}

在iPad上面访问[facebook][1]是一件很爽的事情（现在已经有for iPad的App了，不过我还没试过），常见的方式是使用VPN或者goagent，不过由于被墙的方式只是DNS污染，所以更简单的一个办法是修改hosts文件，在里面静态绑定域名和IP。

我在OS X下面使用[smarthosts][2]来自动设置自己的hosts文件(这里有个段子，愚人节那天，在[微博][3]上有朋友说“facebook/twitter已经解封了，珠海测试成功”，然后我还傻傻的去测试了一下，能访问，并且检查了我翻墙的黑名单发现没存在facebook，于是汇报广州已解封……)，不过这个文件变更得并不频繁，所以我选择手工同步到我的iPad上面。

要更改hosts文件必须先越狱，目前ios6最完善的越狱方案是[evasi0n][4]（只是不支持6.13），使用它越狱以后，可以在cydia下载openssh，然后在iPad设置里面打开ssh访问，并且看到自己的ip地址。接着就可以通过ssh来访问了，例如ssh root@myipad，默认密码是alpine，进去以后用passwd来更改。

登陆以后先备份一下原来的hosts文件

```
cp /etc/hosts /ect/hosts.orig
```

然后看下自己主机（我用了smarthosts）上面的hosts文件：

	agspc98:aWhoCall laoyongchao$ sudo cat /etc/hosts | grep face
	173.252.100.17	api-read.facebook.com
	173.252.100.17	api.facebook.com
	69.171.237.36	apps.facebook.com
	61.213.189.98	b.static.ak.facebook.com
	66.220.145.63	bigzipfiles.facebook.com
	66.220.149.88	c.facebook.com
	69.171.227.26	chat.facebook.com
	66.220.147.96	check4.facebook.com
	184.31.111.139	connect.facebook.net
	69.171.227.19	creativeupload.facebook.com
	69.171.240.99	d.facebook.com
	173.252.100.17	developers.facebook.com
	66.220.149.90	error.facebook.com
	173.252.100.18	facebook.com
	173.252.100.17	graph.facebook.com
	66.220.151.33	hphotos-ak-snc1.facebook.com
	66.220.151.33	hphotos-ak-snc3.facebook.com
	66.220.144.43	ldap.thefacebook.com
	173.252.100.25	m.facebook.com
	66.220.149.96	o.facebook.com
	69.171.233.33	orcart.facebook.com
	69.171.245.18	photos-ak-ash1.facebook.com
	69.171.245.18	photos-ash1.facebook.com
	66.220.149.90	pixel.facebook.com
	118.214.190.105	profile.ak.facebook.com
	69.171.247.22	s-static.facebook.com
	184.26.194.110	s-static.ak.facebook.com
	69.171.227.30	secure-media.facebook.com
	66.220.149.96	ssl.facebook.com
	69.171.247.38	ssl.connect.facebook.com
	69.63.189.76	star.facebook.com
	61.213.189.98	static.ak.facebook.com
	69.171.229.17	upload.facebook.com
	66.220.151.31	vupload.facebook.com
	69.171.225.31	www.connect.facebook.com
	173.252.100.17	www.facebook.com
	69.171.242.72	zh-CN.facebook.com

然后在ipad的shell里面增加这些hosts。

```
cat >> /etc/hosts
```

然后粘贴：

	173.252.100.17	api-read.facebook.com
	173.252.100.17	api.facebook.com
	69.171.237.36	apps.facebook.com
	61.213.189.98	b.static.ak.facebook.com
	66.220.145.63	bigzipfiles.facebook.com
	66.220.149.88	c.facebook.com
	69.171.227.26	chat.facebook.com
	66.220.147.96	check4.facebook.com
	184.31.111.139	connect.facebook.net
	69.171.227.19	creativeupload.facebook.com
	69.171.240.99	d.facebook.com
	173.252.100.17	developers.facebook.com
	66.220.149.90	error.facebook.com
	173.252.100.18	facebook.com
	173.252.100.17	graph.facebook.com
	66.220.151.33	hphotos-ak-snc1.facebook.com
	66.220.151.33	hphotos-ak-snc3.facebook.com
	66.220.144.43	ldap.thefacebook.com
	173.252.100.25	m.facebook.com
	66.220.149.96	o.facebook.com
	69.171.233.33	orcart.facebook.com
	69.171.245.18	photos-ak-ash1.facebook.com
	69.171.245.18	photos-ash1.facebook.com
	66.220.149.90	pixel.facebook.com
	118.214.190.105	profile.ak.facebook.com
	69.171.247.22	s-static.facebook.com
	184.26.194.110	s-static.ak.facebook.com
	69.171.227.30	secure-media.facebook.com
	66.220.149.96	ssl.facebook.com
	69.171.247.38	ssl.connect.facebook.com
	69.63.189.76	star.facebook.com
	61.213.189.98	static.ak.facebook.com
	69.171.229.17	upload.facebook.com
	66.220.151.31	vupload.facebook.com
	69.171.225.31	www.connect.facebook.com
	173.252.100.17	www.facebook.com
	69.171.242.72	zh-CN.facebook.com

最后
```
control + D
```

为了浏览器dns缓存清空，可以重启一下iPad。

访问facebook的时候需要用https://前缀，为了每次都强制使用https方式访问，可以在facebook的设置里面更改：

settings -> security -> Secure Browsing -> enable

[1]: https://www.facebook.com
[2]: https://code.google.com/p/smarthosts/
[3]: http://www.weibo.com
[4]: http://evasi0n.com
