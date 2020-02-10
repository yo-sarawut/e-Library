---
bookFlatSection: true
title: Upgrading Python lists
bookToc: true

---

Upgrading Python lists
===
Adding useful functionalities to Python lists

![enter image description here](https://miro.medium.com/max/724/1*WUhxMtCGKD34OdsYamURCw.jpeg)

## Introduction

Python lists are good. But they’re not great. There is so much functionality that can be easily added to them but is still missing. Indexing with booleans, easily creating dictionaries from them, appending more than one element at a time, so on and so forth. Well, not anymore.

**_Fastai_**  has come up with their own data structure called  `L`  . It can do everything that a Python list can do and much more.

The purpose of this article is to show you how easy it is to write such useful functionalities on your own. Especially if you are a beginner, try creating a mini-version of this library. Try writing some of the functionalities you hoped existed. It’ll be a good learning experience.

For now, let’s learn about  **L**. Here is the Colab link if you’d. Make a copy on your Colab (**File->Save a copy in drive**)and run the first cell only once. Your notebook will crash. But you’ll be ready to use the library right away.

[Google Colaboratory Link](https://colab.research.google.com/drive/1sv_q6X8XUOKz-254diVTEYsjo3nfiNgz).

## What is L?

Like I mentioned before, it is similar to a Python list but can achieve much more. Let’s start by importing the library and creating and instance of  `L.`



![](https://miro.medium.com/max/2294/1*leCqh7-oj8NVTCMl7NVUrw.png)

We see that it prints the length of the list and then the contents. No need to print the length separately all the time anymore.

If you are like me, you don’t like using square brackets. Remove them.



![](https://miro.medium.com/max/2288/1*zCxSL0Piiwo95WKoyjJNVQ.png)

Writing  `.append()`  to append elements is again so tedious. Also you can append only one element at a time. Meh. Remove remove.



![](https://miro.medium.com/max/2306/1*oag7Aqnl1iJCTLBwrvla6g.png)

Note that these things are very easy to code. We are only defining a  `__add__`  magic method behind the hood to decide what the  `+`  operator will do. If you’d like to learn more about magic methods you can read my article on  [How to be fancy with OOP in Python](https://towardsdatascience.com/how-to-be-fancy-with-python-part-2-70fab0a3e492).

Let’s investigate the  `__add__`  method.

![](https://miro.medium.com/max/30/1*kTO2yiWwQ62xYOmvUMZb2A.png?q=20)

![](https://miro.medium.com/max/1910/1*kTO2yiWwQ62xYOmvUMZb2A.png)

It creates a new instance of L with the current elements and the new elements. Pretty simple, right?

Let’s try  `__mul__`  as well.



![](https://miro.medium.com/max/2292/1*xRSy5Zi1CtlYB4fKJkpS6g.png)

It replicates the list 2 times. Also, notice that it prints only the first 10 elements and then displays  `...`  This is much cleaner than Python lists which display all the elements.

You can find unique elements in an L.


![](https://miro.medium.com/max/2282/1*x0Il7TcO1pZOy4gIh90IJg.png)

You can easily convert it to a dictionary.



![](https://miro.medium.com/max/2284/1*OM9Wr1oITnuZypgvKiqbKw.png)

However, the real power of L is with its indexing capabilities.

1.  Indexing with a list of indexes



![](https://miro.medium.com/max/2280/1*_Iyr28dxSBx2-BJKUNQUBA.png)

2. Indexing with booleans



![](https://miro.medium.com/max/2288/1*0DxzoDBFXfAl6HLOWnvDxw.png)

3. Multiple assignment



![](https://miro.medium.com/max/2310/1*N0DTcq3S7xsDui3ssmNv_Q.png)

## Conclusion:

All in all it’s a great data structure and can easily be used instead of lists. Try the notebook. Explore it. That will be it for this article.

~happy learning

## References:

[https://github.com/fastai/fastai_dev/blob/master/dev/01_core_foundation.ipynb](https://github.com/fastai/fastai_dev/blob/master/dev/01_core_foundation.ipynb)




> [Source : ](https://towardsdatascience.com/upgrading-python-lists-35440096ec36).



|NO.|Description  |File  |Link  |Action | Update|
|:----:|--|
|  |  |

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDY5NzQ0MDg2LDY3MDkxNjcxOF19
-->