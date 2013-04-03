---
layout: post
title: windows下安装python虚拟机环境virtualenv
description: ""
category: python
tags: [python]
---
{% include JB/setup %}

###下载安装Python2.7.3
到python官方网站下载windows版本的python，点击可以直接安装，这里我安装在<code>D:\Python27</code>下
###安装setuptools
为了支持easy_install等脚本，安装完Python后要安装[setuptools-0.6c11.win32-py2.7.exe](http://pypi.python.org/pypi/setuptools#files)

然后把python的目录添加到Windows的环境变量path中。

    ;D:\Python27;D:\Python27\Scripts
###安装virtualenv
在控制台中输入命令

    D:\pyproj>easy_install virtualenv
###创建虚拟环境
在项目的目录下运行下面命令：

    D:\pyproj\flasktes>virtualenv env
	New python executable in env\Scripts\python.ex
	Installing setuptools................done.
	Installing pip...................done.
###使用虚拟环境
在项目的Scripts目录下运行下面命令

	D:\pyproj\flasktes\env\Scripts>activate
	(env) D:\pyproj\flasktes\env\Scripts>
###在eclipse的pydev插件下开发
使用pydev开发时，要选择虚拟环境下的python解释器。

![图1](../../../../assets/postimg/pydev.jpg)

但是出现了以下的错误：
![图2](../../../../assets/postimg/pydev2.jpg)

应该错误提示很明显，因为我使用的虚拟环境下的python，所以它需要加载安装python目录下的lib文件夹下的包，所以还要加上下面圈起来的目录。
![图3](../../../../assets/postimg/pydev3.jpg)

