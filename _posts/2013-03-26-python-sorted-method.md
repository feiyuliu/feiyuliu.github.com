---
layout: post
title: python排序
description: ""
category: python
tags: [python]
---
{% include JB/setup %}
最rkdown简单的排序是使用sorted(list)函数。它接收一个list，返回一个新的排好序的list。原生的list没有变化

{% highlight python %}
a = [5, 1, 4, 3]
print sorted(a)  ## [1, 3, 4, 5]
print a  ## [5, 1, 4, 3]
{% endhighlight %}

大部分都是通过传递list到sorted()函数。但是它实际上可以传递任何形式的iterable集合。可以通过添加参数 reverse=True如：sorted(list, reverse=True)来实现倒序。

	strs = ['aa', 'BB', 'zz', 'CC']
	print sorted(strs)  ## ['BB', 'CC', 'aa', 'zz'] (大小写敏感)
	print sorted(strs, reverse=True)   ## ['zz', 'aa', 'CC', 'BB']
###通过key=来自定义排序
为了实现自定义的复杂的排序，可以通过添加参数"key="来指定一个函数在比较之前来处理每一个元素。这个指定的函数它接收每一个待比较的元素，转换为一个中间的值（称为proxy value），然后使用中间的值来排序。

例如，我们来排序一个字符串列表，然后指定key=len(len()函数是python内置的函数)来实现对每个字符串通过字符串的长度来排序。排序通过对每个list元素调用len()函数来计算出长度，转换成一个中间的长度列表，然后对这个长度列表进行排序。

	strs = ['ccc', 'aaaa', 'd', 'bb']
	print sorted(strs, key=len)  ## ['d', 'bb', 'ccc', 'aaaa']
![图示](https://developers.google.com/edu/python/images/sorted-key.png "自定义排序示例")

你也可以实现自己定义的函数来指定key的值。如：

	## Say we have a list of strings we want to sort by the last letter of the string.
	strs = ['xc', 'zb', 'yd' ,'wa']
	## Write a little function that takes a string, and returns its last letter.
	## This will be the key function (takes in 1 value, returns 1 value).
	def MyFn(s):
		return s[-1]

	## Now pass key=MyFn to sorted() to sort by the last letter:
	print sorted(strs, key=MyFn)  ## ['wa', 'zb', 'xc', 'yd']
使用key=来指定排序的函数是，你需要指定一个函数来对每一个元素生成一个中间结果，然后根据中间结果来排序。
###sort()方法
另外一种排序方法是通过sort()方法来排序。如：list.sort()。它改变了原始的列表。而且**返回值是None**

	alist.sort()            ## correct
	alist = blist.sort()    ## NO incorrect, sort() returns None
要注意sort()函数它没有返回一个list而是返回None。而且必须是list来调用。不能通过其他的可列举的集合来调用。而sorted()函数可以。sort()函数它不需要创建一个新的list,所以它的速度可能要快些。

本文翻译自[google python class](https://developers.google.com/edu/python/sorting?hl=zh-CN)
