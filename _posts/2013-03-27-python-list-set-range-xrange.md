---
layout: post
title: python list列表操作
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
list是python内置的列表类型。list和string有点相似，使用len()和[]来操作里面的元素，而且第一个元素下标示从0开始的。

	colors = ['red', 'blue', 'green']
	print colors[0]    ## red
	print colors[2]    ## green
	print len(colors)  ## 3
![图示](https://developers.google.com/edu/python/images/list1.png)
把list赋值给一个变量，它并没有复制一份，只是增加了一个指针。它在内存中还是一个list。

	b = colors   ## Does not copy the list
![图示](https://developers.google.com/edu/python/images/list2.png)
###For and IN遍历list
for var in list语法通过遍历，把每个元素赋值给var,然后就可以在循环中操作var了。**注意：当在遍历list的时候不要添加和删除list里元素**

	squares = [1, 4, 9, 16]
	sum = 0
	for num in squares:
	sum += num
	print sum  ## 30
in可以很容易的来测试是否有个元素在list中。它返回值为True或者False

	list = ['larry', 'curly', 'moe']
	if 'curly' in list:
	print 'yay'
string也可以像list一样使用for in结构。 如for ch in s: print ch 将打印string里的每个字符。
###range和xrangge
在range的方法中，它会生成一个list的对象，但是在xrange中，它生成的却是一个xrange的对象，当返回的东西不是很大的时候，或者在一个循环里，基本上都是从头查到底的情况下，这两个方法的效率差不多。但是，当返回的东西很大，或者循环中常常会被Break出来的话，还是建议使用xrange，这样既省空间，又会提高效率。
在python3中，xrange已经由range替代，已经删除了老式range的功能。

	>>> a = range(0, 100)
	>>> print type(a)
	<type 'list'>
	>>> print a
	[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
	>>> print a[0]
	0
	>>> a = xrange(0, 100)
	>>> print type(a)
	<type 'xrange'>
	>>> print a
	xrange(100)
	>>> print a[0]
	0
##list 方法
list.append(elem) -- 在list末尾添加一个元素。**注意它并没有返回一个新的list，只是修改了原来的list**

list.insert(index, elem) -- 向给定的index处插入一个元素。后面的元素后移


list.index(elem) -- 从list开始出查询elem是否在list中。找到就返回elem在list中的index，找不到就抛出ValueError。可以使用in来检查是否在list中来避免抛出错误。

list.remove(elem) -- 从开始查找第一个elem，找到就删除。没有找到就抛出ValueError。**没有返回值(返回None)**

list.sort() -- 对list排序。推荐使用sorted()函数。

list.reverse() -- 对list颠倒。**没有返回值**。 

list.pop(index) -- 移除下表index的元素并返回这个这个元素。如果没有index参数的话，就返回最后面的元素，这跟append()函数相反。

这些都list对象的方法。

	list = ['larry', 'curly', 'moe']
	list.append('shemp')         ## append elem at end
	list.insert(0, 'xxx')        ## insert elem at index 0
	list.extend(['yyy', 'zzz'])  ## add list of elems at end
	print list  ## ['xxx', 'larry', 'curly', 'moe', 'shemp', 'yyy', 'zzz']
	print list.index('curly')    ## 2

	list.remove('curly')         ## search and remove that element
	list.pop(1)                  ## removes and returns 'larry'
	print list  ## ['xxx', 'moe', 'shemp', 'yyy', 'zzz']
下面的方法不返回值，它是修改原始的list

	list = [1, 2, 3]
	print list.append(4)   ## NO, does not work, append() returns None
	## Correct pattern:
	list.append(4)
	print list  ## [1, 2, 3, 4]
###list切片
就像是对字符串一样，也可以对list来切片

	list = ['a', 'b', 'c', 'd']
	print list[1:-1]   ## ['b', 'c']
	list[0:2] = 'z'    ## replace ['a', 'b'] with ['z']
	print list         ## ['z', 'c', 'd']
###list列表的其他一些妙用
去掉列表中每个元素头尾的空格 

	>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  '] 
	>>> [str.strip() for str in freshfruit] 
	['banana', 'loganberry', 'passion fruit'] 
把列表中，大于3的元素，乘以2 

	>>> vec = [2, 4, 6] 
	>>> [2*x for x in vec if x > 3] 
	[8, 12] 

把列表1的每一个元素和列表2的每一个元素相乘 

	>>> lst1 = [2, 4, 6] 
	>>> lst2 = [4, 3, -9] 
	>>> [x*y for x in lst1 for y in lst2] 
	[8, 6, -18, 16, 12, -36, 24, 18, -54] 

获取[0-10)的平方 

	[x**2 for x in range(10)] 
或
 
	map(lambda x : x*x, range(10)) 

获取[0-10)中奇数的平方 

	[x**2 for x in filter( lambda x : x%2, range(10) )] 
###list去重
比较容易记忆的是用内置的set

	l1 = ['b','c','d','b','c','a','a']
	l2 = list(set(l1))
	print l2
还有一种据说速度更快的，没测试过两者的速度差别

	l1 = ['b','c','d','b','c','a','a']
	l2 = {}.fromkeys(l1).keys()
	print l2
这两种都有个缺点，祛除重复元素后排序变了：

	['a', 'c', 'b', 'd']
保持原来的list可以使用下面的方法：

	l1 = ['b','c','d','b','c','a','a']
	l2 = sorted(set(l1),key=l1.index)
	print l2 #output ['b', 'c', 'd', 'a']