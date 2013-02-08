---
layout: post
title: "jekyll技巧：设置图片最大宽度"
description: ""
category: 网站维护
tags: [jekyll, css, img]
---
{% include JB/setup %}

最近切换到了[jekyll][1]的方案下面编写blog，用markdown作为主要的文章编写语言，倒也很方便，但有一些不好的地方，譬如图片不能设置默认宽度（当然也可以通过嵌html的方式来设置），这就必须用css来解决了。

今天弄了一下，只需要在img的样式里面加上max-width限定就好了，现在页面美观多了：

	img {max-width:100%;}

[1]: https://github.com/mojombo/jekyll
