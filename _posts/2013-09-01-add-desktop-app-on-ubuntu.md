---
layout: post
title: "添加ubunut桌面图标"
description: ""
category: 
tags: [ubuntu configration]
---
{% include JB/setup %}
怎么在ubuntu系统中添加添加桌面图标:

首先要在`/usr/share/applications`中添加一个`.desktop`文件,具体的内容可以参考里面的desktop文件,这里写一下我的goagent的desktop文件
	
	Name=goagent
	Comment=wall agent
	Exec=/home/mac/soft/goagent/local/goagent-gtk.py
	Icon=/home/mac/soft/goagent/local/goagent-logo.png
	Terminal=true //主要是在终端运行python脚本文件
	Type=Application
	Encoding=UTF-8
	Categories=Application;Programing

**注意:要设置`Terminal=true`让其在终端运行python脚本文件.如果在终端中遇到`Permission denied` 要给python脚本添加执行权限`chmod u+x /home/mac/soft/goagent/local/goagent-gtk.py`** 