# 18 Python scripts that help you write code faster

Python is a no-BS programming language. Readability and simplicity of design are two of the biggest reasons for its immense popularity.

This is why it is worthwhile to remember some common Python tricks to help improve your code design. These will save you the trouble of surfing Stack Overflow every time you need to do something.  
The following tricks will prove handy in your day-to-day coding exercises.

## **1. Finding Unique Elements in a String**

The following snippet can be used to find all the unique elements in a string. We use the property that  [all elements in a set are unique.](https://on.morioh.net/b0a3f595aa?r=https://medium.com/python-pandemonium/https-medium-com-python-pandemonium-an-introduction-to-python-sets-part-i-120974a713be "all elements in a set are unique.")

```py
my_string = "aavvccccddddeee"

# converting the string to a set
temp_set = set(my_string)

# stitching set into a string using join
new_string = ''.join(temp_set)

print(new_string)

# Output
# adcev
```

## **2. Using rhe Title Case (First Letter Caps)**

The following snippet can be used to convert a string to title case. This is done using the  `title()`  method of the string class.

```
my_string = "my name is chaitanya baweja"

# using the title() function of string class
new_string = my_string.title()

print(new_string)

# Output
# My Name Is Chaitanya Baweja
```

## **3. Reversing a String**

The following snippet reverses a string using the Python slicing operation.

```
# Reversing a string using slicing

my_string = "ABCDE"
reversed_string = my_string[::-1]

print(reversed_string)

# Output
# EDCBA
```

You can read more about this  [here](https://on.morioh.net/b0a3f595aa?r=https://medium.com/swlh/how-to-reverse-a-string-in-python-66fc4bbc7379 "here").

## **4. Printing a String or a List n Times**

You can use multiplication (*) with strings or lists. This allows us to multiply them as many times as we like.

```
n = 3 # number of repetitions

my_string = "abcd"
my_list = [1,2,3]

print(my_string*n)
# abcdabcdabcd

print(my_list*n)

# [1,2,3,1,2,3,1,2,3]
```

An interesting use case of this could be to define a list with a constant value — let’s say zero.

```
n = 4
my_list = [0]*n # n denotes the length of the required list

# [0, 0, 0, 0]
```

## **5. Combining a List of Strings Into a Single String**

The join() method combines a list of strings passed as an argument into a single string. In our case, we separate them using the comma separator.

```
list_of_strings = ['My', 'name', 'is', 'Chaitanya', 'Baweja']

# Using join with the comma separator
print(','.join(list_of_strings))

# Output
# My,name,is,Chaitanya,Baweja
```

## **6. Swap Values Between Two Variables**

Python makes it quite simple to swap values between two variables without using another variable.

```
a = 1
b = 2

a, b = b, a

print(a) # 2
print(b) # 1
```

## **7. Split a String Into a List of Substrings**

We can split a string into a list of substrings using the .split() method in the string class. You can also pass as an argument the separator on which you wish to split.

```
string_1 = "My name is Chaitanya Baweja"
string_2 = "sample/ string 2"

# default separator ' '
print(string_1.split())
# ['My', 'name', 'is', 'Chaitanya', 'Baweja']

# defining separator as '/'
print(string_2.split('/'))
# ['sample', ' string 2']

```

## **8. List Comprehension**

List comprehension provides us with an elegant way of creating lists based on other lists.  
The following snippet creates a new list by multiplying each element of the old list by two.

```
# Multiplying each element in a list by 2

original_list = [1,2,3,4]

new_list = [2*x for x in original_list]

print(new_list)
# [2,4,6,8]

```

You can read more about it  [here.](https://on.morioh.net/b0a3f595aa?r=https://medium.com/swlh/list-comprehensions-in-python-e8d409bb216e "here.")

## **9. Check If a Given String Is a Palindrome or Not**

We have already discussed how to reverse a string. So palindromes become a straightforward program in Python.

```
my_string = "abcba"

if my_string == my_string[::-1]:
    print("palindrome")
else:
    print("not palindrome")

# Output
# palindrome

```

## **10. Using Enumerate to Get Index/Value Pairs**

The following script uses enumerate to iterate through values in a list along with their indices.

```
my_list = ['a', 'b', 'c', 'd', 'e']

for index, value in enumerate(my_list):
    print('{0}: {1}'.format(index, value))

# 0: a
# 1: b
# 2: c
# 3: d
# 4: e

```

## **11. Find Whether Two Strings are Anagrams**

An interesting application of the  `Counter` class is to find anagrams.

An anagram is a word or phrase formed by rearranging the letters of a different word or phrase.

If the  `Counter`  objects of two strings are equal, then they are anagrams.

```
from collections import Counter

str_1, str_2, str_3 = "acbde", "abced", "abcda"
cnt_1, cnt_2, cnt_3  = Counter(str_1), Counter(str_2), Counter(str_3)

if cnt_1 == cnt_2:
    print('1 and 2 anagram')
if cnt_1 == cnt_3:
    print('1 and 3 anagram')

```

## **12. Using the try-except-else Block**

Error handling in Python can be done easily using the try/except block. Adding an else statement to this block might be useful. It’s run when there is no exception raised in the try block.  
If you need to run something irrespective of exception, use  `finally`.

```
a, b = 1,0

try:
    print(a/b)
    # exception raised when b is 0
except ZeroDivisionError:
    print("division by zero")
else:
    print("no exceptions raised")
finally:
    print("Run this always")

```

## **13. Frequency of Elements in a List**

There are multiple ways of doing this, but my favorite is using the Python  `Counter`  class.

Python counter keeps track of the frequency of each element in the container.  `Counter()`  returns a dictionary with elements as keys and frequency as values.

We also use the  `most_common()`  function to get the`most_frequent`element in the list.

```
# finding frequency of each element in a list
from collections import Counter

my_list = ['a','a','b','b','b','c','d','d','d','d','d']
count = Counter(my_list) # defining a counter object

print(count) # Of all elements
# Counter({'d': 5, 'b': 3, 'a': 2, 'c': 1})

print(count['b']) # of individual element
# 3

print(count.most_common(1)) # most frequent element
# [('d', 5)]

```

## **14. Check the Memory Usage of an Object**

The following script can be used to check the memory usage of an object. Read more about it  [here](https://on.morioh.net/b0a3f595aa?r=https://code.tutsplus.com/tutorials/understand-how-much-memory-your-python-objects-use--cms-25609 "here").

```
import sys

num = 21

print(sys.getsizeof(num))

# In Python 2, 24
# In Python 3, 28

```

## **15. Sampling From a List**

The following snippet generates `n`  number of random samples from a given list using the  `random`  library.

```
import random

my_list = ['a', 'b', 'c', 'd', 'e']
num_samples = 2

samples = random.sample(my_list,num_samples)
print(samples)
# [ 'a', 'e'] this will have any 2 random values

```

I have been recommended the  [secrets](https://on.morioh.net/b0a3f595aa?r=https://docs.python.org/3/library/secrets.html "secrets ") library for generating random samples for cryptography purposes. The following snippet will work  
only on Python 3.

```
import secrets                              # imports secure module.
secure_random = secrets.SystemRandom()      # creates a secure random object.

my_list = ['a','b','c','d','e']
num_samples = 2

samples = secure_random.sample(my_list, num_samples)

print(samples)
# [ 'e', 'd'] this will have any 2 random values

```

## **16. Time Taken to Execute a Piece of Code**

The following snippet uses the  `time`  library to calculate the time taken to execute a piece of code.

```
import time

start_time = time.time()
# Code to check follows
a, b = 1,2
c = a+ b
# Code to check ends
end_time = time.time()
time_taken_in_micro = (end_time- start_time)*(10**6)

print(" Time taken in micro_seconds: {0} ms").format(time_taken_in_micro)

```

## **17. Flattening a List of Lists**

Sometimes you’re not sure about the nesting depth of your list, and you simply want all the elements in a single flat list.  
Here’s how you can get that:

```
from iteration_utilities import deepflatten

# if you only have one depth nested_list, use this
def flatten(l):
  return [item for sublist in l for item in sublist]

l = [[1,2,3],[3]]
print(flatten(l))
# [1, 2, 3, 3]

# if you don't know how deep the list is nested
l = [[1,2,3],[4,[5],[6,7]],[8,[9,[10]]]]

print(list(deepflatten(l, depth=3)))
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```

[Numpy flatten](https://on.morioh.net/b0a3f595aa?r=https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.flatten.htmlhttps://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.flatten.html "Numpy flatten")  is a better way to do this if you have a properly formatted array.

## **18. Merging Two Dictionaries**

While in Python 2, we used the  `update()`  method to merge two dictionaries; Python 3.5 made the process even simpler.  
In the script given below, two dictionaries are merged. Values from the second dictionary are used in case of intersections.

```
dict_1 = {'apple': 9, 'banana': 6}
dict_2 = {'banana': 4, 'orange': 8}

combined_dict = {**dict_1, **dict_2}

print(combined_dict)
# Output
# {'apple': 9, 'banana': 4, 'orange': 8}
```


> [Source : ](https://morioh.com/p/4f4b74ba17cc?f=5c21fb01c16e2556b555ab32&fbclid=IwAR1RdPqOkouQtzq7p5KUO1AIHwHyKnZpDRGVPX5vKMI_07R9TE2y7xALH7Q).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTEwNzYzNzRdfQ==
-->