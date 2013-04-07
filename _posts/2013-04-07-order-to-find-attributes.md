---
layout: post
title: python属性查找顺序
description: ""
category: python
tags: [python]
---
{% include JB/setup %}

	>>> class dormitory:
	...     rooms = 0
	...     def init(self):
	...         dormitory.rooms += 1
	...
	>>> d1 = dormitory()
	>>> d1.init()
	>>> dormitory.rooms
	1
	>>> d2 = dormitory()
	>>> d2.init()
	>>> dormitory.rooms
	2
	>>> d1.rooms
	2
	>>> d2.rooms
	2
	>>> d1.rooms = 23
	>>> d1.rooms
	23
	>>> d2.rooms
	2
问题：

为什么dormitory.rooms会是2，d1和d2的rooms都是2。但是对di的rooms重新赋值后，d2的rooms为什么又没有改变？

如果我在类中init方法使用self.rooms += 1后，为什么dormitory.rooms都是0，d1的rooms和d2的rooms互不干扰？

解答：

和作用域关系不大。和python里属性查找顺序有关。dormitory.rooms是class的属性。两次init后读取instance的rooms属性，是不存在的，所以往上查找找到了class的rooms属性。

而给instance.rooms赋值之后，查找属性就直接找到instance的这个属性了。由于这个赋值没有覆盖掉class的属性，所以d2.rooms还是原值

一旦给d1.rooms赋值之后，会在d1这个实例上创建一个rooms的属性，它其实和类属性是同名的。python在查找一个属性时是有顺序的，先找实例的，再找类的，依次类推。所以d1.rooms = 23之后，再访问的话就直接拿到的实例属性。而d2则还是查到的类属性。