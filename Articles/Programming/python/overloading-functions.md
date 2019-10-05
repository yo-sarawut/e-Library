
Overloading Functions and Operators in Python
==

### What is Overloading?

Overloading, in the context of programming, refers to the ability of a function or an operator to behave in different ways depending on the parameters that are passed to the function, or the operands that the operator acts on. In this article, we will see how we can perform function overloading and operator overloading in Python.

Overloading a method fosters reusability. For instance, instead of writing multiple methods that differ only slightly, we can write one method and overload it. Overloading also improves code clarity and eliminates complexity.

Overloading is a very useful concept. However, it has a number of disadvantages associated with it. Overloading can cause confusion when used across inheritance boundaries. When used excessively, it becomes cumbersome to manage overloaded functions.

In the remaining section of this article, we will be discussing the function and operator overloading in detail.

### Function Overloading in Python

Depending on how the function has been defined, we can call it with zero, one, two, or even many parameters. This is referred to as "function overloading".

Function overloading is further divided into two types: overloading built-in functions and overloading custom functions. We will look at both the types in the upcoming sections.

#### Overloading Built-in Functions

It is possible for us to change the default behavior of Python's built-in functions. We only have to define the corresponding special method in our class.

Let us demonstrate this using Python's  `len()`  function on our Purchase class:

```python
class Purchase:
    def __init__(self, basket, buyer):
        self.basket = list(basket)
        self.buyer = buyer

    def __len__(self):
        return len(self.basket)

purchase = Purchase(['pen', 'book', 'pencil'], 'Python')
print(len(purchase))
```

**Output:**

```
3
```

To change how the  `len()`  function behaves, we defined a special method named  `_len_()`  in our class. Anytime we pass an object of our class to  `len()`, the result will be obtained by calling our custom defined function, that is,  `_len_()`.

The output shows that we are able to use  `len()`  to get the length of the basket.

If we call  `len()`  on the object without the  `__len__()`  function overloaded, we will get a TypeError as shown below:

```python
class Purchase:
    def __init__(self, basket, buyer):
        self.basket = list(basket)
        self.buyer = buyer

purchase = Purchase(['pen', 'book', 'pencil'], 'Python')
print(len(purchase))
```

**Output:**

```
Traceback (most recent call last):
  File "C:/Users/admin/func.py", line 8, in <module>
    print(len(purchase))
TypeError: object of type 'Purchase' has no len()
```

Note: Python expects the  `len()`  function to return an integer, hence this should be put into consideration when overloading the function. If your overloaded function is expected to return anything else other than an integer, you will get a TypeError.

We can change the behavior of the  `len()`  method in the above example from within the definition of its implementation, that is,  `__len__()`. Instead of returning the length of the basket, let us make it return something else:

```python
class Purchase:
    def __init__(self, basket, buyer):
        self.basket = list(basket)
        self.buyer = buyer

    def __len__(self):
        return 10;

purchase = Purchase(['pen', 'book', 'pencil'], 'Python')
print(len(purchase))
```

**Output:**

```
10
```

Instead of returning the length of the basket, it now returns the value that we have specified.

#### Overloading User-Defined Functions

To overload a user-defined function in Python, we need to write the function logic in such a way that depending upon the parameters passed, a different piece of code executes inside the function. Take a look at the following example:

```python
class Student:
    def hello(self, name=None):
        if name is not None:
            print('Hey ' + name)
        else:
            print('Hey ')

# Creating a class instance
std = Student()

# Call the method
std.hello()

# Call the method and pass a parameter
std.hello('Nicholas')
```

**Output:**

```
Hey
Hey Nicholas
```

We have created the class  `Student`  with one function named  `hello()`. The class takes the parameter  `name`  which has been set to  `None`. This means the method can be called with or without a parameter.

We have created an instance of the class which has been used to call the function twice, first with zero parameters and secondly with one parameter. We have implemented function overloading since there are two ways to call the function.

Now we know how function overloading works, the next section focusses on operator overloading.

### Operator Overloading

Python allows us to change the default behavior of an operator depending on the operands that we use. This practice is referred to as "operator overloading".

The functionality of Python operators depends on built-in classes. However, the same operator will behave differently when applied to different types. A good example is the "+" operator. This operator will perform an arithmetic operation when applied on two numbers, will concatenate two strings, and will merge two lists.

#### Examples of Operator Overloading

To see Python's operator overloading in action, launch the Python terminal and run the following commands:

```python
>>> 4 + 4
8
>>> "Py" + "thon"
'Python'
```

In the first command, we have used the "+" operator to add two numbers. In the second command, we used the same operator to concatenate two strings.

In this case, the "+" operator has two interpretations. When used to add numbers, it is referred to as an "addition operator". When used to add strings, it is referred to as "concatenation operator". In short, we can say that the "+" operator has been overloaded for  `int`  and  `str`  classes.

To achieve operator overloading, we define a special method in a class definition. The name of the method should begin and end with a double underscore (__). The + operator is overloaded using a special method named  `__add__()`. This method is implemented by both the  `int`  and  `str`  classes.

Consider the following expression:

```python
x + y
```

