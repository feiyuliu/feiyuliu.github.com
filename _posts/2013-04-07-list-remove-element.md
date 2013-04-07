---
layout: post
title: python在列表删除元素
description: ""
category: python
tags: [python]
---
{% include JB/setup %}

	def subtractList(list1, list2): 
		for i in list1:
			if i in list2:
				list1.remove(i)
		return list1

我是想从list1中删除list2中有的元素。通过测试：subtractList([1,2,3,4,5], [2, 4]) 和 subtractList (['a', 'b', 'c', 'd'], ['x', 'y', 'z']) 都没有问题。但是使用	subtractList(range(5), range(4)) 测试就出问题了。结果为[1, 3, 4] 为什么不是[4]

不要在迭代器中改变数据的结构，这是迭代器的一个准则。因为结构上的改变无法保证迭代器的工作。包括for each in xxx之类

	def subtractList(list1, list2):
		return [each for each in list1 if each in (set(list1) - set(list2))]

	def subtractList(list1, list2): 
		#先复制一个然后再删除
		for i in list1[:]:  
			if i in list2:
			list1.remove(i)
		return list1
