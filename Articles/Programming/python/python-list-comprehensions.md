Python’s List Comprehensions: Uses and Advantages
===

![enter image description here](https://miro.medium.com/max/690/1*jsgLaIkhgF7SzQS1FWIPug.jpeg)

Whether you’re a Data Scientist, a Web Developer working in an API, or any other of a long list of roles, chances are you’ll stumble upon Python at some point.

Some of us love it for its simplicity, its fluidity and legibility. Others hate it for not being as performant as C or pure Assembly, having Duck Typing, or being single-threaded (ish).

No matter what group you belong to, if you’re in a position where you want/have to write Python code, you’ll want it to be as legible as possible. Or you may have stumbled upon a list comprehension in the wild and be confused as to how to tame it. If either of those is true, then this article is for you.

## What are List Comprehensions?

First of all, let’s define our terms. A list comprehension is a piece of syntactic sugar that replaces the following pattern:

With this, equivalent, one:

## Why we should use them

What are the advantages of using List Comprehensions? First of all, you’re reducing 3 lines of code into one, which will be instantly recognizable to anyone who understands list comprehensions. Secondly, the second code is faster, as Python will allocate the list’s memory first, before adding the elements to it, instead of having to resize on runtime. It’ll also avoid having to make calls to ‘append’, which may be cheap but add up. Lastly,  code using comprehensions is considered more ‘Pythonic’ — better fitting Python’s style guidelines.

## Refactoring Code Smells

Another, more subtle advantage is smell detection. Your code without comprehensions may look like this:

If the preceding or following code is long enough in ‘_some_function_’, that bit about the list may get lost. But using list comprehensions directly on those 6 lines wouldn’t look that pretty:

Trying to parse that with your eyes will give you a headache. There are some paper bags below your seats in case any of you need to use them. What’s happening here? Well, it’s clear that bit of logic should be abstracted into a new function, like this:

refactoring with two levels of abstraction

Then those first six lines of code end up just being

another_list = [new_function(i) for i in range(k)]

Which is a lot clearer (if I hadn’t picked such awful names for our functions) and reads faster if you know what’s going on. Some may argue I did end up adding 6 lines of overhead code in order to get to this place. That’s true, but if this behavior appeared at least once more in the code, then even that’s not really a loss. And even if that were not the case, what we lose in code size, we gain in maintainability and legibility, which should be sought after.

> _Good programmers write code that humans can understand._
> 
> — Martin Fowler.

Some other things that are easy to do with list comprehensions are

## unwrapping a matrix into a vector:

vector_version = [1,0,0,0,1,0,0,0,1]

## Filtering a list:

## Generating many instances of a class (in this case modeled with a simple dictionary, like a JSON object):

## Casting a list of objects of a certain type into a list of another type:

We generate a list of the first 100 numbers turned into strings, or just a string joining them with commas. All in one smooth line!

## Performance Boost

In order to verify there was an actual boost in performance, I decided to run some tests. I ran the for-loop version and the list comprehension version of the same code, with and without filtering. Here’s the test’s snippet:

The  _list_a_  methods generate lists the usual way, with a for-loop and appending. The  _list_b_  methods use List Comprehensions.

My results were the following:

-   5.84 seconds for list a
-   4.07 seconds for list b
-   4.85 seconds for filtered list a
-   4.13 seconds for filtered list b

I encourage you to run that same script in your computer and see the boost for yourself, maybe even change the input size.

We see a 33% boost in speed from switching to List Comprehensions  in the unfiltered case, whereas the filtered algorithm only gets a 15% boost. This corroborates our theory that the main performance advantage comes from not having to call the  _append_  method at each iteration, which is skipped on every other iteration in the filtered case.

Finally, I should add that all I just taught you about list comprehensions can be done with Python dictionaries.

## Dictionary Comprehensions:

That was my crash course in list comprehensions, I hope you liked it! If there are any features you feel I should have mentioned and didn’t, or have any complaints about the gists, please let me know.

Finally, there is an O’Reilly book I love and I found it very useful when I started my Data Science journey. It’s actually the book I learned list comprehensions from. It’s called  [**Data Science from Scratch with Python**](https://www.bookdepository.com/book/9781491901427/?a_aid=strikingloo&chan=ws), and it’s probably half the reason I got my job. If you read this far, you may enjoy it!

_P.S: If you want to expand on this topic, I suggest you read my article on_ [_Python’s Generator Expressions_](https://towardsdatascience.com/pythons-list-generators-what-when-how-and-why-2a560abd3879)_. I also encourage you to follow me for more Python tutorials, tips and tricks._






> Written with [StackEdit](https://towardsdatascience.com/how-list-comprehensions-can-help-your-code-look-better-and-run-smoother-3cf8f87172ae).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4NDM5NDE3M119
-->