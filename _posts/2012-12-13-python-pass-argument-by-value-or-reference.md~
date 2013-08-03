---
layout: post
title: "Python pass argument by Value or Reference"
description: "Python passes by reference or value ,here is the discuss"
category: Python
tags: [python]
---
{% include JB/setup %}
##question
When you pass a collection like list, array to another function in python, does it make a copy of it, or is it just a pointer?

###first answer:

Python passes references-to-objects by value (like Java), and everything in Python is an object. This sounds simple, but then you will notice that some data types seem to exhibit pass-by-value characteristics, while others seem to act like pass-by-reference... what's the deal?

It is important to understand mutable and immutable objects. Some objects, like strings, tuples, and numbers, are immutable. Altering them inside a function/method will create a new instance and the original instance outside the function/method is not changed. Other objects, like lists and dictionaries are mutable, which means you can change the object in-place. Therefore, altering an object inside a function/method will also change the original object outside.

###the secend:

Thing is, the whole reference/value concept won't fit into python. Python has no "value" of a variable. Python has only objects and names that refer to objects.

So when you call a function and put a "name" inside the parenthesis, like this:

    def func(x): # defines a function that takes an argument
    ... # do something here

    func(myname) # calling the function
The actual object that **myname** is pointing is passed, not the **name myname itself**. Inside the function **another name (x) **is given to refer to the same object passed.

You can modify the object inside the function if it is mutable, but you **can't change what the outside name is pointing to**. Just the same that happens when you do

    anothername = myname
Therefore I can answer your question with:

**it is "pass by value" but all values are just references to objects.**
####for more discussion , go to [this site](http://stackoverflow.com/questions/534375/passing-values-in-python)