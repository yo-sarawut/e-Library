
# Python Dictionary(Dict): Update, Cmp, Len, Sort, Copy, Items, str Example

Dictionaries are another example of a data structure. A dictionary is used to map or associate things you want to store the keys you need to get them. A dictionary in Python is just like a dictionary in the real world. Python Dictionary are defined into two elements Keys and Values.

-   Keys will be a single element
-   Values can be a list or list within a list, numbers, etc.

In this tutorial, we are going to learn,

-   [Python Dictionary Methods](https://www.guru99.com/python-dictionary-beginners-tutorial.html#1)
-   [Copying dictionary](https://www.guru99.com/python-dictionary-beginners-tutorial.html#2)
-   [Updating Dictionary](https://www.guru99.com/python-dictionary-beginners-tutorial.html#3)
-   [Delete Keys from the dictionary](https://www.guru99.com/python-dictionary-beginners-tutorial.html#4)
-   [Dictionary items() Method](https://www.guru99.com/python-dictionary-beginners-tutorial.html#5)
-   [Sorting the Dictionary](https://www.guru99.com/python-dictionary-beginners-tutorial.html#6)
-   [Python Dictionary in-built Functions](https://www.guru99.com/python-dictionary-beginners-tutorial.html#7)
-   [Dictionary len() Method](https://www.guru99.com/python-dictionary-beginners-tutorial.html#8)
-   [Variable Types](https://www.guru99.com/python-dictionary-beginners-tutorial.html#9)
-   [Python List cmp() Method](https://www.guru99.com/python-dictionary-beginners-tutorial.html#10)
-   [Dictionary Str(dict)](https://www.guru99.com/python-dictionary-beginners-tutorial.html#11)

**Syntax for Python Dictionary**:
```py
  Dict = { ' Tim': 18,  xyz,.. }
```
Dictionary is listed in curly brackets, inside these curly brackets, keys and values are declared. Each key is separated from its value by a colon (:) while each element is separated by commas.

**Properties of Dictionary Keys**

There are two important points while using dictionary keys

-   More than one entry per key is not allowed ( no duplicate key is allowed)
-   The values in the dictionary can be of any type while the keys must be immutable like numbers, tuples or strings.
-   Dictionary keys are case sensitive- Same key name but with the different case are treated as different keys in Python dictionaries.

**Python 2 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print (Dict['Tiffany'])
```
**Python 3 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print((Dict['Tiffany']))
```
-   In code, we have dictionary name "Dict"
-   We declared the name and age of the person in the dictionary, where name is "Keys" and age is the"value"
-   Now run the code
-   It retrieves the age of tiffany from the dictionary.

## Python Dictionary Methods

### Copying dictionary

You can also copy the entire dictionary to new dictionary. For example, here we have copied our original dictionary to new dictionary name "Boys" and "Girls".

**Python 2 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}	
studentX=Boys.copy()
studentY=Girls.copy()
print studentX
print studentY
```
**Python 3 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}	
studentX=Boys.copy()
studentY=Girls.copy()
print(studentX)
print(studentY)
```
-   We have the original dictionary (Dict) with the name and age of the boys and girls together
-   But we want boys list separate from girls list, so we defined the element of boys and girls in a separate dictionary name "Boys" and "Girls."
-   Now again we have created new dictionary name "studentX" and "studentY", where all the keys and values of boy dictionary are copied into studentX, and the girls will be copied in studentY
-   So now you don't have to look into the whole list in main dictionary( Dict) to check who is boy and who is girl, you just have to print studentX if you want boys list and StudentY if you want girls list
-   So, when you run the studentX and studentY dictionary, it will give all the element present in the dictionary of "boys" and "girls" separately

### Updating Dictionary

You can also update a dictionary by adding a new entry or a key-value pair to an existing entry or by deleting an existing entry. Here in the example we will add another name "Sarah" to our existing dictionary.

**Python 2 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
Dict.update({"Sarah":9})
print Dict
```
**Python 3 Example**
```py
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
Dict.update({"Sarah":9})
print(Dict)
```
-   Our existing dictionary "Dict" does not have the name "Sarah."
-   We use the method Dict.update to add Sarah to our existing dictionary
-   Now run the code, it adds Sarah to our existing dictionary

### Delete Keys from the dictionary

Python dictionary gives you the liberty to delete any element from the dictionary list. Suppose you don't want the name Charlie in the list, so you can delete the key element by following code.

**Python 2 Example**
```p
Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
del Dict ['Charlie']
print Dict

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
del Dict ['Charlie']
print(Dict)

When you run this code, it should print the dictionary list without Charlie.

-   We used the code del Dict
-   When code executed, it has deleted the Charlie from the main dictionary

### Dictionary items() Method

The items() method returns a list of tuple pairs (Keys, Value) in the dictionary.

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print "Students Name: %s" % Dict.items()

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print("Students Name: %s" % list(Dict.items()))

-   We use the code items() method for our Dict.
-   When code was executed, it returns a list of items ( keys and values) from the dictionary

**Check if a given key already exists in a dictionary**

For a given list, you can also check whether our child dictionary exists in a main dictionary or not. Here we have two sub-dictionaries "Boys" and "Girls", now we want to check whether our dictionary Boys exist in our main "Dict" or not. For that, we use the forloop method with else if method.

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}
for key in Dict.keys():
    if key in Boys.keys():
        print True
    else:       
        print False

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}
for key in list(Dict.keys()):
    if key in list(Boys.keys()):
        print(True)
    else:       
        print(False)

-   The forloop in code checks each key in the main dictionary for Boys keys
-   If it exists in the main dictionary, it should print true or else it should print false
-   When you execute the code, it will print "True" for three times, as we got three elements in our "Boys" dictionary
-   So it indicates that the "Boys" exist in our main dictionary (Dict)

### Sorting the Dictionary

In the dictionary, you can also sort the elements. For example, if we want to print the name of the elements of our dictionary alphabetically we have to use the forloop. It will sort each element of dictionary accordingly.

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}
Students = Dict.keys()
Students.sort()
for S in Students:
      print":".join((S,str(Dict[S])))

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}
Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}
Students = list(Dict.keys())
Students.sort()
for S in Students:
      print(":".join((S,str(Dict[S]))))

-   We declared the variable students for our dictionary "Dict."
-   Then we use the code Students.sort, which will sort the element inside our dictionary
-   But to sort each element in dictionary, we run the forloop by declaring variable S
-   Now, when we execute the code the forloop will call each element from the dictionary, and it will print the string and value in an order

## Python Dictionary in-built Functions

### Dictionary len() Method

The len() function gives the number of pairs in the dictionary.

For example,

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print "Length : %d" % len (Dict)

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print("Length : %d" % len (Dict))

When len (Dict) function is executed it gives the output at "4" as there are four elements in our dictionary

### Variable Types

Python does not require to explicitly declare the reserve memory space; it happens automatically. The assign values to variable "=" equal sign are used. The code to determine the variable type is " %type (Dict)."

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print "variable Type: %s" %type (Dict)

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print("variable Type: %s" %type (Dict))

-   Use the code %type to know the variable type
-   When code was executed, it tells a variable type is a dictionary

### Python List cmp() Method

The compare method cmp() is used in Python to compare values and keys of two dictionaries. If method returns 0 if both dictionaries are equal, 1 if dic1 > dict2 and -1 if dict1 < dict2.

**Python 2 Example**

Boys = {'Tim': 18,'Charlie':12,'Robert':25}
Girls = {'Tiffany':22}	
print cmp(Girls, Boys)

**Python 3 Example**

cmp is not supported in Python 3

-   We have two dictionary name "Boys" and "Girls."
-   Which ever you declare first in code "cmp(Girls, Boys)" will be considered as dictionary 1. In our case, we declared "Girls" first, so it will be considered as dictionary 1 and boys as dictionary 2
-   When code is executed it prints out -1, It indicates that our dictionary 1 is less than dictionary 2.

### Dictionary Str(dict)

With Str() method, you can make a dictionary into a printable string format.

**Python 2 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print "printable string:%s" % str (Dict)

**Python 3 Example**

Dict = {'Tim': 18,'Charlie':12,'Tiffany':22,'Robert':25}	
print("printable string:%s" % str (Dict))

-   Use the code % str (Dict)
-   It will return the dictionary elements into a printable string format

**Here is the list of all Dictionary Methods**

Method

Description

Syntax

copy()

Copy the entire dictionary to new dictionary

dict.copy()

update()

Update a dictionary by adding a new entry or a key-value pair to an  
existing entry or by deleting an existing entry.

Dict.update([other])

items()

Returns a list of tuple pairs (Keys, Value) in the dictionary.

dictionary.items()

sort()

You can sort the elements

dictionary.sort()

len()

Gives the number of pairs in the dictionary.

len(dict)

cmp()

Compare values and keys of two dictionaries

cmp(dict1, dict2)

Str()

Make a dictionary into a printable string format

Str(dict)

### Summary:

Dictionaries in a programming language is a type of data-structure used to store information connected in someway. Python Dictionary are defined into two elements Keys and Values. Dictionaries do not store their information in any particular order, so you may not get your information back in the same order you entered it.

-   Keys will be a single element
-   Values can be a list or list within a list, numbers, etc.
-   More than one entry per key is not allowed ( no duplicate key is allowed)
-   The values in the dictionary can be of any type while the keys must be immutable like numbers, tuples or strings.
-   Dictionary keys are case sensitive- Same key name but with the different case are treated as different keys in Python dictionaries.

> [Source : ](https://www.guru99.com/python-dictionary-beginners-tutorial.html).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQyNjYxNTczOV19
-->