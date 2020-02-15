---
bookFlatSection: true
title: Web Scraping NBA Stats
bookToc: true 

---

![enter image description here](https://www.dataquest.io/wp-content/uploads/2019/01/1-LPnY8nOLg4S6_TG0DEXwsg-1.png)

Lying at the heart of modern data science and analysis is the Jupyter project lifecycle. Whether you’re rapidly prototyping ideas, demonstrating your work, or producing fully fledged reports, notebooks can provide an efficient edge over IDEs or traditional desktop applications.

Following on from  [Jupyter Notebook for Beginners: A Tutorial](https://www.dataquest.io/blog/jupyter-notebook-tutorial/), this guide will be a Jupyter Notebooks tutorial that takes you on a journey from the truly vanilla to the downright dangerous. That’s right! Jupyter’s wacky world of out-of-order execution has the power to faze, and when it comes to running notebooks inside notebooks, things can get complicated fast.

This Jupyter Notebooks tutorial aims to straighten out some sources of confusion and spread ideas that pique your interest and spark your imagination. There are already plenty of  [great listicles](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)  of neat tips and tricks, so here we will take a more thorough look at Jupyter’s offerings.

This will involve:

-   Warming up with the basics of shell commands and some handy magics, including a look at debugging, timing, and executing multiple languages.
-   Exploring topics like logging, macros, running external code, and Jupyter extensions.
-   Seeing how to enhance charts with Seaborn, beautify notebooks with themes and CSS, and customise notebook output.
-   Finishing off with a deep look at topics like scripted execution, automated reporting pipelines, and working with databases.

If you’re a JupyterLab fan, you’ll be pleased to hear that 99% of this is still applicable and the only difference is that some Jupyter Notebook extensions aren’t compatible with JuputerLab. Fortunately,  [awesome](https://github.com/mauhai/awesome-jupyterlab)  [alternatives](https://github.com/topics/jupyterlab-extension)  are already cropping up on GitHub.

Now we’re ready to become Jupyter wizards!

## Shell Commands

Every user will benefit at least from time-to-time from the ability to interact directly with the operating system from within their notebook. Any line in a code cell that you begin with an exclamation mark will be executed as a shell command. This can be useful when dealing with datasets or other files, and managing your Python packages. As a simple illustration:

```py
!echo Hello World!!
pip freeze | grep pandas
```
```py
Hello World!
pandas==0.23.4
```
It is also possible to use Python variables in your shell commands by prepending a $ symbol consistent with bash style variable names.

```py
message = 'This is nifty'
!echo $message
```
```py
This is nifty
```
Note that the shell in which ! commands are executed is discarded after execution completes, so commands like cd will have no effect. However, IPython magics offer a solution.

Basic Magics
Magics are handy commands built into the IPython kernel that make it easier to perform particular tasks. Although they often resemble unix commands, under the hood they are all implemented in Python. There exist far more magics than it would make sense to cover here, but it’s worth highlighting a variety of examples. We will start with a few basics before moving on to more interesting cases.

There are two categories of magic: line magics and cell magics. Respectively, they act on a single line or can be spread across multiple lines or entire cells. To see the available magics, you can do the following:

%lsmagic
Available line magics:

Available cell magics:%%! %%HTML %%SVG %%bash %%capture %%cmd %%debug %%file %%html %%javascript %%js %%latex %%markdown %%perl %%prun %%pypy %%python %%python2 %%python3 %%ruby %%script %%sh %%svg %%sx %%system %%time %%timeit %%writefile
Automagic is ON, % prefix IS NOT needed for line magics.
As you can see, there are loads! Most are listed in the official documentation, which is intended as a reference but can be somewhat obtuse in places. Line magics start with a percent character %, and cell magics start with two, %%.

It’s worth noting that ! is really just a fancy magic syntax for shell commands, and as you may have noticed IPython provides magics in place of those shell commands that alter the state of the shell and are thus lost by !. Examples include %cd, %alias and %env.

Let’s go through some more examples.

> [Source : ](https://www.dataquest.io/blog/advanced-jupyter-notebooks-tutorial/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI3ODI2MTQ0XX0=
-->