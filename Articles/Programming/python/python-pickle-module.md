Introduction to the Python Pickle Module
===

### Introduction

**Pickling**  is a popular method of preserving food. According to  [Wikipedia](https://en.wikipedia.org/wiki/Pickling), it is also a pretty ancient procedure – although the origins of pickling are unknown, the ancient Mesopotamians probably used the process 4400 years ago. By placing a product in a specific solution, it is possible to drastically increase its shelf life. In other words, it's a method that lets us store food for later consumption.

If you're a Python developer, you might one day find yourself in need of a way to store your Python objects for later use. Well, what if I told you, you can pickle Python objects too?

### Serialization

Serialization is a process of transforming objects or data structures into  **byte streams**  or strings. A byte stream is, well, a stream of bytes – one byte is composed of 8 bits of zeros and ones. These byte streams can then be stored or transferred easily. This allows the developers to save, for example, configuration data or user's progress, and then store it (on disk or in a database) or send it to another location.

Python objects can also be serialized using a module called  [Pickle](https://docs.python.org/3/library/pickle.html).

One of the main differences between pickling Python objects and pickling vegetables is the inevitable and irreversible change of the pickled food's flavor and texture. Meanwhile, pickled Python objects can be easily unpickled back to their original form. This process, by the way, is universally known as  **deserialization**.

Pickling (or  **serialization**  in general) should not be confused with compression. The purpose of pickling is to translate data into a format that can be transferred from RAM to disk. Compression, on the other hand, is a process of encoding data using fewer bits (in order to save disk space).

Serialization is especially useful in any software where it's important to be able to save some progress on disk, quit the program and then load the progress back after reopening the program. Video games might be the most intuitive example of serialization's usefulness, but there are many other programs where saving and loading a user's progress or data is crucial.

### Pickle vs JSON

There is a chance that you have heard of  [JSON](https://en.wikipedia.org/wiki/JSON)  (JavaScript Object Notation), which is a popular format that also lets developers save and transmit objects encoded as strings. This method of serialization has some advantages over pickling. JSON format is human-readable, language-independent, and faster than pickle.

It does have, however, some important limitations as well. Most importantly, by default, only a limited subset of Python built-in types can be represented by JSON. With Pickle, we can easily serialize a very large spectrum of Python types, and, importantly, custom classes. This means we don't need to create a custom schema (like we do for JSON) and write error-prone serializers and parsers. All of the heavy liftings is done for you with Pickle.

### What can be Pickled and Unpickled

The following types can be serialized and deserialized using the Pickle module:

-   All native datatypes supported by Python (booleans, None, integers, floats, complex numbers, strings, bytes, byte arrays)
-   Dictionaries, sets, lists, and tuples - as long as they contain pickleable objects
-   Functions and classes that are defined at the top level of a module

It is important to remember that pickling is not a language-independent serialization method, therefore your pickled data can only be unpickled using Python. Moreover, it's  _important to make sure that objects are pickled using the same version of Python that is going to be used to unpickle them_. Mixing Python versions, in this case, can cause many problems.

Additionally, functions are pickled by their name references, and not by their value. The resulting pickle does not contain information on the function's code or attributes. Therefore, you have to make sure that the environment where the function is unpickled is able to import the function. In other words, if we pickle a function and then unpickle it in an environment where it's either not defined or not imported, an exception will be raised.

It is also very important to note that pickled objects can be used in malevolent ways. For instance, unpickling data from an untrusted source can result in the execution of a malicious piece of code.

### Pickling a Python List

The following very simple example shows the basics of using the Pickle module in  [Python 3](https://www.python.org/download/releases/3.0/):

```python
import pickle

test_list = ['cucumber', 'pumpkin', 'carrot']

with open('test_pickle.pkl', 'wb') as pickle_out:
    pickle.dump(test_list, pickle_out)

```

First, we have to import the  `pickle`  module, which is done in line 1. In line 3 we define a simple, three element list that will be pickled.

In line 5 we state that our output pickle file's name will be  `test_pickle.pkl`. By using the  `wb`  option, we tell the program that we want to write (`w`) binary data (`b`) inside of it (because we want to create a byte stream). Note that the  `pkl`  extension is not necessary – we're using it in this tutorial because that's the extension included in Python's documentation.

In line 6 we use the  `pickle.dump()`  method to pickle our test list and store it inside the  `test_pickle.pkl`  file.

#### Subscribe to our Newsletter

Get occassional tutorials, guides, and reviews in your inbox. No spam ever. Unsubscribe at any time.

Subscribe

I encourage you to try and open the generated pickle file in your text editor. You'll quickly notice that a byte stream is definitely not a human-readable format.

### Unpickling a Python List

Now, let's unpickle the contents of the test pickle file and bring our object back to its original form.

```python
import pickle

with open('test_pickle.pkl', 'rb') as pickle_in:
    unpickled_list = pickle.load(pickle_in)

print(unpickled_list)

```

As you can see, this procedure is not more complicated than when we pickled the object. In line 3 we open our  `test_pickle.pkl`  file again, but this time our goal is to read (`r`) the binary data (`b`) stored within it.

Next, in line 5, we use the  `pickle.load()`  method to unpickle our list and store it in the  `unpickled_list`  variable.

You can then print the contents of the list to see for yourself that it is identical to the list we pickled in the previous example. Here is the output from running the code above:

```
$ python unpickle.py
['cucumber', 'pumpkin', 'carrot']

```

### Pickling and Unpickling Custom Objects

As I mentioned before, using Pickle, you can serialize your own custom objects. Take a look at the following example:

```python
import pickle

class Veggy():
    def __init__(self):
        self.color = ''
    def set_color(self, color):
        self.color = color

cucumber = Veggy()
cucumber.set_color('green')

with open('test_pickle.pkl', 'wb') as pickle_out:
    pickle.dump(cucumber, pickle_out)

with open('test_pickle.pkl', 'rb') as pickle_in:
    unpickled_cucumber = pickle.load(pickle_in)

print(unpickled_cucumber.color)

```

As you can see, this example is almost as simple as the previous one. Between the lines 3 and 7 we define a simple class that contains one attribute and one method that changes this attribute. In line 9 we create an instance of that class and store it in the  `cucumber`  variable, and in line 10 we set its attribute  `color`  to "green".

Then, using the exact same functions as in the previous example, we pickle and unpickle our freshly created  `cucumber`  object. Running the code above results in the following output:

```sh
$ python unpickle_custom.py
green

```

Remember, that we can only unpickle the object in an environment where the class  `Veggy`  is either defined or imported. If we create a new script and try to unpickle the object without importing the  `Veggy`  class, we'll get an "AttributeError". For example, execute the following script:

```python
import pickle

with open('test_pickle.pkl', 'rb') as pickle_in:
    unpickled_cucumber = pickle.load(pickle_in)

print(unpickled_cucumber.color)

```

In the output of the script above, you will see the following error:

```sh
$ python unpickle_simple.py
Traceback (most recent call last):
  File "<pyshell#40>", line 2, in <module>
    unpickled_cucumber = pickle.load(pickle_in)
AttributeError: Can't get attribute 'Veggy' on <module '__main__' (built-in)>

```

### Conclusion

As you can see, thanks to the Pickle module, serialization of Python objects is pretty simple. In our examples, we pickled a simple Python list – but you can use the exact same method to save a large spectrum of Python data types, as long as you make sure your objects contain only other pickleable objects.

Pickling has some disadvantages, the biggest of which might be the fact that you can only unpickle your data using Python – if you need a cross-language solution, JSON is definitely a better option. And finally, remember that pickles can be used to carry the code that you don't necessarily want to execute. Similarly to pickled food, as long as you get your pickles from trusted sources, you should be fine.

Reference : [https://stackabuse.com/introduction-to-the-python-pickle-module/](https://stackabuse.com/introduction-to-the-python-pickle-module/)

ศึกษาเพิ่มเติม : [https://python3.wannaphong.com/](https://python3.wannaphong.com/2016/07/pickle-python.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3MDg4NzY5MSwtMTEzMzI1MTY0OV19
-->