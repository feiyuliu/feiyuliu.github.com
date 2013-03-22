---
layout: post
title: python位置参数*args和命名参数**kwargs
description: ""
category: python study
tags: [python]
---
{% include JB/setup %}
用 \*args 收集"多余"   的位置参数，\*\*kwargs 收集"额外"的命名参数。这两个名字只是惯例，可自由命名。

    >>> def test(a, b, *args, **kwargs):
            print a, b
            print args
            print kwargs
    >>> test(1, 2, "a", "b", "c", x = 100, y = 200)
    1 2
    ('a', 'b', 'c')
    {'y': 200, 'x': 100}

变参只能放在所有参数定义的尾部，且\*\*kwargs 必须是最后一个。

单个"\*"展开序列类型，或者仅是字典的主键列表。"\*\*"展开字典键值对。但
如果没有变参收集，展开后多余的参数将引发异常。

    >>> def test(a, b):
            print a
            print b
    >>> d = dict(a = 1, b = 2)
 
    >>> test(*d)  # 仅展开 keys()，test("a"、"b")。
    a
    b
 
    >>> test(**d)  # 展开 items()，test(a = 1, b = 2)。
    1
    2

    >>> d = dict(a = 1, b = 2, c = 3)
 
    >>> test(*d)  # 因为没有位置变参收集多余的 "c"，导致出错。
 
    TypeError: test() takes exactly 2 arguments (3 given)
 
    >>> test(**d)!     # 因为没有命名变参收集多余的 "c = 3"，导致出错。
 
    TypeError: test() got an unexpected keyword argument 'c'