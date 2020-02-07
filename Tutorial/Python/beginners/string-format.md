---
bookFlatSection: true
title: CSV & Text files
bookToc: true

---
How to Format a String in Python: Interpolation, Concatenation, and More
==

![enter image description here](https://i0.wp.com/therenegadecoder.com/wp-content/uploads/2019/09/how-to-format-a-string-in-python-featured-image.jpeg?resize=1024,640&ssl=1)

[The Renegade Coder](https://therenegadecoder.com/ "Go to The Renegade Coder.")[Articles](https://therenegadecoder.com/articles/ "Go to Articles.")[Code](https://therenegadecoder.com/category/code/ "Go to the Code category archives.")How to Format a String in Python: Interpolation, Concatenation, and More

# How to Format a String in Python: Interpolation, Concatenation, and More

POSTED ON  [SEPTEMBER 6, 2019](https://therenegadecoder.com/code/how-to-format-a-string-in-python/) BY  [JEREMY GRIFSKI](https://therenegadecoder.com/author/jeremy-grifski/)

![How to Format a String in Python Featured Image](https://i0.wp.com/therenegadecoder.com/wp-content/uploads/2019/09/how-to-format-a-string-in-python-featured-image.jpeg?fit=800%2C500&ssl=1)

Last Updated on  January 31, 2020

It’s been awhile since I’ve written one of these “how to” articles, but I’m back at it. This time, I want to talk about string formatting using techniques like interpolation and concatenation. In other words, it’s time to finally learn how to format a string in Python

## Table of Contents

-   [Table of Contents](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#table-of-contents "Table of Contents")
-   [Video Summary](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#video-summary "Video Summary")
-   [Problem Introduction](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#problem-introduction "Problem Introduction")
-   [Solutions](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#solutions "Solutions")
    -   [Format a String Using Concatenation](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-concatenation "Format a String Using Concatenation")
    -   [Format a String Using Multiple Print Statements](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-multiple-print-statements "Format a String Using Multiple Print Statements")
    -   [Format a String Using the Join Function](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-the-join-function "Format a String Using the Join Function")
    -   [Format a String Using the perator](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-the-operator "Format a String Using the % Operator")
    -   [Format a String Using the Format Function](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-the-format-function "Format a String Using the Format Function")
    -   [Format a String Using f-Strings](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#format-a-string-using-f-strings "Format a String Using f-Strings")
-   [Performance](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#performance "Performance")
-   [Challenge](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#challenge "Challenge")
-   [A Little Recap](https://therenegadecoder.com/code/how-to-format-a-string-in-python/#a-little-recap "A Little Recap")

## Video Summary

Once again, I’ve updated one of my Python articles to include a nice video summary. If you’d like to see all the code below executed live, check out this video. In addition to sharing all 6 solutions, I also run through performance testing, and I share a solution to the Mad Libs challenge.

## Problem Introduction

Whether we’re trying to prompt a user or output a nice error message, string formatting can always be challenging. After all, the syntax varies from language to language which can feel like learning a metalanguage. For instance, in languages like Java and C, string formatting relies on understanding concepts like variable arguments and format specifiers:
```py
1.  printf("Hi, %s", Jeremy); # Prints "Hi, Jeremy"
```
Of course, string formatting gets more complicated as we introduce different data types. For example, numbers have their own set of specifiers:  `%d`,  `%f`, etc. And, we can even specify how the numbers look in terms of padding and truncation.

That said, I don’t you’re here to learn string formatting in C, so how do we accomplish the same thing in Python? In this article, we’ll take a look at several methods—some silly—just to illustrate how many ways there are to solve this problem.

To get started, we’ll need a universal example which contains a few pitfalls like mixing numbers and strings. The following code snippet will serve as our base for the remainder of the article:
```py
1.  name = "Jeremy"
2.  age = 25
```
Using these variables, we’ll want to construct the following sentence:
```py
1.  print("My name is Jeremy, and I am 25 years old.")
```
Of course, feel free to swap the name and age with your name and age!

## Solutions

As it turns out, there are quite a few ways to format a string. We’ll start from a few direct approaches, then we’ll move into some the for elegant solutions.

### Format a String Using Concatenation

If you’re like me, concatenation is something you learned when you first started to code. As a result, concatenation can seem like a quick shortcut to string formatting:

1.  print("My name is " + name + ", and I am " + age + " years old.")

Unfortunately,  _a solution like this won’t work_. If you tried to run this code, you’ll get a nasty error that looks something like this:

> Traceback (most recent call last):  
> File “”, line 1, in  
> “My name is ” + name + “, and I am ” + age + ” years old.”  
> TypeError: can only concatenate str (not “int”) to str

Hopefully, the  `TypeError`  gives you the hint that the interpreter doesn’t like it when we try to concatenate a string with an integer. In other words, we need to cast the  `age`  variable to a string:

1.  print("My name is " + name + ", and I am " + str(age) + " years old.")

And, that’s it! For small strings, this is probably fine, but it’s not super readable. Also, it’s really easy to forget spaces on either side of the variables we’re concatenating. Luckily, there are other ways to build a string.

### Format a String Using Multiple Print Statements

Who needs concatenation when we can just call print a bunch of times?

1.  print("My name is ", end="")
2.  print(name, end="")
3.  print(", and I am ", end="")
4.  print(age, end="")
5.  print(" years old.")

Now, I know what you’re thinking; yes, this only works in Python 3+. Oh, and this is a totally ridiculous solution, but it demonstrates something important: there are a lot of ways to solve the same problem.

In this case, we’ve taken the  `print`  function and leveraged one of its default arguments (`end`) to remove the newline behavior. That way, we could string together some text without concatenation.

Again, this is definitely hard to read, and I wouldn’t even advise it for small strings. That said, it does eliminate a type cast. Unfortunately, it introduces a lot of duplicate code.

### Format a String Using the Join Function

Continuing our quest for the most ridiculous way of formatting a string, I bring you the  `join`  function. If you’re not familiar with this function, it’s basically a more efficient way to concatenate strings. In addition, it allows us to provide a separator to place between our concatenated strings. Of course, we won’t be needing that:

1.  print(''.join(["My name is ", name, ", and I am ", str(age), " years old"]))

Here, we’ve called the  `join`  method on an empty separator string. As an argument, we’ve passed it a list of strings. Naturally, join will combine this list of strings into a single string without any separators.

Oddly enough, I sort of like this solution because it’s surprisingly readable. Unfortunately, there are a few drawbacks. For instance, we have to convert all our variables to strings manually. In addition, this line is already pretty long. Though, I suppose we could break everything out onto its own line.

At any rate, with these three out of the way, we can finally start getting to some more reasonable solutions.

### Format a String Using the % Operator

Now, we’re starting to get into the actual string formatting techniques. As it turns out, Python has its own set of formatting tools similar to  `printf`  from C:

1.  print("My name is %s, and I am %d years old."  % (name, age))

Here, we’ve constructed a new string with  `%s`  replaced by  `name`  and  `%d`  replaced by age.

In addition to knowing  [the format specifiers](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting), we’ll want to learn the syntax. In particular, our template string is following by the modulo operator. Of course, in this context, we can call it the string formatting or  **interpolation**  operator.

Then, we create a tuple of values that we want to place in our string. Be very careful to ensure the order of these values. If they are out of order, the resulting string may be incorrect, or the program may crash altogether.

With this method, we get a much cleaner solution. Of course, there are pitfalls here, but they mostly have to do with how the values are mapped to the string. For example, we have to pay attention to how we order our arguments, and we need to know our format specifiers.

Speaking of format specifiers, what if we want to print out an object directly? Fortunately, we have better solutions ahead.

### Format a String Using the Format Function

Instead of using a fancy overloaded operator, we can make our code even more readable by using the  `format`  function for strings:

1.  print("My name is {}, and I am {} years old".format(name, age))

Previously, we would have had to use format specifiers to get the behavior we wanted, but now we can just use braces. In other words, we’ve eliminated a problem from the previous solution.

From what I understand, this method leverages the  `__format__`  method for objects, so we can pass just about anything to this method without issue. There goes yet another problem! Of course, if the class doesn’t have  `__str__`  or  `__repr__`  overridden, then the object will not print nicely. That said, I still count that as a win over the previous solution.

As it turns out, we can eliminate our ordering issue from the previous solution as well. All we have to do is provide keyword arguments:

1.  print("My name is {n}, and I am {a} years old".format(a=age, n=name))

In this example, we named the age keyword  `a`  and the name keyword  `n`. That way, we could place the keywords inside their respective braces. To further drive home the point, we can even reorder the arguments without issue. Now that’s pretty cool!

Of course, I should warn you that this solution  [may pose a security threat](https://lucumr.pocoo.org/2016/12/29/careful-with-str-format/)  to your application depending on how you’re using it. If you’re writing your own format strings, there shouldn’t be any issues. However, if your accepting format strings from your users, you might want to be careful.

### Format a String Using f-Strings

Another way to perform string interpolation is using Python’s latest f-String feature (Python 3.6+). With this feature, all we need to do is prefix a string with the letter  `f`  and insert braces just like before. However, this time, we can insert the name of our variables directly:

1.  print(f"My name is {name}, and I am {age} years old")

Now, that is incredibly elegant. No longer do we have to worry about:

-   Mapping arguments to format specifiers
-   Using format specifiers correctly
-   Remembering obscure syntax

Instead, we prepend and  `f`  and insert our variables. That’s it! Now, I don’t know if there are any sort security vulnerabilities with this solution, but as far as I can tell, there’s no way to apply the  `f`  to an input string.

At any rate, that’s all I have for string formatting solutions. Now, let’s start to compare the performance of these solutions.

## Performance

As always, I like to setup on all of our solutions in strings first:

1.  setup = """
2.  name = "Jeremy"
3.  age = 25
4.  """

6.  concatenation = """
7.  "My name is " + name + ", and I am " + str(age) + " years old."
8.  """

10.  string_join = """
11.  ''.join(["My name is ", name, ", and I am ", str(age), " years old"])
12.  """

14.  modulus = """
15.  "My name is %s, and I am %d years old." % (name, age)
16.  """

18.  format_ordered = """
19.  "My name is {}, and I am {} years old".format(name, age)
20.  """

22.  format_named = """
23.  "My name is {n}, and I am {a} years old".format(a=age, n=name)
24.  """

26.  f_string = """
27.  f"My name is {name}, and I am {age} years old"
28.  """

For my sanity, I had to remove the print statements. As a result, I wasn’t able to test the  `print`  solution. That said, feel free to try your hand at it. I ran into some issues with the output string slowing down the test, and I even tried rerouting  `stdout`  to deal with it. It was a nightmare to say the least.

At any rate, it’s just a matter of calling our  `timeit`  commands now:

1.  >>> import timeit
2.  >>> min(timeit.repeat(stmt=concatenation, setup=setup, repeat=10))
3.  0.4947876000000022
4.  >>> min(timeit.repeat(stmt=string_join, setup=setup, repeat=10))
5.  0.37328679999995984
6.  >>> min(timeit.repeat(stmt=modulus, setup=setup, repeat=10))
7.  0.29478180000000265
8.  >>> min(timeit.repeat(stmt=format_ordered, setup=setup, repeat=10))
9.  0.40419490000000735
10.  >>> min(timeit.repeat(stmt=format_named, setup=setup, repeat=10))
11.  0.49794210000000305
12.  >>> min(timeit.repeat(stmt=f_string, setup=setup, repeat=10))
13.  0.1918610999999828

As is often the case with these new features in Python, they are incredibly optimized. As a matter of fact, the only solution that even comes close to competing with the f-String solution is the modulus operator solution.

Also, I think it’s worth noting how much slower the  `format`  function is when the arguments are named rather than ordered. In fact, it’s about as slow as concatenation which I expected to be horrendous. After all, strings are immutable, so concatenation should be pretty bad.

As always, take these performance metrics with a grain of salt.

## Challenge

If you haven’t had a chance to check out the video above, here’s the challenge. I want you to create a simple script which generates Mad Libs. If you’re not familiar with Mad Libs,  [check out the official site](http://www.madlibs.com/).

To summarize, however, Mad Libs is a word game where a paragraph of text is provided with several words missing. It’s your job to then fill those gaps with the appropriate words (e.g. nouns, verbs, adjectives, etc.) to complete the story:

> Be careful not to vacuum the NOUN when you clean under your bed.
> 
> [Mad Libs](http://www.madlibs.com/tile/summer-fridays/)

Right now, I don’t really have any strict requirements. In other words, you could write a program that prompts the user for a few words then populates a text using the string formatting techniques above.

Likewise, you might choose to make a program which generates random Mad Libs from lists of words. Regardless, the choice is yours! The goal is to practice these string formatting methods.

As always, check the comments below for a copy of my solution to the Mad Libs problem.

## A Little Recap

With all that said, here are all of the solutions in one unified location:

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

And with that, we’re done. If you liked this article and want more content like this to hit your inbox,  [subscribe to our newsletter](https://newsletter.therenegadecoder.com/). Even better,  [become a member of The Renegade Coder community](https://www.patreon.com/TheRenegadeCoder)  and earn cool rewards like attribution at the end of an article like this one.

Alternatively, you’re welcome to do your typical online shopping through the following Amazon affiliate links:

-   [Automate the Boring Stuff with Python: Practical Programming for Total Beginners](https://www.amazon.com/Automate-Boring-Stuff-Python-Programming/dp/1593275994/ref=as_li_ss_tl?crid=ZKFERMUJBOK0&keywords=python+programming&qid=1565977249&s=gateway&sprefix=python,aps,165&sr=8-9&linkCode=ll1&tag=renegadecoder-20&linkId=0929448da72e0c481dd8e52990cc05ef&language=en_US)  by Al Sweigert
-   [Python Programming: The Ultimate Step By Step Guide To Programming With Python](https://www.amazon.com/Python-Programming-Ultimate-Step-Guide-ebook/dp/B07VJ9XHMP/ref=as_li_ss_tl?crid=ZKFERMUJBOK0&keywords=python+programming&qid=1565977249&s=gateway&sprefix=python,aps,165&sr=8-13&linkCode=ll1&tag=renegadecoder-20&linkId=03d55393fcf2f53b82f5feb67440732e&language=en_US)  by Antony Mc Fedden

As always, I try to pick relevant products that I think will bring you some value. If you have any products of your own that you’d like to me to share, drop them down below in the comments.

In the meantime, why not improve my site metrics a bit by browsing some of the following Python articles:

-   [That Time I Shipped Insecure Code](https://therenegadecoder.com/blog/that-time-i-shipped-insecure-code/)
-   [How to Automate Your GitHub Wiki](https://therenegadecoder.com/code/how-to-automate-your-github-wiki/)
-   [How to Clone a List in Python: Slice, Copy, and More](https://therenegadecoder.com/code/how-to-clone-a-list-in-python/)

At ant rate, thanks again for your support, and a special thanks to  [all my patrons](https://www.patreon.com/TheRenegadeCoder)  who make this possible. Until next time!


> [Source : ](https://therenegadecoder.com/code/how-to-format-a-string-in-python/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4NDI0NzQ0NV19
-->