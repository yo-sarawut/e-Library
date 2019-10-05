Tutorial: Python Functions and Functional Programming
===
- [https://www.dataquest.io/blog/introduction-functional-programming-python/](https://www.dataquest.io/blog/introduction-functional-programming-python/)

![](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/fp-python.png "fp-python")

Most of us have been introduced to Python as an  **object-oriented**  language, but Python functions are also useful tools for data scientists and programmers alike. While classes, and objects, are easy to start working with, there are other ways to write your Python code. Languages like Java can make it hard to move away from object-oriented thinking, but Python makes it easy.

Given that Python facilitates different approaches to writing code, a logical follow-up question is: what  _is_  a different way to write code? While there are several answers to this question, the most common alternative style of writing code is called  **functional programming**. Functional programming gets its name from writing functions which provides the main source of logic in a program.

In this post, we will:

-   Explain the basics of functional programming by comparing it to object-oriented programming.
-   Cover why you might want to incorporate functional programming in your own code.
-   Show you how Python allows you to switch between the two.

## Comparing object-oriented to functional

The easiest way to introduce functional programming is to compare it to something we’re already aware of: object-oriented programming. Suppose we wanted to create a line counter class that takes in a file, reads each line, then counts the total amount of lines in the file. Using a  _class_, it could look something like the following:

```python
class LineCounter:
    def __init__(self, filename):
        self.file = open(filename, 'r')
        self.lines = []

        def read(self):
            self.lines = [line for line in self.file]

        def count(self):
            return len(self.lines)
```

While not the best implementation, it does provide an insight into object-oriented design. Within the class, there are the familiar concepts of methods and properties. The properties set and retrieve the  _state_  of the object, and the methods manipulate that state.

For both these concepts to work, the object’s state must change over time. This change of state is evident in the  `lines`  property after calling the  `read()`  method. As an example, here’s how we would use this class:

```python
# example_file.txt contains 100 lines.
lc = LineCounter('example_file.txt')
print(lc.lines)
>> []
print(lc.count())
>> 0

# The lc object must read the file to
# set the lines property.
lc.read()
# The `lc.lines` property has been changed.
# This is called changing the state of the lc
# object.
print(lc.lines)
>> [['Hello world!', ...]]
print(lc.count())
>> 100
```

The ever-changing state of an object is both its blessing and curse. To understand why a changing state can be seen as a negative, we have to introduce an alternative. The alternative is to build the line counter as a series of independent functions.

```python
def read(filename):
    with open(filename, 'r') as f:
        return [line for line in f]

def count(lines):
    return len(lines)

example_lines = read('example_log.txt')
lines_count = count(example_lines)
```

## Working with pure functions

In the previous example, we were able to count the lines only with the use of functions. When we only use functions, we are applying a functional approach to programming which is, non-excitingly, called  [_functional programming_](https://docs.python.org/3.6/howto/functional.html). The concepts behind functional programming requires functions to be  **stateless**, and rely  _only on_  their given inputs to produce an output.

The functions that meet the above criteria are called  **pure functions**. Here’s an example to highlight the difference between pure functions, and non-pure:

```python
# Create a global variable `A`.
A = 5

def impure_sum(b):
    # Adds two numbers, but uses the
    # global `A` variable.
    return b + A

def pure_sum(a, b):
    # Adds two numbers, using
    # ONLY the local function inputs.
    return a + b

print(impure_sum(6))
>> 11

print(pure_sum(4, 6))
>> 10
```

The benefit of using pure functions over impure (non-pure) functions is the reduction of  **side effects**. Side effects occur when there are changes performed within a function’s operation that are outside its scope. For example, they occur when we change the state of an object, perform any I/O operation, or even call  `print()`:

```python
def read_and_print(filename):
    with open(filename) as f:
        # Side effect of opening a
        # file outside of function.
        data = [line for line in f]
    for line in data:
        # Call out to the operating system
        # "println" method (side effect).
        print(line)
```

Programmers reduce side effects in their code to make it easier to follow, test, and debug. The more side effects a codebase has, the harder it is to step through a program and understand its sequence of execution.

While it’s convienent to try and eliminate all side effects, they’re often used to make programming easier. If we were to ban all side effects, then you wouldn’t be able to read in a file, call print, or even assign a variable within a function. Advocates for functional programming understand this tradeoff, and try to eliminate side effects where possible without sacrificing development implementation time.

## The Lambda Expression

Instead of the  `def`  syntax for function declaration, we can use a  [`lambda`  expression](https://docs.python.org/3.5/tutorial/controlflow.html#lambda-expressions)  to write Python functions. The lambda syntax closely follows the  `def`  syntax, but it’s not a 1-to-1 mapping. Here’s an example of building a function that adds two integers:

```python
# Using `def` (old way).
def old_add(a, b):
    return a + b

# Using `lambda` (new way).
new_add = lambda a, b: a + bold_add(10, 5) == new_add(10, 5)
>> True
```

The  `lambda`  expression takes in a comma seperated sequences of inputs (like  `def`). Then, immediately following the colon, it returns the expression without using an explicit return statement. Finally, when assigning the  `lambda`  expression to a variable, it acts exactly like a Python function, and can be called using the the function call syntax:  `new_add()`.

If we didn’t assign  `lambda`  to a variable name, it would be called an  **anonymous function**. These anonymous functions are extremely helpful, especially when using them as an input for another function. For example, the  `sorted()`  [function](https://docs.python.org/3/howto/sorting.html#key-functions)  takes in an optional  `key`  argument (a function) that describes how the items in a list should be sorted.

```python
unsorted = [('b', 6), ('a', 10), ('d', 0), ('c', 4)]

# Sort on the second tuple value (the integer).
print(sorted(unsorted, key=lambda x: x[1]))
>> [('d', 0), ('c', 4), ('b', 6), ('a', 10)]
```

## The Map Function

While the ability to pass in functions as arguments is not unique to Python, it is a recent development in programming languages. Functions that allow for this type of behavior are called  **first-class functions**. Any language that contains first-class functions  _can be written_  in a functional style.

There are a set of important first-class functions that are commonly used within the functional paradigm. These functions take in a  [Python iterable](https://docs.python.org/3/glossary.html#term-iterable), and, like  `sorted()`, apply a function for each element in the list. Over the next few sections, we will examine each of these functions, but they all follow the general form of  `function_name(function_to_apply, iterable_of_elements)`.

The first function we’ll work with is the  `map()`  function. The  `map()`  function takes in an iterable (ie.  `list`), and creates a new iterable object, a special  `map`  object. The new object has the first-class function applied to every element.

```python
# Pseudocode for map.
def map(func, seq):
    # Return `Map` object with
    # the function applied to every
    # element.
    return Map(
        func(x)
        for x in seq
    )
```

Here’s how we could use map to add  `10`  or  `20`  to every element in a list:

```python
values = [1, 2, 3, 4, 5]

# Note: We convert the returned map object to
# a list data structure.
add_10 = list(map(lambda x: x + 10, values))
add_20 = list(map(lambda x: x + 20, values))

print(add_10)
>> [11, 12, 13, 14, 15]

print(add_20)
>> [21, 22, 23, 24, 25]
```

Note that it’s important to cast the return value from  `map()`  as a  `list`  object. Using the returned  `map`  object is difficult to work with if you’re expecting it to function like a  `list`. First, printing it does not show each of its items, and secondly, you can only iterate over it once.

## The Filter Function

The second function we’ll work with is the  `filter()`  function. The  `filter()`  function takes in an iterable, creates a new iterable object (again, a special  `map`  object), and a first-class function that must return a  `bool`  value. The new  `map`  object is a filtered iterable of all elements that returned  `True`.

```python
# Pseudocode for filter.
def filter(evaluate, seq):
    # Return `Map` object with
    # the evaluate function applied to every
    # element.
    return Map(
        x for x in seq
        if evaluate(x) is True
    )
```

Here’s how we could filter odd or even values from a list:

```python
values = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Note: We convert the returned filter object to
# a list data structure.
even = list(filter(lambda x: x % 2 == 0, values))
odd = list(filter(lambda x: x % 2 == 1, values))

print(even)
>> [2, 4, 6, 8, 10]

print(odd)
>> [1, 3, 5, 7, 9]
```

## The Reduce Function

The last function we’ll look at is the  `reduce()`  function from the  [`functools`  package](https://docs.python.org/3/library/functools.html). The  `reduce()`  function takes in an iterable, and then reduces the iterable to a single value. Reduce is different from  `filter()`  and  `map()`, because  `reduce()`  takes in a function that has two input values.

Here’s an example of how we can use  `reduce()`  to sum all elements in a list.

```python
from functools import reduce

values = [1, 2, 3, 4]

summed = reduce(lambda a, b: a + b, values)
print(summed)
>> 10
```

![diagram of reduce](https://dq-content.s3.amazonaws.com/263/s5_reduce_function.svg)

An interesting note to make is that you do  **not**  have to operate on the second value in the  `lambda`  expression. For example, you can write a function that always returns the first value of an iterable:

```python
from functools import reduce

values = [1, 2, 3, 4, 5]

# By convention, we add `_` as a placeholder for an input
# we do not use.
first_value = reduce(lambda a, _: a, values)
print(first_value)
>> 1
```

## Rewriting with list comprehensions

Because we eventually convert to lists, we should rewrite the  `map()`  and  `filter()`  functions using list comprehension instead. This is the more  _pythonic_  way of writing them, as we are taking advantage of the Python syntax for making lists. Here’s how you could translate the previous examples of  `map()`  and  `filter()`  to list comprehensions:

```python
values = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Map.
add_10 = [x + 10 for x in values]
print(add_10)
>> [11, 12, 13, 14, 15, 16, 17, 18, 19, 20]

# Filter.
even = [x for x in values if x % 2 == 0]
print(even)
>> [2, 4, 6, 8, 10]
```

From the examples, you can see that we don’t need to add the lambda expressions. If you are looking to add  `map()`, or  `filter()`  functions to your own code, this is usually the recommended way. However, in the next section, we’ll provide a case to still use the  `map()`  and  `filter()`  functions.

## Writing Function Partials

Sometimes we want to use the behavior of a function, but decrease the number of arguments it takes. The purpose is to “save” one of the inputs, and create a new function that defaults the behavior using the saved input. Suppose we wanted to write a function that would always add 2 to any number:

```python
def add_two(b):
    return 2 + b

print(add_two(4))
>> 6
```

The  `add_two`  function is similar to the general function, $f(a,b) = a + b$, only it defaults one of the arguments ($a = 2$). In Python, we can use the  [`partial`  module](https://docs.python.org/3.6/library/functools.html#functools.partial)  from the  `functools`  package to set these argument defaults. The  `partial`  module takes in a function, and “freezes” any number of args (or kwargs), starting from the first argument, then returns a new function with the default inputs.

```python
from functools import partialdef add(a, b):
    return a + b

add_two = partial(add, 2)
add_ten = partial(add, 10)

print(add_two(4))
>> 6
print(add_ten(4))
>> 14
```

Partials can take in any function, including ones from the standard library.

```python
# A partial that grabs IP addresses using
# the `map` function from the standard library.
extract_ips = partial(
    map,
    lambda x: x.split(' ')[0]
)
lines = read('example_log.txt')
ip_addresses = list(extract_ip(lines))
```

## Next steps

In this post, we introduced the paradigm of functional programming. We learned about the lambda expression in Python, important functional functions, and the concept of partials. Overall, we showed that Python provides a programmer with the tools to easily switch between functional programming and object-oriented programming.

If you’ve enjoyed functional programming, our newest course:  [Building a Data Pipeline](https://www.dataquest.io/course/building-a-data-pipeline)  uses functional programming concepts to build a data pipeline. In this course, you’ll find more advanced Python concepts, examples of good API design, and a final project that uses your own data pipeline built from scratch!
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0OTQ0MjA2XX0=
-->