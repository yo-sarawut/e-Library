Python Dictionary Tutorial
==

-   [Introduction](https://stackabuse.com/python-dictionary-tutorial/#introduction)
-   [Creating a Dictionary](https://stackabuse.com/python-dictionary-tutorial/#creatingadictionary)
-   [Accessing Elements](https://stackabuse.com/python-dictionary-tutorial/#accessingelements)
-   [Adding Elements](https://stackabuse.com/python-dictionary-tutorial/#addingelements)
-   [Updating Elements](https://stackabuse.com/python-dictionary-tutorial/#updatingelements)
-   [Removing Elements](https://stackabuse.com/python-dictionary-tutorial/#removingelements)
-   [Other Common Methods](https://stackabuse.com/python-dictionary-tutorial/#othercommonmethods)
-   [Conclusion](https://stackabuse.com/python-dictionary-tutorial/#conclusion)

### Introduction

Python comes with a variety of built-in data structures, capable of storing different types of data. A Python dictionary is one such data structure that can store data in the form of key-value pairs. The values in a Python dictionary can be accessed using the keys. In this article, we will be discussing the Python dictionary in detail.

### Creating a Dictionary

To create a Python dictionary, we need to pass a sequence of items inside curly braces  `{}`, and separate them using a comma (,). Each item has a key and a value expressed as a "key:value" pair.

The values can belong to any data type and they can repeat, but the keys must remain unique.

The following examples demonstrate how to create Python dictionaries:

**Creating an empty dictionary:**

```python
dict_sample = {}
```

**Creating a dictionary with integer keys:**

```python
dict_sample = {1: 'mango', 2: 'pawpaw'}
```

**Creating a dictionary with mixed keys:**

```python
dict_sample = {'fruit': 'mango', 1: [4, 6, 8]}
```

We can also create a dictionary by explicitly calling the Python's  `dict()`  method:

```python
dict_sample = dict({1:'mango', 2:'pawpaw'})
```

A dictionary can also be created from a sequence as shown below:

```python
dict_sample = dict([(1,'mango'), (2,'pawpaw')])
```

Dictionaries can also be nested, which means that we can create a dictionary inside another dictionary. For example:

```python
dict_sample = {1: {'student1' : 'Nicholas', 'student2' : 'John', 'student3' : 'Mercy'},
        2: {'course1' : 'Computer Science', 'course2' : 'Mathematics', 'course3' : 'Accounting'}}
```

To print the dictionary contents, we can use the Python's  `print()`  function and pass the dictionary name as the argument to the function. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
print(dict_sample)
```

**Output:**

```
{'Company': 'Toyota', 'model': 'Premio', 'year': 2012}
```

### Accessing Elements

To access dictionary items, pass the key inside square brackets  `[]`. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
x = dict_sample["model"]
print(x)
```

**Output:**

```
Premio
```

We created a dictionary named  `dict_sample`. A variable named  `x`  was then created and its value is set to be the value for the key "model" in the dictionary.

Here is another example:

```python
dict = {'Name': 'Mercy', 'Age': 23, 'Course': 'Accounting'}
print("Student Name:", dict['Name'])
print("Course:", dict['Course'])
print("Age:", dict['Age'])
```

**Output:**

```
Student Name: Mercy
Course: Accounting
Age: 23
```

The dictionary object also provides the  `get()`  function, which can be used to access dictionary elements as well. We append the function with the dictionary name using the dot operator and then pass the name of the key as the argument to the function. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
x = dict_sample.get("model")
print(x)
```

**Output:**

```
Premio
```

Now we know how to access dictionary elements using a few different methods. In the next section we'll discuss how to add new elements to an already existing dictionary.

### Adding Elements

There are numerous ways to add new elements to a dictionary. We can use a new index key and assign a value to it. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
dict_sample["Capacity"] = "1800CC"
print(dict_sample)
```

**Output:**

```
{'Capacity': '1800CC', 'year': 2012, 'Company': 'Toyota', 'model': 'Premio'}
```

The new element has "Capacity" as the key and "1800CC" as its corresponding value. It has been added as the first element of the dictionary.

Here is another example. First let's first create an empty dictionary:

```python
MyDictionary = {}
print("An Empty Dictionary: ")
print(MyDictionary)
```

**Output:**

```
An Empty Dictionary:
```

The dictionary returns nothing as it has nothing stored yet. Let us add some elements to it, one at a time:

```python
MyDictionary[0] = 'Apples'
MyDictionary[2] = 'Mangoes'
MyDictionary[3] = 20
print("\n3 elements have been added: ")
print(MyDictionary)
```

**Output:**

```
3 elements have been added:
{0: 'Apples', 2: 'Mangoes', 3: 20}
```

To add the elements, we specified keys as well as the corresponding values. For example:

```python
MyDictionary[0] = 'Apples'
```

In the above example, 0 is the key while "Apples" is the value.

It is even possible for us to add a set of values to one key. For example:

```python
MyDictionary['Values'] = 1, "Pairs", 4
print("\n3 elements have been added: ")
print(MyDictionary)
```

**Output:**

```
3 elements have been added:
{'Values': (1, 'Pairs', 4)}
```

In the above example, the name of the key is "Values" while everything after the  `=`  sign are the actual values for that key, stored as a  [Set](https://docs.python.org/3/tutorial/datastructures.html#sets).

Other than adding new elements to a dictionary, dictionary elements can also be updated/changed, which we'll go over in the next section.

### Updating Elements

After adding a value to a dictionary we can then modify the existing dictionary element. You use the key of the element to change the corresponding value. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

dict_sample["year"] = 2014

print(dict_sample)
```

**Output:**

```
{'year': 2014, 'model': 'Premio', 'Company': 'Toyota'}
```

In this example you can see that we have updated the value for the key "year" from the old value of 2012 to a new value of 2014.

### Removing Elements

The removal of an element from a dictionary can be done in several ways, which we'll discuss one-by-one in this section:

The  `del`  keyword can be used to remove the element with the specified key. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
del dict_sample["year"]
print(dict_sample)
```

**Output:**

```
{'Company': 'Toyota', 'model': 'Premio'}
```

We called the  `del`  keyword followed by the dictionary name. Inside the square brackets that follow the dictionary name, we passed the key of the element we need to delete from the dictionary, which in this example was "year". The entry for "year" in the dictionary was then deleted.

Another way to delete a key-value pair is to use the  `pop()`  function and pass the key of the entry to be deleted as the argument to the function. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
dict_sample.pop("year")
print(dict_sample)
```

**Output:**

```
{'Company': 'Toyota', 'model': 'Premio'}
```

We invoked the  `pop()`  function by appending it with the dictionary name. Again, in this example the entry for "year" in the dictionary will be deleted.

The  `popitem()`  function removes the last item inserted into the dictionary, without needing to specify the key. Take a look at the following example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
dict_sample.popitem()
print(dict_sample)
```

**Output:**

```
{'Company': 'Toyota', 'model': 'Premio'}
```

The last entry into the dictionary was "year". It has been removed after calling the  `popitem()`  function.

#### Subscribe to our Newsletter

Get occassional tutorials, guides, and reviews in your inbox. No spam ever. Unsubscribe at any time.

Subscribe

But what if you want to delete the entire dictionary? It would be difficult and cumbersome to use one of these methods on every single key. Instead, you can use the  `del`  keyword to delete the entire dictionary. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
del dict_sample
print(dict_sample)
```

**Output:**

```
NameError: name 'dict_sample' is not defined
```

The code returns an error. The reason is that we are trying to access a dictionary which doesn't exist since it has been deleted.

However, your use-case may require you to just remove all dictionary elements and be left with an empty dictionary. This can be achieved by calling the  `clear()`  function on the dictionary:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
dict_sample.clear()
print(dict_sample)
```

**Output:**

```
{}
```

The code returns an empty dictionary since all the dictionary elements have been removed.

### Other Common Methods

**The len() Method**

With this method, you can count the number of elements in a dictionary. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
print(len(dict_sample))
```

**Output:**

```
3
```

There are three entries in the dictionary, hence the method returned 3.

**The copy() Method**

This method returns a copy of the existing dictionary. For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}
x = dict_sample.copy()

print(x)
```

**Output:**

```
{'Company': 'Toyota', 'year': 2012, 'model': 'Premio'}
```

We created a copy of dictionary named  `dict_sample`  and assigned it to the variable  `x`. If  `x`  is printed on the console, you will see that it contains the same elements as those stored by  `dict_sample`  dictionary.

Note that this is useful because modifications made to the copied dictionary won't affect the original one.

**The items() Method**

When called, this method returns an iterable object. The iterable object has key-value pairs for the dictionary, as tuples in a list. This method is primarily used when you want to iterate through a dictionary.

The method is simply called on the dictionary object name as shown below:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

for k, v in dict_sample.items():
  print(k, v)
```

**Output:**

```
('Company', 'Toyota')
('model', 'Premio')
('year', 2012)
```

The object returned by  `items()`  can also be used to show the changes that have been implemented on the dictionary. This is demonstrated below:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

x = dict_sample.items()

print(x)

dict_sample["model"] = "Mark X"

print(x)
```

**Output:**

```
dict_items([('Company', 'Toyota'), ('model', 'Premio'), ('year', 2012)])
dict_items([('Company', 'Toyota'), ('model', 'Mark X'), ('year', 2012)])
```

The output shows that when you change a value in the dictionary, the items object is also updated to reflect this change.

**The fromkeys() Method**

This method returns a dictionary having specified keys and values. It takes the syntax given below:

```python
dictionary.fromkeys(keys, value)
```

The value for required  `keys`  parameter is an iterable and it specifies the keys for the new dictionary. The value for  `value`  parameter is optional and it specifies the default value for all the keys. The default value for this is  `None`.

Suppose we need to create a dictionary of three keys all with the same value. We can do so as follows:

```python
name = ('John', 'Nicholas', 'Mercy')
age = 25

dict_sample = dict.fromkeys(name, age)

print(dict_sample)
```

**Output:**

```
{'John': 25, 'Mercy': 25, 'Nicholas': 25}
```

In the script above, we specified the keys and one value. The  `fromkeys()`  method was able to pick the keys and combine them with this value to create a populated dictionary.

The value for the  `keys`  parameter is mandatory. The following example demonstrates what happens when the value for the  `values`  parameter is not specified:

```python
name = ('John', 'Nicholas', 'Mercy')

dict_sample = dict.fromkeys(name)

print(dict_sample)
```

**Output:**

```
{'John': None, 'Mercy': None, 'Nicholas': None}
```

The default value, which is  `None`, was used.

**The setdefault() Method**

This method is applicable when we need to get the value of the element with the specified key. If the key is not found, it will be inserted into the dictionary alongside the specified value.

The method takes the following syntax:

```python
dictionary.setdefault(keyname, value)
```

In this function the  `keyname`  parameter is required. It represents the keyname of the item you need to return a value from. The  `value`  parameter is optional. If the dictionary already has the key, this parameter won't have any effect. If the key doesn't exist, then the value given in this function will become the value of the key. It has a default value of  `None`.

For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

x = dict_sample.setdefault("color", "Gray")

print(x)
```

**Output**

```
Gray
```

The dictionary doesn't have the key for  `color`. The  `setdefault()`  method has inserted this key and the specified a value, that is, "Gray", has been used as its value.

The following example demonstrates how the method behaves if the value for the key  _does_  exist:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

x = dict_sample.setdefault("model", "Allion")

print(x)
```

**Output:**

```
Premio
```

The value "Allion" has no effect on the dictionary since we already have a value for the key.

**The keys() Method**

This method also returns an iterable object. The object returned is a list of all keys in the dictionary. And just like with the  `items()`  method, the returned object can be used to reflect the changes made to the dictionary.

To use this method, we only call it on the name of the dictionary, as shown below:

```python
dictionary.keys()
```

For example:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

x = dict_sample.keys()

print(x)
```

**Output:**

```
dict_keys(['model', 'Company', 'year'])
```

Often times this method is used to iterate through each key in your dictionary, like so:

```python
dict_sample = {
  "Company": "Toyota",
  "model": "Premio",
  "year": 2012
}

for k in dict_sample.keys():
  print(k)
```

**Output:**

```
Company
model
year
```

### Conclusion

This marks the end of this tutorial on Python dictionaries. These dictionaries store data in "key:value" pairs. The "key" acts as the identifier for the item while "value" is the value of the item. The Python dictionary comes with a variety of functions that can be applied for retrieval or manipulation of data. In this article, we saw how Python dictionary can be created, modified and deleted along with some of the most commonly used dictionary methods.

Ref : [https://stackabuse.com/python-dictionary-tutorial/](https://stackabuse.com/python-dictionary-tutorial/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQyNTQ5MzYwMl19
-->