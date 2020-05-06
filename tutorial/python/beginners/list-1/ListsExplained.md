
# Python Lists Explained: Len, Pop, Index, and List Comprehension

![Python Lists Explained: Len, Pop, Index, and List Comprehension](https://images.unsplash.com/photo-1507925921958-8a62f3d1a50d?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ)

Lists in Python are similar to arrays in JavaScript. They are one of the built in data types in Python used to store collections of data.

## Basic usage

### How to create a list

An empty  `list`  is created using a pair of square brackets:

```shell
>>> empty_list = []
>>> type(empty_list)
<class 'list'>
>>> len(empty_list)
0
```

A  `list`  can be created with elements by enclosing a comma separated list of elements with square brackets. Lists allow for the elements to be of different types (heterogeneous) but are most commonly of a single type (homogeneous):

```shell
>>> homogeneous_list = [1, 1, 2, 3, 5, 8]
>>> type(homogeneous_list)
<class 'list'>
>>> print(homogeneous_list)
[1, 1, 2, 3, 5, 8]
>>> len(homogeneous_list)
6
>>> heterogeneous_list = [1, "Hello Campers!"]
>>> print(heterogeneous_list)
[1, "Hello Campers!"]
>>> len(heterogeneous_list)
2
```

The  `list`  constructor can also be used to create a  `list`:

```shell
>>> empty_list = list()                            # Creates an empty list
>>> print(empty_list)
[]
>>> list_from_iterable = list("Hello campers!")    # Creates a list from an iterable.
>>> print(list_from_iterable)
['H', 'e', 'l', 'l', 'o', ' ', 'c', 'a', 'm', 'p', 'e', 'r', 's', '!']
```

You can also use List Comprehension to create lists, which we'll cover later in the article.

### Access elements in a list

```shell
>>> my_list = [1, 2, 9, 16, 25]
>>> print(my_list)
[1, 2, 9, 16, 25]
```

_Zero indexed_

```shell
>>> my_list[0]
1
>>> my_list[1]
2
>>> my_list[2]
9
```

_Wrap around indexing_

```shell
>>> my_list[-1]
25
>>> my_list[-2]
16
```

_Unpacking lists for python-3_

```shell
>>> print(*my_list)
1 2 9 16 25
```

### Lists are mutable

`lists`  are mutable containers. Mutable containers are containers that allow changes to which objects are contained by the container.

Elements from a  `list`  may be extracted and re-arranged using another  `list`  as index.

```shell
>>> my_list = [1, 2, 9, 16, 25, 34, 53, 21]
>>> my_index = [5, 2, 0]
>>> my_new_list = [my_list[i] for i in my_index]
>>> print(my_new_list)
[34, 9, 1]
```

## List methods

### `len()`

The  `len()`  method returns the length of an object, whether that be a list, a string, tuple, or dictionary.

`len()`  takes one argument, which can be a sequence (such as a string, bytes, tuple, list, or range) or collection (such as a dictionary, set, or frozen set).

```text
list1 = [123, 'xyz', 'zara'] # list
print(len(list1)) # prints 3 as there are 3 elements in the list1

str1 = 'basketball' # string
print(len(str1)) # prints 10 as the str1 is made of 10 characters

tuple1 = (2, 3, 4, 5) # tuple 
print(len(tuple1)) # prints 4 as there are 4 elements in the tuple1

dict1 = {'name': 'John', 'age': 4, 'score': 45} # dictionary
print(len(dict1)) # prints 3 as there are 3 key and value pairs in the dict1
```

### `index()`

`index()`  returns the the first occurrence/index of the element in the list given as an argument to the function.

```py
numbers = [1, 2, 2, 3, 9, 5, 6, 10]
words = ["I", "love", "Python", "I", "love"]

print(numbers.index(9)) # 4
print(numbers.index(2)) # 1
print(words.index("I")) # 0
print(words.index("am")) # returns a ValueError as 'am' is not in the `words` list
```

Here the first output is very obvious, but the second and third might seem confusing at first. But remember  `index()`  returns the first occurrence of the element and hence in this case  `1`  and  `0`  are the indices where  `2`  and  `"I"`  occur first in the lists respectively.

Also, if an element is not found in the list, a  `ValueError`  is returned as in the case of indexing  `"am"`  in the  `words`  list.

**Optional arguments**

You can also use optional arguments to limit your search to a particular sub-sequence of the list:

```py
words = ["I", "am", "a", "I", "am", "Pythonista"]

print(words.index("am", 2, 5)) # 4
```

Although the element is searched between the indices 2 (inclusive) and 5 (not inclusive), the returned index is computed relative to the beginning of the full list rather than the start argument.

### `pop()`

The  `pop()`  method removes and returns the last element from a list.

There is an optional parameter which is the index of the element to be removed from the list. If no index is specified,  `pop()`  removes and returns the last item in the list.

If the index passed to the  `pop()`  method is not in the range, it throws the  `IndexError: pop index out of range`  exception.

```py
cities = ['New York', 'Dallas', 'San Antonio', 'Houston', 'San Francisco'];

print "City popped is: ", cities.pop() # City popped is: San Francisco
print "City at index 2 is  : ", cities.pop(2) # City at index 2 is: San Antonio
```

**Basic stack functionality**

The  `pop()`  method is often used in conjunction with  `append()`  to implement basic stack functionality in a Python application:

```py
stack = []

for i in range(5):
    stack.append(i)

while len(stack):
    print(stack.pop())
```

### List Comprehension

List Comprehension is a way of looping through a list to produce a new list based on some conditions. It can be confusing at first but once you are acclimated to the syntax it is very powerful and quick.

The first step in learning how to use list comprehension is to look at the traditional way of looping through a list. The following is a simple example that returns a new list of even numbers.

```python
# Example list for demonstration
some_list = [1, 2, 5, 7, 8, 10]

# Empty list that will be populate with a loop
even_list = []

for number in some_list:
  if number % 2 == 0:
    even_list.append(number)

# even_list now equals [2, 8, 10]
```

First a list is created with some numbers. You then create an empty list that will hold your results from the loop. In the loop you check to see if each number is divisible by 2 and if so you add it the the  `even_list`. This took 5 lines of code not including comments and white space which isn’t much in this example.

Now for the list comprehension example.

```python
# Example list for demonstration
some_list = [1, 2, 5, 7, 8, 10]

# List Comprehension
even_list = [number for number in some_list if number % 2 == 0]

# even_list now equals [2, 8, 10]
```

Another example, with the same two steps: The following will create a list of numbers that correspond to the numbers in  `my_starting_list`  multiplied by 7.

```py
my_starting_list = [1, 2, 3, 4, 5, 6, 7, 8]
my_new_list = []

for item in my_starting_list:
my_new_list.append(item * 7)
```

When this code is run, the final value of  `my_new_list`  is:  `[7, 14, 21, 28, 35, 42, 49, 56]`

A developer using list comprehension could achieve the same result using the following list comprehension, which results in the same  `my_new_list`.

```py
my_starting_list = [1, 2, 3, 4, 5, 6, 7, 8]

my_new_list = [item * 7 for item in my_starting_list]
```

A simple formula to write in a list comprehension way is:

`my_list = [{operation with input n} for n in {python iterable}]`

Replace  `{operation with input n}`  with however you want to change the item returned from the iterable. The above example uses  `n * 7`  but the operation can be as simple or as complex as necessary.

Replace  `{python iterable}`  with any iterable. Sequence types will be most common. A list was used in the above example, but tuples and ranges are also common.

List comprehension adds an element from an existing list to a new list if some condition is met. It is neater, but is also much faster in most cases. In some cases, list comprehension may hinder readability, so the developer must weigh their options when choosing to use list comprehension.

**Examples of list comprehension with conditionals**

The flow of control in list comprehensions can be controlled using conditionals. For example:

```py
only_even_list = [i for i in range(13) if i%2==0]
```

This is equivalent to the following loop:

```py
only_even_list = list()
for i in range(13):
  if i%2 == 0:
    only_even_list.append(i)
```

List comprehension can also contain nested if conditions. Consider the following loop:

```py
divisible = list()
for i in range(50):
  if i%2 == 0:
    if i%3 == 0:
      divisible.append(i)
```

Using list comprehension this can be written as:

```py
divisible = [i for i in range(50) if i%2==0 if i%3==0]
```

If-Else statement can also be used along with list comprehension.

```py
list_1 = [i if i%2==0 else i*-1 for i in range(10)]
```

#### **More Information:**

-   [The Best Python Code Examples](https://www.freecodecamp.org/news/python-example/)

Reference : https://www.freecodecamp.org/news/python-lists-explained-len-pop-index-and-list-comprehension/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1MTQ4ODU0MV19
-->