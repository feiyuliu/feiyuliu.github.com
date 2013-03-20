---
layout: post
title: windows下安装python模块
description: "windows下安装python模块，eclipse能够加载到模块，能够识别中文"
category: pythonlearning
tags: [python]
---
{% include JB/setup %}
由于我用的是windows系统，在其上安装的python2.7环境，然后使用eclipse开发。
首先要安装pydev插件。至于插件怎么安装，你自己google去吧。下面说说我安装python模块的事。
由于python很多的模块在它的安装包里是没有的，这就需要自己额外的安装自己的需要的包文件。下面就我安装lxml模块为例。
首先下载lxml模块的安装包，在这里

    https://pypi.python.org/pypi/lxml/3.1.0
推荐在https://pypi.python.org/pypi/搜索自己需要的安装包，那里面的包都是最新的。
由于它提供了windows的安装包lxml-3.1.0.win32-py2.7.exe，所以只要安装就可以了。如果windows下编译的安装包，就自己下载一个，如cssselect-0.8.tar.gz。
下载完成后，在cmd命令下进入你要的安装目录，如：D:\Python27\pythontools\cssselect-0.8> ，当然，不一定要放在python的目录，但是必须**安装python时，它的路径放到windows的path中**
然后执行：

    python setup.py install
检查安装包是否成功。在python的命令下输入:

    #>>> import cssselect
    #>>> dir(cssselect)
    ['ExpressionError', 'GenericTranslator', 'HTMLTranslator', 'Selector', 'Selector
    Error', 'SelectorSyntaxError', 'VERSION', '__builtins__', '__doc__', '__file__',
     '__name__', '__package__', '__path__', '__version__', 'parse', 'parser', 'xpath
    ']
     #>>>
如果这样就没有问题了。
还有使用eclipse的pydev开发python程序时，遇到编码的问题。在py文件里输入中文时，出现这样的错误：

    SyntaxError: Non-ASCII character '\xe8' in file 
解决方法是子文件的开头输入：

    # -*- coding: utf-8 -*- 
记住还要修改项目的编码为utf-8

