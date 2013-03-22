---
layout: post
title: Python id() 函数
description: ""
category: python study
tags: [python]
---
{% include JB/setup %}
python 的id(object) 返回的是对象的内存地址。

    //python Id函数
    >>> j=10
    >>> id(j)
    8402204
    >>> j=j+1
    >>> id(j)
    8402192
    >>> k=11
    >>> id(k)
    8402192
因为integer是不变的，没一个integer的值都是一个单独的对象，并且有一个唯一的id。由于integer 10和11不一样，执行j=j+1并没有改变已经存在的integer对象。而是改变了j指向的指针指向了11.如果创建一个新的变量k，并且赋值为11，他们的id是一样的。
但是注意,它并非总是如此,每个整数都有且只有一个相应的对象。这只发生小整数,Python决定缓存。对大的整数不适合。如：

    //python 大整数
    >>> x = 123456789
    >>> id(x)
    8404568
    >>> y = 123456789
    >>> id(y)
    8404604
python官方文档里有这些：http://docs.python.org/c-api/int.html#PyInt_FromLong:
它指出，当前实现整数的数组对象是在-5和256之间的,当你创建一个int在这个范围内你实际上只是返回一个引用现有的对象内存地址。如果不在这个范围，可以id不一样。