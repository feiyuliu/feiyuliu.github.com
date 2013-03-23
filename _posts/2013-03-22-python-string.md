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
另外说明一点：字符串对象是immutable，任何对字符串的操作都将创建一个新的字符串对象，而不是改变原来的对象.因此N个字符串相加必将丢弃中间N-1个结果. 
###python字符串连接
python字符串连接有几种方法，第一个方法效率是最低的，等下给大家介绍后面的
2种效率高的方法，希望对大家有帮助。

先介绍下效率比较低的方法，有些新手朋友就会犯这个错误：

    a = ['a','b','c','d']
    content = ''
    for i in a:
        content = content + i
    print content

content的结果是:'abcd'

原因：在循环连接字符串的时候，他每次连接一次，就要重新开辟空间，然后把字符串连接起来，再放入新的空间，再一次循环，又要开辟新的空间，把字符串连接起来放入新的空间，如此反复，内存操作比较频繁，每次都要计算内存空间，然后开辟内存空间，再释放内存空间，效率非常低，你也许操作比较少的数据的时候看不出来，感觉影响不大，但是你碰到操作数据量比较多的时候，这个方法就要退休了，还是看看下面2个比较先进的方法把。

先进方法1：
用字符串的join方法：

    a = ['a','b','c','d']
    content = ''
    content = ''.join(a)
    print content

content的结果:'abcd'

先进方法2：
用字符串的替换占位符替换

    a = ['a','b','c','d']
    content = ''
    content = '%s%s%s%s' % tuple(a)
    print content
content的结果是:'abcd'

###python join方法
就是把一个list中所有的串按照你定义的分隔符连接起来，比如:

    list = ['a','b','c']
    sep = '|'
    join(list,sep)的结果就是a|b|c
也可以：

    >>> a = ('a','b','c')
    >>> "|".join(a)
    'a|b|c'