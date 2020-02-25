# How to using Python Heapq for Beginners (With Examples)

![enter image description here](https://i.morioh.com/2019/11/26/ec8b0b1db451.jpg)

Often when working with collections of data, you may want to find the smallest or largest item. It's easy enough to write a function that iterates through the items and returns the smallest or largest one, or use the builtin min(), max(), or sorted() functions. Another interesting way may be implementing a heap (priority) queue.

Interestingly, the heapq module uses a regular Python list to create Heap. It supports addition and removal of the smallest element in O(log n) time. Hence, it is an obvious choice for implementing priority queues.

The heapq module includes seven functions, the first four of which are used for heap operations. However, you need to provide a list as the heap object itself.

Heap data structure has a property that it always pops out the smallest of its element (Min Heap). Also, it keeps the heap structure intact despite any push or pop operation. The heap[0] would also point to the smallest value of the Heap.

In this article we will guide you using Python heapq. It is a module in Python which uses the binary heap data structure and implements Heap Queue a.k.a. Priority Queue algorithm.

## **What Is A Priority Queue?**

Priority Queue is an advanced data type (ADT) which is a more refined version of a Queue. It dequeues higher-priority items before the lower-priority items. Most programming languages such as Python use Binary heap to implement it.

Python heapq, as stated in the beginning, provides a min-heap implementation.

## **What Is A Heap?**

A heap has multiple meaning in computer science. Sometimes, it refers to a memory area in a program used for dynamic allocation. However, in this tutorial, we are talking about the Heap Data Structure, which is a complete binary tree. It helps in implementing priority queues (PQ), the heapsort, and some graph-based algorithms.

A heap has the following two variants:

-   A max-heap, in which the parent is more than or equal to both of its child nodes.
-   A min-heap, in which the parent is smaller or equal to the child nodes.

Below is a general representation of a binary heap.

![This is image title](https://i.imgur.com/OSmWZmV.png)

## **Heapq Module**

Heapq is a Python module which provides an implementation of the Min heap. It makes use of Binary heap and exposes several functions to implement a priority queue.

You may eventually solve many programming problems using its functions. For example, find the two largest numbers from a list of integers in Python.

There happen to be many ways to address this problem. However, none is as intuitive and faster than a Heapq solution.

Out of many Python heapq functions, one is nlargest(). It returns a list type object containing the desired number of largest elements. Below is a short example before we dig into the more complicated ones.

## **Python Heapq Example**

```py
# A brief heapq example
# Find the two largest integers from a list of numbers

import heapq as hq

list_of_integers = [21, 67, 33, 13, 40, 89, 71, 19]

# Find two largest values
largest_nums = hq.nlargest(2, list_of_integers)

print("Two largest numbers are: ", largest_nums)
```

The output is:

```py
Two largest numbers are: [89, 71]
```

Please note that you can create a heap in either of these two ways:

-   Initialize the list with [].
-   Pass a pre-filled list into heapify() to convert to a heap.

Let’s now check out what functions does this module provide.

## **Python Heapq Functions**

The heapq module has the following methods:

### 1. Heappush()

It adds an element to the heap. Don’t apply it on any old list, instead use the one that you built using Heap functions. That is how you can ensure the elements are in the desired order.

```py
# heappush() Syntax
import heapq as hq
hq.heappush(heap, element)
```

Check out below heapq heappush() example.

```py
# A brief heapq.heappush() example

import heapq as hq
import random as r

init_list = list(range(10, 99, 10))
print("Step-1: Seed data for the heap: ", init_list)

r.shuffle(init_list)
print("Step-2: Randomize the seed data: ", init_list)

# Creating heap from an empty list
heap = []
print("Step-3: Creating heap...")

# Demonstrating heapq.heappush() function
[hq.heappush(heap, x) for x in init_list]

# Printing heap content to see if the smallest item is at 0th index
print(" a. Heap contains: ", heap)

# Adding another smaller item to the heap
hq.heappush(heap, 1)
print(" b. Heap contains: ", heap)
```

This code results in the following:

```py
Step-1: Seed data for the heap:  [10, 20, 30, 40, 50, 60, 70, 80, 90]
Step-2: Randomize the seed data:  [70, 20, 60, 80, 90, 30, 40, 10, 50]
Step-3: Creating heap...
 a. Heap contains:  [10, 20, 30, 50, 90, 60, 40, 80, 70]
 b. Heap contains:  [1, 10, 30, 50, 20, 60, 40, 80, 70, 90]
```

You can observe that heap kept the smallest item at the 0th index. We added a new lower value using the heappush() function. And it pushed that at 0th position by shifting the previous value to 1st index.

### 2. Heappop()

It is used to remove the smallest item that stays at index 0. Moreover, it also ensures that the next lowest replaces this position:

```py
# heappop() Syntax
import heapq as hq
hq.heappop(heap)
```

Check out heapq heappop() example. You need to append this code to the previous heappush() example.

```py
# Exercising heapq.heappop() function
print("Step-4: Removing items from heap...")
out = hq.heappop(heap)
print(" a. heappop() removed {} from heap{}".format(out, heap))
out = hq.heappop(heap)
print(" b. heappop() removed {} from heap{}".format(out, heap))
out = hq.heappop(heap)
print(" c. heappop() removed {} from heap{}".format(out, heap))
```

It will give the following result:

```py
Step-4: Removing items from heap...
 a. heappop() removed 1 from heap[10, 20, 40, 50, 30, 70, 80, 90, 60]
 b. heappop() removed 10 from heap[20, 30, 40, 50, 60, 70, 80, 90]
 c. heappop() removed 20 from heap[30, 50, 40, 90, 60, 70, 80]
```

It is clear from the output that heappop() always poped off the lowest element from the heap.

### 3. Heappushpop()

This function first adds the given item in a Heap, then removes the smallest one and returns it. So, it is an increment of both heappush() and heappop(). But it tends to be a little faster than the two combined.

```py
# heappushpop() Syntax
import heapq as hq
hq.heappushpop(heap, element)
```

Check out heapq heappushpop() example. You need to append it to the previous code sample.

```py
# Exercising heapq.heappushpop() function
print("Step-5: Adding & removing items from heap...")
new_item = 99
out = hq.heappushpop(heap, new_item)
print(" a. heappushpop() added {} and removed {} from heap{}".format(new_item, out, heap))
new_item = 999
out = hq.heappushpop(heap, new_item)
print(" b. heappushpop() added {} and removed {} from heap{}".format(new_item, out, heap))
```

The output is:

```py
Step-5: Adding & removing items from heap...
 a. heappushpop() added 99 and removed 30 from heap[40, 60, 50, 70, 90, 99, 80]
 b. heappushpop() added 999 and removed 40 from heap[50, 60, 80, 70, 90, 99, 999]
```

### 4. Heapify()

This function accepts an arbitrary list and converts it to a heap.

```py
# heapify() Syntax
import heapq as hq
hq.heapify(heap)
```

Check out heapq heapify() example.

```py

# A brief heapq.heapify() example

import heapq as hq

heap = [78, 34, 78, 11, 45, 13, 99]
print("Raw heap: ", heap)

hq.heapify(heap)
print("heapify(heap): ", heap)
```

Here is the output:

```py
Raw heap: [78, 34, 78, 11, 45, 13, 99]
heapify(heap): [11, 34, 13, 78, 45, 78, 99]
```

You can see that the heapify() function transformed the input list and made it a heap.

### 5. Heapreplace()

It deletes the smallest element from the Heap and then inserts a new item. This function is more efficient than calling heappop() and heappush().

```

# heapreplace() Syntax
import heapq as hq
hq.heapreplace(heap, element)


```

Check out heapq heapreplace() example.

```py
# A brief heapq.heapreplace() example

import heapq as hq

heap = [78, 34, 78, 11, 45, 13, 99]
hq.heapify(heap)
print("heap: ", heap)

hq.heapreplace(heap, 12)
print("heapreplace(heap, 12): ", heap)

hq.heapreplace(heap, 100)
print("heapreplace(heap, 100): ", heap)
```

The output is:

```
heap: [11, 34, 13, 78, 45, 78, 99]
heapreplace(heap, 12): [12, 34, 13, 78, 45, 78, 99]
heapreplace(heap, 100): [13, 34, 78, 78, 45, 100, 99]
```

### 6. Nlargest()

It finds the n largest elements from a given iterable. It also accepts a key which is a function of one argument.

The selected items have to satisfy the k function. If any of them fails, then the next higher number is considered.

```py
# nlargest() Syntax
import heapq as hq
hq.nlargest(n, iterable, key=None)
```

Check out heapq nlargest() example. It is requesting for two largest numbers.

```py
# heapq.nlargest() example without a key

import heapq as hq

heap = [78, 34, 78, 11, 45, 13, 99]
hq.heapify(heap)
print("heap: ", heap)

out = hq.nlargest(2, heap)
print("nlargest(heap, 2): ", out)
```

The result is:

```
heap: [11, 34, 13, 78, 45, 78, 99]
nlargest(heap, 2): [99, 78]
```

Check out another heapq nlargest() example. It is not only requesting for two largest numbers but also has an is_even() function as the KEY.

If any of the selected numbers fail to clear the KEY function, then the next one comes in.

```py
# heapq.nlargest() example with key

import heapq as hq

def is_even(num):
if num%2 == 0: return 1
return 0

heap = [78, 34, 78, 11, 45, 13, 99]
hq.heapify(heap)
print("heap: ", heap)

out = hq.nlargest(2, heap, is_even)
print("nlargest(heap, 2): ", out)
```

The output is:

```
heap: [11, 34, 13, 78, 45, 78, 99]
nlargest(heap, 2): [34, 78]
```

### 7. Nsmallest()

It is also similar to the nlargest() in operation. However, it gets the n smallest elements from a given iterable. It too accepts a key which is a function of one argument.

The selected items have to satisfy the k function. If any of them fails, then the next smaller number is considered.
```py
# nsmallest() Syntax
import heapq as hq
hq.nsmallest(n, iterable, key=None)
```

Check out heapq nsmallest() example. It is requesting for two smallest numbers.

```py
# heapq.nsmallest() example

import heapq as hq

heap = [78, 34, 78, 11, 45, 13, 99]
hq.heapify(heap)
print("heap: ", heap)

out = hq.nsmallest(2, heap)
print("nsmallest(heap, 2): ", out)
```

Here is the result:

```
heap: [11, 34, 13, 78, 45, 78, 99]
nsmallest(heap, 2): [11, 13]


```

You can achieve similar behavior through other ways, but the heap algorithm is more memory-efficient and even faster.

## **Heapq Exercises**

### First Exercise

Write a Python program to push elements and pop off the smallest one.

```

import heapq as hq
heap = []
hq.heappush(heap, ('H', 9))
hq.heappush(heap, ('H', 7))
hq.heappush(heap, ('H', 4))
hq.heappush(heap, ('H', 1))
print("Elements in the heap:")
for ele in heap:
   print(ele)
print("----------------------")
print("Calling heappushpop() to push element on the heap and return the smallest one.")
hq.heappushpop(heap, ('H', 11))
for ele in heap:
   print(ele)


```

The output:

```
Elements in the heap:
('H', 1)
('H', 4)
('H', 7)
('H', 9)
----------------------
Calling heappushpop() to push element on the heap and return the smallest one.
('H', 4)
('H', 9)
('H', 7)
('H', 11)


```

### Second Exercise

Write a Python program to perform Heap Sort, push all items to a heap, and then take off the smallest ones one after other.

```

import heapq as hq

def heap_sort(heap):
   in_list = []
   for value in heap:
      hq.heappush(in_list, value)
   return [hq.heappop(in_list) for i in range(len(in_list))]

out = heap_sort([9, 7, 5, 2, 1, 2, 8, 10, 6, 5, 4])
print(out)


```

Here is the result:

```
[1, 2, 2, 4, 5, 5, 6, 7, 8, 9, 10]



```

## Conclusion

With the heapq module, you can implement several kinds of priority queues and schedulers. It has vast usage in different areas such as Artificial Intelligence (AI), Machine Learning, Operating systems (OS), and in graphs.

Anyways, after wrapping up this tutorial, you should feel comfortable in using Python Heapq.

Thanks for reading !

Originally published by  **Meenakshi Agarwal**  at  [techbeamers](https://on.morioh.net/b0a3f595aa?r=https://www.techbeamers.com/python-heapq/ "techbeamers")


> [Source : ](https://morioh.com/p/bbf88af0d8ee?list=5dcd3264203e265d661aa056).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwOTE5MTcxMV19
-->