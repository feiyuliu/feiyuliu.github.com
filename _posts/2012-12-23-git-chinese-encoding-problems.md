---
layout: post
title: git中文乱码问题
description: git在windows上安装出现的一系列的中文乱码问题的解决方法
category: git
tags: [github]
---
{% include JB/setup %}
Git中文乱码问题
在windows中安装GIT后出现的中文乱码问题的解决方案。

1、 在GIT GUI上查看文件时显示的中文乱码。解决方法：

进入“编辑 -> 选项”，把 Default File Contents Encoding 改为 utf-8.
改完后在 C:\Users\Administrator\.gitconfig 可以看到修改结果。

2、 在git bash 先输入ls命令，显示的中文文件或中文目录名乱码问题。解决方法：

在etc/git-completion.bash中增加一行： 

    alias ls='ls --show-control-chars --color=auto'

3、 git commit不能输入中文注释问题，解决方法：

修改问题etc/inputrc中对应的行：

    set output-meta on 
    set convert-meta off
4、 git log无法显示中文注释 

在文件etc/profile中增加一行：

    export LESSCHARSET=iso8859