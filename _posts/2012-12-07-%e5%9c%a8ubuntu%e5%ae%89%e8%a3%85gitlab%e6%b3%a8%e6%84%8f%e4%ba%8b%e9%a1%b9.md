---
title: 在ubuntu安装gitlab注意事项
author: fluke
layout: post
permalink: >
  /2012/12/%e5%9c%a8ubuntu%e5%ae%89%e8%a3%85gitlab%e6%b3%a8%e6%84%8f%e4%ba%8b%e9%a1%b9/
categories:
  - 服务器维护
tags:
  - git
  - gitlab
  - git仓库
---
# 

决定在新的项目里面享受一下[gitlab][1]。安装的方法在github上面有：。

 [1]: http://gitlabhq.com/

在ubuntu的vps上面安装，总体还比较顺利，不过出现了安装bundle以及某句rake时候莫名奇妙的问题，检查了一下，发现文章上用的ruby是1.9.3版本，而ubuntu仓库里面默认的是1.8，难道也和python一样最新版已经没什么出现的必要了？

所以应该安装到ruby 1.9.3 : “aptitude install ruby1.9.3”。

另外第五步的手工创建数据库不需要自己做，因为在后面的“sudo -u gitlab bundle exec rake gitlab:app:setup RAILS_ENV=production”会尝试去建立数据库。

结合数据库的维护，又从自动检查配置情况的脚本的输出来看，文档应该跟不上最新版本的变化了：

> Starting diagnostics
> 
> config/database.yml…………exists
> 
> config/gitlab.yml…………exists
> 
> /home/git/repositories/…………exists
> 
> /home/git/repositories/ is writable?…………YES
> 
> Can clone gitolite-admin?…………YES
> 
> Can git commit?…………YES
> 
> UMASK for .gitolite.rc is 0007? …………YES
> 
> /home/git/.gitolite/hooks/common/post-receive exists? …………YES  
>  

再配置下nginx就能访问网站了，创建的项目默认以localhost来做主机名，要到/home/gitlab/gitlab/config/gitlab.yml里面去修改。 
PS. gitlab好像修改了我mysql root密码，还没来得及去调查清楚。