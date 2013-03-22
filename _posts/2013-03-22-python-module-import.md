---
layout: post
title: python两种导入模块(from module import和import module)
description: ""
category: python study
tags: [python]
---
{% include JB/setup %}
from module import这种语法与你所知的 import module 语法类似，但是有一个重要的区别：导入模块 types 的属性和方法被直接导入到局部名字空间中，所以这些属性和方法是直接有效的，不需要通过模块名来限定。

###import module 对比 from module import

    >>> import types
    >>> types.FunctionType             (1)
    <type 'function'>
    >>> FunctionType                   (2)
    Traceback (innermost last):
      File "<interactive input>", line 1, in ?
    NameError: There is no variable named 'FunctionType'
    >>> from types import FunctionType  (3)
    >>> FunctionType                    (4)
    <type 'function'>
(1)types 模块不包含方法，只有每个Python对象类型的属性。注意， FunctionType 属性必需用 types 模块名进行限定。

(2)FunctionType 本身没有被定义在当前名字空间中；它只存在于 types 的上下文环境中。

(3)这个语法直接从 types 模块中导入 FunctionType 属性到局部名字空间。

(4)现在 FunctionType 可以直接存取，不需要引用 types。

###什么时候你应该使用 from module import？

 1、如果你要经常存取模块的属性和方法，且不想一遍遍地敲入模块名，使用 from module import。
 
 2、如果你想要有选择地导入某些属性和方法，而不想要其它的，使用 from module import。
 
 3、如果模块包含的属性和方法与你的某个模块同名，你必须使用 import module 来避免名字冲突。