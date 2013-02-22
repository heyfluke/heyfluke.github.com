---
layout: post
title: "把gitlab从3.1升级到4.0需要注意的问题"
description: ""
category: 其他技术
tags: [gitlab, 升级gitlab]
date: 2013-02-22 15:14:14 +0800
---
{% include JB/setup %}

现在gitlab已经发展到4.1版本（其实在代码仓库里面已经能看到4.2了，文档似乎还有5.x的了），我的才3.1，所以打算升级一下，最新的版本支持公开仓库和用户自己创建仓库，还是挺吸引的，最重要的是以后平滑升级应该会比较有好处。

按照[From 3.1 to 4.0][1]的升级文档来操作，似乎漏掉了一些问题：

1. gitolite已经需要升级，但是我还没升级，问题不大。但对以后可能会有影响。所以打算过后也升级一下。
2. init脚本始终检测不过，但不影响使用。
3. 有检测脚本用来检测安装情况：

	sudo -u gitlab -H bundle exec rake gitlab:check RAILS_ENV=production

4. 4.0开始不支持在wiki评论了，幸好数据库里面的数据还没变，只是不展示了而已，所以自己可以修改一下：

	UPDATE  `notes` SET noteable_type =  "",noteable_id = NULL WHERE noteable_type =  "Wiki"

5. 检查脚本会报项目没有satellites，我也不知道是什么意思，但是提示了一句更新的shell脚本，其中漏掉了一个参数，原语句为：

	sudo -u gitlab -H bundle exec rake gitlab:satellites:create

需要更新为：

	sudo -u gitlab -H bundle exec rake gitlab:satellites:create RAILS_ENV=production

[1]: https://github.com/gitlabhq/gitlabhq/wiki/From-3.1-to-4.0
