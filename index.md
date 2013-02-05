---
layout: page
title: 欢迎
tagline: 介绍
---
{% include JB/setup %}


## 博文列表

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 关于

站点还在建设中...
