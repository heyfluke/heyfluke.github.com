---
layout: post
title: "升级gitlab到5.0遇到的问题"
description: ""
category: 服务器维护
tags: [gitlab, gitlab升级]
date: 2013-03-24 01:00:17 +0800
---
{% include JB/setup %}

[GitLab已经升级到了5.0版本][1]，并且已经宣称达到了稳定的水平。比较期待新的代码查看风格，所以升级了一下，遇到了两个问题：

1. satellites创建失败。检查一下gitlab.yml里面的satellites路径设置，用 git 用户创建一下这个目录就可以了。

2. wiki升级以后消失了。这是因为换了git的方式来存储wiki，看起来这种方式更加靠谱。不过不靠谱的是自动升级失败，不支持编码：

```
root@xxx:/home/git/gitlab# sudo -u git -H bundle exec rake gitlab:wiki:migrate RAILS_ENV=production

Migrating Wiki for 'xxx'
Initialized empty Git repository in /home/git/repositories/xxx.wiki.git/
  Creating page '翻译文档'...
  Created page '翻译文档' [OK]
    Creating revisions...
  Creating page '项目主页'...
rake aborted!
incompatible character encodings: UTF-8 and ASCII-8BIT
```

[1]: http://blog.gitlab.org/gitlab-5-dot-0-has-been-released/ 