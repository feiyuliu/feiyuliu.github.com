---
layout: post
title: "github重命令帐户后出现提交代码403问题"
description: "github 403 problem"
category: 
tags: [github]
---
{% include JB/setup %}

最近修改了github的用户名，然后提交代码的时候出现如下的错误：
```
$ git push -f origin master
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/feythin/free-programming-books.git/info/refs
fatal: HTTP request failed
```
此时只要reset一下提交的url就可以了，但是得每个项目都得set一次，目前没有想到好的办法
```
$ git remote set-url origin https://feythin@github.com/feythin/free-programming-books.git
$ git push -f origin master
```
