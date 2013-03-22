---
layout: post
title: git返回上一次commit
description: 在电脑上删除没有commit怎么恢复？ 在电脑上删除了，并且commit，怎么恢复
category: git
tags: [github]
---
{% include JB/setup %}
在window上直接删除了某个文件，但是没有commit。用下面的命令

    git pull 
显示的already up-to-date。
怎么恢复呢。网上搜了一下，用命令

    git checkout -- file //file是你删除的文件。

但是我添加了一个test文件，然后commit到github。怎么恢复？
于是又找了，说是用

    git log file 
得到 commit的版本号，然后恢复命令 

    git reset 版本号 file 
    git commit -m "comment" 
但是显示的不行。后来在网上发现可以用

    git revert --no-commit head
来返回上一次commit。不错。
