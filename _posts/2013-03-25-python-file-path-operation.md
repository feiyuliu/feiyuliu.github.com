---
layout: post
title: python文件路径操作
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
python的文件和路径操作函数基本上位于os和os.path模块中。
os.listdir(dirname)：列出dirname下的目录和文件 
os.path.isdir(name):判断name是不是一个目录，name不是目录就返回false 
os.path.isfile(name):判断name是不是一个文件，不存在name也返回false 
os.getcwd()：获得当前工作目录 
os.path.split(name):分割文件名与目录（事实上，如果你完全使用目录，它也会将最后一个目录

作为文件名而分离，同时它不会判断文件或目录是否存在）
os.path.splitext():分离文件名与扩展名 
os.path.basename(path):返回文件名 
os.path.dirname(path):返回文件路径 
os.path.join(path,name):连接目录与文件名或目录 

可以使用简单的方法匹配某个目录下的所有子目录或文件，用法也很简单。 
glob.glob(regression) 返回一个列表
###os.listdir(dirname)
功能相当于在dirname目录下执行dir命令，它返回一个list。不包括dirname的文件和目录的list

	>>> os.listdir("d:/github")
	['about.html', 'book', 'en', 'feiyuliu.github.com', 'life', 'pyssh', 'PythonStud
	y', 'StudyShell']
其中about.html是文件，feiyuliu.github.com是目录。
###os.path.split(path)
path为一个路径，返回一个元组，把path分为两部分。

	>>> os.path.split("d:/github/about.html")
	('d:/github', 'about.html')
	>>> os.path.split("about.html")
	('', 'about.html')
###os.path.splitext(filename)
把文件分为文件名称路径和扩展名。返回一个元组。

	>>> os.path.splitext("about.html")
	('about', '.html')
	>>> os.path.splitext("d:/github/about.html")
	('d:/github/about', '.html')
###os.path.dirname(path)
把目录输出，不输出文件名。返回字符串类型。

	>>> os.path.dirname("d:/github/about.html")
	'd:/github'
	>>> os.path.dirname("about.html")
	'' #输出为空
###os.path.basename(filename)
取得文件名。返回字符串类型

	>>> os.path.basename("d:/github/about.html")
	'about.html' #注意不包括目录



