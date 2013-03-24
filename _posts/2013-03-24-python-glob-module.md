---
layout: post
title: python glob模块
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
glob模块是python自带的模块，可以用它来查找符合特定规则的文件路径名和文件。跟使用windows下的文件搜索差不多。查找文件只用到三个匹配符："*","?","[]"。"*"匹配0个或多个字符；"?"匹配单个字符；"[]"匹配指定范围内的字符，如：[0-9]匹配数字。
主要的方法glob.glob(pathname)
返回所有匹配的文件路径列表。它只有一个参数pathname，定义了文件路径匹配规则，这里可以是绝对路径，也可以是相对路径。
	
	#导入模块
	>>> import glob
	#调用glob()方法
	>>> glob.glob(r'c:\*.txt')
	['c:\\log_client.txt', 'c:\\test.txt'] #返回一个列表
	>>> glob.glob('*.txt')
	['LICENSE.txt', 'NEWS.txt', 'README.txt'] #返回当前目录下的txt文件，不包括文件路径
glob方法的定义如下：

	glob.glob(pathname)
		Return a possibly-empty list of path names that match pathname, which must be a string containing a path specification. pathname can be either absolute (like /usr/src/Python-1.5/Makefile) or relative (like ../../Tools/*/*.gif), and can contain shell-style wildcards. Broken symlinks are included in the results (as in the shell).
