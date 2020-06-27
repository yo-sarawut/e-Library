## The __future__ module

Python 3.x introduced some Python 2-incompatible keywords and features that can be imported via the in-built __future__ module in Python 2. It is recommended to use __future__ imports, if you are planning Python 3.x support for your code.

For example, if we want Python 3.x's integer division behavior in Python 2, add the following import statement.

from __future__ import division

## The print Function

Most notable and most widely known change in Python 3 is how the  **print**  function is used. Use of parenthesis () with print function is now mandatory. It was optional in Python 2.

print  "Hello World"  #is acceptable in Python 2  print  ("Hello World")  # in Python 3, print must be followed by ()

The print() function inserts a new line at the end, by default. In Python 2, it can be suppressed by putting ',' at the end. In Python 3, "end =' '" appends space instead of newline.

print x,  # Trailing comma suppresses newline in Python 2  print(x,  end=" ")  # Appends a space instead of a newline in Python 3

## Reading Input from Keyboard

Python 2 has two versions of input functions,  **input()**  and  **raw_input()**. The input() function treats the received data as string if it is included in quotes '' or "", otherwise the data is treated as number.

In Python 3, raw_input() function is deprecated. Further, the received data is always treated as string.

In  Python  2  >>> x = input('something:') something:10  #entered data is treated as number  >>> x 10  >>> x = input('something:') something:'10'  #entered data is treated as string  >>> x '10'  >>> x = raw_input("something:") something:10  #entered data is treated as string even without ''  >>> x '10'  >>> x = raw_input("something:") something:'10'  #entered data treated as string including ''  >>> x "'10'"  In  Python  3  >>> x = input("something:") something:10  >>> x '10'  >>> x = input("something:") something:'10'  #entered data treated as string with or without ''  >>> x "'10'"  >>> x = raw_input("something:")  # will result NameError  Traceback  (most recent call last):  File  "<pyshell#3>", line 1,  in  <module> x = raw_input("something:")  NameError: name 'raw_input'  is  not  defined

## Integer Division

In Python 2, the result of division of two integers is rounded to the nearest integer. As a result, 3/2 will show 1. In order to obtain a floating-point division, numerator or denominator must be explicitly used as float. Hence, either 3.0/2 or 3/2.0 or 3.0/2.0 will result in 1.5

Python 3 evaluates 3 / 2 as 1.5 by default, which is more intuitive for new programmers.

## Unicode Representation

Python 2 requires you to mark a string with a u if you want to store it as Unicode.

Python 3 stores strings as Unicode, by default. We have Unicode (utf-8) strings, and 2 byte classes: byte and byte arrays.

## xrange() Function Removed

In Python 2 range() returns a list, and xrange() returns an object that will only generate the items in the range when needed, saving memory.

In Python 3, the range() function is removed, and xrange() has been renamed as range(). In addition, the range() object supports slicing in Python 3.2 and later.

## raise exception

Python 2 accepts both notations, the 'old' and the 'new' syntax; Python 3 raises a SyntaxError if we do not enclose the exception argument in parenthesis.

raise  IOError,  "file error"  #This is accepted in Python 2  raise  IOError("file error")  #This is also accepted in Python 2  raise  IOError,  "file error"  #syntax error is raised in Python 3  raise  IOError("file error")  #this is the recommended syntax in Python 3

## Arguments in Exceptions

In Python 3, arguments to exception should be declared with 'as' keyword.

except  Myerror, err:  # In Python2  except  Myerror  as err:  #In Python 3

## next() Function and .next() Method

