---
layout: post
title: python中try except else语句
description: ""
category: python
tags: [python]
---
{% include JB/setup %}

首先来代码分析一下：

	def flatten(nested):
		try:
			# Don't iterate over string-like objects:
			try: nested + ''
			except TypeError: pass
			else: raise TypeError
			for sublist in nested:
				for element in flatten(sublist):
					yield element
		except TypeError:
			yield nested
如果表达式 nested + ''引发异常，就执行except的TypeError。它将执行pass语句，什么也没有发生。然后执行for语句。

如果表达式 nested + ''没有引发异常，就执行try的else语句。它执行 raise TypeError语句，引发一个TypeError异常，然后执行外层的except TypeError:语句。

try首行底下的代码块代表此语句的主要动作：试着执行的程序代码。except分句定义try代码块内引发的异常处理器，而else分句（如果有）则是提供没有发生异常时候要执行的处理器。

如果try代码块语句执行时发生了异常，Python就跳回try，执行try下面第一个符合引发的异常的except分句下面的语句。当except代码执行后（除非except代码块引发另一异常），控制全就会到整个try语句后继续执行。

如果异常发生在try代码块内，没有符合的except分句，异常就会向上传递到程序的之前进入try中，或者到这个进程的顶层（使用Python终止这个程序并打印默认的错误消息）

如果try首行底下执行的语句没有发生异常，Python就会执行else行下的语句（如果有的话），控制权会在整个try语句下继续。

也就是说except分句会捕捉try代码块执行时所有发生的任何异常，而else分句只在try代码执行没有发生异常时才执行，finally分句无法释放发生异常都执行。