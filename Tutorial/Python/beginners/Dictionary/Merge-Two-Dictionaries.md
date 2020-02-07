---
bookFlatSection: true
title: Merge Two Dictionaries
bookToc: true

---

# How to Merge Two Dictionaries in Python: Dictionary Comprehensions and Unpacking

POSTED ON  [JUNE 7, 2019](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/) BY  [JEREMY GRIFSKI](https://therenegadecoder.com/author/jeremy-grifski/)

![enter image description here](https://i0.wp.com/therenegadecoder.com/wp-content/uploads/2019/05/how-to-merge-two-dictionaries-in-python-featured-image.jpeg?resize=1024,640&ssl=1)


When I’m trying to find a topic for this series, I either decide to write about something I just learned, or I choose to write about something I found from the  [list of top Python questions on Stack Overflow](https://stackoverflow.com/questions/tagged/python?sort=votes&pageSize=50). Today, I’m hitting both by covering how to merge two dictionaries in Python.

## Table of Contents

-   [Table of Contents](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#table-of-contents "Table of Contents")
-   [Problem Introduction](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#problem-introduction "Problem Introduction")
-   [Solutions](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#solutions "Solutions")
    -   [Merge Two Dictionaries with Brute Force](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#merge-two-dictionaries-with-brute-force "Merge Two Dictionaries with Brute Force")
    -   [Merge Two Dictionaries with a Dictionary Comprehension](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#merge-two-dictionaries-with-a-dictionary-comprehension "Merge Two Dictionaries with a Dictionary Comprehension")
    -   [Merge Two Dictionaries with Copy and Update](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#merge-two-dictionaries-with-copy-and-update "Merge Two Dictionaries with Copy and Update")
    -   [Merge Two Dictionaries with Dictionary Unpacking](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#merge-two-dictionaries-with-dictionary-unpacking "Merge Two Dictionaries with Dictionary Unpacking")
-   [Performance](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#performance "Performance")
-   [A Little Recap](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/#a-little-recap "A Little Recap")

## Problem Introduction

Earlier in this series, I covered a similar problem where  [I wanted to convert two lists into a dictionary](https://therenegadecoder.com/code/how-to-convert-two-lists-into-a-dictionary-in-python/). In that article, I covered various methods for mapping one list onto the other. This time around I want to convert two dictionaries into a single dictionary like so:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  # Insert merge code here

6.  powers = {
7.  "Yusuke Urameshi": "Spirit Gun",
8.  "Hiei": "Jagan Eye"
9.  }
```
Here, we have two dictionaries:  `yusuke_power`  and  `hiei_power`. Each dictionary maps  [a YuYu Hakasho character](https://myanimelist.net/anime/392/Yuu%E2%98%86Yuu%E2%98%86Hakusho)  to one of their abilities. In this case, I chose Yusuke and his Spirit Gun as well as Hiei and his Jagan Eye. Ultimately, we want to be able to merge these dictionaries, so we have a collection of characters and their powers. Let’s see if we can accomplish that below.

## Solutions

As always, I like to list off a few possible ways to solve the problem. To start, we’ll try a brute force solution, then we’ll dig into some more sophisticated solutions.

### Merge Two Dictionaries with Brute Force

As is tradition in this series, I always like to kick things off with a roll-your-own solution. In this case, we’re looking to iterate over one dictionary and add its items to the other dictionary:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  for key, value in hiei_power.items():
5.  yusuke_power[key] = value
```
Naturally, this solution leaves a lot to be desired, but it gets the job done. At the end of the day,  `yusuke_power`  should look like the  `powers`  dictionary we want.

To accomplish something closer to what we want, we would have to iterate over both dictionaries separately:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}
3.  powers = dict()

5.  for dictionary in  (yusuke_power, hiei_power):
6.  for key, value in dictionary.items():
7.  powers[key] = value
```
Unfortunately, this solution doesn’t scale very well. That said, there are better ways to solve this problem.

### Merge Two Dictionaries with a Dictionary Comprehension

Since I’m a big fan of comprehensions, I think it’s worth mentioning that the solution above can be written in a single line with a dictionary comprehension:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  powers = {key: value for d in  (yusuke_power, hiei_power)  for key, value in d.items()}
```
Here, we have written a dictionary comprehension that iterates over both dictionaries and copies each item into a new dictionary. Naturally, it works just like the brute force solution.

### Merge Two Dictionaries with Copy and Update

As with many of the collections in Python, they have a builtin copy function associated with them. As a result, we can leverage that copy function to generate a new dictionary which includes all the items of the original dictionary. In addition, dictionaries have an update function which can be used to add all the items from one dictionary into another:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  powers = yusuke_power.copy()
5.  powers.update(hiei_power)
```
With this solution, we’re able to generate that  `powers`  dictionary which contains all the items from the original two dictionaries. As an added benefit,  `copy`  and  `update`  are backwards compatible, so Python 2 users won’t feel left out.

It’s worth noting that we can extend this solution to merge any number of dictionaries with a custom function:
```py
1.  def merge_dicts(*dicts: dict):
2.  merged_dict = dict()
3.  for dictionary in dicts:
4.  merge_dict.update(dictionary)
5.  return merged_dict
```
Now, we can generate a new dictionary which contains all the items in any number of dictionaries.

### Merge Two Dictionaries with Dictionary Unpacking

When Python 3.5 rolled out, it introduced a dictionary unpacking syntax which allows us to merge dictionaries with a new operator:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  powers = {**yusuke_power, **hiei_power}
```
Naturally, this solution scales for any number of arguments:
```py
1.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"}
2.  hiei_power = {"Hiei": "Jagan Eye"}

4.  powers = {**yusuke_power, **hiei_power, "Yoko Kurama": "Rose Whip"}
```
Of course, the drawback is backwards compatibility. If you’re still rocking Python 2 or even older versions of Python 3, this feature may not be available to you. Regardless, I think it’s a pretty clever piece of syntax, and I like how it looks.

## Performance

For the first time in this series, I thought it would be beneficial to take a look at the performance of each of the methods above (if you’re lucky, I might update the old articles to include performance as well). To do that, I’m going to use the builtin  `timeit`  library.

To use the  `timeit`  library, we have to set up some strings for testing:
```py
1.  setup = """\
2.  yusuke_power = {"Yusuke Urameshi": "Spirit Gun"};
3.  hiei_power = {"Hiei": "Jagan Eye"};
4.  powers = dict()
5.  """

7.  brute_force = """\
8.  for dictionary in (yusuke_power, hiei_power):
9.  for key, value in dictionary.items():
10.  powers[key] = value
11.  """

13.  dict_comprehension = """\
14.  powers = {key: value for d in (yusuke_power, hiei_power) for key, value in d.items()}
15.  """

17.  copy_and_update = """\
18.  powers = yusuke_power.copy()
19.  powers.update(hiei_power)
20.  """

22.  dict_unpacking = """\
23.  powers = {**yusuke_power, **hiei_power}
24.  """
```
With our strings setup, we can begin our performance test:
```py
1.  >>> import timeit
2.  >>> timeit.timeit(stmt=brute_force, setup=setup)
3.  1.517404469999974
4.  >>> timeit.timeit(stmt=dict_comprehension, setup=setup)
5.  1.6243454339999062
6.  >>> timeit.timeit(stmt=copy_and_update, setup=setup)
7.  0.7273476979999032
8.  >>> timeit.timeit(stmt=dict_unpacking, setup=setup)
9.  0.2897768919999635
```
As it turns out, dictionary unpacking is very fast. For reference, I performed the testing on a Surface Go with Windows 10 and Python 3.7.1.

## A Little Recap

Well, that’s all I have in terms of typical solutions. All that said, be aware that all of these solutions will overwrite duplicate values. In other words, if two dictionaries contain the same key, the last dictionary to be merged will overwrite the previous dictionary’s value.

Also, it’s worth noting that all of these solutions perform  [a shallow copy](https://therenegadecoder.com/code/be-careful-when-copying-mutable-data-types/)  of the dictionaries. As a result, dictionaries that may be nested or store objects will only have their references copied, not the actual values. If that’s a constraint in your application, you may need to write your own recursive copy function.

At any rate, here are all the solutions:
```py
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
```
And, that’s it! As always, I appreciate the support. If you liked this article, do me a favor and share it with someone. For those feeling extra generous,  [consider becoming a member of The Renegade Coder](https://www.patreon.com/TheRenegadeCoder). If you’re not convinced, check out some of these other Python articles:

-   [Rock Paper Scissors Using Modular Arithmetic](https://therenegadecoder.com/code/rock-paper-scissors-using-modular-arithmetic/)
-   [How to Write a List Comprehension in Python](https://therenegadecoder.com/code/how-to-write-a-list-comprehension-in-python/)
-   [The Coolest Programming Language Features](https://therenegadecoder.com/code/the-coolest-programming-language-features/)

Once again, thanks for the support! Before you go, share your recommendation for a topic you’d like to see in the comments.


> [Source : ](https://therenegadecoder.com/code/how-to-merge-two-dictionaries-in-python/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxNDM0ODg0MzBdfQ==
-->