Python will interpret the expression as  `x.__add__(y)`. The version of  `__add__()`  that is called will depend on the types of  `x`  and  `y`. For example:

```python
>>> x, y = 5, 7

>>> x + y

12
>>> x.__add__(y)
12
>>>

```

The above example demonstrates how to use the + operator as well as its special method.

The following example demonstrates how to overload various operators in Python:

```python
import math

class Point:

    def __init__(self, xCoord=0, yCoord=0):
        self.__xCoord = xCoord
        self.__yCoord = yCoord

    # get x coordinate
    def get_xCoord(self):
        return self.__xCoord

    # set x coordinate
    def set_xCoord(self, xCoord):
        self.__xCoord = xCoord

    # get y coordinate
    def get_yCoord(self):
        return self.__yCoord

    # set y coordinate
    def set_yCoord(self, yCoord):
        self.__yCoord = yCoord

    # get current position
    def get_position(self):
        return self.__xCoord, self.__yCoord

    # change x & y coordinates by p & q
    def move(self, p, q):
        self.__xCoord += p
        self.__yCoord += q

    # overload + operator
    def __add__(self, point_ov):
        return Point(self.__xCoord + point_ov.__xCoord, self.__yCoord + point_ov.__yCoord)

    # overload - operator
    def __sub__(self, point_ov):
        return Point(self.__xCoord - point_ov.__xCoord, self.__yCoord - point_ov.__yCoord)

    # overload < (less than) operator
    def __lt__(self, point_ov):
        return math.sqrt(self.__xCoord ** 2 + self.__yCoord ** 2) < math.sqrt(point_ov.__xCoord ** 2 + point_ov.__yCoord ** 2)

    # overload > (greater than) operator
    def __gt__(self, point_ov):
        return math.sqrt(self.__xCoord ** 2 + self.__yCoord ** 2) > math.sqrt(point_ov.__xCoord ** 2 + point_ov.__yCoord ** 2)

    # overload <= (less than or equal to) operator
    def __le__(self, point_ov):
        return math.sqrt(self.__xCoord ** 2 + self.__yCoord ** 2) <= math.sqrt(point_ov.__xCoord ** 2 + point_ov.__yCoord ** 2)

    # overload >= (greater than or equal to) operator
    def __ge__(self, point_ov):
        return math.sqrt(self.__xCoord ** 2 + self.__yCoord ** 2) >= math.sqrt(point_ov.__xCoord ** 2 + point_ov.__yCoord ** 2)

    # overload == (equal to) operator
    def __eq__(self, point_ov):
        return math.sqrt(self.__xCoord ** 2 + self.__yCoord ** 2) == math.sqrt(point_ov.__xCoord ** 2 + point_ov.__yCoord ** 2)

point1 = Point(2, 4)
point2 = Point(12, 8)

print("point1 < point2:", point1 < point2)
print("point1 > point2:", point1 > point2)
print("point1 <= point2:", point1 <= point2)
print("point1 >= point2:", point1 >= point2)
print("point1 == point2:", point1 == point2)```
```
**Output:**

```
point1 < point2: True
point1 > point2: False
point1 <= point2: True
point1 >= point2: False
point1 == point2: False
```

We have two private attributes in the Point class, namely,  `__xCoord`  and  `__yCoord`  representing cartesian plain coordinates named  `xCoord`  and  `yCoord`. We have defined the setter and getter methods for these attributes. The  `get_position()`  method helps us get the current position while the  `move()`  method helps us change the coordinates.

Consider the following line extracted from the code:

```python
    def __add__(self, point_ov):
```

The line helps us overload the + operator for our class. The  `__add__()`  method should create a new Point object by adding the individual coordinates of a single Point object to another Point object. It finally returns the newly created object to the caller. This helps us write expressions such as:

```python
point3 = point1 + point2
```

Python will interpret the above as  `point3 = point1.__add__(point2)`. It will then call the  `__add__()`  method to add two Point objects. The result will be assigned to "point3".

Note that once the  `__add__()`  method is called, the value of  `point1`  will be assigned to  `self`  parameter while the value of  `point2`  will be assigned to  `point_ov`parameter. All the other special methods will work in a similar way.

#### Operators to Overload

The following table shows some of the more commonly overloaded mathematical operators, and the class method to overload:


|Operator|	Method|
|:--:|--|
|+|	```__add__(self, other)```|
|-|	```__sub__(self, other)```|
|*|	```__mul__(self, other)```|
|/	|```__truediv__(self, other)```|
|%|	```__mod__(self, other)```|
|<|	```__lt__(self, other)```|
|<=|	```__le__(self, other)```|
|==|	```__eq__(self, other)```|
|!=|	```__ne__(self, other)```|
|>|```__gt__(self, other)```|
|>=|	```__ge__(self, other)```|


### Conclusion

Python supports both function and operator overloading. In function overloading, we can use the same name for many Python functions but with the different number or types of parameters. With operator overloading, we are able to change the meaning of a Python operator within the scope of a class.

Reference : [https://stackabuse.com/overloading-functions-and-operators-in-python/](https://stackabuse.com/overloading-functions-and-operators-in-python/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUxMTg3OTcxNl19
-->