---
title: 给gitlab加上Google Analytics的统计跟踪代码
author: fluke
layout: post
permalink: >
  /2012/12/%e7%bb%99gitlab%e5%8a%a0%e4%b8%8agoogle-analytics%e7%9a%84%e7%bb%9f%e8%ae%a1%e8%b7%9f%e8%b8%aa%e4%bb%a3%e7%a0%81/
categories:
  - web
tags:
  - gitlab
  - google analytics
  - haml
  - javascript
---
# 

Google Analytics提供了javascript代码来进行跟踪统计，要插入gitlab中，需要编辑它的layout文件，这种文件用的是haml格式（ruby的一种html模板语言）。

要往haml里面添加javascript内容，需要用到**:javascript**过滤器。如果google提供的代码如下：

> 
> 
>  
> 
>   var \_gaq = \_gaq || [];
> 
>   \_gaq.push(['\_setAccount', 'XXXX']);
> 
>   \_gaq.push(['\_trackPageview']);
> 
>  
> 
>   (function() {
> 
>     var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
> 
>     ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') '.google-analytics.com/ga.js';
> 
>     var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
> 
>   })();
> 
>  
> 
> 
> 
> 则需要往gitlab/app/views/layout/_head.html.haml文件最后添加的代码是：
> 
> > :javascript
> > 
> >   var \_gaq = \_gaq || [];
> > 
> >   \_gaq.push(['\_setAccount', 'XXXX']);
> > 
> >   \_gaq.push(['\_trackPageview']);
> > 
> >  
> > 
> >   (function() {
> > 
> >     var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
> > 
> >     ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') '.google-analytics.com/ga.js';
> > 
> >     var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
> > 
> >   })();
> 
>   
>  