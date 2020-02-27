# Dictionary Methods

-   March 26, 2018 • 16 min read
    
-   Key Terms: dictionaries
    

Dictionaries have methods that allow for modification of dictionary structures. I'll cover a few important ones in this tutorial.

**Access dictionary keys**

The `keys()` method outputs a `dict_keys` object that presents a list of a dictionary's keys.

dan =  {'name':  'Dan Friedman',  'location':  'San Francisco',  'profession':  'Data Scientist'}

dan.keys()

dict_keys(['name',  'location',  'profession'])

**Access dictionary values**

The `values()` method outputs a `dict_values` object that presents a list of a dictionary's values.

dan.values()

dict_values(['Dan Friedman',  'San Francisco',  'Data Scientist'])

**Loop over key-value pairs**

The `items()` method outputs a `dict_items` object that's a sequence of tuples in which each tuple is a key-value pair.

dan.items()

dict_items([('name',  'Dan Friedman'),  ('location',  'San Francisco'),  ('profession',  'Data Scientist')])

We can iterate over this `dict_items` object in a `for` loop.

for key, value in dan.items():

 print("A key of {0} corresponds to a value of {1}".format(key, value))

A key of name corresponds to a value of Dan Friedman

A key of location corresponds to a value of San Francisco

A key of profession corresponds to a value of Data Scientist
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY0NjIyMzY1LC0xNDcwMzE5NDg2XX0=
-->