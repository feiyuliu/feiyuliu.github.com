---
layout: post
title: python for in else语法
description: ""
category: python
tags: [python]
---
{% include JB/setup %}

如果循环中有一个break被触发，python认为你找到了你想要找的东西 
如果没有任何break，而是完整循环结束，python认为你没找到你想要找的东西，那么就会执行else。 

典型的用法： 

	found = None 
	for x in objects: 
	  if x is good: 
		found = x 
		break 
	if not found: 
	   print 'no good' 

可以重写成： 

	for x in objects: 
	  if x is good: 
		break 
	else: 
	   print 'no good' 

所以如果循环正常遍历到的结尾，else会被执行。比如刚才的代码： 

	for x in range(3): 
		print x 
	else: 
		print '...' 

try except else
我们把所有可能引发错误的语句放在try块中，然后在except从句/块中处理所有的错误和异常。
如果在 try 块中没有引发异常，else从句将被执行