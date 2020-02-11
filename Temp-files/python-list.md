# TUTORIAL FOR PYTHON LISTS

-   [Home](http://theautomatic.net/)
-   Tutorial for Python Lists

![python lists tutorial](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-lists-tutorial.jpg?w=640)

  

This tutorial goes through how to work with lists in Python, including many of the built-in methods Python makes available for these data structures. Feel free to click on any of the links below to skip to a section of interest.

**  
[Background on lists](http://theautomatic.net/tutorial-for-python-lists/#background)  
[Referring to list elements by index](http://theautomatic.net/tutorial-for-python-lists/#indexing_list)  
[Slicing lists](http://theautomatic.net/tutorial-for-python-lists/#slice_list)  
[Combining lists](http://theautomatic.net/tutorial-for-python-lists/#combining_lists)  
[Lists are mutable](http://theautomatic.net/tutorial-for-python-lists/#lists_are_mutable)  
[Lists support inplace methods](http://theautomatic.net/tutorial-for-python-lists/#lists_inplace_methods)**

[Adding elements to a list](http://theautomatic.net/tutorial-for-python-lists/#add_elements_to_list)  
[How to append elements to a list (individually)](http://theautomatic.net/tutorial-for-python-lists/#append_elements_to_list)  
[How to insert elements at specific locations in a list](http://theautomatic.net/tutorial-for-python-lists/#insert_elements_into_list)  
[How to append another list of elements to a list](http://theautomatic.net/tutorial-for-python-lists/#list_extend_method)

[Removing elements from a list](http://theautomatic.net/tutorial-for-python-lists/#ways_to_remove_elements_from_list)  
[How to remove specific values from a list](http://theautomatic.net/tutorial-for-python-lists/#remove_elements_from_list)  
[Removing an element from a specific index in a list](http://theautomatic.net/tutorial-for-python-lists/#list_pop_method)  
[Removing all elements in a list at once](http://theautomatic.net/tutorial-for-python-lists/#remove_all_elements_in_list)

[Other list operations](http://theautomatic.net/tutorial-for-python-lists/#other_list_operations)  
[How to filter a list](http://theautomatic.net/tutorial-for-python-lists/#filter_list)  
[How to reverse a list](http://theautomatic.net/tutorial-for-python-lists/#reverse_elements_in_list)  
[How to count the occurrence of an element in a list](http://theautomatic.net/tutorial-for-python-lists/#count_occurrence_of_element_in_list)  
[Copying a list](http://theautomatic.net/tutorial-for-python-lists/#copy_list)  
[How to sort a list](http://theautomatic.net/tutorial-for-python-lists/#sort_list)  
[Getting the length of a list](http://theautomatic.net/tutorial-for-python-lists/#length_of_list)  
[Finding the first occurrence of a value in a list](http://theautomatic.net/tutorial-for-python-lists/#index_method)

  
  
  

# **Background on lists**

A  **list**  in  [Python](http://theautomatic.net/category/python/)  is a container of numbers, strings, or other objects (or mixed). Lists can be created using brackets enclosing whatever elements you want in the list, where each element is separated by a comma.

Below we define a list containing five numbers – 4, 5, 10, 20, and 34.

1

`nums` `=` `[``4``,` `5``,` `10``,` `20``,` `34``]`

We can also define a list of strings:

1

`strings` `=` `[``"this"``,` `"is"``,` `"another"``,` `"list"``]`

Or – here’s a mixed data type list:

1

`[``"example"``,` `"of"``,` `"a"``,` `42``,` `10``,` `"mixed"``,` `"data type list"``,` `5``]`

Lists can also contain other lists. These lists are called nested lists. Below we define a list where the last element is just an integer, 100, but the other elements of the list are lists themselves.

1

`nested_list` `=` `[[``"inner list"``,` `10``], [``"second inner list"``],` `100``]`

## **Referring to list elements by index**

One property of lists is that each element in the list can be referred to by an index i.e. there is an order to the elements in the list. In other words, there is the concept of the first element, second element, third element, and so on. Since Python is  [zero-indexed](https://en.wikipedia.org/wiki/Zero-based_numbering), the  **0th**  element of the list defined above is 4. The  **1st**  element is 5, the  **2nd**  is 10, and so on.

We refer to elements in a list by index using bracket notation like this:

1

2

3

4

5

`nums[``0``]` `# returns 4`

`nums[``1``]` `# returns 5`

`nums[``2``]` `# returns 10`

We can also refer to elements starting from the end of the list using negative indices.

1

2

3

4

5

`nums[``-``1``]` `# returns 34`

`nums[``-``2``]` `# returns 20`

`nums[``-``3``]` `# returns 10`

## **Slicing a list**

What if want to grab more than one element at a time from a list? For instance, how would we retrieve the first three elements of our  **nums**  list?

1

2

3

`nums[``0``:``3``]`

`nums[:``3``]`

Each of the above will return the first three elements of the list  **nums**. The  **0:3**  means that Python will return the elements in the list indexed 0, 1, and 2 – but not 3. So it will include all the elements up until, but not including the third-indexed element.

![python slice list](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-slice-list.png?w=640)

Here’s a few more examples:

1

2

3

`nums[``1``:``4``]`

`nums[``1``:``3``]`

The first example above will retrieve the elements indexed 1, 2, and 3 (but not 4) of  **nums**. The second example retrieves the elements indexed 1 and 2 (but not 3).

![python how to slice list](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-slice-list2.png?w=640)

## **How to combine lists**

Lists can be combined using the “+” operator.

1

2

3

4

5

6

`list_1` `=` `[``3``,` `4``,` `5``]`

`list_2` `=` `[``6``,` `7``,` `8``]`

`list_3` `=` `list_1` `+` `list_2`

`list_3`

![python how to combine lists](https://i2.wp.com/theautomatic.net/wp-content/uploads/2019/01/python-combine-lists.png?w=640)

We can also chain together multiple concatenation operations:

1

`[``1``,` `2``,` `3``]` `+` `[``4``,` `5``,` `6``]` `+` `[``"python"``,` `"is"``,` `"awesome"``]` `+` `[[``"nested list"``]]`

![python concatenate lists](https://i1.wp.com/theautomatic.net/wp-content/uploads/2019/01/python-concatenate-lists.png?w=640)

## **Lists are mutable**

Another property of lists is that they are  **mutable**. We’ll see examples of what this means in the below sections. Effectively, though,  **mutable**  means that the  _state_  of a list can be changed after it has been defined. What does that mean in practice?  **Mutability**  means we can change how a list (or some other object in Python for that matter) is defined without formally redefining the list.

Suppose, for example, we wanted to change the 0th element of the strings list above. We can do that by referencing just the 0th element of the list, and setting it equal to some other value.

1

2

3

4

5

`strings` `=` `[``"this"``,` `"is"``,` `"another"``,` `"list"``]`

`strings[``0``]` `=` `"that"`

`strings`

![python change element in list at specific index](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-mutability-example.png?w=640)

The above code is an alternative to the below where we redefine the full list  **strings**. The  **mutability**  of lists gives us the ability to shorten the amount of code we write to adjust the values they contain.

1

`strings` `=` `[``"that"``,` `"is"``,` `"another"``,` `"list"``]`

Some of the additional examples below will show how lists can be mutated, or changed, after they have been defined.

## **Lists support inplace methods**

Lists in Python have several inplace methods. These are methods, or functions, that perform operations on a list with the result being automatically stored back into the same list, thus generally reducing the amount of code that has to be written. If that isn’t clear, we’ll see examples of how this works in several of the sections below.

  

# **Adding elements to a list**

## **How to append elements in a list**

An example of  **mutability**  is via appending elements to a list. To append elements to a list, one at at a time, we can use the (aptly-named)  **append**  method. This method is also an example of an  **inplace**  operation.

1

2

`# append 100 to the end of our list, nums`

`nums.append(``100``)`

![python list append](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/list-append-method.png?w=640)

Below we append 200 to the end of  **nums**, followed by 300.

1

2

3

`nums.append(``200``)`

`nums.append(``300``)`

![python append to list](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-append2.png?w=640)

Each of these append examples demonstrates how lists are mutable because they each show how the definition of  **nums**  can be changed after its initialization without a new initialization. In other words, we could have taken our original list and then redefined that list multiple times to append elements to the end of the list, like this:

1

2

3

4

5

6

7

`nums` `=` `[``4``,` `5``,` `10``,` `20``,` `34``]`

`nums` `=` `[``4``,` `5``,` `10``,` `20``,` `34``,` `100``]`

`nums` `=` `[``4``,` `5``,` `10``,` `20``,` `34``,` `100``,` `200``]`

`nums` `=` `[``4``,` `5``,` `10``,` `20``,` `34``,` `100``,` `200``,` `300``]`

…But we don’t have to. We can accomplish what the code above does with the  **append**  method because of the fact that lists are mutable, and therefore, we can  _mutate_, or change, lists without reinitialization.

Also, because  **append**  is  **inplace**, we don’t have to run the last chunk of code above where we’re redefining  **nums**  because the method automatically changes  **nums**  to have the appended values.

## **How to insert elements at specific locations in a list**

The  **append**  method above appends an element to the  _end_  of a list, but what if we want to insert an element at some other specific location in a list? We can perform this task using the  **insert**  method.

Taking the previous value of  **nums**  as  **[4, 5, 10, 20, 34, 100, 200, 300]**, let’s insert the string “test” into the third indexed position of the list.

1

`nums.insert(``3``,` `"test"``)`

The  **insert**  method takes two parameters. The first is the index in the list we want to insert some element. The second parameter is the element we want to insert. In this case, we insert the string “test” into the third index of the list, nums.

![python insert element into a list at specific index](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-insert-element-into-list.png?w=640)

Putting an element into the nth  position in a list will shift the elements in that position and later to the right. In our case, this means the element in the third position initially will now be in the fourth position, the element in the fourth position shifts to the fifth position, the element in the fifth position shifts to the sixth position, etc.

Below we insert the string “test” again – though this time we put it into the seventh-indexed position.

1

`nums.insert(``7``,` `"test"``)`

![python insert into list](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-insert-method.png?w=640)

## **How to append another list of elements to a list**

One of my favorite methods for dealing with lists is the  **extend**  method because it can append an entire other list of elements at once to your list.

1

`nums.extend([``1000``,` `2000``,` `3000``])`

![python extend method append an entire list to another list](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-extend-method.png?w=640)

The  **extend**  method can be viewed as a shortcut for writing the below code:

1

`nums` `=` `nums` `+` `[``1000``,` `2000``,` `3000``]`

The above code will take the initial list,  **nums**, and append the numbers 1000, 2000, and 3000 to the end of the list – just like the  **extend**  method. The difference is that in this case we have to redefine  **nums**  to be equal to this concatenation, whereas the  **extend**  method is  **inplace**.

  

# **Removing elements from a list**

## **How to remove elements from a list by specific values**

We can remove elements of a list that equal a specific value using the  **remove**  method. The  **remove**  method will take out the first occurrence of the input value for a given list (and only the first occurrence). For instance, let’s say we want to get rid of the string “test” we inserted into  **nums**  in an earlier section.

1

2

3

4

5

`# remove first occurrence of "test"`

`nums.remove(``"test"``)`

`# remove next occurrence of "test"`

`nums.remove(``"test"``)`

Each time we run  **nums.remove(“test”)**, Python will remove the first found occurrence of the string “test” in the list. Thus, running the first line above will remove “test” from the third-indexed position in  **nums**. Running the second line will remove the next (and in this case, only other) occurrence of “test” in the list.

![python list remove first occurrence of element](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-remove-element-first-occurrence.png?w=640)

## **How to remove an element from a specific index**

Elements can also be removed from a list based off index. For example, if we want to remove the element in the third-indexed position from a list, we could do this:

1

2

3

4

5

`# remove element in the third-indexed position`

`nums.pop(``3``)`

`# or remove the element in the fifth-indexed position`

`nums.pop(``5``)`

![python list pop method](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-pop-method.png?w=640)

Notice from the snapshot above that the  **pop**  method returns the value of the element that is removed. Hence, when used above, it returns 20 and then 200, respectively.

Now, we can insert those numbers back into our list:

1

2

3

`nums.insert(``5``,` `200``)`

`nums.insert(``3``,` `20``)`

![python insert list method](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-insert-method.png?w=640)

## **How to remove all elements of a list**

To clear out all elements of a list we can use the  **clear**  method:

1

`nums.clear()`

![python clear all elements from a list](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-list-clear-method.png?w=640)

  

# **Other built-in list operations**

## **Filtering lists**

Lists can be filtered using the  **filter**  function. The  **filter**  function works by taking a function and a list as input. The input function applies a logical condition that returns True or False (i.e. Boolean) for each element in the list. If the function returns True, the output object will retain that list element.

The actual object returned by  **filter**  is not a list (as of Python >= 3.0) – but instead, is called a filter object. To convert this to a list, we just need to wrap the list function around the filter object.

1

2

3

`a` `=` `[``10``,` `20``,` `30``,` `40``]`

`filter``(``lambda` `num: num <` `30``, a)`

1

`list``(``filter``(``lambda` `num: num <` `30``, a))`

![python filter list](https://i0.wp.com/theautomatic.net/wp-content/uploads/2019/01/python-filter-list-function.png?w=640)

## **How to reverse the elements in a list**

#### **Option 1)**

There’s a few different ways to reverse the elements in a list. One way is using the  **inplace**  method called  **reverse**, like so:

1

`nums.reverse()`

This will reverse the elements of our list,  **nums**, while storing the results of that reversal back in nums. So if we run the below line of code, we can see now that nums contains its original elements in reverse.

1

`nums`

![python reverse a list](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-reverse-elements-in-a-list.png?w=640)

#### **Option 2)**

Another way of reversing a list is using bracket notation, like this:

1

`nums[::``-``1``]`

Doing the above will reverse the elements of  **nums**, but won’t store the results back into  **nums**  unless we tell it to, like this:

1

`nums` `=` `nums[::``-``1``]`

![python quick way to reverse a list](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-reverse-list-double-colon.png?w=640)

## **How to count the occurrence of an element in a list**

To count how many times an element occurs in a list, we can use the  **count**  method, like this (using a different list this time):

1

2

3

`x` `=` `[``10``,` `10``,` `30``,` `20``,` `50``,` `50``,` `30``,` `30``,` `30``]`

`x.count(``30``)`

Here, running  **x.count(30)**  will return 4 because 30 occurs four times in  **x**.

![python count how many times an element occurs or appears in a list](https://i2.wp.com/theautomatic.net/wp-content/uploads/2018/12/list-count-method.png?w=640)

Likewise, if we want to count how many times 50 appears, or 10 appears, we would do this:

1

2

3

`x.count(``50``)`

`x.count(``10``)`

![python count how many times an element occurs or appears in a list](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-count-occurence-of-element-in-a-list.png?w=640)

If we try to use the  **count**  method for an element that doesn’t occur in the list, Python will return zero:

1

`x.count(``100``)`

![python count zero elements in a list](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-count-method.png?w=640)

## **How to copy a list**

Lists can be copied using the  **copy**  method.

![python how to copy a list](https://i0.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-how-to-copy-a-list.png?w=640)

## **How to sort a list**

Sorting a list can be done using the  **sort**  method like this:

1

2

3

4

5

6

7

8

`# define a new list`

`new_list` `=` `[``10``,` `4``,` `17``,` `21``,` `8``,` `12``,` `2``]`

`# sort list`

`new_list.sort()`

`# see results stored in new_list`

`new_list`

![how to sort a list in python](https://i1.wp.com/theautomatic.net/wp-content/uploads/2018/12/python-sort-list.png?w=640)

You can also sort a list using the  **sorted**  function:

1

`sorted_list` `=` `sorted``(new_list)`

## **How to get the length of a list**

Getting the length of a list can be done in a couple of different ways. The first, more commonly seen way, is using Python’s built-in  **len**  function.

1

2

3

4

5

`a` `=` `[``4``,` `5``,` `6``]`

`len``(a)` `# returns 3`

`b` `=` `[``10``,` `20``,` `30``,` `40``,` `50``]`

`len``(b)` `# returns 5`

You can also get the length of a list using the  **__len__**  method. Note the double underscore on each side of  _len_.

1

2

3

4

5

`a` `=` `[``4``,` `5``,` `6``]`

`a.__len__()` `# returns 3`

`b` `=` `[``10``,` `20``,` `30``,` `40``,` `50``]`

`b.__len__()` `# returns 5`

## **How to get the index where an element first occurs**

Figuring out where in a list an element first occurs can be done using the  **index**  method.

1

2

3

4

5

`strings` `=` `[``"this"``,` `"is"``,` `"another"``,` `"list"``]`

`strings.index(``"another"``)` `# returns 2`

`strings.index(``"list"``)` `# returns 3`


> [Source : ](http://theautomatic.net/tutorial-for-python-lists/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzODg3MTI5M119
-->