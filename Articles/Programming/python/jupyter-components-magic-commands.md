# Jupyter Notebook Tutorial: Installation, Components and Magic Commands

[Python For Trading](https://blog.quantinsti.com/tag/python-for-trading/)

Oct 09, 2019

19 min read

  

By  [Jay Parmar](https://www.linkedin.com/in/jay-parmar/)

This article on Jupyter Notebooks(previously known as IPython Notebooks), does not require any pre-requisite knowledge and does not assume any familiarity with the framework. This blog is an introductory article where I will primarily address the following questions:  
  
[![Python Basics Handbook](https://d1rwhvwstyk9gu.cloudfront.net/2019/07/Python-Handbook-CTA.png)](https://www.quantinsti.com/python-basics-handbook)

-   [What is Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#what)
-   [How to install the Jupyter Notebook environment?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#install)
-   [How to run or open Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#run)
-   [What are the different components of Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#components)
-   [What are cells in a Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#cells)
-   [How to write in Markdown language?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#markdown)
-   [What are the magic commands in Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#commands)
-   [How to download and share Jupyter Notebook?](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/#share)

After reading this blog, you will be able to:

-   Install the Jupyter Notebook environment
-   Open Jupyter Notebook
-   Understand various components
-   Download and share Juypter Notebooks

Along with the above questions, you will also learn writing in Markdown language in Jupyter notebooks. Let's get started with the first question.

### What is Jupyter Notebook?

If you are a student, you must be using a class notebook to take various class notes, or if you are a business professional, you might be using a writing pad to pen down important notes, either for your purpose or to present to someone else. The typical content that goes in a student's notebook can be text in various formats such as  **bold**  and  _italic_, or a table, a mathematical equation, or creative stuff like hand-drawn images and so on. Not to forget that if it's a programmer's notebook, it will also contain a lot of programming code.

Now, you want to continue with this practice of writing all such stuff in a single place online. Jupyter notebook comes to the rescue here. It is a web-based platform that allows you to write narrative text in various formats, include a table or an image, write equations and code in various programming languages, all in one place. Apart from this, Jupyter notebook also allows you to write LaTeX code, include HTML code and embed a YouTube video. I will talk about how to do so in a bit, but first let's see what its  [official documentation](https://jupyter.org/documentation)  says:

> The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. Uses include data cleaning and transformation, numerical simulation, statistical modelling, data visualization, machine learning, and much more.

You can refer to the below-given list to get an intuitive idea about how a Jupyter notebook looks like:

-   [Support Vector Classifier](https://github.com/goquantra/introduction-to-machine-learning-for-trading/blob/master/section-4/unit-8-notebook-support-vector-classifier-strategy.ipynb)
-   [Trade Analysis](https://github.com/QuantInsti/EPAT/blob/master/Statistical%20Arbitrage/Trade%20Analysis.ipynb)
-   [Sun Pharma Vs HDFC Bank](https://github.com/QuantInsti/quantrautil/blob/master/Sun%20Pharma%20Vs%20HDFC%20Bank.ipynb)

A backdrop: The  _Jupyter Notebook_  is one of two facets of the Jupyter project which started to develop open-source, open-standards for interactive computing across dozens of programming languages. Another being  _JupyterLab_  which is the advanced version of Jupyter Notebook interface. However, both operate in a similar fashion.

Now that you have an idea about what Jupyter notebooks are, let's see its installation process.

### How to install Jupyter environment?

`jupyter notebook`

If the above command fails, you can continue reading this section. Otherwise, you can safely skip this and proceed to the next section. In case the command fails and you get the error similar (not exact) to the one shown below, continue with this section to understand the installation process.

![Jupyter Notebook](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/jupyter_command_not_found-1.png)

Two popular methods using which Python can be installed on your workstation. They are

1.  Installing Python using Anaconda Distribution
2.  Installing Raw Python

While Jupyter runs code in many programming languages, Python is a requirement for installing the Jupyter Notebook.

### Installing Jupyter Notebook using Anaconda

If you have installed Python using Anaconda Distribution, you are good to go. Anaconda Distribution includes Python, the Jupyter Notebook, and other commonly used packages for the scientific community.

If you don't have any version of Python installed, the recommended way to install Python is using Anaconda Distribution. It should be pretty simple to get Python installed.

-   First, download the latest version of Anaconda Distribution.
-   Second, install the downloaded version of Anaconda.

Bam! You have installed Jupyter Notebook. To check whether the installation is successful or not, and run the Jupyter Notebook, run the following command in the Anaconda prompt or command prompt (Windows) or terminal (Mac/Linux).

`jupyter notebook`

If you get an error upon running the above command (which should not happen), try the following method.

### Installing Jupyter Notebook using pip

When you install Python directly from its  [official website](https://www.python.org/), it does not include Jupyter Notebook in its standard library. In this case, you need to install Jupyter Notebook using the pip. The process is as follows:

1.  Open a new command prompt (Windows) or terminal (Mac/Linux)
2.  Execute the following command to install Jupyter Notebook

`python -m pip install jupyter`  
  
or if you are using Python 3  
  
`python3 -m pip install jupyter`  
  
or simply  
  
`pip install jupyter`

Congratulations, you have installed Jupyter Notebook! Onward to running it.

### How to run or open Jupyter Notebooks?

After you have installed the Jupyter Notebook on your computer, you are ready to run the notebook server.

If you are reading this article from the beginning, then you might already know how to run Jupyter Notebook. However, if you have skipped the previous sections and directly jumped here, the below mentioned steps shows how to run the Jupyter Notebook.

First, open a new command prompt (Windows) or terminal (Mac/Linux) on your workstation, and second, execute the following command:

`jupyter notebook`

Upon executing the above command, the terminal or command prompt will print some information about the Jupyter Notebooks being loaded. It might look something like as shown in the below snapshot. Be mindful that the information printed would be different for each workstation.

![Jupyter Server](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/jupyter_server.png)

Keep the terminal open as it is. It will then open the default web browser with the URL mentioned in the command prompt or terminal.

When the notebook opens in your browser, you will see the  _Notebook Homepage_  as shown in the below snapshot. This will list the notebook files and subdirectories in the directory where the notebook server was started.

![Jupyter Home Page](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/jupyter_home_page.png)

In case you are using Anaconda distribution for Python, you can open  Anaconda Navigator  (using the Start Menu(Windows), Applications folder(Mac), or Softwares folder(Linux)) shown below which allows you to open Jupyter Notebook using point and click.

![Anaconda Navigator](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/anaconda_navigator.png)

Once the Navigator application is open, you can click on the Launch button within the Notebook dialogue to launch the Jupyter Notebook application. Upon clicking the Launch button, you will be presented by the homepage that we'd seen earlier.

Now, let's understand how Jupyter environment works, I won't be going technical, though. As the Jupyter Notebook is a web application, it works on a server-client architecture. When you execute the command  `jupyter notebook`, the Jupyter software starts the server locally in the console where the command is executed, and the Jupyter Notebook homepage that opens in the web browser works as the client. Whatever you perform, that is, create or upload a new notebook, or save the existing one, the client notebook on which you are working, will keep communicating with the server running in the console/command line.

To keep notebooks running smoothly, we need to keep the command prompt or terminal open, even after it has opened homepage. If you close it, notebooks that you are working with, won't be able to communicate with the local server, and hence, any work you do, will not be saved on persistent memory.

The next step is to learn various components of Jupyter software.

### What are the different components of Jupyter notebooks?

I assume that you are following the chronological order of this article. If so, then you have learned what Jupyter notebooks are, how to install it, and how to run and open it. If not, then I would recommend you to go through them to get an overall picture. Nevertheless, if you are already familiar with those parts, go on and keep learning.

In this section, I will explain the various components of Jupyter software. When you start Jupyter Notebook application, and you'll be presented with the homepage. Let's start exploring it. Below shown is the snapshot of the homepage that you'd seen earlier, but with numbers assigned to each component to make our learning easier.

![Jupyter Home Page](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/jupyter_home_page_numbered.png)

Here's the description of each numbered point shown in the snapshot.

1.  It is the  _URL_  on which Jupyter server is running. If you are running the Jupyter on localhost, this would be the same URL shown in the console when you started Jupyter software.
2.  The  _Files_  tab lists the directories and files in the home folder, which usually is the home directory of the user logged in to the computer.
3.  The  _Running_  tab shows you a list of all open notebooks. When you start a new notebook or open an existing notebook, a kernel will get attached to it. All such running kernels will be listed under this tab.
4.  If you want to open an existing Jupyter notebook(that ends with .ipynb extension), it needs to be listed in the Files tab. If it is not listed, you need to upload it using the  _Upload_  button which will open a file browser for you to load the file.
5.  _Quit_  and  _Logout_  buttons allow you to logout and shutdown the server. When you quit, all the opened notebooks will be closed, and the server will get shutdown.
6.  The  _New_  button allows you to create a new notebook, text file, folder, or terminal. The snapshot shown below shows that you can create a notebook in Python, Julia, and R language. The notebook that you create will be associated with a respective kernel. When you install Jupyter environment as shown in the previous section, it is very likely that you will have only one option for the kernel, that is, Python. In order to add new languages, you can refer to  this link.

![Create New Notebook](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/new_button.png)

You can create a new notebook by clicking on the respective language name. Regardless of what language you choose, the new notebook that you create will have the same appearance. The difference would be in terms of the kernel attached to it. If I click on  _Python 3_  on the dropdown opened, a new notebook with Python kernel attached to it will be created. The empty Jupyter notebook is shown in the snapshot below.  _(Obviously without numbers :p)_

![Empty Jupyter Notebook](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/a_new_notebook.png)

The newly created notebook has various components which are explained below:

1.  The  _title_  is the name of the notebook. The title you set becomes the file name for the notebook, and it will have the extension as  _.ipynb_  which stands for  _IPython NoteBook_.
2.  The  _checkpoint_  shows you the time when your notebook was saved last.
3.  The  _menu bar_  lists various menus that allow you to download the notebook(in multiple formats), open a new notebook, edit the notebook, customise the headers, manipulate cells, nudge the kernel, access help and so on.
4.  The  _shortcut bar_  lists commonly used shortcuts such as  _save_  to save the notebook,  _add a cell_,  _cut_,  _copy_  to manipulate cells,  _up_  and  _down_  to navigate between cells,  _run_  to execute the cell, and so on. Any extension that you add to Jupyter will have its shortcut on this bar. We will learn what extensions are in the latter part of this article.
5.  The  _Kernel_  shows you the current kernel associated with the notebook. In our case, the kernel is  _Python 3_. The circle beside the kernel shows the status of the kernel. The hollow circle represents that it is ready to take input and run a cell. When a kernel is executing code or processing anything, it changes to solid.
6.  A  _cell_  is the part of a notebook where all the magic happens. Cells are explained in detail in the following section.

### What are cells in a Jupyter Notebook?

Any text or code that you write goes in the cell. Cells are the building block of any Jupyter notebook. Cells operate in two modes:  _command_  and  _edit_  mode, and they are of mainly three types:  _code_,  _markdown_, and  _Raw NBConvert_.

The  _command_  mode allows you to manipulate cells. That is, the action you perform has to do with the cell as a whole. The command mode is represented by a grey border around the cell with a blue indication, as shown in the below snapshot.

![Command Cell](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/a_cell_in_a_command_mode.PNG)

Some of the operations (along with their shortcuts) that you can perform when a cell is in the command mode are as follows:

-   _Insert_  a new cell -- Key in  `A`  to insert a new cell above, and  `B`  to insert a new cell below the current cell.
    -   When a new cell is inserted, it will be a code type cell, by default. We will look at various types in a while.
-   _Merge_  existing cells --  `Shift-M`  allows to merge selected cells or to merge the current cell with the cell below the current cell.
-   _Copy_  cells --  `C`  copies selected cells.
-   _Cut_  cells --  `X`  cuts selected cells.
-   _Paste_  cells -- Use  `Shift-V`  to paste cells.
-   _Delete_  existing dells -- Pressing  `D`,  `D`  deletes the current cell. Be careful with this shortcut.
-   _Change_  the type of a cell -- The shortcut  `Y`  changes the cell type to  _code_,  `M`  changes the cell type to  _markdown_, and  `R`  changes the cell type to  _raw_.
-   _Convert_  the cell to a heading -- There are six heading types in a Jupyter notebook. This works with  _markdown_  cell type only. Heading 1 is the largest heading and heading 6 is the smallest heading.  `1`,  `2`,  `3`,  `4`,  `5`, and  `6`  are used to change the cell type to the respective heading size.
-   _Find and Replace_  in existing cells -- Pressing  `F`  opens find and replace dialogue box.
-   _Save_  and mark the  _Checkpoint_  of the notebook -- Use  `Shift-S`  to save the notebook.
-   _Toggle_  line numbers in a cell -- Pressing  `L`  toggles line number in the current cell.
-   _Toggle_  the output of a cell --  `O`  allows you to toggle the output of the current cell.
-   _Interrupt the kernel_  -- Keying  `I`,  `I`  interrupts the kernel. That is, if any process is being executed by the kernel gets stopped.
-   _Scroll_  the notebook --  `Space`  scrolls the notebook down,  `Shift-Space`  scrolls the notebook up.
-   _Enter_  the edit mode -- Pressing  `return`  key changes the mode of a cell to the edit mode.

The shortcuts mentioned above work only in the  _command_  mode cells. Another mode that a Jupyter notebook cell supports is the  _edit_  mode. This mode specifically allows you to edit the content of a cell and work with it. You can enter into the edit mode of a cell by pressing the  `return`  key or by a mouse click inside a cell. The border around cell changes to Green when the cell is in the  _edit_  mode, as shown in the below snapshot.

![Cell in the edit mode](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/a_cell_in_the_edit_mode.png)

Once the cell is in  _edit_  mode, you can start writing code or text. The below-mentioned are some of the operations that you can perform while the cell is in the  _edit_  mode.

-   _Auto-Completion_  of code -- Use  `Tab`  key to use this facility. It works only for code type cells. In markdown cells, it will simply put tab spaces.
-   _Indentation_  of code -- Jupyter notebooks inherently perform indentation whenever required. However, if you want to change indentation manually, use  `Ctrl-]`  to indent the code in code type cells. In markdown cells, it will insert spaces according to the specifications of the tab key.
-   _Dedentation_  of code -- Anytime you want to dedent the code, use  `Ctrl-[`  to do so. In markdown cells, this shortcut works similar to  `Shift-Tab`  and dedents the content.
-   _Commenting_  a code -- Use  `Ctrl-/`  to comment a code. In markdown cells, this shortcut does not have any effect.
-   _Execute of a cell_  -- Once you write code or text in the cell, you need to execute it to process the content written by you. There are three primary ways to do so.
    -   _Run the current cell and select the next cell_  - Use  `Shift-Enter`  to perform this action.
    -   _Run selected cells_  - Use  `Ctrl-Enter`  to run selected cells or the current cell.
    -   _Run the current cell and insert a new cell_  - Press  `Alt-Enter`  to execute the current cell and insert the new cell below the current cell.
-   _Split a cell_  -- Use the shortcut  `Ctrl-Shift-Minus`  to split the current cell into two separate cells at the cursor.
-   _Entering a Command Mode_  -- Use  `Ctrl-M`  or press  `Esc`  key to exit from the edit mode and enter into the command mode.

By now, you have already encountered  _code_  and  _markdown_  cell types quite a few times. In case you are not aware of the two, now is the time where I will explain them in detail. I will restrict the discussion for these two types only; I won't be covering the  _Raw NBConvert_  type in this article.

Jupyter notebook cells can be multiple types. Often used types are  _code_  and  _markdown_. The code type cells allow you to write live programming code. That is, you can perform any sort of programming in them. Once you run or execute a code cell, Jupyter notebook will present the output just below the cell. This is shown in the below snapshot.

![Cell Output](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/cell_output.png)

In contrast, whatever written in the markdown cell, will get printed in the cell itself, as shown below:

![Code and Markdown](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/code_and_markdown.png)

There are two cells in the above snapshot. The first cell numbered four, is the code cell, which allows tying in Python code as we are working with Python kernel notebook. The next cell is the markdown cell where the normal text is written.

As can be seen, code cells have a number associated with them, whereas markdown cells do not have any numbering. Numbering code cells helps in two ways: First, it shows the sequence in which code executed, and second, it allows us to differentiate between the code cells and markdown cells visually. Now that you know the basics of cells and their workings, let's see how you can use markdown.

### How to write down in Markdown in Jupyter Notebook?

It is the markdown functionality that brings interactivity to Jupyter environment. Markdown cells not only lets you write text, but it allows you to format it, add a hyperlink, and include HTML code. Additionally, it also allows you to define ordered and unordered lists, insert images and tables, add mathematical equations, write in LaTex, and so on. It even allows you to write programming code within the text without losing any syntax.

Once you have a markdown cell (you can use the shortcut  `M`  in command mode to convert a code cell to markdown cell), you can start writing the text the way you want. Below-mentioned are the functionalities supported by markdown cells.

### Headings

To create headings, use the hash symbol  `#`  followed by a space and the heading. Doing so creates a title or level 1 heading. If you want to create a sub-heading, use  `##`  followed by a space and the sub-heading. The notebook allows creating headings up to six levels. Each level will have the equivalent number of  `#`  marks, as shown below:

`# Heading 1`  - Title  
`## Heading 2`  - Heading  
`### Heading 3`  - Sub-heading  
`#### Heading 4`  - Heading at level four  
`##### Heading 5`  - Heading at level five  
`###### Heading 6`  - Heading at level six

### Emphasis

You can make text  _italic_  by surrounding it with  `*`  or  `_`.

Input

Output

`*This is italic text.*`

_This is italic text._

`_This is italic text._`

_This is italic text._

You can make text  **bold**  by surrounding it with  `**`  or  `__`.

Input

Output

`**This is italic text.**`

**This is italic text.**

`__This is italic text.__`

**This is italic text.**

### Monospace Fonts

If you want to refer to some code, filename, or file path within the text, you can use monospace fonts to differentiate the normal text and the  `monospace`  fonts. You can do so by surrounding the text with a single back quotation mark. (`)

`This is written in monospace fonts.`

### Line Breaks

You can use the HTML line break tag  `<br>`  to insert the carriage-return within a line to break it.

### Font Color

You can change the color of text by using the HTML font tag along with its  _color_  attribute. For example, to color the text in blue, you can use the following code:

`<font color='blue'>The color of this text is blue.</font>`

The output of the above code is shown below:

The color of this text is blue.

Change the color attribute of the  `font`  tag to change the text color. Remember, not all markdown text works with the font tag. Hence, review it carefully.

### Blockquotes

Use a greater than sign  `>`  followed by a space to type or insert a blockquote. The output will be indented with Grey horizontal line to the left of it. For example, the output of the line  `> Jupyter makes life easy!`  will be as follows:

> Jupyter makes life easy!

### Unordered Lists

You can create an unordered list using the minus or dash sign  `-`  followed by an item name. The next time goes on the next line.

`- Item 1`  
`- Item 2`  
`- Item 3`

To create a sub list, the same procedure is followed; however, with an indentation. Can you create a list as shown below:

-   Item 1
    -   Item 1.1
    -   Item 1.2
        -   Item 1.2.1
-   Item 2
    -   Item 2.1
    -   Item 2.2

In Jupyter, the first-level list items would generally have solid circles, the next level would have solid squares and the subsequent levels would have hollow circles.

### Ordered Lists

Ordered lists can be created by manually specifying the item number such as  `1`  followed by a dot and space, and finally, item name. To create a sub-list, the procedure would be the same.

1.  Chapter 1
    1.  Section 1.1
2.  Chapter 2
    1.  Section 2.1
    2.  Section 2.2

### Horizontal Lines

You can create a horizontal line by using three asterisks  `***`.

----------

### Hyperlinks

You can convert any normal text into a hyperlink by surrounding it with square brackets followed by the actual link in parenthesis. For example,

`[QuantInsti's Blog]([https://blog.quantinsti.com](https://blog.quantinsti.com/))`

will result in

[QuantInsti's Blog](https://blog.quantinsti.com/)

### Images

The format to insert an image in a markdown cell is very similar to that of hyperlinks. Only the difference is that it prefixes  `!`  before the content. First, the exclamation mark followed by the name of the image in square brackets, and finally URL in the parenthesis. This is shown below:

`![QuantInsti's Logo]([https://dt99qig9iutro.cloudfront.net/production/images/header-logo-green.png](https://dt99qig9iutro.cloudfront.net/production/images/header-logo-green.png))`

Alternatively, you can use the HTML image tag to insert an image as shown below:

`<img src="[https://dt99qig9iutro.cloudfront.net/production/images/header-logo-green.png](https://dt99qig9iutro.cloudfront.net/production/images/header-logo-green.png)" alt="QuantInsti's Logo">`

Both will produce the following result:

![QuantInsti's Logo](https://dt99qig9iutro.cloudfront.net/production/images/header-logo-green.png)

### Geometric Shapes

A UTF-8 Geometric Shape can be included in a Jupyter notebook by using its decimal reference number. Use the following format to insert any of the shapes.

`&#reference_number;`

A black circle can be inserted, as shown below:

●

### Programming Code

You can embed programming code within the text using triple backticks followed by programming language name and ending by triple backticks. Below is the example for Python code embedded within the text.

```python
def func(x):
    return x**2
```

Similarly, the programming code for another language can be written. For example, below code is for Javascript.

```javascript
console.log('Hello World!')
```

### LaTeX Equations

By courtesy of MathJax, you can include mathematical expressions either inline or separately in markdown cells. To type inline, equations are surrounded by  `$`. To print equations separately on a new line, they are surrounded by  `$$`. For example, the formula to calculate the mean value can be written as

`$$\mu = \frac{1}{n}\sum_{i=1}^{n} x_i $$`

which results in the following:

![Latex_equation1](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/Latex1.PNG)

Inline equations can be written as  `$x_t = \phi x_{t-1} + \epsilon_t$`  which results in

![Latex_equation2](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/Latex2.PNG)

You can refer to  [this](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)  thread which lists various LaTeX commands that can be used in markdown cells.

### Tables

You can create tables in markdown cells, as shown below:

```
|This|is|
|-|-|
|a|table|
```

Columns are separated by vertical bar  `|`  and rows are written in a new line. The above table is generated, as shown below:

This

is

a

table

### What are the magic commands in Jupyter Notebook?

Jupyter notebook software comes with a bunch of built-in commands which adds interactivity while working with it. They are called magic commands in Jupyter environment. These commands are dependent on the interpreter or kernel with which you are working. To see which magic commands are available, you can run the following magic command in the code cell:

`%lsmagic`

These magic commands are prefixed with the  `%`  value. Following are some of the commonly used magic commands along with their functionality:

-   `%autosave`  command autosaves your notebook periodically.
    
    # Save notebook every 60 seconds
    %autosave 60
    
-   `%cd`  changes the current working directory to the new directory given as an argument.
-   `%clear`  and  `%cls`  command clear the output of the current cell.
-   `%env`allows you to list all environment variables as well as set the value of particular environment variables.
-   `%history`  shows the history of the previously executed magic commands.
    
    %history
    
-   `%ls`  lists the content of the current directory.
    
    %ls
    
-   `%matplotlib`  allows you to plot charts inline within a notebook.
    
    %matplotlib inline
    
-   `%notebook`  command adds the interactivity while plotting charts.
-   `%pdb`  allows you to debug the code. This magic command is the Jupyter version of Python debugger.
-   `%pip`  enables you to list and install all available packages from Jupyter environment.
    
    %pip install pandas
    
-   `%who`  list all variables from the global scope.
    
    stock = 'AAPL'
    price = 222.15
    %who str
    
-   `%load`  inserts the code from an external script.
    
    %load ./hello_world.py
    
-   `%run`  allows you to run Python code.
    
    %run ./sample_notebook.ipynb
    
-   `%time`  displays the time taken by a cell for execution.

If you are using Anaconda Python, then magic commands mentioned above should work without any issue. Otherwise, you may require to install the following packages:

-   ipython-sql
-   cython

### How to download and share Jupyter Notebook?

Being a programmer, you often want the work that you have done to be shared with other colleagues. Keeping this in mind, Jupyter environment allows you to download files in multiple formats such as HTML file(.html), LaTeX file(.tex), GitHub flavoured Markdown file(.md), PDF file(.pdf), reStructured file(.rst), and so on. The  _Download as_  option in the File menu allows you to download the notebook in a format of your choice, as shown below:

![Jupyter Download Option](https://d1rwhvwstyk9gu.cloudfront.net/2019/10/jupyter_download_option.png)

When you download a notebook, it will be downloaded in whatever state it is. That is the output of executed cells, any error that you might have as an output will be as it is. Hence, it is essential that you make a notebook ready to be shared. To do so, you can perform the following steps:

1.  Go to  _Cell_  menu, select  _All Output_  option, and finally choose the  _Clear_  option. This action will clear the output of all cells.
2.  Next, go to  _Kernel_  menu, and select the  _Restart & Run All_  option. This action will restart the kernel and execute all cells.

After performing the above steps, ensure that the notebook is in the state in which you would like to share with others.

Besides exporting notebooks to your local workstation, you can create, list and load it on GitHub Gists. Gists are a way to share your work on the cloud. You can find more information  [here](https://github.com/mozilla/jupyter-notebook-gist).

Also, you can use  [JupyerHub](https://github.com/jupyterhub/jupyterhub), which serves Jupyter notebooks to multiple users. In other words, it is the hosting platform for notebooks on a server with multiple users.

Additionally, you can use the  [nbviewer](https://github.com/jupyter/nbviewer)  to render Jupyter notebooks as static web pages. Platforms such as  [RISE](https://github.com/damianavila/RISE)  and  [nbpresent](https://github.com/Anaconda-Platform/nbpresent)  allow you to convert Jupyter notebooks to slideshows.

## Final Thoughts

I hope this introductory guide to Jupyter notebooks provides you with the foundation. In this relatively a multi-part article, First, I started with the explanation of Jupyter notebook, its installation process, running locally on your workstation and so on. Next, during the process, you also got exposed to various components of Jupyter notebooks and keyboard shortcuts. Then, you learnt writing in markdown language. After that, you learnt various magic commands in Jupyter notebook. Finally, you learnt how to download and share Jupyter notebooks.

Thanks for reading.

There are many people who might be new to Python or programming in general or never created any trading strategy. The learning curve could be steep if you are a beginner in both these skills. However, you can build the required skills gradually and practice regularly on the hands-on learning exercises given in our course by enrolling here:  [Algorithmic Trading for Everyone](https://quantra.quantinsti.com/learning-track/algorithmic-trading-for-everyone).

If you want to learn various aspects of Algorithmic trading then check out our  [Executive Programme in Algorithmic Trading (EPAT®)](https://www.quantinsti.com/epat/). The course covers training modules like Statistics & Econometrics, Financial Computing & Technology, and Algorithmic & Quantitative Trading. EPAT® is designed to equip you with the right skill sets to be a successful trader.  [Enroll now](https://www.quantinsti.com/epat/)!

_Disclaimer: All data and information provided in this article are for informational purposes only. QuantInsti® makes no representations as to accuracy, completeness, currentness, suitability, or validity of any information in this article and will not be liable for any errors, omissions, or delays in this information or any losses, injuries, or damages arising from its display or use. All information is provided on an as-is basis._


> [Source : ](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDUzOTk1MzBdfQ==
-->