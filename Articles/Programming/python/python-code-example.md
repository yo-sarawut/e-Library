Python Code Examples
========
[**By : freeCodeCamp**](https://www.freecodecamp.org/news/python-example/)

![enter image description here](https://images.unsplash.com/photo-1522857884396-6d2c1c34e4e6?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ)

[Python](https://www.python.org/)  is a general purpose programming language which is dynamically typed, interpreted, and known for its easy readability with great design principles.



# Python Data Structures Example

Some general information about floating point numbers and how they work in Python, can be found  [here](https://docs.python.org/3/tutorial/floatingpoint.html).

Nearly all implementations of Python follow the IEEE 754 specification: Standard for Binary Floating-Point Arithmetic. More information found on the  [IEEE site](http://grouper.ieee.org/groups/754/).

Float objects can be created using  [floating point literals](https://docs.python.org/3/reference/lexical_analysis.html#floating-point-literals):

```python
3.14
3.14
314\.    # Trailing zero(s) not required.
314.0
.314    # Leading zero(s) not required.
0.314
3e0
3.0
3E0     # 'e' or 'E' can be used.
3.0
3e1     # Positive value after e moves the decimal to the right.
30.0
3e-1    # Negative value after e moves the decimal to the left.
0.3
3.14e+2 # '+' not required but can be used for exponent part.
314.0
```

Numeric literals do not contain a sign, however creating negative float objects is possible by prefixing with a unary  `-`  (minus) operator with no space before the literal:

```python
-3.141592653589793
-3.141592653589793
type(-3.141592653589793)
<class 'float'>
```

Likewise, positive float objects can be prefixed with a unary  `+`  (plus) operator with no space before the literal. Usually  `+`  is omitted:

```python
+3.141592653589793
3.141592653589793
```

Note that leading and trailing zero(s) are valid for floating point literals.

```python
0.0
0.0
00.00
0.0
00100.00100
100.001
001e0010      # Same as 1e10
10000000000.0
```

The  [`float`  constructor](https://docs.python.org/3/library/functions.html#float)  is another way to create  `float`  objects.

Creating  `float`  objects with floating point literals is preferred when possible:

```python
a = 3.14         # Prefer floating point literal when possible.
type(a)
<class 'float'>
b = int(3.14)    # Works but unnecessary.
type(b)
<class 'float'>
```

However, the float constructor allows for creating float objects from other number types:

```python
a = 4
type(a)
<class 'int'>
print(a)
4
b = float(4)
type(b)
<class 'float'>
print(b)
4.0
float(400000000000000000000000000000000)
4e+32
float(.00000000000000000000000000000004)
4e-32
float(True)
1.0
float(False)
0.0
```

The  `float`  constructor will also make  `float`  objects from strings that represent number literals:

```python
float('1')
1.0
float('.1')
0.1
float('3.')
3.0
float('1e-3')
0.001
float('3.14')
3.14
float('-.15e-2')
-0.0015
```

The  `float`  constructor can also be used to make numeric representations of  `NaN`  (Not a Number), negative  `infinity`  and  `infinity`  (note that strings for these are case insensitive):

```python
float('nan')
nan
float('inf')
inf
float('-inf')
-inf
float('infinity')
inf
float('-infinity')
-inf
```

# Python Bools Example

`bool()`  is a built-in function in Python 3. This function returns a Boolean value, i.e. True or False. It takes one argument,  `x`.

## **Arguments**

It takes one argument,  `x`.  `x`  is converted using the standard  [Truth Testing Procedure](https://docs.python.org/3/library/stdtypes.html#truth).

## **Return Value**

If  `x`  is false or omitted, this returns  `False`; otherwise it returns  `True`.

## **Code Sample**

```python
print(bool(4 > 2)) # Returns True as 4 is greater than 2
print(bool(4 < 2)) # Returns False as 4 is not less than 2
print(bool(4 == 4)) # Returns True as 4 is equal to 4
print(bool(4 != 4)) # Returns False as 4 is equal to 4 so inequality doesn't holds
print(bool(4)) # Returns True as 4 is a non-zero value
print(bool(-4)) # Returns True as -4 is a non-zero value
print(bool(0)) # Returns False as it is a zero value
print(bool('dskl')) # Returns True as the string is a non-zero value
print(bool([1, 2, 3])) # Returns True as the list is a non-zero value
print(bool((2,3,4))) # Returns True as tuple is a non-zero value
print(bool([])) # Returns False as list is empty and equal to 0 according to truth value testing
```

# Python Bool Operators Example

[`and`](https://docs.python.org/3/reference/expressions.html#and),  [`or`](https://docs.python.org/3/reference/expressions.html#or),  [`not`](https://docs.python.org/3/reference/expressions.html#not)

[Python Docs - Boolean Operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)

These are the Boolean operations, ordered by ascending priority:

OperationResultNotes x or y if x is false, then y, else x (1) x and y if x is false, then x, else y (2) not x if x is false, then True, else False (3).

****Notes:****

1.  This is a short-circuit operator, so it only evaluates the second argument if the first one is False.
2.  This is a short-circuit operator, so it only evaluates the second argument if the first one is True.
3.  not has a lower priority than non-Boolean operators, so not ```a == b``` is interpreted as not```(a == b)```, and ```a == not b``` is a syntax error.

## **Examples:**

### **`not`:**

```python
not True
False
not False
True
```

### **`and`:**

```python
True and False    # Short-circuited at first argument.
False
False and True    # Second argument is evaluated.
False
True and True     # Second argument is evaluated.
True
```

### **`or`:**

```python
True or False    # Short-circuited at first argument.
True
False or True    # Second argument is evaluated.
True
False or False   # Second argument is evaluated.
False
```

# Python Constant Example

Three commonly used built-in constants:

-   `True`: The true value of the  _bool_  type. Assignments to  `True`  raise a  _SyntaxError_.
-   `False`: The false value of the  _bool_  type. Assignments to  `False`  raise a  _SyntaxError_.
-   `None`  : The sole value of the type  _NoneType_. None is frequently used to represent the absence of a value, as when default arguments are not passed to a function. Assignments to  `None`  raise a  _SyntaxError_.

Other built-in constants:

-   `NotImplemented`: Special value which should be returned by the binary special methods, such as  `__eg__()`,  `__add__()`,  `__rsub__()`, etc.) to indicate that the operation is not implemented with respect to the other type.
-   `Ellipsis`: Special value used mostly in conjunction with extended slicing syntax for user-defined container data types.
-   `__debug__`: True if Python was not started with an -o option.

Constants added by the site module. The site module (which is imported automatically during startup, except if the -S command-line option is given) adds several constants to the built-in namespace. They are useful for the interactive interpreter shell and should not be used in programs.

Objects that, when printed, print a message like “Use quit() or Ctrl-D (i.e. EOF) to exit”, and when called, raise SystemExit with the specified exit code:

-   quit(code=None)
-   exit(code=None)

Objects that, when printed, print a message like “Type license() to see the full license text”, and when called, display the corresponding text in a pager-like fashion (one screen at a time):

-   copyright
-   license
-   credits

# Calling Python Function Example

A function definition statement does not execute the function. Executing (calling) a function is done by using the name of the function followed by parenthesis enclosing required arguments (if any).

```python
def say_hello():
...     print('Hello')
...
say_hello()
Hello
```

The execution of a function introduces a new symbol table used for the local variables of the function. More precisely, all variable assignments in a function store the value in the local symbol table.

On the other hand, variable references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names. Thus, global variables cannot be directly assigned a value within a function (unless named in a global statement), although they may be referenced.

```python
a = 1
b = 10
def fn():
...     print(a)    # local a is not assigned, no enclosing function, global a referenced.
...     b = 20      # local b is assigned in the local symbol table for the function.
...     print(b)    # local b is referenced.
...
fn()
1
20
b               # global b is not changed by the function call.
10
```

The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called. In this way, arguments are passed using call by value (where the value is always an object reference, not the value of the object). When a function calls another function, a new local symbol table is created for that call.

```python
def greet(s):
...     s = "Hello " + s    # s in local symbol table is reassigned.
...     print(s)
...
person = "Bob"
greet(person)
Hello Bob
person                  # person used to call remains bound to original object, 'Bob'.
'Bob'
```

The arguments used to call a function cannot be reassigned by the function, but arguments that reference mutable objects can have their values changed:

```python
def fn(arg):
...     arg.append(1)
...
a = [1, 2, 3]
fn(a)
a
[1, 2, 3, 1]
```

# Python Class Example

Classes provide a means of bundling data and functionality together. Creating a new class creates a new type of object, allowing new instances of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods (defined by its class) for modifying its state.

Compared with other programming languages, Python’s class mechanism adds classes with a minimum of new syntax and semantics. It is a mixture of the class mechanisms found in C++.

Python classes provide all the standard features of Object Oriented Programming: the class inheritance mechanism allows multiple base classes, a derived class can override any methods of its base class or classes, and a method can call the method of a base class with the same name.

Objects can contain arbitrary amounts and kinds of data. As is true for modules, classes partake of the dynamic nature of Python: they are created at runtime, and can be modified further after creation.

#### **Class Definition Syntax :**

The simplest form of class definition looks like this:

```python
class ClassName:
    <statement-1>
        ...
        ...
        ...
    <statement-N>
```

#### **Class Objects:**

Class objects support two kinds of operations: attribute references and instantiation.

Attribute references use the standard syntax used for all attribute references in Python:  `obj.name`. Valid attribute names are all the names that were in the class’s namespace when the class object was created. So, if the class definition looked like this:

```python
class MyClass:
    """ A simple example class """
    i = 12345

    def f(self):
        return 'hello world'
```

Then  `MyClass.i`  and  `MyClass.f`  are valid attribute references, returning an integer and a function object, respectively. Class attributes can also be assigned to, so you can change the value of  `MyClass.i`  by assignment.  `__doc__`  is also a valid attribute, returning the docstring belonging to the class:  `"A simple example class"`.

Class instantiation uses function notation. Just pretend that the class object is a parameterless function that returns a new instance of the class. For example (assuming the above class):

```python
x = MyClass()
```

Creates a new instance of the class and assigns this object to the local variable x.

The instantiation operation (“calling” a class object) creates an empty object. Many classes like to create objects with instances customized to a specific initial state. Therefore a class may define a special method named  ****init****(), like this:

```python
def __init__(self):
    self.data = []
```

When a class defines an  `__init__()`  method, class instantiation automatically invokes  `__init__()`  for the newly-created class instance. So in this example, a new, initialized instance can be obtained by:

```python
x = MyClass()
```

Of course, the  `__init__()`  method may have arguments for greater flexibility. In that case, arguments given to the class instantiation operator are passed on to  `__init__()`. For example,

```python
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
              ...

x = Complex(3.0, -4.5)
x.r, x.i
(3.0, -4.5)
```

# Python Code Blocks and Indention Example

It is generally good practice for you not to mix tabs and spaces when coding in Python. Doing this can possibly cause a  `TabError`, and your program will crash. Be consistent when you code - choose either to indent using tabs or spaces and follow your chosen convention throughout your program.

#### **Code Blocks and Indentation**

One of the most distinctive features of Python is its use of indentation to mark blocks of code. Consider the if-statement from our simple password-checking program:

```python
if pwd == 'apple':
    print('Logging on ...')
else:
    print('Incorrect password.')

print('All done!')
```

The lines print(‘Logging on …’) and print(‘Incorrect password.’) are two separate code blocks. These happen to be only a single line long, but Python lets you write code blocks consisting of any number of statements.

To indicate a block of code in Python, you must indent each line of the block by the same amount. The two blocks of code in our example if-statement are both indented four spaces, which is a typical amount of indentation for Python.

In most other programming languages, indentation is used only to help make the code look pretty. But in Python, it is required for indicating what block of code a statement belongs to. For instance, the final print(‘All done!’) is not indented, and so is not part of the else-block.

Programmers familiar with other languages often bristle at the thought that indentation matters: Many programmers like the freedom to format their code how they please. However, Python indentation rules are quite simple, and most programmers already use indentation to make their code readable. Python simply takes this idea one step further and gives meaning to the indentation.

#### **If/elif-statements**

An if/elif-statement is a generalized if-statement with more than one condition. It is used for making complex decisions. For example, suppose an airline has the following “child” ticket rates: Kids 2 years old or younger fly for free, kids older than 2 but younger than 13 pay a discounted child fare, and anyone 13 years or older pays a regular adult fare. The following program determines how much a passenger should pay:

```python
# airfare.py
age = int(input('How old are you? '))
if age <= 2:
    print(' free')
elif 2 < age < 13:
    print(' child fare)
else:
    print('adult fare')
```

After Python gets age from the user, it enters the if/elif-statement and checks each condition one after the other in the order they are given.

So first it checks if age is less than 2, and if so, it indicates that the flying is free and jumps out of the elif-condition. If age is not less than 2, then it checks the next elif-condition to see if age is between 2 and 13. If so, it prints the appropriate message and jumps out of the if/elif-statement. If neither the if-condition nor the elif-condition is True, then it executes the code in the else-block.

#### **Conditional expressions**

Python has one more logical operator that some programmers like (and some don’t!). It’s essentially a shorthand notation for if-statements that can be used directly within expressions. Consider this code:

```python
food = input("What's your favorite food? ")
reply = 'yuck' if food == 'lamb' else 'yum'
```

The expression on the right-hand side of = in the second line is called a conditional expression, and it evaluates to either ‘yuck’ or ‘yum’. It’s equivalent to the following:

```python
food = input("What's your favorite food? ")
if food == 'lamb':
   reply = 'yuck'
else:
   reply = 'yum'
```

Conditional expressions are usually shorter than the corresponding if/else-statements, although not quite as flexible or easy to read. In general, you should use them when they make your code simpler.

# Python Comparison Operator Example

There are eight comparison operations in Python. They all have the same priority (which is higher than that of the Boolean operations). Comparisons can be chained arbitrarily; for example,  `x < y <= z`  is equivalent to  `x < y and y <= z`, except that  `y`  is evaluated only once (but in both cases  `z`  is not evaluated at all when  `x < y`  is found to be false).

The following summarizes the comparison operations:

OperationMeaning`<`strictly less than`<=`less than or equal to`>`strictly greater than`>=`greater than or equal to`==`equal to`!=`not equal to  `is`  object identity  `is not`negated object identity

Objects of different types, except different numeric types, never compare equal. Furthermore, some types (for example, function objects) support only a degenerate notion of comparison where any two objects of that type are unequal. The  `<`,  `<=`,  `>`  and  `>=`  operators will raise a  `TypeError`  exception when comparing a complex number with another built-in numeric type, when the objects are of different types that cannot be compared, or in other cases where there is no defined ordering.

Non-identical instances of a class normally compare as non-equal unless the class defines the  `__eq__()`method.

Instances of a class cannot be ordered with respect to other instances of the same class, or other types of object, unless the class defines enough of the methods  `__lt__()`,  `__le__()`,  `__gt__()`, and  `__ge__()`  (in general,  `__lt__()`  and  `__eq__()`  are sufficient, if you want the conventional meanings of the comparison operators).

The behavior of the  `is`  and  `is not`  operators cannot be customized; also they can be applied to any two objects and never raise an exception.

We can also chain  `<`  and  `>`  operators together. For instance,  `3 < 4 < 5`  will return  `True`, but  `3 < 4 > 5`will not. We can also chain the equality operator. For instance,  `3 == 3 < 5`  will return  `True`  but  `3 == 5 < 5`  will not.

### **Equality Comparisons - “is” vs ”==”**

In Python, there are two comparison operators which allow us to check to see if two objects are equal. The  `is`  operator and the  `==`  operator. However, there is a key difference between them!

The key difference between ‘is’ and ’==’ can be summed up as:

-   `is`  is used to compare  ****identity****
-   `==`  is used to compare  ****equality****

## **Example**

First, create a list in Python.

```python
myListA = [1,2,3]
```

Next, create a copy of that list.

```python
myListB = myListA
```

If we use the ’==’ operator or the ‘is’ operator, both will result in a  ****True****  output.

```python
myListA == myListB # both lists contains similar elements
True
myListB is myListA # myListB contains the same elements
True
```

This is because both myListA and myListB are pointing to the same list variable, which I defined at beginning of my Python program. Both lists are exactly the same, both in identity and in content.

However, what if I now create a new list?

```python
myListC = [1,2,3]
```

Performing the  `==`  operator still shows that both lists are the same, in terms of content.

```python
myListA == myListC
True
```

However, performing the  `is`  operator will now produce a  `False`  output. This is because myListA and myListC are two different variables, despite containing the same data. Even though they look the same, they are  ****different****.

```python
myListA is myListC
False # both lists have different reference
```

To sum up:

-   An  `is`  expression outputs  `True`  if both variables are pointing to the same reference
-   An  `==`  expression outputs  `True`  if both variables contain the same data

# Python Dictionary Example

A Dictionary (a.k.a “dict”) in python is a built-in datatype that can be used to store  ****`key-value`****  pairs. This allows you to treat a  ****`dict`****  like it’s a  _database_  to store and organize data.

The special thing about dictionaries is the way they are implemented. Hash-table-like structure makes it easy to check for existence - which means that we can easily determine if a specific key is present in the dictionary without needing to examine every element. The Python interpreter can just go to the location key and check if the key is there.

Dictionaries can use almost any arbitrary datatypes, like strings, integers etc, for keys. However, values that are not hashable, that is, values containing lists, dictionaries or other mutable types (that are compared by value rather than by object identity) may not be used as keys. Numeric types used for keys obey the normal rules for numeric comparison: if two numbers compare equal (such as  `1`  and  `1.0`) then they can be used interchangeably to index the same dictionary entry. (Note however, that since computers store floating-point numbers as approximations it is usually unwise to use them as dictionary keys.)

One most important requirement of a dictionary is that the keys  ****must****  be unique.  
To create an empty dictionary just use a pair of braces:

```python
    teams = {}
    type(teams)
    <class 'dict'>
```

To create a non-empty dictionary with some initial values, place a comma-seperated list of key-value pairs:

```python
    teams = {'barcelona': 1875, 'chelsea': 1910}
    teams
    {'barcelona': 1875, 'chelsea': 1910}
```

It’s easy to add key-value pairs to an existing dictionary:

```python
    teams['santos'] = 1787
    teams
    {'chelsea': 1910, 'barcelona': 1875, 'santos': 1787} # Notice the order - Dictionaries are unordered !
    # extracting value - Just provide the key
    ...
    teams['barcelona']
    1875
```

****`del`****  operator is used to delete a key-value pair from the dict. In scenarios where a key that’s already in use is again used to store values, the old value associated with that key is completely lost. Also, keep in mind that it’s an error to extract the value using a non-existent key.

```python
    del teams['santos']
    teams
    {'chelsea': 1910, 'barcelona': 1875}
    teams['chelsea'] = 2017 # overwriting    
    teams
    {'chelsea': 2017, 'barcelona': 1875}
```

****`in`****  keyword can be used to check whether a key exist in the dict or not:

```python
    'sanots' in teams
    False    
    'barcelona' in teams
    True
    'chelsea' not in teams
    False
```

****`keys`****  is a built-in  _method_  that can be used to get the keys of a given dictionary. To extract the keys present in a dict as lists:

```python
    club_names = list(teams.keys())    
    club_names
    ['chelsea', 'barcelona']
```

Yet another way of creating a dictionary is using the  ****`dict()`****  method:

```python
    players = dict( [('messi','argentina'), ('ronaldo','portugal'), ('kaka','brazil')] ) # sequence of key-value pair is passed  
    players
    {'ronaldo': 'portugal', 'kaka': 'brazil', 'messi': 'argentina'}
    
    # If keys are simple strings, it's quite easier to specify pairs using keyword arguments
    ...
    dict( totti = 38, zidane = 43 )
    {'zidane': 43, 'totti': 38}
```

Dict comprehensions can be used as well to create dictionaries from arbitrary key and value expressions:

```python
    {x: x**2 for x in (2, 4, 6)}
    {2: 4, 4: 16, 6: 36}
```

****Looping in Dictionary****  
To simply loop over the keys in the dictionary, rather than the keys and values:

```python
    d = {'x': 1, 'y': 2, 'z': 3} 
    for key in d:
    ...     print(key) # do something
    ...
    x
    y
    z
```

To loop over both key and value, you can use the following:  
For Python 2.x:

```python
    for key, item in d.iteritems():
    ...     print items
    ...
    1
    2
    3
```

Use  ****`items()`****  for Python 3.x:

```python
    for key, item in d.items():
    ...     print(key, items)
    ...
    x 1
    y 2
    z 3
```

# Python Objects Example

In Python, everything is an  _object_.

_Objects_  represent a logical grouping of attributes. Attributes are data and/or functions. When an object is created in Python it is created with an  _identity_,  _type_, and  _value_.

In other languages,  _primitives_  are  _values_  that have no  _properties_  (attributes). For example, in javascript  `undefined`,  `null`,  `boolean`,  `string`,  `number`, and  `symbol`  (new in ECMAScript 2015) are primitives.

In Python, there are no primitives.  `None`,  _booleans_,  _strings_,  _numbers_, and even  _functions_are all  _objects_ regardless how they are created.

We can demonstrate this using some built-in functions:

-   [`id`](https://docs.python.org/3/library/functions.html#id)
-   [`type`](https://docs.python.org/3/library/functions.html#type)
-   [`dir`](https://docs.python.org/3/library/functions.html#dir)
-   [`issubclass`](https://docs.python.org/3/library/functions.html#issubclass)

Built-in constants  `None`,  `True`, and  `False`  are  _objects_:

We test the  `None`  object here.

```python
id(None)
4550218168
type(None)
<class 'NoneType'>
dir(None)
[__bool__', '__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']
issubclass(type(None), object)
True
```

Next, let’s inspect  `True`.

```python
id(True)
4550117616
type(True)
<class 'bool'>
dir(True)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
issubclass(type(True), object)
True
```

No reason to leave out  `False`!

```python
id(False)
4550117584
type(False)
<class 'bool'>
dir(False)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
issubclass(type(False), object)
True
```

_Strings_, even when created by a string literals, are also  _objects_.

```python
id("Hello campers!")
4570186864
type('Hello campers!')
<class 'str'>
dir("Hello campers!")
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
issubclass(type('Hello campers!'), object)
True
```

Same with  _numbers._

```python
id(42)
4550495728
type(42)
<class 'int'>
dir(42)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
issubclass(type(42), object)
True
```

## **Functions are Objects Too**

In Python, functions are first class objects.

_Functions_  in Python are also  _objects_, created with an  _identity_,  _type_, and  _value_. They too can be passed into other  _functions_:

```python
id(dir)
4568035688
type(dir)
<class 'builtin_function_or_method'>
dir(dir)
['__call__', '__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__self__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__text_signature__']
issubclass(type(dir), object)
True
```

It is also possible to bind functions to a name and called the bound function using that name:

```python
a = dir
print(a)
<built-in function dir>
a(a)
['__call__', '__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__self__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__text_signature__']
```

# Python Tuples

A tuple is a sequence of Python objects. Tuples are immutable which means they cannot be modified after creation, unlike lists.

****Creation:****

An empty  `tuple`  is created using a pair of round brackets,  `()`:

```py
    empty_tuple = ()
    print(empty_tuple)
    ()
    type(empty_tuple)
    <class 'tuple'>
    len(empty_tuple)
    0
```

A  `tuple`  with elements is created by separating the elements with commas (surrounding round brackets,  `()`, are optional with exceptions):

```py
    tuple_1 = 1, 2, 3       # Create tuple without round brackets.
    print(tuple_1)
    (1, 2, 3)
    type(tuple_1)
    <class 'tuple'>
    len(tuple_1)
    3
    tuple_2 = (1, 2, 3)     # Create tuple with round brackets.
    print(tuple_2)
    (1, 2, 3)
    tuple_3 = 1, 2, 3,      # Trailing comma is optional.
    print(tuple_3)
    (1, 2, 3)
    tuple_4 = (1, 2, 3,)    # Trailing comma in round brackets is also optional.
    print(tuple_4)
    (1, 2, 3)
```

A  `tuple`  with a single element must have the trailing comma (with or without round brackets):

```py
    not_tuple = (2)    # No trailing comma makes this not a tuple.
    print(not_tuple)
    2
    type(not_tuple)
    <class 'int'>
    a_tuple = (2,)     # Single element tuple. Requires trailing comma.
    print(a_tuple)
    (2,)
    type(a_tuple)
    <class 'tuple'>
    len(a_tuple)
    1
    also_tuple = 2,    # Round brackets omitted. Requires trailing comma.
    print(also_tuple)
    (2,)
    type(also_tuple)
    <class 'tuple'>
```

Round brackets are required in cases of ambiguity (if the tuple is part of a larger expression):

Note that it is actually the comma which makes a tuple, not the parentheses. The parentheses are optional, except in the empty tuple case, or when they are needed to avoid syntactic ambiguity.

For example,  `f(a, b, c)`  is a function call with three arguments, while  `f((a, b, c))`  is a function call with a 3-tuple as the sole argument.

```py
    print(1,2,3,4,)          # Calls print with 4 arguments: 1, 2, 3, and 4
    1 2 3 4
    print((1,2,3,4,))        # Calls print with 1 argument: (1, 2, 3, 4,)
    (1, 2, 3, 4)
    1, 2, 3 == (1, 2, 3)     # Equivalent to 1, 2, (3 == (1, 2, 3))
    (1, 2, False)
    (1, 2, 3) == (1, 2, 3)   # Use surrounding round brackets when ambiguous.
    True
```

A  `tuple`  can also be created with the  `tuple`  constructor:

```py
    empty_tuple = tuple()
    print(empty_tuple)
    ()
    tuple_from_list = tuple([1,2,3,4])
    print(tuple_from_list)
    (1, 2, 3, 4)
    tuple_from_string = tuple("Hello campers!")
    print(tuple_from_string)
    ('H', 'e', 'l', 'l', 'o', ' ', 'c', 'a', 'm', 'p', 'e', 'r', 's', '!')
    a_tuple = 1, 2, 3
    b_tuple = tuple(a_tuple)    # If the constructor is called with a tuple for
    the iterable,
    a_tuple is b_tuple          # the tuple argument is returned.
    True
```

****Accessing elements of a  `tuple`:****

Elements of  `tuples`  are accessed and indexed the same way that  `lists`  are.

```py
    my_tuple = 1, 2, 9, 16, 25
    print(my_tuple)
    (1, 2, 9, 16, 25)
```

_Zero indexed_

```py
    my_tuple[0]
    1
    my_tuple[1]
    2
    my_tuple[2]
    9
```

_Wrap around indexing_

```shell
    my_tuple[-1]
    25
    my_tuple[-2]
    16
```

****Packing and Unpacking:****

The statement  `t = 12345, 54321, 'hello!'`  is an example of tuple packing: the values  `12345`,  `54321`and  `'hello!'`  are packed together in a tuple. The reverse operation is also possible:

```py
    x, y, z = t                
```

This is called, appropriately enough, sequence unpacking and works for any sequence on the right-hand side. Sequence unpacking requires that there are as many variables on the left side of the equals sign as there are elements in the sequence. Note that multiple assignment is really just a combination of tuple packing and sequence unpacking.

```py
    t = 1, 2, 3    # Tuple packing.
    print(t)
    (1, 2, 3)
    a, b, c = t    # Sequence unpacking.
    print(a)
    1
    print(b)
    2
    print(c)
    3
    d, e, f = 4, 5, 6    # Multiple assignment combines packing and unpacking.
    print(d)
    4
    print(e)
    5
    print(f)
    6
    a, b = 1, 2, 3       # Multiple assignment requires each variable (right)
    have a matching element (left).
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: too many values to unpack (expected 2)
```

****Immutable:****

`tuples`  are immutable containers, guaranteeing  ****which****  objects they contain will not change. It does  ****not**** guarantee that the objects they contain will not change:

```py
    a_list = []
    a_tuple = (a_list,)    # A tuple (immutable) with a list (mutable) element.
    print(a_tuple)
    ([],)

    a_list.append("Hello campers!")
    print(a_tuple)         # Element of the immutable is mutated.
    (['Hello campers!'],)
```

****Uses:****

Functions can only return a single value, however, a heterogenuous  `tuple`  can be used to return multiple values from a function. One example is the built-in  `enumerate`function that returns an iterable of heterogenuous  `tuples`:

```py
    greeting = ["Hello", "campers!"]
    enumerator = enumerate(greeting)
    enumerator.next()
    enumerator.__next__()
    (0, 'Hello')
    enumerator.__next__()
    (1, 'campers!')
```

# Python Decorators

Decorators essentially work as wrappers. They modify the behaviour of the code before and after a target function execution, without the need to modify the function itself, augmenting the original functionality, thus decorating it.

Before going in detail about decorators, there are some concepts that should be clear. In Python, functions are objects and we can do a lot of useful stuff with them.

### ****Assigning funtions to a variables:****

```python
def greet(name):
  return "Hello "+name
greet_someone = greet
print greet_someone("John")
```

Output: Hello John

[Run code](https://repl.it/CXGk)

### ****Defining functions inside other functions:****

```python
def greet(name):
  def get_message():
    return "Hello "
  result = get_message()+name
  return result
print(greet("John"))
```

Output: Hello John

[Run code](https://repl.it/CXGu)

### ****Functions can also be passed as parameters to other functions:****

```python
def greet(name):
  return "Hello " + name
def call_func(func):
  other_name = "John"
  return func(other_name)  
print call_func(greet)
```

Output: Hello John

[Run code](https://repl.it/CXHC)

### ****Functions can return other functions:****

In other words, functions generating other functions.

```python
def compose_greet_func():
  def get_message():
    return "Hello there!"
  return get_message
greet = compose_greet_func()
print(greet())
```

Output: Hello there!

[Run code](https://repl.it/CXHG)

### ****Inner functions have access to the enclosing scope****

More commonly known as a  [closure](http://www.shutupandship.com/2012/01/python-closures-explained.html). A very powerful pattern that we will come across while building decorators. Another thing to note, Python only allows  [read access to the outer scope](http://www.tech-thoughts-blog.com/2013/07/writing-closure-in-python.html)  and not assignment. Notice how we modified the example above to read a “name” argument from the enclosing scope of the inner function and return the new function.

```python
def compose_greet_func(name):
  def get_message():
      return "Hello there "+name+"!"
  return get_message
greet = compose_greet_func("John")
print(greet())
```

Output: Hello there John!

[Run code](https://repl.it/CXHI)

## **Composition of Decorators**

Function decorators are simply wrappers to existing functions. Putting the ideas mentioned above together, we can build a decorator. In this example let’s consider a function that wraps the string output of another function by p tags.

```python
def get_text(name):
   return "lorem ipsum, {0} dolor sit amet".format(name)

def p_decorate(func):
   def func_wrapper(name):
       return "`<p>`{0}`</p>`".format(func(name))
   return func_wrapper

my_get_text = p_decorate(get_text)
print (my_get_text("John"))
```

Output:  `<p>`lorem ipsum, John dolor sit amet`</p>`

[Run code](https://repl.it/CXHL)

That was our first decorator. A function that takes another function as an argument, generates a new function, augmenting the work of the original function, and returning the generated function so we can use it anywhere. To have  `get_text`  itself be decorated by  `p_decorate`, we just have to assign get  _text to the result of p_ decorate.

```python
get_text = p_decorate(get_text)
print (get_text("John"))
```

Output: lorem ipsum, John dolor sit amet

Another thing to notice is that our decorated function takes a name argument. All that we have to do in the decorator is to let the wrapper of get_text pass that argument.

### ****Python’s Decorator Syntax****

Python makes creating and using decorators a bit cleaner and nicer for the programmer through some  [syntactic sugar](http://en.wikipedia.org/wiki/Syntactic_sugar). To decorate get_text we don’t have to get_text = p_decorator(get_text). There is a neat shortcut for that, which is to mention the name of the decorating function before the function to be decorated. The name of the decorator should be perpended with an @ symbol.

```python
def p_decorate(func):
   def func_wrapper(name):
       return "`<p>`{0}`</p>`".format(func(name))
   return func_wrapper

@p_decorate
def get_text(name):
   return "lorem ipsum, {0} dolor sit amet".format(name)

print get_text("John")
```

Output:  `<p>`lorem ipsum, John dolor sit amet`</p>`

[Run code](https://repl.it/CXHN)

Now let’s consider we wanted to decorate our get_text function by 2 other functions to wrap a div and strong tag around the string output.

```python
def p_decorate(func):
   def func_wrapper(name):
       return "`<p>`{0}`</p>`".format(func(name))
   return func_wrapper

def strong_decorate(func):
    def func_wrapper(name):
        return "`<strong>`{0}`</strong>`".format(func(name))
    return func_wrapper

def div_decorate(func):
    def func_wrapper(name):
        return "`<div>`{0}`</div>`".format(func(name))
    return func_wrapper
```

With the basic approach, decorating get_text would be along the lines of

```python
get_text = div_decorate(p_decorate(strong_decorate(get_text)))
```

With Python’s decorator syntax, the same thing can be achieved with much more expressive power.

```python
@div_decorate
@p_decorate
@strong_decorate
def get_text(name):
   return "lorem ipsum, {0} dolor sit amet".format(name)

print (get_text("John"))
```

Output:  `<div><p><strong>`lorem ipsum, John dolor sit amet`</strong></p></div>`

[Run code](https://repl.it/CXHQ)

One important thing to notice here is that the order of setting our decorators matters. If the order was different in the example above, the output would have been different.

### Decorating Methods

In Python, methods are functions that expect their first parameter to be a reference to the current object. We can build decorators for methods the same way, while taking self into consideration in the wrapper function.

```python
def p_decorate(func):
  def func_wrapper(self):
    return "`<p>`{0}`</p>`".format(func(self))
  return func_wrapper

class Person(object):
  def __init__(self):
    self.name = "John"
    self.family = "Doe"
  @p_decorate
  def get_fullname(self):
    return self.name+" "+self.family

my_person = Person()
print (my_person.get_fullname())
```

Output:  `<p>`John Doe`</p>`

[Run code](https://repl.it/CXH2)

A much better approach would be to make our decorator useful for functions and methods alike. This can be done by putting  [*args and **kwargs](http://docs.python.org/2/tutorial/controlflow.html#arbitrary-argument-lists)  as parameters for the wrapper, then it can accept any arbitrary number of arguments and keyword arguments.

```python
def p_decorate(func):
   def func_wrapper(*args, **kwargs):
       return "`<p>`{0}`</p>`".format(func(*args, **kwargs))
   return func_wrapper

class Person(object):
    def __init__(self):
        self.name = "John"
        self.family = "Doe"
    @p_decorate
    def get_fullname(self):
        return self.name+" "+self.family

my_person = Person()
print (my_person.get_fullname())
```

Output :  `<p>`John Doe`</p>`

[Run code](https://repl.it/CXH5)

### Passing arguments to decorators

Looking back at the example before the one above, you can notice how redundant the decorators in the example are. 3 decorators (divdecorate, pdecorate, strong_decorate) each with the same functionality, but wrapping the string with different tags.

We can definitely do much better than that. Why not have a more general implementation for one that takes the tag to wrap with as a string? Yes please!

```python
def tags(tag_name):
    def tags_decorator(func):
        def func_wrapper(name):
            return "<{0}>{1}</{0}>".format(tag_name, func(name))
        return func_wrapper
    return tags_decorator

@tags("p")
def get_text(name):
    return "Hello "+name

print (get_text("John"))
```

Output:  `<p>`Hello John`</p>`

[Run code](https://repl.it/CXH6)

It took a bit more work in this case. Decorators expect to receive a function as an argument, that is why we will have to build a function that takes those extra arguments and generate our decorator on the fly. In the example above, tags is our decorator generator.

### Debugging decorated functions

At the end of the day, decorators are just wrapping our functions. In case of debugging, that can be problematic since the wrapper function does not carry the name, module and docstring of the original function. Based on the example above if we do:

```python
print (get_text.__name__)
```

Output: func_wrapper. The output was expected to be get_text yet, the attributes  ****name****,  ****doc****, and  ****module****  of get_text got overridden by those of the wrapper(func_wrapper.

Obviously we can re-set them within func_wrapper but Python provides a much nicer way.

**Functools to the rescue**

```python
from functools import wraps
def tags(tag_name):
    def tags_decorator(func):
        @wraps(func)
        def func_wrapper(name):
            return "`<{0}>`{1}`</{0}>`".format(tag_name, func(name))
        return func_wrapper
    return tags_decorator

@tags("p")
def get_text(name):
    """returns some text"""
    return "Hello "+name

print (get_text.__name__) # get_text
print (get_text.__doc__) # returns some text
print (get_text.__module__) # __main__
```

[Run code](https://repl.it/CXHb)

You can notice from the output that the attributes of get_text are the correct ones now.

# Python For Loop Statement Example

Python utilizes a for loop to iterate over a list of elements. This is unlike C or Java, which use the for loop to change a value in steps and access something such as an array using that value.

For loops iterate over collection-based data structures like lists, tuples, and dictionaries.

The basic syntax is:

```python
for value in list_of_values:
  # use value inside this block
```

In general, you can use anything as the iterator value, where entries of the iterable can be assigned to. E.g. you can unpack tuples from a list of tuples:

```python
list_of_tuples = [(1,2), (3,4)]

for a, b in list_of_tuples:
  print("a:", a, "b:", b)
```

On the other hand, you can loop over anything that is iterable. You can call a function or use a list literal.

```python
for person in load_persons():
  print("The name is:", person.name)
```

```python
for character in ["P", "y", "t", "h", "o", "n"]:
  print("Give me a '{}'!".format(character))
```

Some ways in which For loops are used:

****Iterate over the range() function****

```python
for i in range(10):
    print(i)
```

Rather than being a function, range is actually an immutable sequence type. The output will contain results from lower bound i.e 0 to the upper bound i.e 10, but excluding 10. By default the lower bound or the starting index is set to zero. Output:

```
0
1
2
3
4
5
6
7
8
9
```

Additionally, one can specify the lower bound of the sequence and even the step of the sequence by adding a second and a third parameter.

```python
for i in range(4,10,2): #From 4 to 9 using a step of two
    print(i)
```

Output:

```
4
6
8
```

****xrange() function****

For the most part, xrange and range are the exact same in terms of functionality. They both provide a way to generate a list of integers for you to use, however you please. The only difference is that range returns a Python list object and xrange returns an xrange object. It means that xrange doesn’t actually generate a static list at run-time like range does. It creates the values as you need them with a special technique called yielding. This technique is used with a type of object known as generators.

One more thing to add. In Python 3.x, the xrange function does not exist anymore. The range function now does what xrange does in Python 2.x

****Iterate over values in a list or tuple****

```python
A = ["hello", 1, 65, "thank you", [2, 3]]
for value in A:
    print(value)
```

Output:

```
hello
1
65
thank you
[2, 3]
```

****Iterate over keys in a dictionary (aka hashmap)****

```python
fruits_to_colors = {"apple": "#ff0000",
                    "lemon": "#ffff00",
                    "orange": "#ffa500"}

for key in fruits_to_colors:
    print(key, fruits_to_colors[key])
```

Output:

```
apple #ff0000
lemon #ffff00
orange #ffa500
```

****Iterate over two lists of same size in a single loop with the zip() function****

```python
A = ["a", "b", "c"]
B = ["a", "d", "e"]

for a, b in zip(A, B):
  print a, b, a == b
  
```

Output:

```
>
a a True
b d False
c e False
>
```

****Iterate over a list and get the corresponding index with the enumerate() function****

```python
A = ["this", "is", "something", "fun"]

for index,word in enumerate(A):
    print(index, word)
```

Output:

```bush
0 this
1 is
2 something
3 fun
```

A common use case is iterating over a dictionary:

```python
for name, phonenumber in contacts.items():
  print(name, "is reachable under", phonenumber)
```

If you absolutely need to access the current index of your iteration, do  ****NOT****  use  `range(len(iterable))`! This is an extremely bad practice and will get you plenty of chuckles from senior Python developers. Use the built in function  `enumerate()`  instead:

```python
for index, item in enumerate(shopping_basket):
  print("Item", index, "is a", item)
```

****for/else statements****  Pyhton permits you to use else with for loops, the else case is executed when none of the conditions with in the loop body was satisfied. To use the else we have to make use of  `break`  statement so that we can break out of the loop on a satisfied condition. If we do not break out then the else part will be executed.

```python
week_days = ['Monday','Tuesday','Wednesday','Thursday','Friday']
today = 'Saturday'
for day in week_days:
  if day == today:
    print('today is a week day')
    break
else:
  print('today is not a week day')
```

In the above case the output will be  `today is not a week day`  since the break within the loop will never be executed.

****Iterate over a list using inline loop function****

We could also iterate inline using python. For example if we need to uppercase all the words in a list from a list, we could simply do the following:

```python
A = ["this", "is", "awesome", "shinning", "star"]

UPPERCASE = [word.upper() for word in A]
print (UPPERCASE)
```

Output:

```result
['THIS', 'IS', 'AWESOME', 'SHINNING', 'STAR']
```

# Python Function Example

A function allows you to define a reusable block of code that can be executed many times within your program.

Functions allow you to create more modular and  [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)  solutions to complex problems.

While Python already provides many built-in functions such as  `print()`  and  `len()`, you can also define your own functions to use within your projects.

One of the great advantages of using functions in your code is that it reduces the overall number of lines of code in your project.

### **Syntax**

In Python, a function definition has the following features:

1.  The keyword  `def`
2.  a function name
3.  parentheses’()’, and within parentheses input parameters, although the input parameters are optional.
4.  a colon ’:’
5.  some block of code to execute
6.  a return statement (optional)

```python
# a function with no parameters or returned values
def sayHello():
  print("Hello!")

sayHello()  # calls the function, 'Hello!' is printed to the console

# a function with a parameter
def helloWithName(name):
  print("Hello " + name + "!")

helloWithName("Ada")  # calls the function, 'Hello Ada!' is printed to the console

# a function with multiple parameters with a return statement
def multiply(val1, val2):
  return val1 * val2

multiply(3, 5)  # prints 15 to the console
```

Functions are blocks of code that can be reused simply by calling the function. This enables simple, elegant code reuse without explicitly re-writing sections of code. This makes code more readable, easier to debug, and limits typing errors.

Functions in Python are created using the  `def`  keyword, followed by a function name and function parameters inside parentheses.

A function always returns a value. The  `return`  keyword is used by the function to return a value. If you don’t want to return any value, the default value  `None`  will be returned.

The function name is used to call the function, passing the needed parameters inside parentheses.

```python
# this is a basic sum function
def sum(a, b):
  return a + b

result = sum(1, 2)
# result = 3
```

You can define default values for the parameters, and that way Python will interpret that the value of that parameter is the default one if none is given.

```python
def sum(a, b=3):
  return a + b

result = sum(1)
# result = 4
```

You can pass the parameters in the order you want, using the name of the parameter.

```python
result = sum(b=2, a=2)
# result = 4
```

However, it is not possible to pass a keyword argument before a non-keyword one.

```python
result = sum(3, b=2)
#result = 5
result2 = sum(b=2, 3)
#Will raise SyntaxError
```

Functions are also Objects, so you can assign them to a variable, and use that variable like a function.

```python
s = sum
result = s(1, 2)
# result = 3
```

### **Notes**

If a function definition includes parameters, you must provide the same number of parameters when you call the function.

```python
print(multiply(3))  # TypeError: multiply() takes exactly 2 arguments (0 given)

print(multiply('a', 5))  # 'aaaaa' printed to the console

print(multiply('a', 'b'))  # TypeError: Python can't multiply two strings
```

The block of code that the function will run includes all statements indented within the function.

```python
def myFunc():
print('this will print')
print('so will this')

x = 7
# the assignment of x is not a part of the function since it is not indented
```

Variables defined within a function only exist within the scope of that function.

```python
def double(num):
x = num * 2
return x

print(x)  # error - x is not defined
print(double(4))  # prints 8
```

Python interprets the function block only when the function is called and not when the function is defined. So even if the function definition block contains some sort of error, the python interpreter will point that out only when the function is called.

# Python Generator Example

Generators are a special type of function that allows you to return values without ending a function. It does this by using the  `yield`  keyword. Similar to  `return`, the  `yield`expression will return a value to the caller. The key difference between the two is that  `yield`  will suspend the function, allowing for more values to be returned in the future.

Generators are iterable so they can be used cleanly with for loops or anything else that iterates.

```python
def my_generator():
    yield 'hello'
    yield 'world'
    yield '!'

for item in my_generator():
    print(item)

# output:
# hello
# world
# !
```

Like other iterators, generators can be passed to the  `next`  function to retrieve the next item. When a generator has no more values to yield, a  `StopIteration`  error is raised.

```python
g = my_generator()
print(next(g))
# 'hello'
print(next(g))
# 'world'
print(next(g))
# '!'
print(next(g))
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# StopIteration
```

Generators are particularly useful when you need to create a large set of values but do not need to keep them all in memory at the same time. For example, if you need to print the first million fibonacci numbers, you would typically return a list of a million values and iterate over the list to print each value. However with a generator, you can return each value one at a time:

```python
def fib(n):
    a = 1
    b = 1
    for i in range(n):
        yield a
        a, b = b, a + b

for x in fib(1000000):
    print(x)
```

# Python Iterator Example

Python supports a concept of iteration over containers. This is implemented using two distinct methods; these are used to allow user-defined classes to support iteration.

[Python Docs - Iterator Types](https://docs.python.org/3/library/stdtypes.html#iterator-types)

Iteration is the process of programmatically repeating a step a given number of times. A programmer can make use of iteration to perform the same operation on every item in a collection of data, for example printing out every item in a list.

-   Objects can implement a  `__iter__()`  method that returns an iterator object to support iteration.

Iterator objects must implement:

-   `__iter__()`: returns the iterator object.
-   `__next__()`: returns the next object of the container.iterator_object = ‘abc’.****iter****() print(iterator_object) print(id(iterator_object)) print(id(iterator_object.****iter****())) # Returns the iterator itself. print(iterator_object.****next****()) # Returns 1st object and advances iterator. print(iterator_object.****next****()) # Returns 2nd object and advances iterator. print(iterator_object.****next****()) # Returns 3rd object and advances iterator. print(iterator_object.****next****()) # Raises StopIteration Exception.

Output :

```python
<str_iterator object at 0x102e196a0>
4343305888
4343305888
a
b
c
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-1-d466eea8c1b0> in <module>()
      6 print(iterator_object.__next__())     # Returns 2nd object and advances iterator.
      7 print(iterator_object.__next__())     # Returns 3rd object and advances iterator.
----> 8 print(iterator_object.__next__())     # Raises StopIteration Exception.

StopIteration:
```

# **Ternary operator in Python Example**

Ternary operations in Python, often also referred to as conditional expressions, allow the programmer to perform an evaluation and return a value based on the truth of the given condition.

The ternary operator differs from a standard  `if`,  `else`,  `elif`  structure in the sense that it is not a control flow structure, and behaves more like other operators such as  `==`  or  `!=`  in the Python language.

### **Example**

In this example, the string  `Even`  is returned if the  `val`  variable is even, otherwise the string  `Odd`  is returned. The returned string is then assigned to the  `is_even`  variable and printed to the console.

#### **Input**

```python
for val in range(1, 11):
    is_even = "Even" if val % 2 == 0 else "Odd"
    print(val, is_even, sep=' = ')
```

#### **Output**

```python
1 = Odd
2 = Even
3 = Odd
4 = Even
5 = Odd
6 = Even
7 = Odd
8 = Even
9 = Odd
10 = Even
```

# Python While Loop Statement Example

Python utilizes the  `while`  loop similarly to other popular languages. The  `while`  loop evaluates a condition then executes a block of code if the condition is true. The block of code executes repeatedly until the condition becomes false.

The basic syntax is:

```python
counter = 0
while counter < 10:
   # Execute the block of code here as
   # long as counter is less than 10
```

An example is shown below:

```python
days = 0    
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
while days < 7:
   print("Today is " + week[days])
   days += 1
```

Output:

```python
Today is Monday
Today is Tuesday
Today is Wednesday
Today is Thursday
Today is Friday
Today is Saturday
Today is Sunday
```

Line-by-Line explanation of the above CODE:

1.  the variable ‘days’ is set to a value 0.
2.  a variable week is assigned to a list containing all the days of the week.
3.  while loop starts
4.  the block of code will be executed until the condition returns ‘true’.
5.  the condition is ‘days<7’ which roughly says run the while loop until the point the variable days is less than 7
6.  So when the days=7 the while loop stops executing.
7.  the days variable gets updated on every iteration.
8.  When the while loop runs for the first time, the line ‘Today is Monday’ is printed onto the console and the variable days becomes equal to 1.
9.  Since the variable days is equal to 1 which is less than 7, the while loop is executed again.
10.  It goes on again and again and when the console prints ‘Today is Sunday’ the variable days is now equal to 7 and the while loop stops executing.

# How to Install Python 3

You can download Python from this official  [link](https://www.python.org/downloads/). Based on your OS (Windows or Linux or OSX), you might want to install Python 3 following  [these instructions](http://docs.python-guide.org/en/latest/starting/installation/).

## **Using Virtual Environments**

It is always a great idea to  [sandbox](https://en.wikipedia.org/wiki/Sandbox_(computer_security))  your Python installation and keep it separate from your  _System Python_. The  _System Python_  is the path to Python interpreter, which is used by other modules installed along with your OS.

It’s  ****not safe****  to install Python Web-frameworks or libraries directly using  _System Python_. Instead, you can use  [Virtualenv](https://virtualenv.readthedocs.org/en/latest/)  to create and spawn a separate Python process when you are developing Python applications.

### **Virtualenvwrapper**

The  [Virtualenvwrapper module](https://virtualenvwrapper.readthedocs.org/en/latest/)  makes it easy for you to manage and sandbox multiple Python sandboxed environments in one machine, without corrupting any modules or services written in Python and used by your machine.

Of course, most cloud hosted development environments such as  [Nitrous](https://www.nitrous.io/)  or  [Cloud9](https://c9.io/)  also come with these pre-installed and ready for you to get coding! You can quickly pick a box from your dashboard and start coding after activating a Python 3 environment.

In  [Cloud9](https://c9.io/), you need to select the Django box while creating a new development environment.

A few shell command examples follow. If you wish to copy-paste, do note that the  `$`  sign is a shorthand for the terminal prompt, it’s not part of the command. My terminal prompt looks something like this:

```python
alayek:~/workspace (master) $
```

And, an  `ls`  would look like

```python
alayek:~/workspace (master) $ ls
```

But, while writing the same in this documentation, I would be writing it as

```python
$ ls
```

Getting back to our discussion, you can create a Python 3 interpreter-included sandbox on Cloud9 by running on your cloud terminal:

```python
$ mkvirtualenv py3 --python=/usr/bin/python3
```

You have to run it only once after creating a new box for your project. Once executed, this command would create a new sandboxed virtualenv ready for you to use, named  `py3`.

To view available virtual environments, you can use

```python
$ workon
```

To activate  `py3`, you can use the  `workon`  command with the name of the environment:

```python
$ workon py3
```

All three terminal commands above would also work on local Linux machines or OSX machines. These are  [virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/#introduction)  commands; so if you are planning on using them, make sure you have this module installed and added to  `PATH`  variable.

If you are inside a virtual environment; you can easily find that out by checking your terminal prompt. The environment name will be clearly shown in your terminal prompt.

For instance, when I am inside the  `py3`  environment, I will be seeing this as my terminal prompt:

```python
(py3)alayek:~/workspace (master) $
```

Notice the  `(py3)`  in braces! If for some reason you are not seeing this, even if you are inside a virtual env; you can try doing one of the things  [mentioned here](http://stackoverflow.com/questions/1871549/python-determine-if-running-inside-virtualenv).

To get out of a virtual environment or to deactivate one - use this command:

```python
$ deactivate
```

Again, this works only with virtualenvwrapper module.

### **Pipenv**

An alternative to using virtualenvwrapper is  [Pipenv](https://docs.pipenv.org/). It automatically creates virtual environments for your projects, and maintains a  `Pipfile`  which contains the dependencies. Using Pipenv means you no longer need to use pip and virtualenv separately, or manage your own  `requirements.txt`  file. For those familiar with JavaScript, Pipenv is similar to using a packaging tool like  `npm`.

To get started with Pipenv, you can follow this very detailed  [guide](https://docs.pipenv.org/install.html#installing-pipenv). Pipenv makes it easy to  [specify which version of Python](https://docs.pipenv.org/basics.html#specifying-versions-of-python)  you wish to use for each project,  [import](https://docs.pipenv.org/basics.html#importing-from-requirements-txt)  from an existing  `requirements.txt`  file and  [graph](https://docs.pipenv.org/#pipenv-graph)  your dependencies.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY2MTUxMjc3LDMzMTcwNDk0MSwxODMxOT
I0NjgzXX0=
-->