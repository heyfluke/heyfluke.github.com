---
layout: post
title: "错怪了jekyll和ruby"
description: ""
category: 网站维护
tags: [jekyll, ruby, mac, markdown]
---
{% include JB/setup %}

## 发现问题

在进行jekyll的时候，发现有一些错误提示信息很诡异，看起来似乎残留了homebrew的信息。

	 ___________________________________________________________________________
	| Maruku tells you:
	+---------------------------------------------------------------------------
	| String finished while reading (break on []) already read: "brew doctor' \\*before\\* you install 	anything."
	| ---------------------------------------------------------------------------
	| You should run `brew doctor' \*before\* you install anything.EOF
	| -------------------------------------------------------------|--------------
	|                                                              +--- Byte 61
	| Shown bytes [0 to 61] of 61:
	| >You should run `brew doctor' \*before\* you install anything.
	| 
	| At line 84
	|    header1     |==> Installation successful!|
	|      empty     ||
	|       text     |You should run `brew doctor' \*before\* you install anything.|
	|      empty --> ||
	|       text     |Now type: brew help|
	+---------------------------------------------------------------------------
	!/Library/Ruby/Gems/1.8/gems/maruku-0.6.1/lib/maruku/errors_management.rb:49:in `maruku_error'
	!/Library/Ruby/Gems/1.8/gems/maruku-0.6.1/lib/maruku/input/parse_span_better.rb:402:in `read_simple'
	!/Library/Ruby/Gems/1.8/gems/maruku-0.6.1/lib/maruku/input/parse_span_better.rb:521:in `read_inline_	code'
	!/Library/Ruby/Gems/1.8/gems/maruku-0.6.1/lib/maruku/input/parse_span_better.rb:89:in `read_span'
	!/Library/Ruby/Gems/1.8/gems/maruku-0.6.1/lib/maruku/input/parse_span_better.rb:46:in `parse_span_	better'
	\___________________________________________________________________________

## 解决问题 

由于不懂ruby，暂时也没时间去学习，所以暂时怀疑是ruby安装的一些包是经过homebrew的，所以想办法先卸载所有的ruby包，这里把所有的gem都卸载掉。

	for x in `gem list --no-versions`; do sudo gem uninstall $x -a -x -I; done

然后重新安装jekyll:sudo gem install jekyll。

重新运行jekyll以后发现问题并没有被解决掉。。

后来当然是从要处理的文档入手，jekyll肯定是在处理某条blog的过程中发生了问题，通过二分法很快找到了出问题的文档，竟然是“试用homebrew，一个优雅的包管理”这篇文章的……所以里面出现homebrew相关字样也就不足为奇了。

主要是导出的markdown格式处理起来有问题，顺便也发现了通过插件把wordpress导出到jekyll的过程，可能缺失或者弄错了一些东西，包括链接可能会丢失，单行区块引用可能会出问题等。
