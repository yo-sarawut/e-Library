Python Programming…in R
===

> All code used in this tutorial can be found here:  [https://github.com/joelalcedo/Python_in_R](https://github.com/joelalcedo/Python_in_R)

I am a Data Scientist working in New York. I have worked on a number of different projects spanning data visualization, machine learning and software development all in hopes to better understand the complexities associated with the financial markets. I started learning how to program about 10 years ago in visual basic. One thing led to another  _(as it does)_  and I learned SQL, R,  [Python](https://hackernoon.com/tagged/python),  [JavaScript](https://hackernoon.com/tagged/javascript)  _(regrettably)_, C++ and others. Currently, I am working on some Flutter projects, using Google’s Dart framework.

Do my credentials sound like an alphabet soup? If you yourself are a programmer, chances are you have a few languages on the resume. If you are interested in hiring a programmer, but do not know quite what to look for, chances are you have been inundated with a spectrum of  [programming](https://hackernoon.com/tagged/programming)  languages and obscure libraries on candidate resumes, wondering to yourself,  _“am I still reading English?”._

Why am I writing this? To address a question I hear all time on Wall Street from aspiring programmers:

**_“Should I learn Python or R?”_**

Well gather around, because I am about to show you it is possible to use both  [Python](https://hackernoon.com/tagged/python)  and R seamlessly. Personally, I say learn them both. There are certain advantages Python brings to the table versus R, and vice-versa.

Using the  [reticulate](https://rstudio.github.io/reticulate/articles/introduction.html)  package in R, it is very easy to interface between the two. I will write a simple function in Python to pull some data in from  [Quandl](http://www.quandl.com/), then clean up and visualize the data in R using ggplot2.

Here’s the 30,000 foot view. We have some directory that contains our Python code and R code  _(you can download the full directory_ [_here on my GitHub_](https://github.com/joelalcedo/Python_in_R)_)_. Using the reticulate package in R, we will call a Python file, which will then port over to R, which can then continue to be used in R.

![](https://miro.medium.com/max/30/1*-VHMCjHHrUHP8IZp81QVWg.png?q=20)

![](https://miro.medium.com/max/547/1*-VHMCjHHrUHP8IZp81QVWg.png)

Here’s our function in Python:

![](https://miro.medium.com/max/30/1*JMsrindK3s5WRdexERApfg.png?q=20)

![](https://miro.medium.com/max/827/1*JMsrindK3s5WRdexERApfg.png)

Full code is available on my GitHub

If you don’t have an API key in Quandl, sign up for an account to get an API key— it is free. You don’t necessarily need an API key for this, but if you make enough queries they will time you out.

Anyhow, here’s what the output looks like in Python:

![](https://miro.medium.com/max/30/1*NGALRYn96BEk7B5YuwMb2A.png?q=20)

![](https://miro.medium.com/max/520/1*NGALRYn96BEk7B5YuwMb2A.png)

Passing “WIKI/AAPL” through “grab_from_quandl”, will return the data as expected.

Just in case an incorrect code is input, I added a custom handler:

![](https://miro.medium.com/max/30/1*ij8Q4PLotRBMRMz1cV0VDg.png?q=20)

![](https://miro.medium.com/max/368/1*ij8Q4PLotRBMRMz1cV0VDg.png)

Output of error handler.

Let’s port this Python function over to R.

![](https://miro.medium.com/max/30/1*6ONxL2Oitq_cqYebHivMxw.png?q=20)

![](https://miro.medium.com/max/1622/1*6ONxL2Oitq_cqYebHivMxw.png)

All it takes is one line of code!

The “source_python” function essentially ports your Python code into R, which then will enable you to continue using your Python function in R:

![](https://miro.medium.com/max/30/1*TwJrlxUhUGiYUWgk9FJYuw.png?q=20)

![](https://miro.medium.com/max/706/1*TwJrlxUhUGiYUWgk9FJYuw.png)

The error handler works, too:

![](https://miro.medium.com/max/30/1*TstyFCWFiaIloSeyn8JYSw.png?q=20)

![](https://miro.medium.com/max/736/1*TstyFCWFiaIloSeyn8JYSw.png)

Now that we can run our Python code in R, we can use dplyr to wrangle the data and ggplot2 to visualize the results…

![](https://miro.medium.com/max/30/1*Ri61pAeolT9cTrrdl-uXTA.png?q=20)

![](https://miro.medium.com/max/1259/1*Ri61pAeolT9cTrrdl-uXTA.png)

Voila! There you have it. While this was a simple example, the benefits of the reticulate package in R are very broad in scope.

Hopefully you find this helpful. Give me a shout if you have questions about any of this..

_Joel Alcedo is a Data Scientist working at BNP Paribas in New York. Prior to his time at BNP Paribas, he worked at Porsche North America HQ, Virgin Galactic and Cantor Fitzgerald._

[**Source :**](https://medium.com/hackernoon/python-programming-in-r-baa513b01bc8)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM4NjMyNTc2Ml19
-->