In Python 2, next() as a method of generator object, is allowed. In Python 2, the next() function, to iterate over generator object, is also accepted. In Python 3, however, next(0 as a generator method is discontinued and raises AttributeError.

gen =  (letter for letter in  'Hello World')  # creates generator object  next(my_generator)  #allowed in Python 2 and Python 3 my_generator.next()  #allowed in Python 2. raises AttributeError in Python 3

## 2to3 Utility

Along with Python 3 interpreter, 2to3.py script is usually installed in tools/scripts folder. It reads Python 2.x source code and applies a series of fixers to transform it into a valid Python 3.x code.

Here  is a sample Python  2 code (area.py):  def area(x,y =  3.14): a = y*x*x print a return a

a = area(10)  print  "area",a To convert into  Python  3 version: $2to3 -w area.py Converted code :  def area(x,y =  3.14):  # formal parameters a = y*x*x print  (a)  return a

a = area(10)  print("area",a)

# Python 3 - Overview

Python is a high-level, interpreted, interactive and object-oriented scripting language. Python is designed to be highly readable. It uses English keywords frequently whereas the other languages use punctuations. It has fewer syntactical constructions than other languages.

-   **Python is Interpreted**  − Python is processed at runtime by the interpreter. You do not need to compile your program before executing it. This is similar to PERL and PHP.
    
-   **Python is Interactive**  − You can actually sit at a Python prompt and interact with the interpreter directly to write your programs.
    
-   **Python is Object-Oriented**  − Python supports Object-Oriented style or technique of programming that encapsulates code within objects.
    
-   **Python is a Beginner's Language**  − Python is a great language for the beginner-level programmers and supports the development of a wide range of applications from simple text processing to WWW browsers to games.
    

## History of Python

Python was developed by Guido van Rossum in the late eighties and early nineties at the National Research Institute for Mathematics and Computer Science in the Netherlands.

-   Python is derived from many other languages, including ABC, Modula-3, C, C++, Algol-68, SmallTalk, and Unix shell and other scripting languages.
    
-   Python is copyrighted. Like Perl, Python source code is now available under the GNU General Public License (GPL).
    
-   Python is now maintained by a core development team at the institute, although Guido van Rossum still holds a vital role in directing its progress.
    
-   Python 1.0 was released in November 1994. In 2000, Python 2.0 was released. Python 2.7.11 is the latest edition of Python 2.
    
-   Meanwhile, Python 3.0 was released in 2008. Python 3 is not backward compatible with Python 2. The emphasis in Python 3 had been on the removal of duplicate programming constructs and modules so that "There should be one -- and preferably only one -- obvious way to do it." Python 3.5.1 is the latest version of Python 3.
    

## Python Features

Python's features include −

-   **Easy-to-learn**  − Python has few keywords, simple structure, and a clearly defined syntax. This allows a student to pick up the language quickly.
    
-   **Easy-to-read**  − Python code is more clearly defined and visible to the eyes.
    
-   **Easy-to-maintain**  − Python's source code is fairly easy-to-maintain.
    
-   **A broad standard library**  − Python's bulk of the library is very portable and cross-platform compatible on UNIX, Windows, and Macintosh.
    
-   **Interactive Mode**  − Python has support for an interactive mode which allows interactive testing and debugging of snippets of code.
    
-   **Portable**  − Python can run on a wide variety of hardware platforms and has the same interface on all platforms.
    
-   **Extendable**  − You can add low-level modules to the Python interpreter. These modules enable programmers to add to or customize their tools to be more efficient.
    
-   **Databases**  − Python provides interfaces to all major commercial databases.
    
-   **GUI Programming**  − Python supports GUI applications that can be created and ported to many system calls, libraries and windows systems, such as Windows MFC, Macintosh, and the X Window system of Unix.
    
-   **Scalable**  − Python provides a better structure and support for large programs than shell scripting.
    

Apart from the above-mentioned features, Python has a big list of good features. A, few are listed below −

-   It supports functional and structured programming methods as well as OOP.
    
-   It can be used as a scripting language or can be compiled to byte-code for building large applications.
    
-   It provides very high-level dynamic data types and supports dynamic type checking.
    
-   It supports automatic garbage collection.
    
-   It can be easily integrated with C, C++, COM, ActiveX, CORBA, and Java.
    

# Python 3 - Environment Setup

Python 3 is available for Windows, Mac OS and most of the flavors of Linux operating system. Even though Python 2 is available for many other OSs, Python 3 support either has not been made available for them or has been dropped.

## Local Environment Setup

Open a terminal window and type "python" to find out if it is already installed and which version is installed.

## Getting Python

### Windows platform

Binaries of latest version of Python 3 (Python 3.5.1) are available on  [this download page](https://www.python.org/downloads/windows/)

The following different installation options are available.

-   Windows x86-64 embeddable zip file
-   Windows x86-64 executable installer
-   Windows x86-64 web-based installer
-   Windows x86 embeddable zip file
-   Windows x86 executable installer
-   Windows x86 web-based installer

**Note**  − In order to install Python 3.5.1, minimum OS requirements are Windows 7 with SP1. For versions 3.0 to 3.4.x Windows XP is acceptable.

### Linux platform

Different flavors of Linux use different package managers for installation of new packages.

On Ubuntu Linux, Python 3 is installed using the following command from the terminal.

$sudo apt-get install python3-minimal

Installation from source

Download Gzipped source tarball from Python's download URL −  [https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tgz](https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tgz)

Extract the tarball
tar xvfz Python-3.5.1.tgz  Configure  and  Install: cd Python-3.5.1  ./configure --prefix =  /opt/python3.5.1 make  
sudo make install

### Mac OS

Download Mac OS installers from this URL −  [https://www.python.org/downloads/mac-osx/](https://www.python.org/downloads/mac-osx/)

-   Mac OS X 64-bit/32-bit installer − python-3.5.1-macosx10.6.pkg
-   Mac OS X 32-bit i386/PPC installer − python-3.5.1-macosx10.5.pkg

Double click this package file and follow the wizard instructions to install.

The most up-to-date and current source code, binaries, documentation, news, etc., is available on the official website of Python −

**Python Official Website**  −  [https://www.python.org/](https://www.python.org/)

You can download Python documentation from the following site. The documentation is available in HTML, PDF and PostScript formats.

**Python Documentation Website**  −  [www.python.org/doc/](https://www.python.org/doc/)

## Setting up PATH

Programs and other executable files can be in many directories. Hence, the operating systems provide a search path that lists the directories that it searches for executables.

The important features are −

-   The path is stored in an environment variable, which is a named string maintained by the operating system. This variable contains information available to the command shell and other programs.
    
-   The path variable is named as  **PATH**  in Unix or  **Path**  in Windows (Unix is case-sensitive; Windows is not).
    
-   In Mac OS, the installer handles the path details. To invoke the Python interpreter from any particular directory, you must add the Python directory to your path.
    

## Setting Path at Unix/Linux

To add the Python directory to the path for a particular session in Unix −

-   **In the csh shell**  − type setenv PATH "$PATH:/usr/local/bin/python3" and press Enter.
    
-   **In the bash shell (Linux)**  − type export PYTHONPATH=/usr/local/bin/python3.4 and press Enter.
    
-   **In the sh or ksh shell**  − type PATH="$PATH:/usr/local/bin/python3" and press Enter.
    

**Note**  − /usr/local/bin/python3 is the path of the Python directory.

## Setting Path at Windows

To add the Python directory to the path for a particular session in Windows −

-   **At the command prompt**  − type path %path%;C:\Python and press Enter.
    

**Note**  − C:\Python is the path of the Python directory

## Python Environment Variables

Here are important environment variables, which are recognized by Python −

Sr.No.

Variable & Description

1

**PYTHONPATH**

It has a role similar to PATH. This variable tells the Python interpreter where to locate the module files imported into a program. It should include the Python source library directory and the directories containing Python source code. PYTHONPATH is sometimes preset by the Python installer.

2

**PYTHONSTARTUP**

It contains the path of an initialization file containing Python source code. It is executed every time you start the interpreter. It is named as .pythonrc.py in Unix and it contains commands that load utilities or modify PYTHONPATH.

3

**PYTHONCASEOK**

It is used in Windows to instruct Python to find the first case-insensitive match in an import statement. Set this variable to any value to activate it.

4

**PYTHONHOME**

It is an alternative module search path. It is usually embedded in the PYTHONSTARTUP or PYTHONPATH directories to make switching module libraries easy.

## Running Python

There are three different ways to start Python −

### Interactive Interpreter

You can start Python from Unix, DOS, or any other system that provides you a command-line interpreter or shell window.

Enter  **python**  the command line.

Start coding right away in the interactive interpreter.

$python             # Unix/Linux
or
python%             # Unix/Linux
or
C:>python           # Windows/DOS

Here is the list of all the available command line options −

Sr.No.

Option & Description

1

**-d**

provide debug output

2

**-O**

generate optimized bytecode (resulting in .pyo files)

3

**-S**

do not run import site to look for Python paths on startup

4

**-v**

verbose output (detailed trace on import statements)

5

**-X**

disable class-based built-in exceptions (just use strings); obsolete starting with version 1.6

6

**-c cmd**

run Python script sent in as cmd string

7

**file**

run Python script from given file

### Script from the Command-line

A Python script can be executed at the command line by invoking the interpreter on your application, as shown in the following example.

$python  script.py # Unix/Linux  or python% script.py # Unix/Linux  or C:>python script.py # Windows/DOS

**Note**  − Be sure the file permission mode allows execution.

### Integrated Development Environment

You can run Python from a Graphical User Interface (GUI) environment as well, if you have a GUI application on your system that supports Python.

-   **Unix**  − IDLE is the very first Unix IDE for Python.
    
-   **Windows**  −  **PythonWin**  is the first Windows interface for Python and is an IDE with a GUI.
    
-   **Macintosh**  − The Macintosh version of Python along with the IDLE IDE is available from the main website, downloadable as either MacBinary or BinHex'd files.
    

If you are not able to set up the environment properly, then you can take the help of your system admin. Make sure the Python environment is properly set up and working perfectly fine.

**Note**  − All the examples given in subsequent chapters are executed with Python 3.4.1 version available on Windows 7 and Ubuntu Linux.

We have already set up Python Programming environment online, so that you can execute all the available examples online while you are learning theory. Feel free to modify any example and execute it online.

# Python 3 - Basic Syntax

The Python language has many similarities to Perl, C, and Java. However, there are some definite differences between the languages.

## First Python Program

Let us execute the programs in different modes of programming.

### Interactive Mode Programming

Invoking the interpreter without passing a script file as a parameter brings up the following prompt −

$ python Python  3.3.2  (default,  Dec  10  2013,  11:35:01)  [GCC 4.6.3] on Linux  Type  "help",  "copyright",  "credits",  or  "license"  for more information.  >>>  On  Windows:  Python  3.4.3  (v3.4.3:9b73f1c3e601,  Feb  24  2015,  22:43:06)  [MSC v.1600  32 bit (Intel)] on win32 Type  "copyright",  "credits"  or  "license()"  for more information.  >>>

Type the following text at the Python prompt and press Enter −

>>>  print  ("Hello, Python!")

If you are running the older version of Python (Python 2.x), use of parenthesis as  **inprint**  function is optional. This produces the following result −

Hello, Python!

### Script Mode Programming

Invoking the interpreter with a script parameter begins execution of the script and continues until the script is finished. When the script is finished, the interpreter is no longer active.

Let us write a simple Python program in a script. Python files have the extension  **.py**. Type the following source code in a test.py file −

[Live Demo](http://tpcg.io/GBhBAj)

print  ("Hello, Python!")

We assume that you have the Python interpreter set in  **PATH**  variable. Now, try to run this program as follows −

**On Linux**

$ python test.py 

This produces the following result −

Hello, Python!

**On Windows**

C:\Python34>Python test.py

This produces the following result −

Hello, Python!

Let us try another way to execute a Python script in Linux. Here is the modified test.py file −

[Live Demo](http://tpcg.io/LheT18)

#!/usr/bin/python3  print  ("Hello, Python!")

We assume that you have Python interpreter available in the /usr/bin directory. Now, try to run this program as follows −

$ chmod +x test.py # This is to make file executable $./test.py

This produces the following result −

Hello, Python!

## Python Identifiers

A Python identifier is a name used to identify a variable, function, class, module or other object. An identifier starts with a letter A to Z or a to z or an underscore (_) followed by zero or more letters, underscores and digits (0 to 9).

Python does not allow punctuation characters such as @, $, and % within identifiers. Python is a case sensitive programming language. Thus,  **Manpower**  and  **manpower**  are two different identifiers in Python.

Here are naming conventions for Python identifiers −

-   Class names start with an uppercase letter. All other identifiers start with a lowercase letter.
    
-   Starting an identifier with a single leading underscore indicates that the identifier is private.
    
-   Starting an identifier with two leading underscores indicates a strong private identifier.
    
-   If the identifier also ends with two trailing underscores, the identifier is a language-defined special name.
    

## Reserved Words

The following list shows the Python keywords. These are reserved words and you cannot use them as constants or variables or any other identifier names. All the Python keywords contain lowercase letters only.

and

exec

not

as

finally

or

assert

for

pass

break

from

print

class

global

raise

continue

if

return

def

import

try

del

in

while

elif

is

with

else

lambda

yield

except

## Lines and Indentation

Python does not use braces({}) to indicate blocks of code for class and function definitions or flow control. Blocks of code are denoted by line indentation, which is rigidly enforced.

The number of spaces in the indentation is variable, but all statements within the block must be indented the same amount. For example −

if  True:  print  ("True")  else:  print  ("False")

However, the following block generates an error −

if  True:  print  ("Answer")  print  ("True")  else:  print  "(Answer")  print  ("False")

Thus, in Python all the continuous lines indented with the same number of spaces would form a block. The following example has various statement blocks −

**Note**  − Do not try to understand the logic at this point of time. Just make sure you understood the various blocks even if they are without braces.

#!/usr/bin/python3  import sys

file_finish =  "end" file_text =  "" contents=[] file_name=input("Enter filename: ")  if len(file_name)  ==  0:  print("Please enter filename") sys.exit()  try:  # open file stream file = open(file_name,  "w")  except  IOError:  print  ("There was an error writing to", file_name) sys.exit()  print  ("Enter '", file_finish,)  print  ("' When finished")  while file_text != file_finish: file_text = input("Enter text: ") contents.append(file_text)  if file_text == file_finish:  # close the file file.close()  break  print(contents) data =  ' '.join([str(elem)  for elem in contents])  print(data) file.write(data) file.close() file_name = input("Enter filename: ")  if len(file_name)  ==  0:  print  ("Next time please enter something") sys.exit()  try: file = open(file_name,  "r")  except  IOError:  print  ("There was an error reading file") sys.exit() file_text = file.read() file.close()  print  (file_text)

## Multi-Line Statements

Statements in Python typically end with a new line. Python, however, allows the use of the line continuation character (\) to denote that the line should continue. For example −

total = item_one + \
        item_two + \
        item_three

The statements contained within the [], {}, or () brackets do not need to use the line continuation character. For example −

days =  ['Monday',  'Tuesday',  'Wednesday',  'Thursday',  'Friday']

## Quotation in Python

Python accepts single ('), double (") and triple (''' or """) quotes to denote string literals, as long as the same type of quote starts and ends the string.

The triple quotes are used to span the string across multiple lines. For example, all the following are legal −

word =  'word' sentence =  "This is a sentence." paragraph =  """This is a paragraph. It is
made up of multiple lines and sentences."""

## Comments in Python

A hash sign (#) that is not inside a string literal is the beginning of a comment. All characters after the #, up to the end of the physical line, are part of the comment and the Python interpreter ignores them.

[Live Demo](http://tpcg.io/e9zmst)

#!/usr/bin/python3  # First comment  print  ("Hello, Python!")  # second comment

This produces the following result −

Hello,  Python!

You can type a comment on the same line after a statement or expression −

name =  "Madisetti"  # This is again comment

Python does not have multiple-line commenting feature. You have to comment each line individually as follows −

# This is a comment.  # This is a comment, too.  # This is a comment, too.  # I said that already.

## Using Blank Lines

A line containing only whitespace, possibly with a comment, is known as a blank line and Python totally ignores it.

In an interactive interpreter session, you must enter an empty physical line to terminate a multiline statement.

## Waiting for the User

The following line of the program displays the prompt and, the statement saying “Press the enter key to exit”, and then waits for the user to take action −

#!/usr/bin/python3 input("\n\nPress the enter key to exit.")

Here, "\n\n" is used to create two new lines before displaying the actual line. Once the user presses the key, the program ends. This is a nice trick to keep a console window open until the user is done with an application.

## Multiple Statements on a Single Line

The semicolon ( ; ) allows multiple statements on a single line given that no statement starts a new code block. Here is a sample snip using the semicolon −

import sys; x =  'foo'; sys.stdout.write(x +  '\n')

## Multiple Statement Groups as Suites

Groups of individual statements, which make a single code block are called  **suites**  in Python. Compound or complex statements, such as if, while, def, and class require a header line and a suite.

Header lines begin the statement (with the keyword) and terminate with a colon ( : ) and are followed by one or more lines which make up the suite. For example −

if expression : suite elif expression : suite else  : suite

## Command Line Arguments

Many programs can be run to provide you with some basic information about how they should be run. Python enables you to do this with -**h**  −

$ python -h
usage: python [option]  ...  [-c cmd |  -m mod | file |  -]  [arg]  ...  Options  and arguments (and corresponding environment variables):  -c cmd : program passed in  as  string  (terminates option list)  -d : debug output from parser (also PYTHONDEBUG=x)  -E : ignore environment variables (such as PYTHONPATH)  -h :  print  this help message and  exit  [ etc.  ]

You can also program your script in such a way that it should accept various options.  [Command Line Arguments](https://www.tutorialspoint.com/python3/python_command_line_arguments.htm)  is an advanced topic. Let us understand it.

# Python 3 - Variable Types

Variables are nothing but reserved memory locations to store values. It means that when you create a variable, you reserve some space in the memory.

Based on the data type of a variable, the interpreter allocates memory and decides what can be stored in the reserved memory. Therefore, by assigning different data types to the variables, you can store integers, decimals or characters in these variables.

## Assigning Values to Variables

Python variables do not need explicit declaration to reserve memory space. The declaration happens automatically when you assign a value to a variable. The equal sign (=) is used to assign values to variables.

The operand to the left of the = operator is the name of the variable and the operand to the right of the = operator is the value stored in the variable. For example −

[Live Demo](http://tpcg.io/DF7KqE)

#!/usr/bin/python3 counter =  100  # An integer assignment miles =  1000.0  # A floating point name =  "John"  # A string  print  (counter)  print  (miles)  print  (name)

Here, 100, 1000.0 and "John" are the values assigned to counter, miles, and name variables, respectively. This produces the following result −

100
1000.0
John

## Multiple Assignment

Python allows you to assign a single value to several variables simultaneously.

For example −

a = b = c = 1

Here, an integer object is created with the value 1, and all the three variables are assigned to the same memory location. You can also assign multiple objects to multiple variables. For example −

a, b, c = 1, 2, "john"

Here, two integer objects with values 1 and 2 are assigned to the variables a and b respectively, and one string object with the value "john" is assigned to the variable c.

## Standard Data Types

The data stored in memory can be of many types. For example, a person's age is stored as a numeric value and his or her address is stored as alphanumeric characters. Python has various standard data types that are used to define the operations possible on them and the storage method for each of them.

Python has five standard data types −

-   Numbers
-   String
-   List
-   Tuple
-   Dictionary

## Python Numbers

Number data types store numeric values. Number objects are created when you assign a value to them. For example −

var1 = 1
var2 = 10

You can also delete the reference to a number object by using the  **del**  statement. The syntax of the  **del**  statement is −

del var1[,var2[,var3[....,varN]]]]

You can delete a single object or multiple objects by using the  **del**  statement.

For example −

del var
del var_a, var_b

Python supports three different numerical types −

-   int (signed integers)
-   float (floating point real values)
-   complex (complex numbers)

All integers in Python3 are represented as long integers. Hence, there is no separate number type as long.

### Examples

Here are some examples of numbers −

int

float

complex

10

0.0

3.14j

100

15.20

45.j

-786

-21.9

9.322e-36j

080

32.3+e18

.876j

-0490

-90.

-.6545+0J

-0x260

-32.54e100

3e+26J

0x69

70.2-E12

4.53e-7j

A complex number consists of an ordered pair of real floating-point numbers denoted by x + yj, where x and y are real numbers and j is the imaginary unit.

## Python Strings

Strings in Python are identified as a contiguous set of characters represented in the quotation marks. Python allows either pair of single or double quotes. Subsets of strings can be taken using the slice operator ([ ] and [:] ) with indexes starting at 0 in the beginning of the string and working their way from -1 to the end.

The plus (+) sign is the string concatenation operator and the asterisk (*) is the repetition operator. For example −

[Live Demo](http://tpcg.io/I93mP1)

#!/usr/bin/python3 str =  'Hello World!'  print  (str)  # Prints complete string  print  (str[0])  # Prints first character of the string  print  (str[2:5])  # Prints characters starting from 3rd to 5th  print  (str[2:])  # Prints string starting from 3rd character  print  (str *  2)  # Prints string two times  print  (str +  "TEST")  # Prints concatenated string

This will produce the following result −

Hello World!
H
llo
llo World!
Hello World!Hello World!
Hello World!TEST

## Python Lists

Lists are the most versatile of Python's compound data types. A list contains items separated by commas and enclosed within square brackets ([]). To some extent, lists are similar to arrays in C. One of the differences between them is that all the items belonging to a list can be of different data type.

The values stored in a list can be accessed using the slice operator ([ ] and [:]) with indexes starting at 0 in the beginning of the list and working their way to end -1. The plus (+) sign is the list concatenation operator, and the asterisk (*) is the repetition operator. For example −

[Live Demo](http://tpcg.io/qZUZTc)

#!/usr/bin/python3 list =  [  'abcd',  786  ,  2.23,  'john',  70.2  ] tinylist =  [123,  'john']  print  (list)  # Prints complete list  print  (list[0])  # Prints first element of the list  print  (list[1:3])  # Prints elements starting from 2nd till 3rd  print  (list[2:])  # Prints elements starting from 3rd element  print  (tinylist *  2)  # Prints list two times  print  (list + tinylist)  # Prints concatenated lists

This produces the following result −

['abcd', 786, 2.23, 'john', 70.200000000000003]
abcd
[786, 2.23]
[2.23, 'john', 70.200000000000003]
[123, 'john', 123, 'john']
['abcd', 786, 2.23, 'john', 70.200000000000003, 123, 'john']

## Python Tuples

A tuple is another sequence data type that is similar to the list. A tuple consists of a number of values separated by commas. Unlike lists, however, tuples are enclosed within parenthesis.

The main difference between lists and tuples are − Lists are enclosed in brackets ( [ ] ) and their elements and size can be changed, while tuples are enclosed in parentheses ( ( ) ) and cannot be updated. Tuples can be thought of as  **read-only**  lists. For example −

[Live Demo](http://tpcg.io/ZvI4k3)

#!/usr/bin/python3 tuple =  (  'abcd',  786  ,  2.23,  'john',  70.2  ) tinytuple =  (123,  'john')  print  (tuple)  # Prints complete tuple  print  (tuple[0])  # Prints first element of the tuple  print  (tuple[1:3])  # Prints elements starting from 2nd till 3rd  print  (tuple[2:])  # Prints elements starting from 3rd element  print  (tinytuple *  2)  # Prints tuple two times  print  (tuple + tinytuple)  # Prints concatenated tuple

This produces the following result −

('abcd', 786, 2.23, 'john', 70.200000000000003)
abcd
(786, 2.23)
(2.23, 'john', 70.200000000000003)
(123, 'john', 123, 'john')
('abcd', 786, 2.23, 'john', 70.200000000000003, 123, 'john')

The following code is invalid with tuple, because we attempted to update a tuple, which is not allowed. Similar case is possible with lists −

#!/usr/bin/python3 tuple =  (  'abcd',  786  ,  2.23,  'john',  70.2  ) list =  [  'abcd',  786  ,  2.23,  'john',  70.2  ] tuple[2]  =  1000  # Invalid syntax with tuple list[2]  =  1000  # Valid syntax with list

## Python Dictionary

Python's dictionaries are kind of hash-table type. They work like associative arrays or hashes found in Perl and consist of key-value pairs. A dictionary key can be almost any Python type, but are usually numbers or strings. Values, on the other hand, can be any arbitrary Python object.

Dictionaries are enclosed by curly braces ({ }) and values can be assigned and accessed using square braces ([]). For example −

[Live Demo](http://tpcg.io/N2CwyM)

#!/usr/bin/python3 dict =  {} dict['one']  =  "This is one" dict[2]  =  "This is two" tinydict =  {'name':  'john','code':6734,  'dept':  'sales'}  print  (dict['one'])  # Prints value for 'one' key  print  (dict[2])  # Prints value for 2 key  print  (tinydict)  # Prints complete dictionary  print  (tinydict.keys())  # Prints all the keys  print  (tinydict.values())  # Prints all the values

This produces the following result −

This is one
This is two
{'name': 'john', 'dept': 'sales', 'code': 6734}
dict_keys(['name', 'dept', 'code'])
dict_values(['john', 'sales', 6734])

Dictionaries have no concept of order among the elements. It is incorrect to say that the elements are "out of order"; they are simply unordered.

## Data Type Conversion

Sometimes, you may need to perform conversions between the built-in types. To convert between types, you simply use the type-names as a function.

There are several built-in functions to perform conversion from one data type to another. These functions return a new object representing the converted value.

Sr.No.

Function & Description

1

**int(x [,base])**

Converts x to an integer. The base specifies the base if x is a string.

2

**float(x)**

Converts x to a floating-point number.

3

**complex(real [,imag])**

Creates a complex number.

4

**str(x)**

Converts object x to a string representation.

5

**repr(x)**

Converts object x to an expression string.

6

**eval(str)**

Evaluates a string and returns an object.

7

**tuple(s)**

Converts s to a tuple.

8

**list(s)**

Converts s to a list.

9

**set(s)**

Converts s to a set.

10

**dict(d)**

Creates a dictionary. d must be a sequence of (key,value) tuples.

11

**frozenset(s)**

Converts s to a frozen set.

12

**chr(x)**

Converts an integer to a character.

13

**unichr(x)**

Converts an integer to a Unicode character.

14

**ord(x)**

Converts a single character to its integer value.

15

**hex(x)**

Converts an integer to a hexadecimal string.

16

**oct(x)**

Converts an integer to an octal string.

# Python 3 - Basic Operators

Operators are the constructs, which can manipulate the value of operands. Consider the expression 4 + 5 = 9. Here, 4 and 5 are called the operands and + is called the operator.

## Types of Operator

Python language supports the following types of operators −

-   Arithmetic Operators
-   Comparison (Relational) Operators
-   Assignment Operators
-   Logical Operators
-   Bitwise Operators
-   Membership Operators
-   Identity Operators

Let us have a look at all the operators one by one.

## Python Arithmetic Operators

Assume variable  **a**  holds the value 10 and variable  **b**  holds the value 21, then −

[Show Example](https://www.tutorialspoint.com/python3/arithmetic_operators_example.htm)

Operator

Description

Example

+ Addition

Adds values on either side of the operator.

a + b = 31

- Subtraction

Subtracts right hand operand from left hand operand.

a – b = -11

* Multiplication

Multiplies values on either side of the operator

a * b = 210

/ Division

Divides left hand operand by right hand operand

b / a = 2.1

% Modulus

Divides left hand operand by right hand operand and returns remainder

b % a = 1

** Exponent

Performs exponential (power) calculation on operators

a**b =10 to the power 20

//

Floor Division - The division of operands where the result is the quotient in which the digits after the decimal point are removed. But if one of the operands is negative, the result is floored, i.e., rounded away from zero (towards negative infinity):

9//2 = 4 and 9.0//2.0 = 4.0, -11//3 = -4, -11.0//3 = -4.0

## Python Comparison Operators

These operators compare the values on either side of them and decide the relation among them. They are also called Relational operators.

Assume variable  **a**  holds the value 10 and variable  **b**  holds the value 20, then −

[Show Example](https://www.tutorialspoint.com/python3/comparison_operators_example.htm)

Operator

Description

Example

==

If the values of two operands are equal, then the condition becomes true.

(a == b) is not true.

!=

If values of two operands are not equal, then condition becomes true.

(a!= b) is true.

>

If the value of left operand is greater than the value of right operand, then condition becomes true.

(a > b) is not true.

<

If the value of left operand is less than the value of right operand, then condition becomes true.

(a < b) is true.

>=

If the value of left operand is greater than or equal to the value of right operand, then condition becomes true.

(a >= b) is not true.

<=

If the value of left operand is less than or equal to the value of right operand, then condition becomes true.

(a <= b) is true.

## Python Assignment Operators

Assume variable  **a**  holds the value 10 and variable  **b**  holds the value 20, then −

[Show Example](https://www.tutorialspoint.com/python3/assignment_operators_example.htm)

Operator

Description

Example

=

Assigns values from right side operands to left side operand

c = a + b assigns value of a + b into c

+= Add AND

It adds right operand to the left operand and assign the result to left operand

c += a is equivalent to c = c + a

-= Subtract AND

It subtracts right operand from the left operand and assign the result to left operand

c -= a is equivalent to c = c - a

*= Multiply AND

It multiplies right operand with the left operand and assign the result to left operand

c *= a is equivalent to c = c * a

/= Divide AND

It divides left operand with the right operand and assign the result to left operand

c /= a is equivalent to c = c / ac /= a is equivalent to c = c / a

%= Modulus AND

It takes modulus using two operands and assign the result to left operand

c %= a is equivalent to c = c % a

**= Exponent AND

Performs exponential (power) calculation on operators and assign value to the left operand

c **= a is equivalent to c = c ** a

//= Floor Division

It performs floor division on operators and assign value to the left operand

c //= a is equivalent to c = c // a

## Python Bitwise Operators

Bitwise operator works on bits and performs bit-by-bit operation. Assume if a = 60; and b = 13; Now in binary format they will be as follows −

a = 0011 1100

b = 0000 1101

-----------------

a&b = 0000 1100

a|b = 0011 1101

a^b = 0011 0001

~a = 1100 0011

Python's built-in function bin() can be used to obtain binary representation of an integer number.

The following Bitwise operators are supported by Python language −

[Show Example](https://www.tutorialspoint.com/python3/bitwise_operators_example.htm)

Operator

Description

Example

& Binary AND

Operator copies a bit, to the result, if it exists in both operands

(a & b) (means 0000 1100)

| Binary OR

It copies a bit, if it exists in either operand.

(a | b) = 61 (means 0011 1101)

^ Binary XOR

It copies the bit, if it is set in one operand but not both.

(a ^ b) = 49 (means 0011 0001)

~ Binary Ones Complement

It is unary and has the effect of 'flipping' bits.

(~a ) = -61 (means 1100 0011 in 2's complement form due to a signed binary number.

<< Binary Left Shift

The left operand's value is moved left by the number of bits specified by the right operand.

a << 2 = 240 (means 1111 0000)

>> Binary Right Shift

The left operand's value is moved right by the number of bits specified by the right operand.

a >> 2 = 15 (means 0000 1111)

## Python Logical Operators

The following logical operators are supported by Python language. Assume variable  **a**  holds True and variable  **b**  holds False then −

[Show Example](https://www.tutorialspoint.com/python3/logical_operators_example.htm)

Operator

Description

Example

and Logical AND

If both the operands are true then condition becomes true.

(a and b) is False.

or Logical OR

If any of the two operands are non-zero then condition becomes true.

(a or b) is True.

not Logical NOT

Used to reverse the logical state of its operand.

Not(a and b) is True.

## Python Membership Operators

Python’s membership operators test for membership in a sequence, such as strings, lists, or tuples. There are two membership operators as explained below −

[Show Example](https://www.tutorialspoint.com/python3/membership_operators_example.htm)

Operator

Description

Example

in

Evaluates to true if it finds a variable in the specified sequence and false otherwise.

x in y, here in results in a 1 if x is a member of sequence y.

not in

Evaluates to true if it does not finds a variable in the specified sequence and false otherwise.

x not in y, here not in results in a 1 if x is not a member of sequence y.

## Python Identity Operators

Identity operators compare the memory locations of two objects. There are two Identity operators as explained below −

[Show Example](https://www.tutorialspoint.com/python3/identity_operators_example.htm)

Operator

Description

Example

is

Evaluates to true if the variables on either side of the operator point to the same object and false otherwise.

x is y, here  **is**  results in 1 if id(x) equals id(y).

is not

Evaluates to false if the variables on either side of the operator point to the same object and true otherwise.

x is not y, here  **is not**  results in 1 if id(x) is not equal to id(y).

## Python Operators Precedence

The following table lists all operators from highest precedence to the lowest.

[Show Example](https://www.tutorialspoint.com/python3/operators_precedence_example.htm)

Sr.No.

Operator & Description

1

******

Exponentiation (raise to the power)

2

**~ + -**

Complement, unary plus and minus (method names for the last two are +@ and -@)

3

*** / % //**

Multiply, divide, modulo and floor division

4

**+ -**

Addition and subtraction

5

**>> <<**

Right and left bitwise shift

6

**&**

Bitwise 'AND'

7

**^ |**

Bitwise exclusive `OR' and regular `OR'

8

**<= < > >=**

Comparison operators

9

**<> == !=**

Equality operators

10

**= %= /= //= -= += *= **=**

Assignment operators

11

**is is not**

Identity operators

12

**in not in**

Membership operators

13

**not or and**

Logical operators

# Python 3 - Decision Making

Decision-making is the anticipation of conditions occurring during the execution of a program and specified actions taken according to the conditions.

Decision structures evaluate multiple expressions, which produce TRUE or FALSE as the outcome. You need to determine which action to take and which statements to execute if the outcome is TRUE or FALSE otherwise.

Following is the general form of a typical decision making structure found in most of the programming languages −

![Decision making](https://www.tutorialspoint.com/python3/images/decision_making.jpg)

Python programming language assumes any  **non-zero**  and  **non-null**  values as TRUE, and any  **zero**  or  **null values**  as FALSE value.

Python programming language provides the following types of decision-making statements.

Sr.No.

Statement & Description

1

[if statements](https://www.tutorialspoint.com/python3/python_if_statement.htm)

An  **if statement**  consists of a boolean expression followed by one or more statements.

2

[if...else statements](https://www.tutorialspoint.com/python3/python_if_else.htm)

An  **if statement**  can be followed by an optional  **else statement**, which executes when the boolean expression is FALSE.

3

[nested if statements](https://www.tutorialspoint.com/python3/nested_if_statements_in_python.htm)

You can use one  **if**  or  **else if**  statement inside another  **if**  or  **else if**  statement(s).

Let us go through each decision-making statement quickly.

## Single Statement Suites

If the suite of an  **if**  clause consists only of a single line, it may go on the same line as the header statement.

### Example

Here is an example of a  **one-line if**  clause −

[Live Demo](http://tpcg.io/eJSqVe)

#!/usr/bin/python3  var  =  100  if  (  var  ==  100  )  :  print  ("Value of expression is 100")  print  ("Good bye!")

### Output

When the above code is executed, it produces the following result −

Value of expression is 100
Good bye!

# Python 3 - Loops

In general, statements are executed sequentially − The first statement in a function is executed first, followed by the second, and so on. There may be a situation when you need to execute a block of code several number of times.

Programming languages provide various control structures that allow more complicated execution paths.

A loop statement allows us to execute a statement or group of statements multiple times. The following diagram illustrates a loop statement −

![Loop Architecture](https://www.tutorialspoint.com/python3/images/loop_architecture.jpg)

Python programming language provides the following types of loops to handle looping requirements.

Sr.No.

Loop Type & Description

1

[while loop](https://www.tutorialspoint.com/python3/python_while_loop.htm "WHILE loop in Python")

Repeats a statement or group of statements while a given condition is TRUE. It tests the condition before executing the loop body.

2

[for loop](https://www.tutorialspoint.com/python3/python_for_loop.htm "FOR loop in Python")

Executes a sequence of statements multiple times and abbreviates the code that manages the loop variable.

3

[nested loops](https://www.tutorialspoint.com/python3/python_nested_loops.htm "nested loops in Python")

You can use one or more loop inside any another while, or for loop.

## Loop Control Statements

The Loop control statements change the execution from its normal sequence. When the execution leaves a scope, all automatic objects that were created in that scope are destroyed.

Python supports the following control statements.

Sr.No.

Control Statement & Description

1

[break statement](https://www.tutorialspoint.com/python3/python_break_statement.htm "break statement in Python")

Terminates the loop statement and transfers execution to the statement immediately following the loop.

2

[continue statement](https://www.tutorialspoint.com/python3/python_continue_statement.htm "continue statement in Python")

Causes the loop to skip the remainder of its body and immediately retest its condition prior to reiterating.

3

[pass statement](https://www.tutorialspoint.com/python3/python_pass_statement.htm "pass statement in Python")

The pass statement in Python is used when a statement is required syntactically but you do not want any command or code to execute.

Let us go through the loop control statements briefly.

## Iterator and Generator

**Iterator**  is an object which allows a programmer to traverse through all the elements of a collection, regardless of its specific implementation. In Python, an iterator object implements two methods,  **iter()**  and  **next()**.

String, List or Tuple objects can be used to create an Iterator.

list =  [1,2,3,4] it = iter(list)  # this builds an iterator object  print  (next(it))  #prints next available element in iterator  Iterator  object can be traversed using regular for statement !usr/bin/python3 for x in it:  print  (x,  end=" ")  or  using  next()  function  while  True:  try:  print  (next(it))  except  StopIteration: sys.exit()  #you have to import sys module for this

A  **generator**  is a function that produces or yields a sequence of values using yield method.

When a generator function is called, it returns a generator object without even beginning execution of the function. When the next() method is called for the first time, the function starts executing until it reaches the yield statement, which returns the yielded value. The yield keeps track i.e. remembers the last execution and the second next() call continues from previous value.

### Example

The following example defines a generator, which generates an iterator for all the Fibonacci numbers.

#!usr/bin/python3  import sys def fibonacci(n):  #generator function a, b, counter =  0,  1,  0  while  True:  if  (counter > n):  return  yield a
      a, b = b, a + b
      counter +=  1 f = fibonacci(5)  #f is iterator object  while  True:  try:  print  (next(f),  end=" ")  except  StopIteration: sys.exit()

# Python 3 - Numbers

Number data types store numeric values. They are immutable data types. This means, changing the value of a number data type results in a newly allocated object.

Number objects are created when you assign a value to them. For example −

var1 =  1 var2 =  10

You can also delete the reference to a number object by using the  **del**  statement. The syntax of the  **del**  statement is −

del var1[,var2[,var3[....,varN]]]]

You can delete a single object or multiple objects by using the  **del**  statement. For example −

del  var  del var_a, var_b

Python supports different numerical types −

-   **int (signed integers)**  − They are often called just integers or  **ints**. They are positive or negative whole numbers with no decimal point. Integers in Python 3 are of unlimited size. Python 2 has two integer types - int and long. There is no '**long integer**' in Python 3 anymore.
    
-   **float (floating point real values)**  − Also called floats, they represent real numbers and are written with a decimal point dividing the integer and the fractional parts. Floats may also be in scientific notation, with E or e indicating the power of 10 (2.5e2 = 2.5 x 102  = 250).
    
-   **complex (complex numbers)**  − are of the form a + bJ, where a and b are floats and J (or j) represents the square root of -1 (which is an imaginary number). The real part of the number is a, and the imaginary part is b. Complex numbers are not used much in Python programming.
    

It is possible to represent an integer in hexa-decimal or octal form

>>> number =  0xA0F  #Hexa-decimal  >>> number 2575  >>> number =  0o37  #Octal  >>> number 31

### Examples

Here are some examples of numbers.

int

float

complex

10

0.0

3.14j

100

15.20

45.j

-786

-21.9

9.322e-36j

080

32.3+e18

.876j

-0490

-90.

-.6545+0J

-0×260

-32.54e100

3e+26J

0×69

70.2-E12

4.53e-7j

A complex number consists of an ordered pair of real floating-point numbers denoted by a + bj, where a is the real part and b is the imaginary part of the complex number.

## Number Type Conversion

Python converts numbers internally in an expression containing mixed types to a common type for evaluation. Sometimes, you need to coerce a number explicitly from one type to another to satisfy the requirements of an operator or function parameter.

-   Type  **int(x)**  to convert x to a plain integer.
    
-   Type  **long(x)**  to convert x to a long integer.
    
-   Type  **float(x)**  to convert x to a floating-point number.
    
-   Type  **complex(x)**  to convert x to a complex number with real part x and imaginary part zero.
    
-   Type  **complex(x, y)**  to convert x and y to a complex number with real part x and imaginary part y. x and y are numeric expressions
    

## Mathematical Functions

Python includes the following functions that perform mathematical calculations.

Sr.No.

Function & Returns ( Description )

1

[abs(x)](https://www.tutorialspoint.com/python3/number_abs.htm)

The absolute value of x: the (positive) distance between x and zero.

2

[ceil(x)](https://www.tutorialspoint.com/python3/number_ceil.htm)

The ceiling of x: the smallest integer not less than x.

3

**cmp(x, y)**

-1 if x < y, 0 if x == y, or 1 if x > y.  **Deprecated**  in Python 3. Instead use  **return (x>y)-(x<y)**.

4

[exp(x)](https://www.tutorialspoint.com/python3/number_exp.htm)

The exponential of x: ex

5

[fabs(x)](https://www.tutorialspoint.com/python3/number_fabs.htm)

The absolute value of x.

6

[floor(x)](https://www.tutorialspoint.com/python3/number_floor.htm)

The floor of x: the largest integer not greater than x.

7

[log(x)](https://www.tutorialspoint.com/python3/number_log.htm)

The natural logarithm of x, for x > 0.

8

[log10(x)](https://www.tutorialspoint.com/python3/number_log10.htm)

The base-10 logarithm of x for x > 0.

9

[max(x1, x2,...)](https://www.tutorialspoint.com/python3/number_max.htm)

The largest of its arguments: the value closest to positive infinity

10

[min(x1, x2,...)](https://www.tutorialspoint.com/python3/number_min.htm)

The smallest of its arguments: the value closest to negative infinity.

11

[modf(x)](https://www.tutorialspoint.com/python3/number_modf.htm)

The fractional and integer parts of x in a two-item tuple. Both parts have the same sign as x. The integer part is returned as a float.

12

[pow(x, y)](https://www.tutorialspoint.com/python3/number_pow.htm)

The value of x**y.

13

[round(x [,n])](https://www.tutorialspoint.com/python3/number_round.htm)

**x**  rounded to n digits from the decimal point. Python rounds away from zero as a tie-breaker: round(0.5) is 1.0 and round(-0.5) is -1.0.

14

[sqrt(x)](https://www.tutorialspoint.com/python3/number_sqrt.htm)

The square root of x for x > 0.

## Random Number Functions

Random numbers are used for games, simulations, testing, security, and privacy applications. Python includes the following functions that are commonly used.

Sr.No.

Function & Description

1

[choice(seq)](https://www.tutorialspoint.com/python3/number_choice.htm)

A random item from a list, tuple, or string.

2

[randrange ([start,] stop [,step])](https://www.tutorialspoint.com/python3/number_randrange.htm)

A randomly selected element from range(start, stop, step).

3

[random()](https://www.tutorialspoint.com/python3/number_random.htm)

A random float r, such that 0 is less than or equal to r and r is less than 1

4

[seed([x])](https://www.tutorialspoint.com/python3/number_seed.htm)

Sets the integer starting value used in generating random numbers. Call this function before calling any other random module function. Returns None.

5

[shuffle(lst)](https://www.tutorialspoint.com/python3/number_shuffle.htm)

Randomizes the items of a list in place. Returns None.

6

[uniform(x, y)](https://www.tutorialspoint.com/python3/number_uniform.htm)

A random float r, such that x is less than or equal to r and r is less than y.

## Trigonometric Functions

Python includes the following functions that perform trigonometric calculations.

Sr.No.

Function & Description

1

[acos(x)](https://www.tutorialspoint.com/python3/number_acos.htm)

Return the arc cosine of x, in radians.

2

[asin(x)](https://www.tutorialspoint.com/python3/number_asin.htm)

Return the arc sine of x, in radians.

3

[atan(x)](https://www.tutorialspoint.com/python3/number_atan.htm)

Return the arc tangent of x, in radians.

4

[atan2(y, x)](https://www.tutorialspoint.com/python3/number_atan2.htm)

Return atan(y / x), in radians.

5

[cos(x)](https://www.tutorialspoint.com/python3/number_cos.htm)

Return the cosine of x radians.

6

[hypot(x, y)](https://www.tutorialspoint.com/python3/number_hypot.htm)

Return the Euclidean norm, sqrt(x*x + y*y).

7

[sin(x)](https://www.tutorialspoint.com/python3/number_sin.htm)

Return the sine of x radians.

8

[tan(x)](https://www.tutorialspoint.com/python3/number_tan.htm)

Return the tangent of x radians.

9

[degrees(x)](https://www.tutorialspoint.com/python3/number_degrees.htm)

Converts angle x from radians to degrees.

10

[radians(x)](https://www.tutorialspoint.com/python3/number_radians.htm)

Converts angle x from degrees to radians.

## Mathematical Constants

The module also defines two mathematical constants −

Sr.No.

Constants & Description

1

**pi**

The mathematical constant pi.

2

**e**

The mathematical constant e.

# Python 3 - Strings

Strings are amongst the most popular types in Python. We can create them simply by enclosing characters in quotes. Python treats single quotes the same as double quotes. Creating strings is as simple as assigning a value to a variable. For example −

var1 =  'Hello World!' var2 =  "Python Programming"

## Accessing Values in Strings

Python does not support a character type; these are treated as strings of length one, thus also considered a substring.

To access substrings, use the square brackets for slicing along with the index or indices to obtain your substring. For example −

[Live Demo](http://tpcg.io/53XKOs)

#!/usr/bin/python3 var1 =  'Hello World!' var2 =  "Python Programming"  print  ("var1[0]: ", var1[0])  print  ("var2[1:5]: ", var2[1:5])

When the above code is executed, it produces the following result −

var1[0]:  H
var2[1:5]:  ytho

## Updating Strings

You can "update" an existing string by (re)assigning a variable to another string. The new value can be related to its previous value or to a completely different string altogether. For example −

[Live Demo](http://tpcg.io/pDICcS)

#!/usr/bin/python3 var1 =  'Hello World!'  print  ("Updated String :- ", var1[:6]  +  'Python')

When the above code is executed, it produces the following result −

Updated String :-  Hello Python

## Escape Characters

Following table is a list of escape or non-printable characters that can be represented with backslash notation.

An escape character gets interpreted; in a single quoted as well as double quoted strings.

Backslash notation

Hexadecimal character

Description

\a

0x07

Bell or alert

\b

0x08

Backspace

\cx

Control-x

\C-x

Control-x

\e

0x1b

Escape

\f

0x0c

Formfeed

\M-\C-x

Meta-Control-x

\n

0x0a

Newline

\nnn

Octal notation, where n is in the range 0.7

\r

0x0d

Carriage return

\s

0x20

Space

\t

0x09

Tab

\v

0x0b

Vertical tab

\x

Character x

\xnn

Hexadecimal notation, where n is in the range 0.9, a.f, or A.F

## String Special Operators

Assume string variable  **a**  holds 'Hello' and variable  **b**  holds 'Python', then −

Operator

Description

Example

+

Concatenation - Adds values on either side of the operator

a + b will give HelloPython

*

Repetition - Creates new strings, concatenating multiple copies of the same string

a*2 will give -HelloHello

[]

Slice - Gives the character from the given index

a[1] will give e

[ : ]

Range Slice - Gives the characters from the given range

a[1:4] will give ell

in

Membership - Returns true if a character exists in the given string

H in a will give 1

not in

Membership - Returns true if a character does not exist in the given string

M not in a will give 1

r/R

Raw String - Suppresses actual meaning of Escape characters. The syntax for raw strings is exactly the same as for normal strings with the exception of the raw string operator, the letter "r," which precedes the quotation marks. The "r" can be lowercase (r) or uppercase (R) and must be placed immediately preceding the first quote mark.

print r'\n' prints \n and print R'\n'prints \n

%

Format - Performs String formatting

See at next section

## String Formatting Operator

One of Python's coolest features is the string format operator %. This operator is unique to strings and makes up for the pack of having functions from C's printf() family. Following is a simple example −

[Live Demo](http://tpcg.io/5lu2E8)

#!/usr/bin/python3  print  ("My name is %s and weight is %d kg!"  %  ('Zara',  21))  

When the above code is executed, it produces the following result −

My name is Zara and weight is 21 kg!

Here is the list of complete set of symbols which can be used along with % −

Sr.No.

Format Symbol & Conversion

1

**%c**

character

2

**%s**

string conversion via str() prior to formatting

3

**%i**

signed decimal integer

4

**%d**

signed decimal integer

5

**%u**

unsigned decimal integer

6

**%o**

octal integer

7

**%x**

hexadecimal integer (lowercase letters)

8

**%X**

hexadecimal integer (UPPERcase letters)

9

**%e**

exponential notation (with lowercase 'e')

10

**%E**

exponential notation (with UPPERcase 'E')

11

**%f**

floating point real number

12

**%g**

the shorter of %f and %e

13

**%G**

the shorter of %f and %E

Other supported symbols and functionality are listed in the following table −

Sr.No.

Symbol & Functionality

1

*****

argument specifies width or precision

2

**-**

left justification

3

**+**

display the sign

4

**<sp>**

leave a blank space before a positive number

5

**#**

add the octal leading zero ( '0' ) or hexadecimal leading '0x' or '0X', depending on whether 'x' or 'X' were used.

6

**0**

pad from left with zeros (instead of spaces)

7

**%**

'%%' leaves you with a single literal '%'

8

**(var)**

mapping variable (dictionary arguments)

9

**m.n.**

m is the minimum total width and n is the number of digits to display after the decimal point (if appl.)

## Triple Quotes

Python's triple quotes comes to the rescue by allowing strings to span multiple lines, including verbatim NEWLINEs, TABs, and any other special characters.

The syntax for triple quotes consists of three consecutive  **single or double**  quotes.

[Live Demo](http://tpcg.io/3kxxUj)

#!/usr/bin/python3 para_str =  """this is a long string that is made up of
several lines and non-printable characters such as
TAB ( \t ) and they will show up that way when displayed.
NEWLINEs within the string, whether explicitly given like
this within the brackets [ \n ], or just a NEWLINE within
the variable assignment will also show up.
"""  print  (para_str)

When the above code is executed, it produces the following result. Note how every single special character has been converted to its printed form, right down to the last NEWLINE at the end of the string between the "up." and closing triple quotes. Also note that NEWLINEs occur either with an explicit carriage return at the end of a line or its escape code (\n) −

this is a long string that is made up of
several lines and non-printable characters such as
TAB (    ) and they will show up that way when displayed.
NEWLINEs within the string, whether explicitly given like
this within the brackets [
 ], or just a NEWLINE within
the variable assignment will also show up.

Raw strings do not treat the backslash as a special character at all. Every character you put into a raw string stays the way you wrote it −

[Live Demo](http://tpcg.io/NvFyWy)

#!/usr/bin/python3  print  ('C:\\nowhere')

When the above code is executed, it produces the following result −

C:\nowhere

Now let's make use of raw string. We would put expression in  **r'expression'**  as follows −

[Live Demo](http://tpcg.io/BDtCUu)

#!/usr/bin/python3  print  (r'C:\\nowhere')

When the above code is executed, it produces the following result −

C:\\nowhere

## Unicode String

In Python 3, all strings are represented in Unicode.In Python 2 are stored internally as 8-bit ASCII, hence it is required to attach 'u' to make it Unicode. It is no longer necessary now.

### Built-in String Methods

Python includes the following built-in methods to manipulate strings −

Sr.No.

Methods & Description

1

[capitalize()](https://www.tutorialspoint.com/python3/string_capitalize.htm)

Capitalizes first letter of string

2

[center(width, fillchar)](https://www.tutorialspoint.com/python3/string_center.htm)

Returns a string padded with  _fillchar_  with the original string centered to a total of  _width_  columns.

3

[count(str, beg = 0,end = len(string))](https://www.tutorialspoint.com/python3/string_count.htm)

Counts how many times str occurs in string or in a substring of string if starting index beg and ending index end are given.

4

[decode(encoding = 'UTF-8',errors = 'strict')](https://www.tutorialspoint.com/python3/string_decode.htm)

Decodes the string using the codec registered for encoding. encoding defaults to the default string encoding.

5

[encode(encoding = 'UTF-8',errors = 'strict')](https://www.tutorialspoint.com/python3/string_encode.htm)

Returns encoded string version of string; on error, default is to raise a ValueError unless errors is given with 'ignore' or 'replace'.

6

[endswith(suffix, beg = 0, end = len(string))](https://www.tutorialspoint.com/python3/string_endswith.htm)

Determines if string or a substring of string (if starting index beg and ending index end are given) ends with suffix; returns true if so and false otherwise.

7

[expandtabs(tabsize = 8)](https://www.tutorialspoint.com/python3/string_expandtabs.htm)

Expands tabs in string to multiple spaces; defaults to 8 spaces per tab if tabsize not provided.

8

[find(str, beg = 0 end = len(string))](https://www.tutorialspoint.com/python3/string_find.htm)

Determine if str occurs in string or in a substring of string if starting index beg and ending index end are given returns index if found and -1 otherwise.

9

[index(str, beg = 0, end = len(string))](https://www.tutorialspoint.com/python3/string_index.htm)

Same as find(), but raises an exception if str not found.

10

[isalnum()](https://www.tutorialspoint.com/python3/string_isalnum.htm)

Returns true if string has at least 1 character and all characters are alphanumeric and false otherwise.

11

[isalpha()](https://www.tutorialspoint.com/python3/string_isalpha.htm)

Returns true if string has at least 1 character and all characters are alphabetic and false otherwise.

12

[isdigit()](https://www.tutorialspoint.com/python3/string_isdigit.htm)

Returns true if string contains only digits and false otherwise.

13

[islower()](https://www.tutorialspoint.com/python3/string_islower.htm)

Returns true if string has at least 1 cased character and all cased characters are in lowercase and false otherwise.

14

[isnumeric()](https://www.tutorialspoint.com/python3/string_isnumeric.htm)

Returns true if a unicode string contains only numeric characters and false otherwise.

15

[isspace()](https://www.tutorialspoint.com/python3/string_isspace.htm)

Returns true if string contains only whitespace characters and false otherwise.

16

[istitle()](https://www.tutorialspoint.com/python3/string_istitle.htm)

Returns true if string is properly "titlecased" and false otherwise.

17

[isupper()](https://www.tutorialspoint.com/python3/string_isupper.htm)

Returns true if string has at least one cased character and all cased characters are in uppercase and false otherwise.

18

[join(seq)](https://www.tutorialspoint.com/python3/string_join.htm)

Merges (concatenates) the string representations of elements in sequence seq into a string, with separator string.

19

[len(string)](https://www.tutorialspoint.com/python3/string_len.htm)

Returns the length of the string

20

[ljust(width[, fillchar])](https://www.tutorialspoint.com/python3/string_ljust.htm)

Returns a space-padded string with the original string left-justified to a total of width columns.

21

[lower()](https://www.tutorialspoint.com/python3/string_lower.htm)

Converts all uppercase letters in string to lowercase.

22

[lstrip()](https://www.tutorialspoint.com/python3/string_lstrip.htm)

Removes all leading whitespace in string.

23

[maketrans()](https://www.tutorialspoint.com/python3/string_maketrans.htm)

Returns a translation table to be used in translate function.

24

[max(str)](https://www.tutorialspoint.com/python3/string_max.htm)

Returns the max alphabetical character from the string str.

25

[min(str)](https://www.tutorialspoint.com/python3/string_min.htm)

Returns the min alphabetical character from the string str.

26

[replace(old, new [, max])](https://www.tutorialspoint.com/python3/string_replace.htm)

Replaces all occurrences of old in string with new or at most max occurrences if max given.

27

[rfind(str, beg = 0,end = len(string))](https://www.tutorialspoint.com/python3/string_rfind.htm)

Same as find(), but search backwards in string.

28

[rindex( str, beg = 0, end = len(string))](https://www.tutorialspoint.com/python3/string_rindex.htm)

Same as index(), but search backwards in string.

29

[rjust(width,[, fillchar])](https://www.tutorialspoint.com/python3/string_rjust.htm)

Returns a space-padded string with the original string right-justified to a total of width columns.

30

[rstrip()](https://www.tutorialspoint.com/python3/string_rstrip.htm)

Removes all trailing whitespace of string.

31

[split(str="", num=string.count(str))](https://www.tutorialspoint.com/python3/string_split.htm)

Splits string according to delimiter str (space if not provided) and returns list of substrings; split into at most num substrings if given.

32

[splitlines( num=string.count('\n'))](https://www.tutorialspoint.com/python3/string_splitlines.htm)

Splits string at all (or num) NEWLINEs and returns a list of each line with NEWLINEs removed.

33

[startswith(str, beg=0,end=len(string))](https://www.tutorialspoint.com/python3/string_startswith.htm)

Determines if string or a substring of string (if starting index beg and ending index end are given) starts with substring str; returns true if so and false otherwise.

34

[strip([chars])](https://www.tutorialspoint.com/python3/string_strip.htm)

Performs both lstrip() and rstrip() on string

35

[swapcase()](https://www.tutorialspoint.com/python3/string_swapcase.htm)

Inverts case for all letters in string.

36

[title()](https://www.tutorialspoint.com/python3/string_title.htm)

Returns "titlecased" version of string, that is, all words begin with uppercase and the rest are lowercase.

37

[translate(table, deletechars="")](https://www.tutorialspoint.com/python3/string_translate.htm)

Translates string according to translation table str(256 chars), removing those in the del string.

38

[upper()](https://www.tutorialspoint.com/python3/string_upper.htm)

Converts lowercase letters in string to uppercase.

39

[zfill (width)](https://www.tutorialspoint.com/python3/string_zfill.htm)

Returns original string leftpadded with zeros to a total of width characters; intended for numbers, zfill() retains any sign given (less one zero).

40

[isdecimal()](https://www.tutorialspoint.com/python3/string_isdecimal.htm)

Returns true if a unicode string contains only decimal characters and false otherwise.

# Python 3 - Lists

The most basic data structure in Python is the  **sequence**. Each element of a sequence is assigned a number - its position or index. The first index is zero, the second index is one, and so forth.

Python has six built-in types of sequences, but the most common ones are lists and tuples, which we would see in this tutorial.

There are certain things you can do with all the sequence types. These operations include indexing, slicing, adding, multiplying, and checking for membership. In addition, Python has built-in functions for finding the length of a sequence and for finding its largest and smallest elements.

## Python Lists

The list is the most versatile datatype available in Python, which can be written as a list of comma-separated values (items) between square brackets. Important thing about a list is that the items in a list need not be of the same type.

Creating a list is as simple as putting different comma-separated values between square brackets. For example −

list1 =  ['physics',  'chemistry',  1997,  2000]; list2 =  [1,  2,  3,  4,  5  ]; list3 =  ["a",  "b",  "c",  "d"];

Similar to string indices, list indices start at 0, and lists can be sliced, concatenated and so on.

## Accessing Values in Lists

To access values in lists, use the square brackets for slicing along with the index or indices to obtain value available at that index. For example −

[Live Demo](http://tpcg.io/WMFil4)

#!/usr/bin/python3 list1 =  ['physics',  'chemistry',  1997,  2000] list2 =  [1,  2,  3,  4,  5,  6,  7  ]  print  ("list1[0]: ", list1[0])  print  ("list2[1:5]: ", list2[1:5])

When the above code is executed, it produces the following result −

list1[0]:  physics
list2[1:5]:  [2, 3, 4, 5]

## Updating Lists

You can update single or multiple elements of lists by giving the slice on the left-hand side of the assignment operator, and you can add to elements in a list with the append() method. For example −

[Live Demo](http://tpcg.io/CottRC)

#!/usr/bin/python3 list =  ['physics',  'chemistry',  1997,  2000]  print  ("Value available at index 2 : ", list[2]) list[2]  =  2001  print  ("New value available at index 2 : ", list[2])

**Note**  − The append() method is discussed in the subsequent section.

When the above code is executed, it produces the following result −

Value available at index 2 :  1997
New value available at index 2 :  2001

## Delete List Elements

To remove a list element, you can use either the  **del**  statement if you know exactly which element(s) you are deleting. You can use the remove() method if you do not know exactly which items to delete. For example −

[Live Demo](http://tpcg.io/sKywHN)

#!/usr/bin/python3 list =  ['physics',  'chemistry',  1997,  2000]  print  (list)  del list[2]  print  ("After deleting value at index 2 : ", list)

When the above code is executed, it produces the following result −

['physics', 'chemistry', 1997, 2000]
After deleting value at index 2 :  ['physics', 'chemistry', 2000]

**Note**  − remove() method is discussed in subsequent section.

## Basic List Operations

Lists respond to the + and * operators much like strings; they mean concatenation and repetition here too, except that the result is a new list, not a string.

In fact, lists respond to all of the general sequence operations we used on strings in the prior chapter.

Python Expression

Results

Description

len([1, 2, 3])

3

Length

[1, 2, 3] + [4, 5, 6]

[1, 2, 3, 4, 5, 6]

Concatenation

['Hi!'] * 4

['Hi!', 'Hi!', 'Hi!', 'Hi!']

Repetition

3 in [1, 2, 3]

True

Membership

for x in [1,2,3] : print (x,end = ' ')

1 2 3

Iteration

## Indexing, Slicing and Matrixes

Since lists are sequences, indexing and slicing work the same way for lists as they do for strings.

Assuming the following input −

L =  ['C++'', 'Java', 'Python']

Python Expression

Results

Description

L[2]

'Python'

Offsets start at zero

L[-2]

'Java'

Negative: count from the right

L[1:]

['Java', 'Python']

Slicing fetches sections

## Built-in List Functions and Methods

Python includes the following list functions −

Sr.No.

Function & Description

1

[len(list)](https://www.tutorialspoint.com/python3/list_len.htm)

Gives the total length of the list.

2

[max(list)](https://www.tutorialspoint.com/python3/list_max.htm)

Returns item from the list with max value.

3

[min(list)](https://www.tutorialspoint.com/python3/list_min.htm)

Returns item from the list with min value.

4

[list(seq)](https://www.tutorialspoint.com/python3/list_list.htm)

Converts a tuple into list.

Python includes the following list methods −

Sr.No.

Methods & Description

1

[list.append(obj)](https://www.tutorialspoint.com/python3/list_append.htm)

Appends object obj to list

2

[list.count(obj)](https://www.tutorialspoint.com/python3/list_count.htm)

Returns count of how many times obj occurs in list

3

[list.extend(seq)](https://www.tutorialspoint.com/python3/list_extend.htm)

Appends the contents of seq to list

4

[list.index(obj)](https://www.tutorialspoint.com/python3/list_index.htm)

Returns the lowest index in list that obj appears

5

[list.insert(index, obj)](https://www.tutorialspoint.com/python3/list_insert.htm)

Inserts object obj into list at offset index

6

[list.pop(obj = list[-1])](https://www.tutorialspoint.com/python3/list_pop.htm)

Removes and returns last object or obj from list

7

[list.remove(obj)](https://www.tutorialspoint.com/python3/list_remove.htm)

Removes object obj from list

8

[list.reverse()](https://www.tutorialspoint.com/python3/list_reverse.htm)

Reverses objects of list in place

9

[list.sort([func])](https://www.tutorialspoint.com/python3/list_sort.htm)

Sorts objects of list, use compare func if given

# Python 3 - Tuples

A tuple is a collection of objects which ordered and immutable. Tuples are sequences, just like lists. The main difference between the tuples and the lists is that the tuples cannot be changed unlike lists. Tuples use parentheses, whereas lists use square brackets.

Creating a tuple is as simple as putting different comma-separated values. Optionally, you can put these comma-separated values between parentheses also. For example −

tup1 =  ('physics',  'chemistry',  1997,  2000) tup2 =  (1,  2,  3,  4,  5  ) tup3 =  "a",  "b",  "c",  "d"

The empty tuple is written as two parentheses containing nothing −

tup1 = ();

To write a tuple containing a single value you have to include a comma, even though there is only one value −

tup1 = (50,)

Like string indices, tuple indices start at 0, and they can be sliced, concatenated, and so on.

## Accessing Values in Tuples

To access values in tuple, use the square brackets for slicing along with the index or indices to obtain the value available at that index. For example −

[Live Demo](http://tpcg.io/f2A4XX)

#!/usr/bin/python3 tup1 =  ('physics',  'chemistry',  1997,  2000) tup2 =  (1,  2,  3,  4,  5,  6,  7  )  print  ("tup1[0]: ", tup1[0])  print  ("tup2[1:5]: ", tup2[1:5])

When the above code is executed, it produces the following result −

tup1[0]:  physics
tup2[1:5]:  (2, 3, 4, 5)

## Updating Tuples

Tuples are immutable, which means you cannot update or change the values of tuple elements. You are able to take portions of the existing tuples to create new tuples as the following example demonstrates −

[Live Demo](http://tpcg.io/ektEVm)

#!/usr/bin/python3 tup1 =  (12,  34.56) tup2 =  ('abc',  'xyz')  # Following action is not valid for tuples  # tup1[0] = 100;  # So let's create a new tuple as follows tup3 = tup1 + tup2 print  (tup3)

When the above code is executed, it produces the following result −

(12, 34.56, 'abc', 'xyz')

## Delete Tuple Elements

Removing individual tuple elements is not possible. There is, of course, nothing wrong with putting together another tuple with the undesired elements discarded.

To explicitly remove an entire tuple, just use the  **del**  statement. For example −

#!/usr/bin/python3 tup =  ('physics',  'chemistry',  1997,  2000);  print  (tup)  del tup;  print  ("After deleting tup : ")  print  (tup)

This produces the following result.

**Note**  − An exception is raised. This is because after  **del tup**, tuple does not exist any more.

('physics', 'chemistry', 1997, 2000)
After deleting tup :
Traceback (most recent call last):
   File "test.py", line 9, in <module>
      print tup;
NameError: name 'tup' is not defined

## Basic Tuples Operations

Tuples respond to the + and * operators much like strings; they mean concatenation and repetition here too, except that the result is a new tuple, not a string.

In fact, tuples respond to all of the general sequence operations we used on strings in the previous chapter.

Python Expression

Results

Description

len((1, 2, 3))

3

Length

(1, 2, 3) + (4, 5, 6)

(1, 2, 3, 4, 5, 6)

Concatenation

('Hi!',) * 4

('Hi!', 'Hi!', 'Hi!', 'Hi!')

Repetition

3 in (1, 2, 3)

True

Membership

for x in (1,2,3) : print (x, end = ' ')

1 2 3

Iteration

## Indexing, Slicing, and Matrixes

Since tuples are sequences, indexing and slicing work the same way for tuples as they do for strings, assuming the following input −

T=('C++', 'Java', 'Python')

Python Expression

Results

Description

T[2]

'Python'

Offsets start at zero

T[-2]

'Java'

Negative: count from the right

T[1:]

('Java', 'Python')

Slicing fetches sections

## No Enclosing Delimiters

No enclosing Delimiters is any set of multiple objects, comma-separated, written without identifying symbols, i.e., brackets for lists, parentheses for tuples, etc., default to tuples, as indicated in these short examples.

## Built-in Tuple Functions

Python includes the following tuple functions −

Sr.No.

Function & Description

1

[cmp(tuple1, tuple2)](https://www.tutorialspoint.com/python3/tuple_cmp.htm)

Compares elements of both tuples.

2

[len(tuple)](https://www.tutorialspoint.com/python3/tuple_len.htm)

Gives the total length of the tuple.

3

[max(tuple)](https://www.tutorialspoint.com/python3/tuple_max.htm)

Returns item from the tuple with max value.

4

[min(tuple)](https://www.tutorialspoint.com/python3/tuple_min.htm)

Returns item from the tuple with min value.

5

[tuple(seq)](https://www.tutorialspoint.com/python3/tuple_tuple.htm)

Converts a list into tuple.

# Python 3 - Dictionary

Each key is separated from its value by a colon (:), the items are separated by commas, and the whole thing is enclosed in curly braces. An empty dictionary without any items is written with just two curly braces, like this: {}.

Keys are unique within a dictionary while values may not be. The values of a dictionary can be of any type, but the keys must be of an immutable data type such as strings, numbers, or tuples.

## Accessing Values in Dictionary

To access dictionary elements, you can use the familiar square brackets along with the key to obtain its value. Following is a simple example −

[Live Demo](http://tpcg.io/MHnJJD)

#!/usr/bin/python3 dict =  {'Name':  'Zara',  'Age':  7,  'Class':  'First'}  print  ("dict['Name']: ", dict['Name'])  print  ("dict['Age']: ", dict['Age'])

When the above code is executed, it produces the following result −

dict['Name']:  Zara
dict['Age']:  7

If we attempt to access a data item with a key, which is not a part of the dictionary, we get an error as follows −

[Live Demo](http://tpcg.io/vQGIzw)

#!/usr/bin/python3 dict =  {'Name':  'Zara',  'Age':  7,  'Class':  'First'};  print  ("dict['Alice']: ", dict['Alice'])

When the above code is executed, it produces the following result −

dict['Zara']:
Traceback (most recent call last):
   File "test.py", line 4, in <module>
      print "dict['Alice']: ", dict['Alice'];
KeyError: 'Alice'

## Updating Dictionary

You can update a dictionary by adding a new entry or a key-value pair, modifying an existing entry, or deleting an existing entry as shown in a simple example given below.

[Live Demo](http://tpcg.io/cXjIA7)

#!/usr/bin/python3 dict =  {'Name':  'Zara',  'Age':  7,  'Class':  'First'} dict['Age']  =  8;  # update existing entry dict['School']  =  "DPS School"  # Add new entry  print  ("dict['Age']: ", dict['Age'])  print  ("dict['School']: ", dict['School'])

When the above code is executed, it produces the following result −

dict['Age']:  8
dict['School']:  DPS School

## Delete Dictionary Elements

You can either remove individual dictionary elements or clear the entire contents of a dictionary. You can also delete entire dictionary in a single operation.

To explicitly remove an entire dictionary, just use the  **del**  statement. Following is a simple example −

[Live Demo](http://tpcg.io/oCEFM1)

#!/usr/bin/python3 dict =  {'Name':  'Zara',  'Age':  7,  'Class':  'First'}  del dict['Name']  # remove entry with key 'Name' dict.clear()  # remove all entries in dict  del dict # delete entire dictionary  print  ("dict['Age']: ", dict['Age'])  print  ("dict['School']: ", dict['School'])

This produces the following result.

An exception is raised because after  **del dict**, the dictionary does not exist anymore.

dict['Age']:
Traceback (most recent call last):
   File "test.py", line 8, in <module>
      print "dict['Age']: ", dict['Age'];
TypeError: 'type' object is unsubscriptable

**Note**  − The del() method is discussed in subsequent section.

## Properties of Dictionary Keys

Dictionary values have no restrictions. They can be any arbitrary Python object, either standard objects or user-defined objects. However, same is not true for the keys.

There are two important points to remember about dictionary keys −

**(a)**  More than one entry per key is not allowed. This means no duplicate key is allowed. When duplicate keys are encountered during assignment, the last assignment wins. For example −

[Live Demo](http://tpcg.io/K4elKR)

#!/usr/bin/python3 dict =  {'Name':  'Zara',  'Age':  7,  'Name':  'Manni'}  print  ("dict['Name']: ", dict['Name'])

When the above code is executed, it produces the following result −

dict['Name']:  Manni

**(b)**  Keys must be immutable. This means you can use strings, numbers or tuples as dictionary keys but something like ['key'] is not allowed. Following is a simple example −

[Live Demo](http://tpcg.io/psctl5)

#!/usr/bin/python3 dict =  {['Name']:  'Zara',  'Age':  7}  print  ("dict['Name']: ", dict['Name'])

When the above code is executed, it produces the following result −

Traceback (most recent call last):
   File "test.py", line 3, in <module>
      dict = {['Name']: 'Zara', 'Age': 7}
TypeError: list objects are unhashable

## Built-in Dictionary Functions and Methods

Python includes the following dictionary functions −

Sr.No.

Function & Description

1

[cmp(dict1, dict2)](https://www.tutorialspoint.com/python3/dictionary_cmp.htm)

No longer available in Python 3.

2

[len(dict)](https://www.tutorialspoint.com/python3/dictionary_len.htm)

Gives the total length of the dictionary. This would be equal to the number of items in the dictionary.

3

[str(dict)](https://www.tutorialspoint.com/python3/dictionary_str.htm)

Produces a printable string representation of a dictionary

4

[type(variable)](https://www.tutorialspoint.com/python3/dictionary_type.htm)

Returns the type of the passed variable. If passed variable is dictionary, then it would return a dictionary type.

Python includes the following dictionary methods −

Sr.No.

Method & Description

1

[dict.clear()](https://www.tutorialspoint.com/python3/dictionary_clear.htm)

Removes all elements of dictionary  _dict_

2

[dict.copy()](https://www.tutorialspoint.com/python3/dictionary_copy.htm)

Returns a shallow copy of dictionary  _dict_

3

[dict.fromkeys()](https://www.tutorialspoint.com/python3/dictionary_fromkeys.htm)

Create a new dictionary with keys from seq and values  _set_  to  _value_.

4

[dict.get(key, default=None)](https://www.tutorialspoint.com/python3/dictionary_get.htm)

For  _key_  key, returns value or default if key not in dictionary

5

[dict.has_key(key)](https://www.tutorialspoint.com/python3/dictionary_has_key.htm)

Removed, use the  _in_  operation instead.

6

[dict.items()](https://www.tutorialspoint.com/python3/dictionary_items.htm)

Returns a list of  _dict_'s (key, value) tuple pairs

7

[dict.keys()](https://www.tutorialspoint.com/python3/dictionary_keys.htm)

Returns list of dictionary dict's keys

8

[dict.setdefault(key, default = None)](https://www.tutorialspoint.com/python3/dictionary_setdefault.htm)

Similar to get(), but will set dict[key] = default if  _key_  is not already in dict

9

[dict.update(dict2)](https://www.tutorialspoint.com/python3/dictionary_update.htm)

Adds dictionary  _dict2_'s key-values pairs to  _dict_

10

[dict.values()](https://www.tutorialspoint.com/python3/dictionary_values.htm)

Returns list of dictionary  _dict_'s values

# Python 3 - Date & Time

A Python program can handle date and time in several ways. Converting between date formats is a common chore for computers. Python's time and calendar modules help track dates and times.

## What is Tick?

Time intervals are floating-point numbers in units of seconds. Particular instants in time are expressed in seconds since 12:00am, January 1, 1970(epoch).

There is a popular  **time**  module available in Python which provides functions for working with times, and for converting between representations. The function  **time.time()**  returns the current system time in ticks since 12:00am, January 1, 1970(epoch).

### Example

[Live Demo](http://tpcg.io/b5IfW3)

#!/usr/bin/python3  import time;  # This is required to include time module. ticks = time.time()  print  ("Number of ticks since 12:00am, January 1, 1970:", ticks)

This would produce a result something as follows −

Number of ticks since 12:00am, January 1, 1970: 1455508609.34375

Date arithmetic is easy to do with ticks. However, dates before the epoch cannot be represented in this form. Dates in the far future also cannot be represented this way - the cutoff point is sometime in 2038 for UNIX and Windows.

## What is TimeTuple?

Many of the Python's time functions handle time as a tuple of 9 numbers, as shown below −

Index

Field

Values

0

4-digit year

2016

1

Month

1 to 12

2

Day

1 to 31

3

Hour

0 to 23

4

Minute

0 to 59

5

Second

0 to 61 (60 or 61 are leap-seconds)

6

Day of Week

0 to 6 (0 is Monday)

7

Day of year

1 to 366 (Julian day)

8

Daylight savings

-1, 0, 1, -1 means library determines DST

For Example −

[Live Demo](http://tpcg.io/JznzAJ)

import time print  (time.localtime());

This would produce a result as follows −

time.struct_time(tm_year = 2016, tm_mon = 2, tm_mday = 15, tm_hour = 9, 
   tm_min = 29, tm_sec = 2, tm_wday = 0, tm_yday = 46, tm_isdst = 0)

The above tuple is equivalent to  **struct_time**  structure. This structure has following attributes −

Index

Attributes

Values

0

tm_year

2016

1

tm_mon

1 to 12

2

tm_mday

1 to 31

3

tm_hour

0 to 23

4

tm_min

0 to 59

5

tm_sec

0 to 61 (60 or 61 are leap-seconds)

6

tm_wday

0 to 6 (0 is Monday)

7

tm_yday

1 to 366 (Julian day)

8

tm_isdst

-1, 0, 1, -1 means library determines DST

## Getting current time

To translate a time instant from seconds since the epoch floating-point value into a timetuple, pass the floating-point value to a function (e.g., localtime) that returns a time-tuple with all valid nine items.

[Live Demo](http://tpcg.io/KO5lOd)

#!/usr/bin/python3  import time

localtime = time.localtime(time.time())  print  ("Local current time :", localtime)

This would produce the following result, which could be formatted in any other presentable form −

Local current time : time.struct_time(tm_year = 2016, tm_mon = 2, tm_mday = 15, 
   tm_hour = 9, tm_min = 29, tm_sec = 2, tm_wday = 0, tm_yday = 46, tm_isdst = 0)

## Getting formatted time

You can format any time as per your requirement, but a simple method to get time in a readable format is  **asctime()**  −

[Live Demo](https://www.tutorialspoint.com/python3/python_quick_guide.htm)

[Live Demo](http://tpcg.io/srMQHp)

#!/usr/bin/python3  import time

localtime = time.asctime( time.localtime(time.time())  )  print  ("Local current time :", localtime)

This would produce the following result −

Local current time : Mon Feb 15 09:34:03 2016

## Getting calendar for a month

The calendar module gives a wide range of methods to play with yearly and monthly calendars. Here, we print a calendar for a given month ( Jan 2008 ) −

[Live Demo](http://tpcg.io/K5F8pR)

#!/usr/bin/python3  import calendar

cal = calendar.month(2016,  2)  print  ("Here is the calendar:")  print  (cal)

This would produce the following result −

Here is the calendar:
   February 2016
Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29

## The time Module

There is a popular  **time**  module available in Python, which provides functions for working with times and for converting between representations. Here is the list of all available methods.

Sr.No.

Function & Description

1

[time.altzone](https://www.tutorialspoint.com/python3/time_altzone.htm)

The offset of the local DST timezone, in seconds west of UTC, if one is defined. This is negative if the local DST timezone is east of UTC (as in Western Europe, including the UK). Use this if the daylight is nonzero.

2

[time.asctime([tupletime])](https://www.tutorialspoint.com/python3/time_asctime.htm)

Accepts a time-tuple and returns a readable 24-character string such as 'Tue Dec 11 18:07:14 2008'.

3

[time.clock( )](https://www.tutorialspoint.com/python3/time_clock.htm)

Returns the current CPU time as a floating-point number of seconds. To measure computational costs of different approaches, the value of time.clock is more useful than that of time.time().

4

[time.ctime([secs])](https://www.tutorialspoint.com/python3/time_ctime.htm)

Like asctime(localtime(secs)) and without arguments is like asctime( )

5

[time.gmtime([secs])](https://www.tutorialspoint.com/python3/time_gmtime.htm)

Accepts an instant expressed in seconds since the epoch and returns a time-tuple t with the UTC time. Note − t.tm_isdst is always 0

6

[time.localtime([secs])](https://www.tutorialspoint.com/python3/time_localtime.htm)

Accepts an instant expressed in seconds since the epoch and returns a time-tuple t with the local time (t.tm_isdst is 0 or 1, depending on whether DST applies to instant secs by local rules).

7

[time.mktime(tupletime)](https://www.tutorialspoint.com/python3/time_mktime.htm)

Accepts an instant expressed as a time-tuple in local time and returns a floating-point value with the instant expressed in seconds since the epoch.

8

[time.sleep(secs)](https://www.tutorialspoint.com/python3/time_sleep.htm)

Suspends the calling thread for secs seconds.

9

[time.strftime(fmt[,tupletime])](https://www.tutorialspoint.com/python3/time_strftime.htm)

Accepts an instant expressed as a time-tuple in local time and returns a string representing the instant as specified by string fmt.

10

[time.strptime(str,fmt = '%a %b %d %H:%M:%S %Y')](https://www.tutorialspoint.com/python3/time_strptime.htm)

Parses str according to format string fmt and returns the instant in time-tuple format.

11

[time.time( )](https://www.tutorialspoint.com/python3/time_time.htm)

Returns the current time instant, a floating-point number of seconds since the epoch.

12

[time.tzset()](https://www.tutorialspoint.com/python3/time_tzset.htm)

Resets the time conversion rules used by the library routines. The environment variable TZ specifies how this is done.

There are two important attributes available with time module. They are −

Sr.No.

Attribute & Description

1

**time.timezone**

Attribute time.timezone is the offset in seconds of the local time zone (without DST) from UTC (>0 in the Americas; <=0 in most of Europe, Asia, Africa).

2

**time.tzname**

Attribute time.tzname is a pair of locale-dependent strings, which are the names of the local time zone without and with DST, respectively.

## The calendar Module

The calendar module supplies calendar-related functions, including functions to print a text calendar for a given month or year.

By default, calendar takes Monday as the first day of the week and Sunday as the last one. To change this, call the  **calendar.setfirstweekday()**  function.

Here is a list of functions available with the  **calendar**  module −

Sr.No.

Function & Description

1

**calendar.calendar(year,w = 2,l = 1,c = 6)**

Returns a multiline string with a calendar for year year formatted into three columns separated by c spaces. w is the width in characters of each date; each line has length 21*w+18+2*c. l is the number of lines for each week.

2

**calendar.firstweekday( )**

Returns the current setting for the weekday that starts each week. By default, when calendar is first imported, this is 0, meaning Monday.

3

**calendar.isleap(year)**

Returns True if year is a leap year; otherwise, False.

4

**calendar.leapdays(y1,y2)**

Returns the total number of leap days in the years within range(y1,y2).

5

**calendar.month(year,month,w = 2,l = 1)**

Returns a multiline string with a calendar for month month of year year, one line per week plus two header lines. w is the width in characters of each date; each line has length 7*w+6. l is the number of lines for each week.

6

**calendar.monthcalendar(year,month)**

Returns a list of lists of ints. Each sublist denotes a week. Days outside month month of year year are set to 0; days within the month are set to their day-of-month, 1 and up.

7

**calendar.monthrange(year,month)**

Returns two integers. The first one is the code of the weekday for the first day of the month month in year year; the second one is the number of days in the month. Weekday codes are 0 (Monday) to 6 (Sunday); month numbers are 1 to 12.

8

**calendar.prcal(year,w = 2,l = 1,c = 6)**

Like print calendar.calendar(year,w,l,c).

9

**calendar.prmonth(year,month,w = 2,l = 1)**

Like print calendar.month(year,month,w,l).

10

**calendar.setfirstweekday(weekday)**

Sets the first day of each week to weekday code weekday. Weekday codes are 0 (Monday) to 6 (Sunday).

11

**calendar.timegm(tupletime)**

The inverse of time.gmtime: accepts a time instant in time-tuple form and returns the same instant as a floating-point number of seconds since the epoch.

12

**calendar.weekday(year,month,day)**

Returns the weekday code for the given date. Weekday codes are 0 (Monday) to 6 (Sunday); month numbers are 1 (January) to 12 (December).

## Other Modules and Functions

If you are interested, then here you would find a list of other important modules and functions to play with date & time in Python −

-   [The datetime Module](https://docs.python.org/library/datetime.html#module-datetime)
-   [The pytz Module](http://www.twinsun.com/tz/tz-link.htm)
-   [The dateutil Module](https://labix.org/python-dateutil)

# Python 3 - Functions

A function is a block of organized, reusable code that is used to perform a single, related action. Functions provide better modularity for your application and a high degree of code reusing.

As you already know, Python gives you many built-in functions like print(), etc. but you can also create your own functions. These functions are called  _user-defined functions._

### Defining a Function

You can define functions to provide the required functionality. Here are simple rules to define a function in Python.

-   Function blocks begin with the keyword  **def**  followed by the function name and parentheses ( ( ) ).
    
-   Any input parameters or arguments should be placed within these parentheses. You can also define parameters inside these parentheses.
    
-   The first statement of a function can be an optional statement - the documentation string of the function or  _docstring_.
    
-   The code block within every function starts with a colon (:) and is indented.
    
-   The statement return [expression] exits a function, optionally passing back an expression to the caller. A return statement with no arguments is the same as return None.
    

### Syntax

def functionname( parameters ):
   "function_docstring"
   function_suite
   return [expression]

By default, parameters have a positional behavior and you need to inform them in the same order that they were defined.

### Example

The following function takes a string as input parameter and prints it on standard screen.

def printme( str ):  "This prints a passed string into this function"  print  (str)  return

## Calling a Function

Defining a function gives it a name, specifies the parameters that are to be included in the function and structures the blocks of code.

Once the basic structure of a function is finalized, you can execute it by calling it from another function or directly from the Python prompt. Following is an example to call the  **printme()**  function −

[Live Demo](http://tpcg.io/gh41CO)

#!/usr/bin/python3  # Function definition is here  def printme( str ):  "This prints a passed string into this function"  print  (str)  return  # Now you can call printme function printme("This is first call to the user defined function!") printme("Again second call to the same function")

When the above code is executed, it produces the following result −

This is first call to the user defined function!
Again second call to the same function

## Pass by Reference vs Value

All parameters (arguments) in the Python language are passed by reference. It means if you change what a parameter refers to within a function, the change also reflects back in the calling function. For example −

[Live Demo](http://tpcg.io/89otk5)

#!/usr/bin/python3  # Function definition is here  def changeme( mylist ):  "This changes a passed list into this function"  print  ("Values inside the function before change: ", mylist) mylist[2]=50  print  ("Values inside the function after change: ", mylist)  return  # Now you can call changeme function mylist =  [10,20,30] changeme( mylist )  print  ("Values outside the function: ", mylist)

Here, we are maintaining reference of the passed object and appending values in the same object. Therefore, this would produce the following result −

Values inside the function before change:  [10, 20, 30]
Values inside the function after change:  [10, 20, 50]
Values outside the function:  [10, 20, 50]

There is one more example where argument is being passed by reference and the reference is being overwritten inside the called function.

[Live Demo](http://tpcg.io/tJpndT)

#!/usr/bin/python3  # Function definition is here  def changeme( mylist ):  "This changes a passed list into this function" mylist =  [1,2,3,4]  # This would assi new reference in mylist  print  ("Values inside the function: ", mylist)  return  # Now you can call changeme function mylist =  [10,20,30] changeme( mylist )  print  ("Values outside the function: ", mylist)

The parameter  **mylist**  is local to the function changeme. Changing mylist within the function does not affect mylist. The function accomplishes nothing and finally this would produce the following result −

Values inside the function:  [1, 2, 3, 4]
Values outside the function:  [10, 20, 30]

## Function Arguments

You can call a function by using the following types of formal arguments −

-   Required arguments
-   Keyword arguments
-   Default arguments
-   Variable-length arguments

## Required Arguments

Required arguments are the arguments passed to a function in correct positional order. Here, the number of arguments in the function call should match exactly with the function definition.

To call the function  **printme()**, you definitely need to pass one argument, otherwise it gives a syntax error as follows −

[Live Demo](http://tpcg.io/ceXIug)

#!/usr/bin/python3  # Function definition is here  def printme( str ):  "This prints a passed string into this function"  print  (str)  return  # Now you can call printme function printme()

When the above code is executed, it produces the following result −

Traceback (most recent call last):
   File "test.py", line 11, in <module>
      printme();
TypeError: printme() takes exactly 1 argument (0 given)

## Keyword Arguments

Keyword arguments are related to the function calls. When you use keyword arguments in a function call, the caller identifies the arguments by the parameter name.

This allows you to skip arguments or place them out of order because the Python interpreter is able to use the keywords provided to match the values with parameters. You can also make keyword calls to the  **printme()**  function in the following ways −

[Live Demo](http://tpcg.io/cOAFB8)

#!/usr/bin/python3  # Function definition is here  def printme( str ):  "This prints a passed string into this function"  print  (str)  return  # Now you can call printme function printme( str =  "My string")

When the above code is executed, it produces the following result −

My string

The following example gives a clearer picture. Note that the order of parameters does not matter.

[Live Demo](http://tpcg.io/6Vv9cq)

#!/usr/bin/python3  # Function definition is here  def printinfo( name, age ):  "This prints a passed info into this function"  print  ("Name: ", name)  print  ("Age ", age)  return  # Now you can call printinfo function printinfo( age =  50, name =  "miki"  )

When the above code is executed, it produces the following result −

Name:  miki
Age  50

## Default Arguments

A default argument is an argument that assumes a default value if a value is not provided in the function call for that argument. The following example gives an idea on default arguments, it prints default age if it is not passed −

[Live Demo](http://tpcg.io/e6K9mu)

#!/usr/bin/python3  # Function definition is here  def printinfo( name, age =  35  ):  "This prints a passed info into this function"  print  ("Name: ", name)  print  ("Age ", age)  return  # Now you can call printinfo function printinfo( age =  50, name =  "miki"  ) printinfo( name =  "miki"  )

When the above code is executed, it produces the following result −

Name:  miki
Age  50
Name:  miki
Age  35

## Variable-length Arguments

You may need to process a function for more arguments than you specified while defining the function. These arguments are called  _variable-length_  arguments and are not named in the function definition, unlike required and default arguments.

Syntax for a function with non-keyword variable arguments is given below −

def functionname([formal_args,] *var_args_tuple ):
   "function_docstring"
   function_suite
   return [expression]

An asterisk (*) is placed before the variable name that holds the values of all nonkeyword variable arguments. This tuple remains empty if no additional arguments are specified during the function call. Following is a simple example −

[Live Demo](http://tpcg.io/JFDYk7)

#!/usr/bin/python3  # Function definition is here  def printinfo( arg1,  *vartuple ):  "This prints a variable passed arguments"  print  ("Output is: ")  print  (arg1)  for  var  in vartuple:  print  (var)  return  # Now you can call printinfo function printinfo(  10  ) printinfo(  70,  60,  50  )

When the above code is executed, it produces the following result −

Output is:
10
Output is:
70
60
50

## The Anonymous Functions

These functions are called anonymous because they are not declared in the standard manner by using the  **def**  keyword. You can use the  **lambda**  keyword to create small anonymous functions.

-   Lambda forms can take any number of arguments but return just one value in the form of an expression. They cannot contain commands or multiple expressions.
    
-   An anonymous function cannot be a direct call to print because lambda requires an expression.
    
-   Lambda functions have their own local namespace and cannot access variables other than those in their parameter list and those in the global namespace.
    
-   Although it appears that lambdas are a one-line version of a function, they are not equivalent to inline statements in C or C++, whose purpose is to stack allocation by passing function, during invocation for performance reasons.
    

### Syntax

The syntax of  **lambda**  functions contains only a single statement, which is as follows −

lambda  [arg1 [,arg2,.....argn]]:expression

Following is an example to show how  **lambda**  form of function works −

[Live Demo](http://tpcg.io/GXNTkx)

#!/usr/bin/python3  # Function definition is here sum =  lambda arg1, arg2: arg1 + arg2 # Now you can call sum as a function  print  ("Value of total : ", sum(  10,  20  ))  print  ("Value of total : ", sum(  20,  20  ))

When the above code is executed, it produces the following result −

Value of total :  30
Value of total :  40

## The return Statement

The statement return [expression] exits a function, optionally passing back an expression to the caller. A return statement with no arguments is the same as return None.

All the examples given below are not returning any value. You can return a value from a function as follows −

[Live Demo](http://tpcg.io/d2UiXP)

#!/usr/bin/python3  # Function definition is here  def sum( arg1, arg2 ):  # Add both the parameters and return them." total = arg1 + arg2 print  ("Inside the function : ", total)  return total # Now you can call sum function total = sum(  10,  20  )  print  ("Outside the function : ", total )

When the above code is executed, it produces the following result −

Inside the function :  30
Outside the function :  30

## Scope of Variables

All variables in a program may not be accessible at all locations in that program. This depends on where you have declared a variable.

The scope of a variable determines the portion of the program where you can access a particular identifier. There are two basic scopes of variables in Python −

-   Global variables
-   Local variables

## Global vs. Local variables

Variables that are defined inside a function body have a local scope, and those defined outside have a global scope.

This means that local variables can be accessed only inside the function in which they are declared, whereas global variables can be accessed throughout the program body by all functions. When you call a function, the variables declared inside it are brought into scope. Following is a simple example −

[Live Demo](http://tpcg.io/mR877c)

#!/usr/bin/python3 total =  0  # This is global variable.  # Function definition is here  def sum( arg1, arg2 ):  # Add both the parameters and return them." total = arg1 + arg2;  # Here total is local variable.  print  ("Inside the function local total : ", total)  return total # Now you can call sum function sum(  10,  20  )  print  ("Outside the function global total : ", total )

When the above code is executed, it produces the following result −

Inside the function local total :  30
Outside the function global total :  0

# Python 3 - Modules

A module allows you to logically organize your Python code. Grouping related code into a module makes the code easier to understand and use. A module is a Python object with arbitrarily named attributes that you can bind and reference.

Simply, a module is a file consisting of Python code. A module can define functions, classes and variables. A module can also include runnable code.

### Example

The Python code for a module named aname normally resides in a file namedaname.py. Here is an example of a simple module, support.py −

def print_func( par ):  print  "Hello : ", par return

## The import Statement

You can use any Python source file as a module by executing an import statement in some other Python source file. The  **import**  has the following syntax −

import module1[, module2[,... moduleN]

When the interpreter encounters an import statement, it imports the module if the module is present in the search path. A search path is a list of directories that the interpreter searches before importing a module. For example, to import the module hello.py, you need to put the following command at the top of the script −

#!/usr/bin/python3  # Import module support  import support # Now you can call defined function that module as follows support.print_func("Zara")

When the above code is executed, it produces the following result −

Hello : Zara

A module is loaded only once, regardless of the number of times it is imported. This prevents the module execution from happening repeatedly, if multiple imports occur.

## The from...import Statement

Python's  **from**  statement lets you import specific attributes from a module into the current namespace. The  **from...import**  has the following syntax −

from modname import name1[, name2[, ... nameN]]

For example, to import the function fibonacci from the module fib, use the following statement −

#!/usr/bin/python3  # Fibonacci numbers module  def fib(n):  # return Fibonacci series up to n result =  [] a, b =  0,  1  while b < n: result.append(b) a, b = b, a + b return result >>>  from fib import fib >>> fib(100)  [1,  1,  2,  3,  5,  8,  13,  21,  34,  55,  89]

This statement does not import the entire module fib into the current namespace; it just introduces the item fibonacci from the module fib into the global symbol table of the importing module.

## The from...import * Statement

It is also possible to import all the names from a module into the current namespace by using the following import statement −

from modname import *

This provides an easy way to import all the items from a module into the current namespace; however, this statement should be used sparingly.

## Executing Modules as Scripts

Within a module, the module’s name (as a string) is available as the value of the global variable __name__. The code in the module will be executed, just as if you imported it, but with the __name__ set to "__main__".

Add this code at the end of your module −

[Live Demo](http://tpcg.io/m8xId0)

#!/usr/bin/python3  # Fibonacci numbers module  def fib(n):  # return Fibonacci series up to n result =  [] a, b =  0,  1  while b < n: result.append(b) a, b = b, a + b return result if __name__ ==  "__main__": f = fib(100)  print(f)

When you run the above code, the following output will be displayed.

[1,  1,  2,  3,  5,  8,  13,  21,  34,  55,  89]

## Locating Modules

When you import a module, the Python interpreter searches for the module in the following sequences −

-   The current directory.
    
-   If the module is not found, Python then searches each directory in the shell variable PYTHONPATH.
    
-   If all else fails, Python checks the default path. On UNIX, this default path is normally /usr/local/lib/python3/.
    

The module search path is stored in the system module sys as the  **sys.path**  variable. The sys.path variable contains the current directory, PYTHONPATH, and the installation-dependent default.

## The PYTHONPATH Variable

The PYTHONPATH is an environment variable, consisting of a list of directories. The syntax of PYTHONPATH is the same as that of the shell variable PATH.

Here is a typical PYTHONPATH from a Windows system −

set PYTHONPATH = c:\python34\lib;

And here is a typical PYTHONPATH from a UNIX system −

set PYTHONPATH =  /usr/local/lib/python

## Namespaces and Scoping

Variables are names (identifiers) that map to objects. A  _namespace_  is a dictionary of variable names (keys) and their corresponding objects (values).

-   A Python statement can access variables in a  _local namespace_  and in the  _global namespace_. If a local and a global variable have the same name, the local variable shadows the global variable.
    
-   Each function has its own local namespace. Class methods follow the same scoping rule as ordinary functions.
    
-   Python makes educated guesses on whether variables are local or global. It assumes that any variable assigned a value in a function is local.
    
-   Therefore, in order to assign a value to a global variable within a function, you must first use the global statement.
    
-   The statement  _global VarName_  tells Python that VarName is a global variable. Python stops searching the local namespace for the variable.

For example, we define a variable  _Money_  in the global namespace. Within the function Money, we assign Money a value, therefore Python assumes Money as a local variable.

However, we accessed the value of the local variable  _Money_  before setting it, so an UnboundLocalError is the result. Uncommenting the global statement fixes the problem.

[Live Demo](http://tpcg.io/lHdtHD)

#!/usr/bin/python3  Money  =  2000  def  AddMoney():  # Uncomment the following line to fix the code:  # global Money  Money  =  Money  +  1  print  (Money)  AddMoney()  print  (Money)

## The dir( ) Function

The dir() built-in function returns a sorted list of strings containing the names defined by a module.

The list contains the names of all the modules, variables and functions that are defined in a module. Following is a simple example −

[Live Demo](http://tpcg.io/NLz0dc)

#!/usr/bin/python3  # Import built-in module math  import math

content = dir(math)  print  (content)

When the above code is executed, it produces the following result −

['__doc__',  '__file__',  '__name__',  'acos',  'asin',  'atan',  'atan2',  'ceil',  'cos',  'cosh',  'degrees',  'e',  'exp',  'fabs',  'floor',  'fmod',  'frexp',  'hypot',  'ldexp',  'log',  'log10',  'modf',  'pi',  'pow',  'radians',  'sin',  'sinh',  'sqrt',  'tan',  'tanh']

Here, the special string variable __name__ is the module's name, and __file__ is the filename from which the module was loaded.

## The globals() and locals() Functions

The  **globals()**  and  **locals()**  functions can be used to return the names in the global and local namespaces depending on the location from where they are called.

-   If  **locals()**  is called from within a function, it will return all the names that can be accessed locally from that function.
    
-   If  **globals()**  is called from within a function, it will return all the names that can be accessed globally from that function.
    

The return type of both these functions is dictionary. Therefore, names can be extracted using the  **keys()**  function.

## The reload() Function

When a module is imported into a script, the code in the top-level portion of a module is executed only once.

Therefore, if you want to reexecute the top-level code in a module, you can use the  _reload()_  function. The reload() function imports a previously imported module again. The syntax of the reload() function is this −

reload(module_name)

Here, module_name is the name of the module you want to reload and not the string containing the module name. For example, to reload hello module, do the following −

reload(hello)

## Packages in Python

A package is a hierarchical file directory structure that defines a single Python application environment that consists of modules and subpackages and sub-subpackages, and so on.

Consider a file  _Pots.py_  available in Phone directory. This file has the following line of source code −

#!/usr/bin/python3  def  Pots():  print  ("I'm Pots Phone")  

Similar, we have other two files having different functions with the same name as above. They are −

-   _Phone/Isdn.py_  file having function Isdn()
    
-   _Phone/G3.py_  file having function G3()
    

Now, create one more file __init__.py in the  _Phone_  directory −

-   Phone/__init__.py

To make all of your functions available when you have imported Phone, you need to put explicit import statements in __init__.py as follows −

from  Pots  import  Pots  from  Isdn  import  Isdn  from G3 import G3

After you add these lines to __init__.py, you have all of these classes available when you import the Phone package.

#!/usr/bin/python3  # Now import your Phone Package.  import  Phone  Phone.Pots()  Phone.Isdn()  Phone.G3()

When the above code is executed, it produces the following result −

I'm Pots Phone
I'm 3G  Phone I'm ISDN Phone

In the above example, we have taken example of a single function in each file, but you can keep multiple functions in your files. You can also define different Python classes in those files and then you can create your packages out of those classes.

# Python 3 - Files I/O

This chapter covers all the basic I/O functions available in Python 3. For more functions, please refer to the standard Python documentation.

## Printing to the Screen

The simplest way to produce output is using the  _print_  statement where you can pass zero or more expressions separated by commas. This function converts the expressions you pass into a string and writes the result to standard output as follows −

[Live Demo](http://tpcg.io/fYN916)

#!/usr/bin/python3  print  ("Python is really a great language,",  "isn't it?")

This produces the following result on your standard screen −

Python is really a great language, isn't it?

## Reading Keyboard Input

Python 2 has two built-in functions to read data from standard input, which by default comes from the keyboard. These functions are  **input()**  and  **raw_input()**

In Python 3, raw_input() function is deprecated. Moreover, input() functions read data from keyboard as string, irrespective of whether it is enclosed with quotes ('' or "" ) or not.

## The input Function

The  **input([prompt])**  function is equivalent to raw_input, except that it assumes that the input is a valid Python expression and returns the evaluated result to you.

#!/usr/bin/python3  >>> x = input("something:") something:10  >>> x '10'  >>> x = input("something:") something:'10'  #entered data treated as string with or without ''  >>> x "'10'"

## Opening and Closing Files

Until now, you have been reading and writing to the standard input and output. Now, we will see how to use actual data files.

Python provides basic functions and methods necessary to manipulate files by default. You can do most of the file manipulation using a  **file**  object.

## The open Function

Before you can read or write a file, you have to open it using Python's built-in open() function. This function creates a  **file**  object, which would be utilized to call other support methods associated with it.

### Syntax

file object = open(file_name [, access_mode][, buffering])

Here are parameter details −

-   **file_name**  − The file_name argument is a string value that contains the name of the file that you want to access.
    
-   **access_mode**  − The access_mode determines the mode in which the file has to be opened, i.e., read, write, append, etc. A complete list of possible values is given below in the table. This is an optional parameter and the default file access mode is read (r).
    
-   **buffering**  − If the buffering value is set to 0, no buffering takes place. If the buffering value is 1, line buffering is performed while accessing a file. If you specify the buffering value as an integer greater than 1, then buffering action is performed with the indicated buffer size. If negative, the buffer size is the system default(default behavior).
    

Here is a list of the different modes of opening a file −

Sr.No.

Mode & Description

1

**r**

Opens a file for reading only. The file pointer is placed at the beginning of the file. This is the default mode.

2

**rb**

Opens a file for reading only in binary format. The file pointer is placed at the beginning of the file. This is the default mode.

3

**r+**

Opens a file for both reading and writing. The file pointer placed at the beginning of the file.

4

**rb+**

Opens a file for both reading and writing in binary format. The file pointer placed at the beginning of the file.

5

**w**

Opens a file for writing only. Overwrites the file if the file exists. If the file does not exist, creates a new file for writing.

6

**wb**

Opens a file for writing only in binary format. Overwrites the file if the file exists. If the file does not exist, creates a new file for writing.

7

**w+**

Opens a file for both writing and reading. Overwrites the existing file if the file exists. If the file does not exist, creates a new file for reading and writing.

8

**wb+**

Opens a file for both writing and reading in binary format. Overwrites the existing file if the file exists. If the file does not exist, creates a new file for reading and writing.

9

**a**

Opens a file for appending. The file pointer is at the end of the file if the file exists. That is, the file is in the append mode. If the file does not exist, it creates a new file for writing.

10

**ab**

Opens a file for appending in binary format. The file pointer is at the end of the file if the file exists. That is, the file is in the append mode. If the file does not exist, it creates a new file for writing.

11

**a+**

Opens a file for both appending and reading. The file pointer is at the end of the file if the file exists. The file opens in the append mode. If the file does not exist, it creates a new file for reading and writing.

12

**ab+**

Opens a file for both appending and reading in binary format. The file pointer is at the end of the file if the file exists. The file opens in the append mode. If the file does not exist, it creates a new file for reading and writing.

## The file Object Attributes

Once a file is opened and you have one  _file_  object, you can get various information related to that file.

Here is a list of all the attributes related to a file object −

Sr.No.

Attribute & Description

1

**file.closed**

Returns true if file is closed, false otherwise.

2

**file.mode**

Returns access mode with which file was opened.

3

**file.name**

Returns name of the file.

**Note**  − softspace attribute is not supported in Python 3.x

### Example

[Live Demo](http://tpcg.io/Ux8rpv)

#!/usr/bin/python3  # Open a file fo = open("foo.txt",  "wb")  print  ("Name of the file: ", fo.name)  print  ("Closed or not : ", fo.closed)  print  ("Opening mode : ", fo.mode) fo.close()

This produces the following result −

Name of the file:  foo.txt
Closed or not :  False
Opening mode :  wb

## The close() Method

The close() method of a file object flushes any unwritten information and closes the file object, after which no more writing can be done.

Python automatically closes a file when the reference object of a file is reassigned to another file. It is a good practice to use the close() method to close a file.

### Syntax

fileObject.close();

### Example

[Live Demo](http://tpcg.io/xXErpK)

#!/usr/bin/python3  # Open a file fo = open("foo.txt",  "wb")  print  ("Name of the file: ", fo.name)  # Close opened file fo.close()

This produces the following result −

Name of the file:  foo.txt

## Reading and Writing Files

The file object provides a set of access methods to make our lives easier. We would see how to use  **read()**  and  **write()**  methods to read and write files.

## The write() Method

The  **write()**  method writes any string to an open file. It is important to note that Python strings can have binary data and not just text.

The write() method does not add a newline character ('\n') to the end of the string −

### Syntax

fileObject.write(string);

Here, passed parameter is the content to be written into the opened file.

### Example

#!/usr/bin/python3  # Open a file fo = open("foo.txt",  "w") fo.write(  "Python is a great language.\nYeah its great!!\n")  # Close opend file fo.close()

The above method would create foo.txt file and would write given content in that file and finally it would close that file. If you would open this file, it would have the following content −

Python is a great language.
Yeah its great!!

## The read() Method

The  **read()**  method reads a string from an open file. It is important to note that Python strings can have binary data. apart from text data.

### Syntax

fileObject.read([count]);

Here, passed parameter is the number of bytes to be read from the opened file. This method starts reading from the beginning of the file and if  _count_  is missing, then it tries to read as much as possible, maybe until the end of file.

### Example

Let us take a file  _foo.txt_, which we created above.

#!/usr/bin/python3  # Open a file fo = open("foo.txt",  "r+") str = fo.read(10)  print  ("Read String is : ", str)  # Close opened file fo.close()

This produces the following result −

Read String is :  Python is

## File Positions

The  _tell()_  method tells you the current position within the file; in other words, the next read or write will occur at that many bytes from the beginning of the file.

The  _seek(offset[, from])_  method changes the current file position. The  **offset**  argument indicates the number of bytes to be moved. The  **from**  argument specifies the reference position from where the bytes are to be moved.

If  _from_  is set to 0, the beginning of the file is used as the reference position. If it is set to 1, the current position is used as the reference position. If it is set to 2 then the end of the file would be taken as the reference position.

### Example

Let us take a file  _foo.txt_, which we created above.

#!/usr/bin/python3  # Open a file fo = open("foo.txt",  "r+") str = fo.read(10)  print  ("Read String is : ", str)  # Check current position position = fo.tell()  print  ("Current file position : ", position)  # Reposition pointer at the beginning once again position = fo.seek(0,  0) str = fo.read(10)  print  ("Again read String is : ", str)  # Close opened file fo.close()

This produces the following result −

Read String is :  Python is
Current file position :  10
Again read String is :  Python is

## Renaming and Deleting Files

Python  **os**  module provides methods that help you perform file-processing operations, such as renaming and deleting files.

To use this module, you need to import it first and then you can call any related functions.

## The rename() Method

The  **rename()**  method takes two arguments, the current filename and the new filename.

### Syntax

os.rename(current_file_name, new_file_name)

### Example

Following is an example to rename an existing file  _test1.txt_  −

#!/usr/bin/python3  import os # Rename a file from test1.txt to test2.txt os.rename(  "test1.txt",  "test2.txt"  )

## The remove() Method

You can use the  **remove()**  method to delete files by supplying the name of the file to be deleted as the argument.

### Syntax

os.remove(file_name)

### Example

Following is an example to delete an existing file  _test2.txt_  −

#!/usr/bin/python3  import os # Delete file test2.txt os.remove("text2.txt")

## Directories in Python

All files are contained within various directories, and Python has no problem handling these too. The  **os**  module has several methods that help you create, remove, and change directories.

## The mkdir() Method

You can use the  **mkdir()**  method of the  **os**  module to create directories in the current directory. You need to supply an argument to this method, which contains the name of the directory to be created.

### Syntax

os.mkdir("newdir")

### Example

Following is an example to create a directory  _test_  in the current directory −

#!/usr/bin/python3  import os # Create a directory "test" os.mkdir("test")

## The chdir() Method

You can use the  _chdir()_  method to change the current directory. The chdir() method takes an argument, which is the name of the directory that you want to make the current directory.

### Syntax

os.chdir("newdir")

### Example

Following is an example to go into "/home/newdir" directory −

#!/usr/bin/python3  import os # Changing a directory to "/home/newdir" os.chdir("/home/newdir")

## The getcwd() Method

The  **getcwd()**  method displays the current working directory.

### Syntax

os.getcwd()

### Example

Following is an example to give current directory −

#!/usr/bin/python3  import os # This would give location of the current directory os.getcwd()

## The rmdir() Method

The  **rmdir()**  method deletes the directory, which is passed as an argument in the method.

Before removing a directory, all the contents in it should be removed.

### Syntax

os.rmdir('dirname')

### Example

Following is an example to remove the "/tmp/test" directory. It is required to give fully qualified name of the directory, otherwise it would search for that directory in the current directory.

#!/usr/bin/python3  import os # This would  remove "/tmp/test"  directory. os.rmdir(  "/tmp/test"  )

## File and Directory Related Methods

There are three important sources, which provide a wide range of utility methods to handle and manipulate files & directories on Windows and Unix operating systems. They are as follows −

-   [File Object Methods](https://www.tutorialspoint.com/python3/file_methods.htm)
    
    The  **file**  object provides functions to manipulate files.
    
-   [OS Object Methods](https://www.tutorialspoint.com/python3/os_file_methods.htm)
    
    This provides methods to process files as well as directories.
    

# Python 3 - Exceptions Handling

Python provides two very important features to handle any unexpected error in your Python programs and to add debugging capabilities in them −

-   **Exception Handling**  − This would be covered in this tutorial. Here is a list standard Exceptions available in Python −  [Standard Exceptions](https://www.tutorialspoint.com/python3/python_exceptions.htm#standard_exceptions).
    
-   **Assertions**  − This would be covered in  [Assertions in Python 3](https://www.tutorialspoint.com/python3/python_exceptions.htm#assertion_python)  tutorial.
    

## Standard Exceptions

Here is a list of Standard Exceptions available in Python. −

Sr.No.

Exception Name & Description

1

**Exception**

Base class for all exceptions

2

**StopIteration**

Raised when the next() method of an iterator does not point to any object.

3

**SystemExit**

Raised by the sys.exit() function.

4

**StandardError**

Base class for all built-in exceptions except StopIteration and SystemExit.

5

**ArithmeticError**

Base class for all errors that occur for numeric calculation.

6

**OverflowError**

Raised when a calculation exceeds maximum limit for a numeric type.

7

**FloatingPointError**

Raised when a floating point calculation fails.

8

**ZeroDivisonError**

Raised when division or modulo by zero takes place for all numeric types.

9

**AssertionError**

Raised in case of failure of the Assert statement.

10

**AttributeError**

Raised in case of failure of attribute reference or assignment.

11

**EOFError**

Raised when there is no input from either the raw_input() or input() function and the end of file is reached.

12

**ImportError**

Raised when an import statement fails.

13

**KeyboardInterrupt**

Raised when the user interrupts program execution, usually by pressing Ctrl+c.

14

**LookupError**

Base class for all lookup errors.

15

**IndexError**

Raised when an index is not found in a sequence.

16

**KeyError**

Raised when the specified key is not found in the dictionary.

17

**NameError**

Raised when an identifier is not found in the local or global namespace.

18

**UnboundLocalError**

Raised when trying to access a local variable in a function or method but no value has been assigned to it.

19

**EnvironmentError**

Base class for all exceptions that occur outside the Python environment.

20

**IOError**

Raised when an input/ output operation fails, such as the print statement or the open() function when trying to open a file that does not exist.

21

**OSError**

Raised for operating system-related errors.

22

**SyntaxError**

Raised when there is an error in Python syntax.

23

**IndentationError**

Raised when indentation is not specified properly.

24

**SystemError**

Raised when the interpreter finds an internal problem, but when this error is encountered the Python interpreter does not exit.

25

**SystemExit**

Raised when Python interpreter is quit by using the sys.exit() function. If not handled in the code, causes the interpreter to exit.

26

**TypeError**

Raised when an operation or function is attempted that is invalid for the specified data type.

27

**ValueError**

Raised when the built-in function for a data type has the valid type of arguments, but the arguments have invalid values specified.

28

**RuntimeError**

Raised when a generated error does not fall into any category.

29

**NotImplementedError**

Raised when an abstract method that needs to be implemented in an inherited class is not actually implemented.

## Assertions in Python

An assertion is a sanity-check that you can turn on or turn off when you are done with your testing of the program.

-   The easiest way to think of an assertion is to liken it to a  **raise-if**  statement (or to be more accurate, a raise-if-not statement). An expression is tested, and if the result comes up false, an exception is raised.
    
-   Assertions are carried out by the assert statement, the newest keyword to Python, introduced in version 1.5.
    
-   Programmers often place assertions at the start of a function to check for valid input, and after a function call to check for valid output.
    

### The assert Statement

When it encounters an assert statement, Python evaluates the accompanying expression, which is hopefully true. If the expression is false, Python raises an  _AssertionError_  exception.

The syntax for assert is −

assert Expression[, Arguments]

If the assertion fails, Python uses ArgumentExpression as the argument for the AssertionError. AssertionError exceptions can be caught and handled like any other exception, using the try-except statement. If they are not handled, they will terminate the program and produce a traceback.

### Example

Here is a function that converts a given temperature from degrees Kelvin to degrees Fahrenheit. Since 0° K is as cold as it gets, the function bails out if it sees a negative temperature −

[Live Demo](http://tpcg.io/r1PgMi)

#!/usr/bin/python3  def  KelvinToFahrenheit(Temperature):  assert  (Temperature  >=  0),"Colder than absolute zero!"  return  ((Temperature-273)*1.8)+32  print  (KelvinToFahrenheit(273))  print  (int(KelvinToFahrenheit(505.78)))  print  (KelvinToFahrenheit(-5))

When the above code is executed, it produces the following result −

32.0
451
Traceback (most recent call last):
File "test.py", line 9, in <module>
print KelvinToFahrenheit(-5)
File "test.py", line 4, in KelvinToFahrenheit
assert (Temperature >= 0),"Colder than absolute zero!"
AssertionError: Colder than absolute zero!

## What is Exception?

An exception is an event, which occurs during the execution of a program that disrupts the normal flow of the program's instructions. In general, when a Python script encounters a situation that it cannot cope with, it raises an exception. An exception is a Python object that represents an error.

When a Python script raises an exception, it must either handle the exception immediately otherwise it terminates and quits.

## Handling an exception

If you have some  _suspicious_  code that may raise an exception, you can defend your program by placing the suspicious code in a  **try:**  block. After the try: block, include an  **except:**  statement, followed by a block of code which handles the problem as elegantly as possible.

### Syntax

Here is simple syntax of  _try....except...else_  blocks −

try:  You  do your operations here ......................  except  ExceptionI:  If there is  ExceptionI,  then execute this block.  except  ExceptionII:  If there is  ExceptionII,  then execute this block.  ......................  else:  If there is  no exception then execute this block.  

Here are few important points about the above-mentioned syntax −

-   A single try statement can have multiple except statements. This is useful when the try block contains statements that may throw different types of exceptions.
    
-   You can also provide a generic except clause, which handles any exception.
    
-   After the except clause(s), you can include an else-clause. The code in the else-block executes if the code in the try: block does not raise an exception.
    
-   The else-block is a good place for code that does not need the try: block's protection.
    

### Example

This example opens a file, writes content in the, file and comes out gracefully because there is no problem at all −

[Live Demo](http://tpcg.io/oxCWSE)

#!/usr/bin/python3  try: fh = open("testfile",  "w") fh.write("This is my test file for exception handling!!")  except  IOError:  print  ("Error: can\'t find file or read data")  else:  print  ("Written content in the file successfully") fh.close()

This produces the following result −

Written content in the file successfully

### Example

This example tries to open a file where you do not have the write permission, so it raises an exception −

[Live Demo](http://tpcg.io/ceZWjn)

#!/usr/bin/python3  try: fh = open("testfile",  "r") fh.write("This is my test file for exception handling!!")  except  IOError:  print  ("Error: can\'t find file or read data")  else:  print  ("Written content in the file successfully")

This produces the following result −

Error: can't find file or read data

## The except Clause with No Exceptions

You can also use the except statement with no exceptions defined as follows −

try:  You  do your operations here ......................  except:  If there is any exception,  then execute this block.  ......................  else:  If there is  no exception then execute this block.  

This kind of a  **try-except**  statement catches all the exceptions that occur. Using this kind of try-except statement is not considered a good programming practice though, because it catches all exceptions but does not make the programmer identify the root cause of the problem that may occur.

## The except Clause with Multiple Exceptions

You can also use the same  _except_  statement to handle multiple exceptions as follows −

try:  You  do your operations here ......................  except(Exception1[,  Exception2[,...ExceptionN]]]):  If there is any exception from the given exception list,  then execute this block.  ......................  else:  If there is  no exception then execute this block.  

## The try-finally Clause

You can use a  **finally:**  block along with a  **try:**  block. The  **finally:**  block is a place to put any code that must execute, whether the try-block raised an exception or not. The syntax of the try-finally statement is this −

try:  You  do your operations here;  ......................  Due to any exception,  this may be skipped.  finally:  This would always be executed.  ......................

**Note**  − You can provide except clause(s), or a finally clause, but not both. You cannot use  _else_  clause as well along with a finally clause.

### Example

[Live Demo](http://tpcg.io/RR5c1J)

#!/usr/bin/python3  try: fh = open("testfile",  "w") fh.write("This is my test file for exception handling!!")  finally:  print  ("Error: can\'t find file or read data") fh.close()

If you do not have permission to open the file in writing mode, then this will produce the following result −

Error: can't find file or read data

Same example can be written more cleanly as follows −

[Live Demo](http://tpcg.io/s2jDA4)

#!/usr/bin/python3  try: fh = open("testfile",  "w")  try: fh.write("This is my test file for exception handling!!")  finally:  print  ("Going to close the file") fh.close()  except  IOError:  print  ("Error: can\'t find file or read data")

This produces the following result −

Going to close the file

When an exception is thrown in the  _try_  block, the execution immediately passes to the  _finally_  block. After all the statements in the  _finally_  block are executed, the exception is raised again and is handled in the  _except_  statements if present in the next higher layer of the  _try-except_  statement.

## Argument of an Exception

An exception can have an  _argument_, which is a value that gives additional information about the problem. The contents of the argument vary by exception. You capture an exception's argument by supplying a variable in the except clause as follows −

try:  You  do your operations here ......................  except  ExceptionType  as  Argument:  You can print  value  of  Argument here...

If you write the code to handle a single exception, you can have a variable follow the name of the exception in the except statement. If you are trapping multiple exceptions, you can have a variable follow the tuple of the exception.

This variable receives the value of the exception mostly containing the cause of the exception. The variable can receive a single value or multiple values in the form of a tuple. This tuple usually contains the error string, the error number, and an error location.

### Example

Following is an example for a single exception −

[Live Demo](http://tpcg.io/aP6Dfo)

#!/usr/bin/python3  # Define a function here.  def temp_convert(var):  try:  return  int(var)  except  ValueError  as  Argument:  print  ("The argument does not contain numbers\n",  Argument)  # Call above function here. temp_convert("xyz")

This produces the following result −

The argument does not contain numbers
invalid literal for int() with base 10: 'xyz'

## Raising an Exception

You can raise exceptions in several ways by using the raise statement. The general syntax for the  **raise**  statement is as follows −

### Syntax

raise [Exception [, args [, traceback]]]

Here,  _Exception_  is the type of exception (for example, NameError) and  _argument_  is a value for the exception argument. The argument is optional; if not supplied, the exception argument is None.

The final argument, traceback, is also optional (and rarely used in practice), and if present, is the traceback object used for the exception.

### Example

An exception can be a string, a class or an object. Most of the exceptions that the Python core raises are classes, with an argument that is an instance of the class. Defining new exceptions is quite easy and can be done as follows −

def functionName( level ):  if level <1:  raise  Exception(level)  # The code below to this would not be executed  # if we raise the exception  return level

**Note**  − In order to catch an exception, an "except" clause must refer to the same exception thrown either as a class object or a simple string. For example, to capture the above exception, we must write the except clause as follows −

try:  Business  Logic here...  except  Exception  as e:  Exception handling here using e.args...  else:  Rest  of the code here...

The following example illustrates the use of raising an exception −

[Live Demo](http://tpcg.io/j1AB30)

#!/usr/bin/python3  def functionName( level ):  if level <1:  raise  Exception(level)  # The code below to this would not be executed  # if we raise the exception  return level try: l = functionName(-10)  print  ("level = ",l)  except  Exception  as e:  print  ("error in level argument",e.args[0])

This will produce the following result

error in level argument -10

## User-Defined Exceptions

Python also allows you to create your own exceptions by deriving classes from the standard built-in exceptions.

Here is an example related to  _RuntimeError_. Here, a class is created that is subclassed from  _RuntimeError_. This is useful when you need to display more specific information when an exception is caught.

In the try block, the user-defined exception is raised and caught in the except block. The variable e is used to create an instance of the class  _Networkerror_.

class  Networkerror(RuntimeError):  def __init__(self, arg):  self.args = arg

So once you have defined the above class, you can raise the exception as follows −

try:  raise  Networkerror("Bad hostname")  except  Networkerror,e:  print e.args

# Python 3 - Object Oriented

Python has been an object-oriented language since the time it existed. Due to this, creating and using classes and objects are downright easy. This chapter helps you become an expert in using Python's object-oriented programming support.

If you do not have any previous experience with object-oriented (OO) programming, you may want to consult an introductory course on it or at least a tutorial of some sort so that you have a grasp of the basic concepts.

However, here is a small introduction of Object-Oriented Programming (OOP) to help you −

## Overview of OOP Terminology

-   **Class**  − A user-defined prototype for an object that defines a set of attributes that characterize any object of the class. The attributes are data members (class variables and instance variables) and methods, accessed via dot notation.
    
-   **Class variable**  − A variable that is shared by all instances of a class. Class variables are defined within a class but outside any of the class's methods. Class variables are not used as frequently as instance variables are.
    
-   **Data member**  − A class variable or instance variable that holds data associated with a class and its objects.
    
-   **Function overloading**  − The assignment of more than one behavior to a particular function. The operation performed varies by the types of objects or arguments involved.
    
-   **Instance variable**  − A variable that is defined inside a method and belongs only to the current instance of a class.
    
-   **Inheritance**  − The transfer of the characteristics of a class to other classes that are derived from it.
    
-   **Instance**  − An individual object of a certain class. An object obj that belongs to a class Circle, for example, is an instance of the class Circle.
    
-   **Instantiation**  − The creation of an instance of a class.
    
-   **Method** − A special kind of function that is defined in a class definition.
    
-   **Object**  − A unique instance of a data structure that is defined by its class. An object comprises both data members (class variables and instance variables) and methods.
    
-   **Operator overloading**  − The assignment of more than one function to a particular operator.
    

## Creating Classes

The  _class_  statement creates a new class definition. The name of the class immediately follows the keyword  _class_  followed by a colon as follows −

class  ClassName:  'Optional class documentation string' class_suite

-   The class has a documentation string, which can be accessed via  _**ClassName.__doc__**_.
    
-   The  _**class_suite**_  consists of all the component statements defining class members, data attributes and functions.
    

### Example

Following is an example of a simple Python class −

class  Employee:  'Common base class for all employees' empCount =  0  def __init__(self, name, salary):  self.name = name self.salary = salary Employee.empCount +=  1  def displayCount(self):  print  ("Total Employee %d"  %  Employee.empCount)  def displayEmployee(self):  print  ("Name : ",  self.name,  ", Salary: ",  self.salary)

-   The variable  _empCount_  is a class variable whose value is shared among all the instances of a in this class. This can be accessed as  _Employee.empCount_  from inside the class or outside the class.
    
-   The first method  ___init__()_  is a special method, which is called class constructor or initialization method that Python calls when you create a new instance of this class.
    
-   You declare other class methods like normal functions with the exception that the first argument to each method is  _self_. Python adds the  _self_  argument to the list for you; you do not need to include it when you call the methods.
    

## Creating Instance Objects

To create instances of a class, you call the class using class name and pass in whatever arguments its  ___init___  method accepts.

This would create first object  of  Employee  class emp1 =  Employee("Zara",  2000)  This would create second object  of  Employee  class emp2 =  Employee("Manni",  5000)

## Accessing Attributes

You access the object's attributes using the dot operator with object. Class variable would be accessed using class name as follows −

emp1.displayEmployee() emp2.displayEmployee()  print  ("Total Employee %d"  %  Employee.empCount)

Now, putting all the concepts together −

[Live Demo](http://tpcg.io/vWFIez)

#!/usr/bin/python3  class  Employee:  'Common base class for all employees' empCount =  0  def __init__(self, name, salary):  self.name = name self.salary = salary Employee.empCount +=  1  def displayCount(self):  print  ("Total Employee %d"  %  Employee.empCount)  def displayEmployee(self):  print  ("Name : ",  self.name,  ", Salary: ",  self.salary)  #This would create first object of Employee class" emp1 =  Employee("Zara",  2000)  #This would create second object of Employee class" emp2 =  Employee("Manni",  5000) emp1.displayEmployee() emp2.displayEmployee()  print  ("Total Employee %d"  %  Employee.empCount)

When the above code is executed, it produces the following result −

Name :  Zara ,Salary:  2000
Name :  Manni ,Salary:  5000
Total Employee 2

You can add, remove, or modify attributes of classes and objects at any time −

emp1.salary = 7000  # Add an 'salary' attribute.
emp1.name = 'xyz'  # Modify 'age' attribute.
del emp1.salary  # Delete 'age' attribute.

Instead of using the normal statements to access attributes, you can use the following functions −

-   The  **getattr(obj, name[, default])**  − to access the attribute of object.
    
-   The  **hasattr(obj,name)**  − to check if an attribute exists or not.
    
-   The  **setattr(obj,name,value)**  − to set an attribute. If attribute does not exist, then it would be created.
    
-   The  **delattr(obj, name)**  − to delete an attribute.
    

hasattr(emp1,  'salary')  # Returns true if 'salary' attribute exists getattr(emp1,  'salary')  # Returns value of 'salary' attribute setattr(emp1,  'salary',  7000)  # Set attribute 'salary' at 7000 delattr(emp1,  'salary')  # Delete attribute 'salary'

## Built-In Class Attributes

Every Python class keeps following built-in attributes and they can be accessed using dot operator like any other attribute −

-   **__dict__**  − Dictionary containing the class's namespace.
    
-   **__doc__**  − Class documentation string or none, if undefined.
    
-   **__name__**  − Class name.
    
-   **__module__**  − Module name in which the class is defined. This attribute is "__main__" in interactive mode.
    
-   **__bases__**  − A possibly empty tuple containing the base classes, in the order of their occurrence in the base class list.
    

For the above class let us try to access all these attributes −

[Live Demo](http://tpcg.io/YzU4mJ)

#!/usr/bin/python3  class  Employee:  'Common base class for all employees' empCount =  0  def __init__(self, name, salary):  self.name = name self.salary = salary Employee.empCount +=  1  def displayCount(self):  print  ("Total Employee %d"  %  Employee.empCount)  def displayEmployee(self):  print  ("Name : ",  self.name,  ", Salary: ",  self.salary) emp1 =  Employee("Zara",  2000) emp2 =  Employee("Manni",  5000)  print  ("Employee.__doc__:",  Employee.__doc__)  print  ("Employee.__name__:",  Employee.__name__)  print  ("Employee.__module__:",  Employee.__module__)  print  ("Employee.__bases__:",  Employee.__bases__)  print  ("Employee.__dict__:",  Employee.__dict__ )

When the above code is executed, it produces the following result −

Employee.__doc__: Common base class for all employees
Employee.__name__: Employee
Employee.__module__: __main__
Employee.__bases__: (<class 'object'>,)
Employee.__dict__: {
   'displayCount': <function Employee.displayCount at 0x0160D2B8>, 
   '__module__': '__main__', '__doc__': 'Common base class for all employees', 
   'empCount': 2, '__init__': 
   <function Employee.__init__ at 0x0124F810>, 'displayEmployee': 
   <function Employee.displayEmployee at 0x0160D300>,
   '__weakref__': 
   <attribute '__weakref__' of 'Employee' objects>, '__dict__': 
   <attribute '__dict__' of 'Employee' objects>
}

## Destroying Objects (Garbage Collection)

Python deletes unneeded objects (built-in types or class instances) automatically to free the memory space. The process by which Python periodically reclaims blocks of memory that no longer are in use is termed as Garbage Collection.

Python's garbage collector runs during program execution and is triggered when an object's reference count reaches zero. An object's reference count changes as the number of aliases that point to it changes.

An object's reference count increases when it is assigned a new name or placed in a container (list, tuple, or dictionary). The object's reference count decreases when it is deleted with  _del_, its reference is reassigned, or its reference goes out of scope. When an object's reference count reaches zero, Python collects it automatically.

a =  40  # Create object <40> b = a # Increase ref. count  of <40> c =  [b]  # Increase ref. count  of <40>  del a # Decrease ref. count  of <40> b =  100  # Decrease ref. count  of <40> 
c[0]  =  -1  # Decrease ref. count  of <40> 

You normally will not notice when the garbage collector destroys an orphaned instance and reclaims its space. However, a class can implement the special method  ___del__()_, called a destructor, that is invoked when the instance is about to be destroyed. This method might be used to clean up any non-memory resources used by an instance.

### Example

This __del__() destructor prints the class name of an instance that is about to be destroyed −

[Live Demo](http://tpcg.io/IQRoOS)

#!/usr/bin/python3  class  Point:  def __init__(  self, x=0, y=0):  self.x = x self.y = y def __del__(self): class_name =  self.__class__.__name__ print  (class_name,  "destroyed") pt1 =  Point() pt2 = pt1
pt3 = pt1 print  (id(pt1), id(pt2), id(pt3))  # prints the ids of the obejcts  del pt1 del pt2 del pt3

When the above code is executed, it produces the following result −

140338326963984 140338326963984 140338326963984
Point destroyed

**Note**  − Ideally, you should define your classes in a separate file, then you should import them in your main program file using  _import_  statement.

In the above example, assuming definition of a Point class is contained in  _point.py_  and there is no other executable code in it.

#!/usr/bin/python3  import point

p1 = point.Point()

## Class Inheritance

Instead of starting from a scratch, you can create a class by deriving it from a pre-existing class by listing the parent class in parentheses after the new class name.

The child class inherits the attributes of its parent class, and you can use those attributes as if they were defined in the child class. A child class can also override data members and methods from the parent.

### Syntax

Derived classes are declared much like their parent class; however, a list of base classes to inherit from is given after the class name −

class  SubClassName  (ParentClass1[,  ParentClass2,  ...]):  'Optional class documentation string' class_suite

### Example

[Live Demo](http://tpcg.io/WygN4z)

#!/usr/bin/python3  class  Parent:  # define parent class parentAttr =  100  def __init__(self):  print  ("Calling parent constructor")  def parentMethod(self):  print  ('Calling parent method')  def setAttr(self, attr):  Parent.parentAttr = attr def getAttr(self):  print  ("Parent attribute :",  Parent.parentAttr)  class  Child(Parent):  # define child class  def __init__(self):  print  ("Calling child constructor")  def childMethod(self):  print  ('Calling child method') c =  Child()  # instance of child c.childMethod()  # child calls its method c.parentMethod()  # calls parent's method c.setAttr(200)  # again call parent's method c.getAttr()  # again call parent's method

When the above code is executed, it produces the following result −

Calling child constructor
Calling child method
Calling parent method
Parent attribute : 200

In a similar way, you can drive a class from multiple parent classes as follows −

class A:  # define your class A  .....  class B:  # define your calss B  .....  class C(A, B):  # subclass of A and B  .....

You can use issubclass() or isinstance() functions to check a relationships of two classes and instances.

-   The  **issubclass(sub, sup)**  boolean function returns True, if the given subclass  **sub**  is indeed a subclass of the superclass  **sup**.
    
-   The  **isinstance(obj, Class)**  boolean function returns True, if  _obj_  is an instance of class  _Class_  or is an instance of a subclass of Class
    

## Overriding Methods

You can always override your parent class methods. One reason for overriding parent's methods is that you may want special or different functionality in your subclass.

### Example

[Live Demo](http://tpcg.io/fPAqko)

#!/usr/bin/python3  class  Parent:  # define parent class  def myMethod(self):  print  ('Calling parent method')  class  Child(Parent):  # define child class  def myMethod(self):  print  ('Calling child method') c =  Child()  # instance of child c.myMethod()  # child calls overridden method

When the above code is executed, it produces the following result −

Calling child method

## Base Overloading Methods

The following table lists some generic functionality that you can override in your own classes −

Sr.No.

Method, Description & Sample Call

1

**__init__ ( self [,args...] )**

Constructor (with any optional arguments)

Sample Call :  _obj = className(args)_

2

**__del__( self )**

Destructor, deletes an object

Sample Call :  _del obj_

3

**__repr__( self )**

Evaluatable string representation

Sample Call :  _repr(obj)_

4

**__str__( self )**

Printable string representation

Sample Call :  _str(obj)_

5

**__cmp__ ( self, x )**

Object comparison

Sample Call :  _cmp(obj, x)_

## Overloading Operators

Suppose you have created a Vector class to represent two-dimensional vectors. What happens when you use the plus operator to add them? Most likely Python will yell at you.

You could, however, define the  ___add___  method in your class to perform vector addition and then the plus operator would behave as per expectation −

### Example

[Live Demo](http://tpcg.io/ShqzOr)

#!/usr/bin/python3  class  Vector:  def __init__(self, a, b):  self.a = a self.b = b def __str__(self):  return  'Vector (%d, %d)'  %  (self.a,  self.b)  def __add__(self,other):  return  Vector(self.a + other.a,  self.b + other.b) v1 =  Vector(2,10) v2 =  Vector(5,-2)  print  (v1 + v2)

When the above code is executed, it produces the following result −

Vector(7,8)

## Data Hiding

An object's attributes may or may not be visible outside the class definition. You need to name attributes with a double underscore prefix, and those attributes then will not be directly visible to outsiders.

### Example

[Live Demo](http://tpcg.io/e2b3LI)

#!/usr/bin/python3  class  JustCounter: __secretCount =  0  def count(self):  self.__secretCount +=  1  print  (self.__secretCount) counter =  JustCounter() counter.count() counter.count()  print  (counter.__secretCount)

When the above code is executed, it produces the following result −

1
2
Traceback (most recent call last):
   File "test.py", line 12, in <module>
      print counter.__secretCount
AttributeError: JustCounter instance has no attribute '__secretCount'

Python protects those members by internally changing the name to include the class name. You can access such attributes as  _object._className__attrName_. If you would replace your last line as following, then it works for you −

.........................  print  (counter._JustCounter__secretCount)

When the above code is executed, it produces the following result −

1
2
2

# Python 3 - Regular Expressions

A  _regular expression_  is a special sequence of characters that helps you match or find other strings or sets of strings, using a specialized syntax held in a pattern. Regular expressions are widely used in UNIX world.

The module  **re**  provides full support for Perl-like regular expressions in Python. The  **re**  module raises the exception  **re.error**  if an error occurs while compiling or using a regular expression.

We would cover two important functions, which would be used to handle regular expressions. Nevertheless, a small thing first: There are various characters, which would have special meaning when they are used in regular expression. To avoid any confusion while dealing with regular expressions, we would use Raw Strings as  **r'expression'**.

### Basic patterns that match single chars

Sr.No.

Expression & Matches

1

**a, X, 9, <**

ordinary characters just match themselves exactly.

2

**. (a period)**

matches any single character except newline '\n'

3

**\w**

matches a "word" character: a letter or digit or underbar [a-zA-Z0-9_].

4

**\W**

matches any non-word character.

5

**\b**

boundary between word and non-word

6

**\s**

matches a single whitespace character -- space, newline, return, tab

7

**\S**

matches any non-whitespace character.

8

**\t, \n, \r**

tab, newline, return

9

**\d**

decimal digit [0-9]

10

**^**

matches start of the string

11

**$**

match the end of the string

12

**\**

inhibit the "specialness" of a character.

### Compilation flags

Compilation flags let you modify some aspects of how regular expressions work. Flags are available in the re module under two names, a long name such as  **IGNORECASE**  and a short, one-letter form such as I.

Sr.No.

Flag & Meaning

1

**ASCII, A**

Makes several escapes like \w, \b, \s and \d match only on ASCII characters with the respective property.

2

**DOTALL, S**

Make, match any character, including newlines

3

**IGNORECASE, I**

Do case-insensitive matches

4

**LOCALE, L**

Do a locale-aware match

5

**MULTILINE, M**

Multi-line matching, affecting ^ and $

6

**VERBOSE, X (for ‘extended’)**

Enable verbose REs, which can be organized more cleanly and understandably

## The match Function

This function attempts to match RE  _pattern_  to  _string_  with optional  _flags_.

Here is the syntax for this function −

re.match(pattern, string, flags = 0)

Here is the description of the parameters −

Sr.No.

Parameter & Description

1

**pattern**

This is the regular expression to be matched.

2

**string**

This is the string, which would be searched to match the pattern at the beginning of string.

3

**flags**

You can specify different flags using bitwise OR (|). These are modifiers, which are listed in the table below.

The  _re.match_  function returns a  **match**  object on success,  **None**  on failure. We use_group(num)_  or  _groups()_  function of  **match**  object to get matched expression.

Sr.No.

Match Object Method & Description

1

**group(num = 0)**

This method returns entire match (or specific subgroup num)

2

**groups()**

This method returns all matching subgroups in a tuple (empty if there weren't any)

### Example

[Live Demo](http://tpcg.io/qdhjSh)

#!/usr/bin/python3  import re

line =  "Cats are smarter than dogs" matchObj = re.match( r'(.*) are (.*?) .*', line, re.M|re.I)  if matchObj:  print  ("matchObj.group() : ", matchObj.group())  print  ("matchObj.group(1) : ", matchObj.group(1))  print  ("matchObj.group(2) : ", matchObj.group(2))  else:  print  ("No match!!")

When the above code is executed, it produces the following result −

matchObj.group() :  Cats are smarter than dogs
matchObj.group(1) :  Cats
matchObj.group(2) :  smarter

## The search Function

This function searches for first occurrence of RE  _pattern_  within  _string_  with optional  _flags_.

Here is the syntax for this function −

re.search(pattern,  string, flags =  0)

Here is the description of the parameters −

Sr.No.

Parameter & Description

1

**pattern**

This is the regular expression to be matched.

2

**string**

This is the string, which would be searched to match the pattern anywhere in the string.

3

**flags**

You can specify different flags using bitwise OR (|). These are modifiers, which are listed in the table below.

The  _re.search_  function returns a  **match**  object on success,  **none**  on failure. We use  _group(num)_ or  _groups()_ function of  **match**  object to get the matched expression.

Sr.No.

Match Object Method & Description

1

**group(num = 0)**

This method returns entire match (or specific subgroup num)

2

**groups()**

This method returns all matching subgroups in a tuple (empty if there weren't any)

### Example

[Live Demo](http://tpcg.io/whH8IF)

#!/usr/bin/python3  import re

line =  "Cats are smarter than dogs"; searchObj = re.search( r'(.*) are (.*?) .*', line, re.M|re.I)  if searchObj:  print  ("searchObj.group() : ", searchObj.group())  print  ("searchObj.group(1) : ", searchObj.group(1))  print  ("searchObj.group(2) : ", searchObj.group(2))  else:  print  ("Nothing found!!")

When the above code is executed, it produces the following result −

matchObj.group() :  Cats are smarter than dogs
matchObj.group(1) :  Cats
matchObj.group(2) :  smarter

## Matching Versus Searching

Python offers two different primitive operations based on regular expressions:  **match**  checks for a match only at the beginning of the string, while  **search**  checks for a match anywhere in the string (this is what Perl does by default).

### Example

[Live Demo](http://tpcg.io/bQalTd)

#!/usr/bin/python3  import re

line =  "Cats are smarter than dogs"; matchObj = re.match( r'dogs', line, re.M|re.I)  if matchObj:  print  ("match --> matchObj.group() : ", matchObj.group())  else:  print  ("No match!!") searchObj = re.search( r'dogs', line, re.M|re.I)  if searchObj:  print  ("search --> searchObj.group() : ", searchObj.group())  else:  print  ("Nothing found!!")

When the above code is executed, it produces the following result −

No match!!
search --> matchObj.group() :  dogs

## Search and Replace

One of the most important  **re**  methods that use regular expressions is  **sub**.

### Syntax

re.sub(pattern, repl, string, max=0)

This method replaces all occurrences of the RE  _pattern_  in  _string_  with  _repl_, substituting all occurrences unless  _max_  is provided. This method returns modified string.

### Example

[Live Demo](http://tpcg.io/O89PGM)

#!/usr/bin/python3  import re

phone =  "2004-959-559 # This is Phone Number"  # Delete Python-style comments num = re.sub(r'#.*$',  "", phone)  print  ("Phone Num : ", num)  # Remove anything other than digits num = re.sub(r'\D',  "", phone)  print  ("Phone Num : ", num)

When the above code is executed, it produces the following result −

Phone Num :  2004-959-559
Phone Num :  2004959559



<!--stackedit_data:
eyJoaXN0b3J5IjpbNDAwMDY4MDM5XX0=
-->