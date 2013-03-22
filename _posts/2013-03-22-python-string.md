---
layout: post
title: python字符串
description: ""
category: python study
tags: [python]
---
{% include JB/setup %}
字符串常量定义简单自由，可以是单引号、双引号或三引号

    >>> "a" + "b"   #字符串连接
    'ab'
    >>> "a" * 3     #字符串重复连接
    'aaa'
    >>> ",".join(["a","b","c"])  #合并字符串
    'a,b,c'
    >>> "a,b,c".split(",")       #字符串分割
    ['a', 'b', 'c']
    >>> "a\nb\nc".splitlines() #按行分割
    ['a', 'b', 'c']
判断字符串是否以特定的子字符串开始或者结束

    >>> "abc".startswith("ab")
    True
    >>> "abc".endswith("bc")
    True
字符串大小写转换

    >>> "abc".upper(),"abc".lower()
    ('ABC', 'abc')
字符串查找find(str,pos_start,pos_end)  str:被查找“字串”（气味字符串的函数）；pos_start:查找的首字母位置（从0开始计数。默认：0）；pos_end:查找的末尾位置（不包括末尾位置。默认-1）

    >>> "abcdef".find("de"),"adfegfeg".find("fe",2)
    (3, 2)
字符串删除前后空格

    >>> "   adsf".lstrip(),"af  ".rstrip(),"  ggh ".strip()
    ('adsf', 'af', 'ggh')
字符串替换，可以指定替换次数

    >>> "tgwertg".replace("wer","asdf")
    'tgasdftg'
字符串填充

    >>> "123".ljust(6,"0"),"456".rjust(6,"0"),"abc".center(10,"*")
    '123000', '000456', '***abc****')

字符串是不可变的数据类型，不可以使用下面的赋值：

    >>> s = "cocobear"
    >>> s[0] = s
字符串与列表的相互连接：

    >>> [1, 2] + "34" # same as "[1, 2]" + "34"
    '[1, 2]34'
    >>> [1, 2] + list("34") # same as [1, 2] + ["3", "4"]
    [1, 2, '3', '4']