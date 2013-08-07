---
layout: post
title: "改变Drupal目录以后发生的include错误的解决办法"
description: ""
category: 其他技术
tags: [Drupal, PHP, PEAR]
date: Wed Aug 07 12:13:07 +0800 2013
---
{% include JB/setup %}

在改变Drupal目录以后，出现inc引用路径出错的问题，错误显示还是原来的绝对路径，而到源码里面看DRUPAL_ROOT都是getcwd()得到的，所以问题显得很诡异。

错误形如：

     Fatal error: require_once(): Failed opening required '/Users/fluke/Public/sites/local/www/d1/includes/database/query.inc' (include_path='.::/opt/local/lib/php/pear') in /Users/fluke/Public/sites/local/www/d1/includes/database/select.inc on line 7

经过修改文件发现，每次修改.inc文件以后，这个错误就不存在了，轮到了下一个inc。

猜测PHP或者PEAR里面对inc文件有缓存，所以看到的错误也是和原来的路径一样。

尝试touch一下就好了： for f in `find . -name "*.inc"`; do touch $f ; done


