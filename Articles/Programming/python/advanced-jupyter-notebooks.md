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
Hello World!
pandas==0.23.4
It is also possible to use Python variables in your shell commands by prepending a $ symbol consistent with bash style variable names.


message = 'This is nifty'
!echo $message

This is nifty

> [Source : ](https://www.dataquest.io/blog/advanced-jupyter-notebooks-tutorial/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODE4OTEwOTMwXX0=
-->