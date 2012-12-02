---
layout: post
title: "用Jekyll写技术博客"
description: "用Jekyll写技术博客"
category: Jekyll
tags: [Jekyll]
---
{% include JB/setup %}
####缘由
曾经也有过写技术博客的冲动。申请过bloger，msn space。但总觉得这些blog如果写一些日常的感受还可以，但总是让人不能专注于写作，很小的编辑框，还要时刻注意换行，稍不注意，显示的格式就不对了。
   
直到最近，我在一篇blog上知道了－－Jekyll
   
老外写书已经采用编程和项目的方式了, The Pragmatic Bookshelf的书都是这么写出来的，通过git做版本管理，通过Rake执行图书排版，甚至通过hudson进行每次提交进行排版。
   
Jekyll时ruby的一个项目。允许通过git进行版本管理，托管在github上作为一个项目。并通过静态页面进行访问。Tom是Jekyll的作者，同时也是github的创始人，[这篇文章](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)中Tom介绍了开发jekyll的初衷。
   
####使用
   
   更详细的使用步骤参见[这里](http://jekyllbootstrap.com/)
###写post
    $ rake post title="Jekyll-Intrduction"
   
####本地preview
在_post目录中完成编辑，使用vim 本地启动server，进行预览,如果在预览的过程中又对文件进行了编辑，会动态生成新的网页。

    $ rake preview
####提交到github
将文章提交到github上。如果使用了github提供的个人主页服务，则提交之后即能够访问。首先要创建一个 “用户名.github.com”的仓库.具体步骤[参见](http://jekyllbootstrap.com/usage/deployment-and-hosting.html)

    $ git add .
    $ git commit
    $ git push
    
   
   