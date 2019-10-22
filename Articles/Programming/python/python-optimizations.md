
Python Optimizations
===
![enter image description here](https://miro.medium.com/max/1600/1*VXi1sWm5p5_90KXYu6tJ5w.jpeg)

Peephole is a way Python optimizes certain things of your program at compile time by either pre-calculating constant expressions or transforming certain data structures.

## Constant Expressions

Optimizing constant expressions is really simple. What Python does is basically pre-calculate constants. Suppose that along your program you have the following multiplication for some reason,

secondsInADay = 60*60*24

What python will do is pre-calculate that multiplication and will replace it for  `86400`  . You might be wondering why not just write directly  `86400`  in code, the answer is clarity. On the expression above you can see that in order to calculate how many seconds a day has, you have to multiply 60 seconds time 60 minutes of an hour times 24 hours of a day. This way your code might look clearer. Python won’t make that calculation each time that multiplication appears, it will just pre-calculate it and replace it for the final value.

Short sequences also get pre-calculated. Imagine you have this code,

myTuple = (2, 4)*5      # -> (2, 4, 2, 4, 2, 4, 2, 4, 2, 4)  
myString = "qwerty "*2  # -> "qwerty qwerty "

As you can see on the code above we have two variables, the first one is a tuple multiplied by 5 and the second one is a short string multiplied by 2, this short sequences will be pre-calculated and Python will replace the original expression with the value on the comments. It is worth to mention that Python has to balance between storage and computation, if it pre-calculates long sequences the program might be faster but it will end up using a lot of memory.

In order to see that this is happening you can simply open a Python console and write the following code,

**def** my_func():  
    a = 60*60*24  
    myString = (**"querty "**) * 2  
    myTupple = (2, 4) *5  
    myString = (**"This is a sequence with a lot of characters"**) * 100

Once this function is declared you can write the following code to access all the constants declared on the scope of that funcion,

my_func.__code__.co_consts

The output should be the following,

>>> my_func.__code__.co_consts(None,   
86400,   
'querty querty ',   
(2, 4, 2, 4, 2, 4, 2, 4, 2, 4),   
'This is a sequence with a lot of characters',   
100)

As you can see, on the output above Python has already pre-calculated the constant values and short sequences, instead of having  `60*60*24`  the function has already the constant value  `86400`  , the same thing happens with the tuple and the short string, but as you can see the long sequence didn’t get pre-calculated and instead we get two different constants,  `'This is a sequence with a lot of characters'`  and  `100`  . As mentioned above, Python has to balance between storage and computation.

## Membership Tests: Replacing mutable data structures for inmutable data structures

What Python does here is basically transforming mutable data structures to its inmutable version.  _Lists_  get transformed into  _tuples_  and  _sets_  to  _frozensets_.

For instance,

**def** my_func(element):  
    **if** element **in** [**"a"**, **"b"**, **"c"**]:  
        print(element)

The code above will be transformed to this,

**def** my_func(element):  
    **if** element **in ("a"**, **"b"**, **"c")**:  
        print(element)

This is done just because accessing to the inmutable version of a data structure is faster than accessing the mutable one. You can check this doing the same thing as before running the follwing code,

my_func.__code__.co_consts

The output should be the following,

>>> my_func.__code__.co_consts(None, ('a', 'b', 'c'))

As you can see, the function has a constant value which is the inmutable version (a  _tuple_) of the declared  _list_.

Finally doing the same as before but with a  _set_  you will see that it will be transformed into a  _frozenset,_

**def** my_func(element):  
    **if** element **in {"a"**, **"b"**, **"c"}**:  
        print(element)>>> my_func.__code__.co_consts(None, frozenset({'a', 'b', 'c'}))

----------

If you are interested on Python optimizations you could check out my article about  [Python optimizations (Intering)](https://medium.com/@gmotzespina/python-optimizations-216205001b83).

> Written with [StackEdit](https://medium.com/@gmotzespina/python-optimizations-a822db1f6bf5).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTI2NzI5MzU5XX0=
-->