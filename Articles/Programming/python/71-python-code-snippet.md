
[The Renegade Coder](https://therenegadecoder.com/ "Go to The Renegade Coder.")[Articles](https://therenegadecoder.com/articles/ "Go to Articles.")[Code](https://therenegadecoder.com/category/code/ "Go to the Code category archives.")71 Python Code Snippets for Everyday Problems

# 71 Python Code Snippets for Everyday Problems

POSTED ON  [DECEMBER 27, 2019](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/) BY  [JEREMY GRIFSKI](https://therenegadecoder.com/author/jeremy-grifski/)

![Python Code Snippets for Everyday Problems Feature Image](https://i1.wp.com/therenegadecoder.com/wp-content/uploads/2019/12/python-code-snippets-for-everyday-problems-feature-image.jpeg?fit=800%2C400&ssl=1)

Last Updated on  February 3, 2020

If you’ve been following me for any amount of time, you know that I regularly publish  [Python code snippets for everyday problems](https://therenegadecoder.com/series/how-to-python/). Well, I figured I’d finally aggregate all those responses in one massive article with links to all those resources.

As a heads up, I’m looking to start porting all of the code snippets in this article to Jupyter Notebooks. If you’re interested in that kind of project, head on over to  [the GitHub repo](https://github.com/TheRenegadeCoder/how-to-python-code). I’d appreciate the help!

## Table of Contents

-   [Table of Contents](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#table-of-contents "Table of Contents")
-   [Everyday Problems](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#everyday-problems "Everyday Problems")
    -   [Inverting a Dictionary](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#inverting-a-dictionary "Inverting a Dictionary")
    -   [Summing Elements of Two Lists](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#summing-elements-of-two-lists "Summing Elements of Two Lists")
    -   [Checking if a File Exists](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#checking-if-a-file-exists "Checking if a File Exists")
    -   [Converting Two Lists Into a Dictionary](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#converting-two-lists-into-a-dictionary "Converting Two Lists Into a Dictionary")
    -   [Checking if a List Is Empty](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#checking-if-a-list-is-empty "Checking if a List Is Empty")
    -   [Cloning a List](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#cloning-a-list "Cloning a List")
    -   [Retrieving the Last Item of a List](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#retrieving-the-last-item-of-a-list "Retrieving the Last Item of a List")
    -   [Making a Python Script Shortcut](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#making-a-python-script-shortcut "Making a Python Script Shortcut")
    -   [Sorting a List of Strings](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#sorting-a-list-of-strings "Sorting a List of Strings")
    -   [Parsing a Spreadsheet](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#parsing-a-spreadsheet "Parsing a Spreadsheet")
    -   [Sorting a List of Dictionaries](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#sorting-a-list-of-dictionaries "Sorting a List of Dictionaries")
    -   [Writing a List Comprehension](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#writing-a-list-comprehension "Writing a List Comprehension")
    -   [Merging Two Dictionaries](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#merging-two-dictionaries "Merging Two Dictionaries")
    -   [Formatting a String](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#formatting-a-string "Formatting a String")
    -   [Printing on the Same Line](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#printing-on-the-same-line "Printing on the Same Line")
    -   [Testing Performance](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#testing-performance "Testing Performance")
-   [Share Your Own Problems](https://therenegadecoder.com/code/python-code-snippets-for-everyday-problems/?fbclid=IwAR0DnaOnDMrQ1BDghl4ozvvhmm6ceu0xVmwHyPTKQTT8_YzS7Zn67C9G9Hs#share-your-own-problems "Share Your Own Problems")

## Everyday Problems

In this section, we’ll take a look at various common scenarios that arise and how to solve them with Python code. Specifically, I’ll share a brief explanation of the problem with a list of Python code solutions. Then, I’ll link all the resources I have.

### Inverting a Dictionary

Sometimes when we have a dictionary, we want to be able to flip its keys and values. Of course, there are concerns like “how do we deal with duplicate values?” and “what if the values aren’t hashable?” That said, in the simple case, there are a few solutions:

1.  # Use to invert dictionaries that have unique values
2.  my_inverted_dict = dict(map(reversed, my_dict.items()))

4.  # Use to invert dictionaries that have unique values
5.  my_inverted_dict = {value: key for key, value in my_dict.items()}

7.  # Use to invert dictionaries that have non-unique values
8.  from collections import defaultdict
9.  my_inverted_dict = defaultdict(list)
10.  {my_inverted_dict[v].append(k)  for k, v in my_dict.items()}

12.  # Use to invert dictionaries that have non-unique values
13.  my_inverted_dict = dict()
14.  for key, value in my_dict.items():
15.  my_inverted_dict.setdefault(value, list()).append(key)

17.  # Use to invert dictionaries that have lists of values
18.  my_dict = {value: key for key in my_inverted_dict for value in my_map[key]}

For more explanation, check out my article titled “[How to Invert a Dictionary in Python](https://therenegadecoder.com/code/how-to-invert-a-dictionary-in-python/).” It includes a breakdown of each solution, their performance metrics, and when they’re applicable. Likewise,  [I have a YouTube video](https://youtu.be/lN5qX73H2Bc)  which covers the same topic.

### Summing Elements of Two Lists

Let’s say you have two lists, and you want to merge them together into a single list by element. In other words, you want to add the first element of the first list to the first element of the second list and store the result in a new list. Well, there are several ways to do that:

1.  ethernet_devices = [1, [7], [2], [8374163], [84302738]]
2.  usb_devices = [1, [7], [1], [2314567], [0]]

4.  # The long way
5.  all_devices = [
6.  ethernet_devices[0] + usb_devices[0],
7.  ethernet_devices[1] + usb_devices[1],
8.  ethernet_devices[2] + usb_devices[2],
9.  ethernet_devices[3] + usb_devices[3],
10.  ethernet_devices[4] + usb_devices[4]
11.  ]

13.  # Some comprehension magic
14.  all_devices = [x + y for x, y in  zip(ethernet_devices, usb_devices)]

16.  # Let's use maps
17.  import operator
18.  all_devices = list(map(operator.add, ethernet_devices, usb_devices))

20.  # We can't forget our favorite computation library
21.  import numpy as np
22.  all_devices = np.add(ethernet_devices, usb_devices)

If you’d like a deeper explanation, check out my article titled “[How to Sum Elements of Two Lists in Python](https://therenegadecoder.com/code/how-to-sum-elements-of-two-lists-in-python/)” which even includes a fun challenge. Likewise, you might get some value out of  [my YouTube video on the same topic](https://youtu.be/-ueWDzP88eQ).

### Checking if a File Exists

One of the amazing perks of Python is how easy it is to manage files. Unlike Java, Python has a built-in syntax for file reading and writing. As a result, checking if a file exists is a rather brief task:

1.  # Brute force with a try-except block (Python 3+)
2.  try:
3.  with  open('/path/to/file', 'r')  as fh:
4.  pass
5.  except  FileNotFoundError:
6.  pass

8.  # Leverage the OS package (possible race condition)
9.  import os
10.  exists = os.path.isfile('/path/to/file')

12.  # Wrap the path in an object for enhanced functionality
13.  from pathlib import  Path
14.  config = Path('/path/to/file')
15.  if config.is_file():
16.  pass

As always, you can learn more about these solutions in my article titled “[How to Check if a File Exists in Python](https://therenegadecoder.com/code/how-to-check-if-a-file-exists-in-python/)” which features three solutions and performances metrics.

### Converting Two Lists Into a Dictionary

Previously, we talked about summing two lists in Python. As it turns out, there’s a lot we can do with two lists. For example, we could try mapping one onto the other to create a dictionary.

As with many of these problems, there are a few concerns. For instance, what if the two lists aren’t the same size? Likewise, what if the keys aren’t unique or hashable? That said, in the simple case, there are some straightforward solutions:

1.  column_names = ['id', 'color', 'style']
2.  column_values = [1, 'red', 'bold']

4.  # Convert two lists into a dictionary with zip and the dict constructor
5.  name_to_value_dict = dict(zip(column_names, column_values))

7.  # Convert two lists into a dictionary with a dictionary comprehension
8.  name_to_value_dict = {key:value  for key, value in  zip(column_names, column_values)}

10.  # Convert two lists into a dictionary with a loop
11.  name_value_tuples = zip(column_names, column_values)
12.  name_to_value_dict = {}
13.  for key, value in name_value_tuples:
14.  if key in name_to_value_dict:
15.  pass  # Insert logic for handling duplicate keys
16.  else:
17.  name_to_value_dict[key] = value

Once again, you can find an explanation for each of these solutions and more in my article titled “[How to Convert Two Lists Into a Dictionary in Python](https://therenegadecoder.com/code/how-to-convert-two-lists-into-a-dictionary-in-python/).” If you are a visual person, you might prefer  [my YouTube video which covers mapping lists to dictionaries](https://youtu.be/SPmFkdfD_Ho)  as well.

### Checking if a List Is Empty

If you come from a statically typed language like Java or C, you might be bothered by the lack of static types in Python. Sure, not knowing the type of a variable can sometimes be frustrating, but there are perks as well. For instance, we can check if a list is empty by its type flexibility—among other methods:

1.  my_list = list()

3.  # Check if a list is empty by its length
4.  if  len(my_list) == 0:
5.  pass  # the list is empty

7.  # Check if a list is empty by direct comparison (only works for lists)
8.  if my_list == []:
9.  pass  # the list is empty

11.  # Check if a list is empty by its type flexibility **preferred method**
12.  if  not my_list:
13.  pass  # the list is empty

If you’d like to learn more about these three solutions, check out my article titled “[How to Check if a List in Empty in Python](https://therenegadecoder.com/code/how-to-check-if-a-list-is-empty-in-python/).” If you’re in a pinch, check out  [my YouTube video which covers the same topic](https://youtu.be/k1lE5QxNAM4).

### Cloning a List

One of my favorite subjects in programming is copying data types. After all, it’s never easy in this reference-based world we live, and that’s true for Python as well. Luckily, if we want to copy a list, there are a few ways to do it:

1.  my_list = [27, 13, -11, 60, 39, 15]

3.  # Clone a list by brute force
4.  my_duplicate_list = [item for item in my_list]

6.  # Clone a list with a slice
7.  my_duplicate_list = my_list[:]

9.  # Clone a list with the list constructor
10.  my_duplicate_list = list(my_list)

12.  # Clone a list with the copy function (Python 3.3+)
13.  my_duplicate_list = my_list.copy()  # preferred method

15.  # Clone a list with the copy package
16.  import copy
17.  my_duplicate_list = copy.copy(my_list)
18.  my_deep_duplicate_list = copy.deepcopy(my_list)

20.  # Clone a list with multiplication?
21.  my_duplicate_list = my_list * 1  # do not do this

When it comes to cloning, it’s important to be aware of the difference between shallow and deep copies. Luckily,  [I have an article covering that topic](https://therenegadecoder.com/code/be-careful-when-copying-mutable-data-types/).

Finally, you can find out more about the solutions listed above in my article titled “[How to Clone a List in Python](https://therenegadecoder.com/code/how-to-clone-a-list-in-python/).” In addition, you might find value in my related YouTube video titled “[7 Ways to Copy a List in Python Featuring The Pittsburgh Penguins](https://youtu.be/ZMCte_LHml0).”

### Retrieving the Last Item of a List

Since we’re on the topic of lists, lets talk about getting the last item of a list. In most languages, this involves some convoluted mathematical expression involving the length of the list. What if I told you there is are several more interesting solutions in Python?

1.  my_list = ['red', 'blue', 'green']

3.  # Get the last item with brute force using len
4.  last_item = my_list[len(my_list) - 1]

6.  # Remove the last item from the list using pop
7.  last_item = my_list.pop()

9.  # Get the last item using negative indices *preferred & quickest method*
10.  last_item = my_list[-1]

12.  # Get the last item using iterable unpacking
13.  *_, last_item = my_list

As always, you can learn more about these solutions from my article titled “[How to Get the Last Item of a List in Python](https://therenegadecoder.com/code/how-to-get-the-last-item-of-a-list-in-python/)” which features a challenge, performance metrics, and  [a YouTube video](https://youtu.be/wAJ1Nlk-T7w).

### Making a Python Script Shortcut

Sometimes when you create a script, you want to be able to run it conveniently at the click of a button. Fortunately, there are several ways to do that.

First, we can create a Windows shortcut with the following settings:

1.  \path\to\trc-image-titler.py -o \path\to\output

Likewise, we can also create a batch file with the following code:

1.  @echo off
2.  \path\to\trc-image-titler.py -o \path\to\output

Finally, we can create a bash script with the following code:

1.  #!/bin/sh
2.  python /path/to/trc-image-titler.py -o /path/to/output

If you’re looking for more explanation, check out the article titled “[How to Make a Python Script Shortcut with Arguments](https://therenegadecoder.com/code/how-to-make-a-python-script-shortcut-with-arguments/).”

### Sorting a List of Strings

Sorting is a common task that you’re expected to know how to implement in Computer Science. Despite the intense focus on sorting algorithms in most curriculum, no one really tells you how complicated sorting can actually get. For instance, sorting numbers is straightforward, but what about sorting strings? How do we decide a proper ordering? Fortunately, there are a lot of options in Python:

1.  my_list = ["leaf", "cherry", "fish"]

3.  # Brute force method using bubble sort
4.  my_list = ["leaf", "cherry", "fish"]
5.  size = len(my_list)
6.  for i in  range(size):
7.  for j in  range(size):
8.  if my_list[i] < my_list[j]:
9.  temp = my_list[i]
10.  my_list[i] = my_list[j]
11.  my_list[j] = temp

13.  # Generic list sort *fastest*
14.  my_list.sort()

16.  # Casefold list sort
17.  my_list.sort(key=str.casefold)

19.  # Generic list sorted
20.  my_list = sorted(my_list)

22.  # Custom list sort using casefold (>= Python 3.3)
23.  my_list = sorted(my_list, key=str.casefold)

25.  # Custom list sort using current locale
26.  import locale
27.  from functools import cmp_to_key
28.  my_list = sorted(my_list, key=cmp_to_key(locale.strcoll))

30.  # Custom reverse list sort using casefold (>= Python 3.3)
31.  my_list = sorted(my_list, key=str.casefold, reverse=True)

If you’re curious about how some of these solutions work, or you just want to know what some of the potential risks are, check out my article titled “[How to Sort a List of Strings in Python](https://therenegadecoder.com/code/how-to-sort-a-list-of-strings-in-python/).”

### Parsing a Spreadsheet

One of the more interesting use cases for Python is data science. Unfortunately, however, that means handling a lot of raw data in various formats like text files and spreadsheets. Luckily, Python has plenty of built-in utilities for reading different file formats. For example, we can parse a spreadsheet with ease:

1.  # Brute force solution
2.  csv_mapping_list = []
3.  with  open("/path/to/data.csv")  as my_data:
4.  line_count = 0
5.  for line in my_data:
6.  row_list = [val.strip()  for val in line.split(",")]
7.  if line_count == 0:
8.  header = row_list
9.  else:
10.  row_dict = {key: value for key, value in  zip(header, row_list)}
11.  csv_mapping_list.append(row_dict)
12.  line_count += 1

14.  # CSV reader solution
15.  import csv
16.  csv_mapping_list = []
17.  with  open("/path/to/data.csv")  as my_data:
18.  csv_reader = csv.reader(my_data, delimiter=",")
19.  line_count = 0
20.  for line in csv_reader:
21.  if line_count == 0:
22.  header = line
23.  else:
24.  row_dict = {key: value for key, value in  zip(header, line)}
25.  csv_mapping_list.append(row_dict)
26.  line_count += 1

28.  # CSV DictReader solution
29.  import csv
30.  with  open("/path/to/dict.csv")  as my_data:
31.  csv_mapping_list = list(csv.DictReader(my_data))

In this case, we try to get our output in a list of dictionaries. If you want to know more about how this works, check out the complete article titled “[How to Parse a Spreadsheet in Python](https://therenegadecoder.com/code/how-to-parse-a-spreadsheet-in-python/).”

### Sorting a List of Dictionaries

Once you have a list of dictionaries, you might want to organize them in some specific order. For example, if the dictionaries have a key for date, we can try sorting them in chronological order. Luckily, sorting is another relatively painless task:

1.  csv_mapping_list = [
2.  {
3.  "Name": "Jeremy",
4.  "Age": 25,
5.  "Favorite Color": "Blue"
6.  },
7.  {
8.  "Name": "Ally",
9.  "Age": 41,
10.  "Favorite Color": "Magenta"
11.  },
12.  {
13.  "Name": "Jasmine",
14.  "Age": 29,
15.  "Favorite Color": "Aqua"
16.  }
17.  ]

19.  # Custom sorting
20.  size = len(csv_mapping_list)
21.  for i in  range(size):
22.  min_index = i
23.  for j in  range(i + 1, size):
24.  if csv_mapping_list[min_index]["Age"] > csv_mapping_list[j]["Age"]:
25.  min_index = j
26.  csv_mapping_list[i], csv_mapping_list[min_index] = csv_mapping_list[min_index], csv_mapping_list[i]

28.  # List sorting function
29.  csv_mapping_list.sort(key=lambda item: item.get("Age"))

31.  # List sorting using itemgetter
32.  from operator import itemgetter
33.  f = itemgetter('Name')
34.  csv_mapping_list.sort(key=f)

36.  # Iterable sorted function
37.  csv_mapping_list = sorted(csv_mapping_list, key=lambda item: item.get("Age"))

All these solutions and more outlined in my article titled “[How to Sort a List of Dictionaries in Python](https://therenegadecoder.com/code/how-to-sort-a-list-of-dictionaries-in-python/).”

### Writing a List Comprehension

One of my favorite Python topics to chat about is list comprehensions. As someone who grew up on languages like Java, C/C++, and C#, I had never seen anything quite like a list comprehension until I played with Python. Now, I’m positively obsessed with them. As a result, I put together an entire list of examples:

1.  # Define a generic 1D list of constants
2.  my_list = [2, 5, -4, 6]

4.  # Duplicate a 1D list of constants
5.  [item for item in my_list]

7.  # Duplicate and scale a 1D list of constants
8.  [2 * item for item in my_list]

10.  # Duplicate and filter out non-negatives from 1D list of constants
11.  [item for item in my_list if item < 0]

13.  # Duplicate, filter, and scale a 1D list of constants
14.  [2 * item for item in my_list if item < 0]

16.  # Generate all possible pairs from two lists
17.  [(a, b)  for a in  (1, 3, 5)  for b in  (2, 4, 6)]

19.  # Redefine list of contents to be 2D
20.  my_list = [[1, 2], [3, 4]]

22.  # Duplicate a 2D list
23.  [[item for item in sub_list]  for sub_list in my_list]

25.  # Duplicate an n-dimensional list
26.  def deep_copy(to_copy):
27.  if  type(to_copy)  is  list:
28.  return  [deep_copy(item)  for item in to_copy]
29.  else:
30.  return to_copy

As always, you can find a more formal explanation of all this code in my article titled “[How to Write a List Comprehension in Python](https://therenegadecoder.com/code/how-to-write-a-list-comprehension-in-python/).” As an added bonus, I have  [a YouTube video which shares several examples of list comprehensions](https://youtu.be/AEG8D4h7kls).

### Merging Two Dictionaries

In this collection, we talk a lot about handling data structures like lists and dictionaries. Well, this one is no different. In particular, we’re looking at merging two dictionaries. Of course, combining two dictionaries comes with risks. For example, what if there are duplicate keys? Luckily, we have solutions for that:

1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}
3.  powers = dict()

5.  # Brute force
6.  for dictionary in  (yusuke_power, hiei_power):
7.  for key, value in dictionary.items():
8.  powers[key] = value

10.  # Dictionary Comprehension
11.  powers = {key: value for d in  (yusuke_power, hiei_power)  for key, value in d.items()}

13.  # Copy and update
14.  powers = yusuke_power.copy()
15.  powers.update(hiei_power)

17.  # Dictionary unpacking (Python 3.5+)
18.  powers = {**yusuke_power, **hiei_power}

20.  # Backwards compatible function for any number of dicts
21.  def merge_dicts(*dicts: dict):
22.  merged_dict = dict()
23.  for dictionary in dicts:
24.  merge_dict.update(dictionary)
25.  return merged_dict

If you’re interested, I have an article which covers this exact topic called “[How to Merge Two Dictionaries in Python](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/)” which features four solutions as well performance metrics.

### Formatting a String

Whether we like to admit it or not, we often find ourselves burying print statements throughout our code for quick debugging purposes. After all, a well placed print statement can save you a lot of time. Unfortunately, it’s not always easy or convenient to actually display what we want. Luckily, Python has a lot of formatting options:

1.  name = "Jeremy"
2.  age = 25

4.  # String formatting using concatenation
5.  print("My name is " + name + ", and I am " + str(age) + " years old.")

7.  # String formatting using multiple prints
8.  print("My name is ", end="")
9.  print(name, end="")
10.  print(", and I am ", end="")
11.  print(age, end="")
12.  print(" years old.")

14.  # String formatting using join
15.  print(''.join(["My name is ", name, ", and I am ", str(age), " years old"]))

17.  # String formatting using modulus operator
18.  print("My name is %s, and I am %d years old."  % (name, age))

20.  # String formatting using format function with ordered parameters
21.  print("My name is {}, and I am {} years old".format(name, age))

23.  # String formatting using format function with named parameters
24.  print("My name is {n}, and I am {a} years old".format(a=age, n=name))

26.  # String formatting using f-Strings (Python 3.6+)
27.  print(f"My name is {name}, and I am {age} years old")

Keep in mind that these solutions don’t have to be used with print statements. In other words, feel free to use solutions like f-strings wherever you need them.

As always, you can find an explanation of all these solutions and more in my article titled “[How to Format a String in Python](https://therenegadecoder.com/code/how-to-format-a-string-in-python/).” If you’d rather see these snippets in action, check out my YouTube video titled “[6 Ways to Format a String in Python Featuring My Cat](https://youtu.be/qZMYur8VRlU).”

### Printing on the Same Line

Along a similar line as formatting strings, sometimes you just need to print on the same line in Python. As the  `print`  command is currently designed, it automatically applies a newline to the end of your string. Luckily, there are a few ways around that:

1.  # Python 2 only
2.  print  "Live PD",

4.  # Backwards compatible (also fastest)
5.  import sys
6.  sys.stdout.write("Breaking Bad")

8.  # Python 3 only
9.  print("Mob Psycho 100", end="")

As always, if you plan to use any of these solutions, check out the article titled “[How to Print on the Same Line in Python](https://therenegadecoder.com/code/how-to-print-on-the-same-line-in-python/)” for additional use cases and caveats.

### Testing Performance

Finally, sometimes you just want to compare a couple chunks of code. Luckily, Python has a few straightforward options:

1.  # Brute force solution
2.  import datetime
3.  start_time = datetime.datetime.now()
4.  [(a, b)  for a in  (1, 3, 5)  for b in  (2, 4, 6)]  # example snippet
5.  end_time = datetime.datetime.now()
6.  print end_time - start_time

8.  # timeit solution
9.  import timeit
10.  min(timeit.repeat("[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)]"))

12.  # cProfile solution
13.  import cProfile
14.  cProfile.run("[(a, b) for a in (1, 3, 5) for b in (2, 4, 6)]")

Again, if you want more details, check the article titled “[How to Performance Test Python Code](https://therenegadecoder.com/code/how-to-performance-test-python-code/).”

## Share Your Own Problems

As you can see, this article and its associated series is already quite large. That said, I’d love to continue growing them. As a result, you should consider sharing some of your own problems. After all, there has be something you Google regularly. Why not share it with us?

In the meantime, help grow this collection by  [hopping on my newsletter](https://newsletter.therenegadecoder.com/),  [visiting the shop](https://therenegadecoder.com/shop/),  [subscribing to my YouTube channel](https://www.youtube.com/channel/UCpyoVwOqYRlSAEUPEn7P9hw), and/or  [becoming a patron](https://www.patreon.com/TheRenegadeCoder). In addition, you’re welcome to browse the following related articles:

-   [The Controversy Behind the Walrus Operator in Python](https://therenegadecoder.com/code/the-controversy-behind-the-walrus-operator-in-python/)
-   [Rock Paper Scissors Using Modular Arithmetic](https://therenegadecoder.com/code/rock-paper-scissors-using-modular-arithmetic/)

Otherwise, thanks for stopping by! I appreciate the support.

> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4NjA4OTMyNl19
-->