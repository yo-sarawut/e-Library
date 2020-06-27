## Regular Expression Modifiers: Option Flags

Regular expression literals may include an optional modifier to control various aspects of matching. The modifiers are specified as an optional flag. You can provide multiple modifiers using exclusive OR (|), as shown previously and may be represented by one of these −

Sr.No.

Modifier & Description

1

**re.I**

Performs case-insensitive matching.

2

**re.L**

Interprets words according to the current locale. This interpretation affects the alphabetic group (\w and \W), as well as word boundary behavior (\b and \B).

3

**re.M**

Makes $ match the end of a line (not just the end of the string) and makes ^ match the start of any line (not just the start of the string).

4

**re.S**

Makes a period (dot) match any character, including a newline.

5

**re.U**

Interprets letters according to the Unicode character set. This flag affects the behavior of \w, \W, \b, \B.

6

**re.X**

Permits "cuter" regular expression syntax. It ignores whitespace (except inside a set [] or when escaped by a backslash) and treats unescaped # as a comment marker.

## Regular Expression Patterns

Except for the control characters,  **(+ ? . * ^ $ ( ) [ ] { } | \)**, all characters match themselves. You can escape a control character by preceding it with a backslash.

The following table lists the regular expression syntax that is available in Python −

Here is the list of regular expression syntax in Python.

## Regular Expression Examples

### Literal characters

Sr.No.

Example & Description

1

**python**

Match "python".

## Character classes

Sr.No.

Example & Description

1

**[Pp]ython**

Match "Python" or "python"

2

**rub[ye]**

Match "ruby" or "rube"

3

**[aeiou]**

Match any one lowercase vowel

4

**[0-9]**

Match any digit; same as [0123456789]

5

**[a-z]**

Match any lowercase ASCII letter

6

**[A-Z]**

Match any uppercase ASCII letter

7

**[a-zA-Z0-9]**

Match any of the above

8

**[^aeiou]**

Match anything other than a lowercase vowel

9

**[^0-9]**

Match anything other than a digit

## Special Character Classes

Sr.No.

Example & Description

1

**.**

Match any character except newline

2

**\d**

Match a digit: [0-9]

3

**\D**

Match a nondigit: [^0-9]

4

**\s**

Match a whitespace character: [ \t\r\n\f]

5

**\S**

Match nonwhitespace: [^ \t\r\n\f]

6

**\w**

Match a single word character: [A-Za-z0-9_]

7

**\W**

Match a nonword character: [^A-Za-z0-9_]

## Repetition Cases

Sr.No.

Example & Description

1

**ruby?**

Match "rub" or "ruby": the y is optional

2

**ruby***

Match "rub" plus 0 or more ys

3

**ruby+**

Match "rub" plus 1 or more ys

4

**\d{3}**

Match exactly 3 digits

5

**\d{3,}**

Match 3 or more digits

6

**\d{3,5}**

Match 3, 4, or 5 digits

## Nongreedy repetition

This matches the smallest number of repetitions −

Sr.No.

Example & Description

1

**<.*>**

Greedy repetition: matches "<python>perl>"

2

**<.*?>**

Nongreedy: matches "<python>" in "<python>perl>"

## Grouping with Parentheses

Sr.No.

Example & Description

1

**\D\d+**

No group: + repeats \d

2

**(\D\d)+**

Grouped: + repeats \D\d pair

3

**([Pp]ython(,)?)+**

Match "Python", "Python, python, python", etc.

## Backreferences

This matches a previously matched group again −

Sr.No.

Example & Description

1

**([Pp])ython&\1ails**

Match python&pails or Python&Pails

2

**(['"])[^\1]*\1**

Single or double-quoted string. \1 matches whatever the 1st group matched. \2 matches whatever the 2nd group matched, etc.

## Alternatives

Sr.No.

Example & Description

1

**python|perl**

Match "python" or "perl"

2

**rub(y|le)**

Match "ruby" or "ruble"

3

**Python(!+|\?)**

"Python" followed by one or more ! or one ?

## Anchors

This needs to specify match position.

Sr.No.

Example & Description

1

**^Python**

Match "Python" at the start of a string or internal line

2

**Python$**

Match "Python" at the end of a string or line

3

**\APython**

Match "Python" at the start of a string

4

**Python\Z**

Match "Python" at the end of a string

5

**\bPython\b**

Match "Python" at a word boundary

6

**\brub\B**

\B is nonword boundary: match "rub" in "rube" and "ruby" but not alone

7

**Python(?=!)**

Match "Python", if followed by an exclamation point.

8

**Python(?!!)**

Match "Python", if not followed by an exclamation point.

## Special Syntax with Parentheses

Sr.No.

Example & Description

1

**R(?#comment)**

Matches "R". All the rest is a comment

2

**R(?i)uby**

Case-insensitive while matching "uby"

3

**R(?i:uby)**

Same as above

4

**rub(?:y|le))**

Group only without creating \1 backreference

# Python 3 - CGI Programming

The Common Gateway Interface, or CGI, is a set of standards that define how information is exchanged between the web server and a custom script. The CGI specs are currently maintained by the NCSA.

## What is CGI?

-   The Common Gateway Interface, or CGI, is a standard for external gateway programs to interface with information servers such as HTTP servers.
    
-   The current version is CGI/1.1 and CGI/1.2 is under progress.
    

## Web Browsing

To understand the concept of CGI, let us see what happens when we click a hyper link to browse a particular web page or URL.

-   Your browser contacts the HTTP web server and demands for the URL, i.e., filename.
    
-   Web Server parses the URL and looks for the filename. If it finds that file then sends it back to the browser, otherwise sends an error message indicating that you requested a wrong file.
    
-   Web browser takes response from web server and displays either the received file or error message.
    

However, it is possible to set up the HTTP server so that whenever a file in a certain directory is requested that file is not sent back; instead it is executed as a program, and whatever that program outputs is sent back for your browser to display. This function is called the Common Gateway Interface or CGI and the programs are called CGI scripts. These CGI programs can be a Python Script, PERL Script, Shell Script, C or C++ program, etc.

## CGI Architecture Diagram

![CGI Architecture](https://www.tutorialspoint.com/python/images/cgiarch.gif)

## Web Server Support and Configuration

Before you proceed with CGI Programming, make sure that your Web Server supports CGI and it is configured to handle CGI Programs. All the CGI Programs to be executed by the HTTP server are kept in a pre-configured directory. This directory is called CGI Directory and by convention it is named as /var/www/cgi-bin. By convention, CGI files have extension as.  **cgi,**  but you can keep your files with python extension  **.py**  as well.

By default, the Linux server is configured to run only the scripts in the cgi-bin directory in /var/www. If you want to specify any other directory to run your CGI scripts, comment the following lines in the httpd.conf file −

<Directory  "/var/www/cgi-bin"> AllowOverride None
   Options ExecCGI
   Order allow,deny
   Allow from all </Directory>  <Directory  "/var/www/cgi-bin"> Options All </Directory>

Here, we assume that you have Web Server up and running successfully and you are able to run any other CGI program like Perl or Shell, etc.

## First CGI Program

Here is a simple link, which is linked to a CGI script called  [hello.py](https://www.tutorialspoint.com/cgi-bin/hello.py). This file is kept in /var/www/cgi-bin directory and it has following content. Before running your CGI program, make sure you have change mode of file using  **chmod 755 hello.py**  UNIX command to make file executable.

[Live Demo](http://tpcg.io/A8eYTd)

#!/usr/bin/python  print  ("Content-type:text/html\r\n\r\n")  print  ('<html>')  print  ('<head>')  print  ('<title>Hello Word - First CGI Program</title>')  print  ('</head>')  print  ('<body>')  print  ('<h2>Hello Word! This is my first CGI program</h2>')  print  ('</body>')  print  ('</html>')

**Note**  − First line in the script must be path to Python executable. In Linux it should be #!/usr/bin/python3

Enter following URL in yor browser

http://localhost:8080/cgi-bin/hello.py

## Hello Word! This is my first CGI program

This hello.py script is a simple Python script, which writes its output on STDOUT file, i.e., screen. There is one important and extra feature available which is first line to be printed  **Content-type:text/html\r\n\r\n**. This line is sent back to the browser and it specifies the content type to be displayed on the browser screen.

By now you must have understood basic concept of CGI and you can write many complicated CGI programs using Python. This script can interact with any other external system also to exchange information such as RDBMS.

## HTTP Header

The line  **Content-type:text/html\r\n\r\n**  is part of HTTP header which is sent to the browser to understand the content. All the HTTP header will be in the following form −

HTTP Field Name: Field Content

For Example
Content-type: text/html\r\n\r\n

There are few other important HTTP headers, which you will use frequently in your CGI Programming.

Sr.No.

Header & Description

1

**Content-type:**

A MIME string defining the format of the file being returned. Example is Content-type:text/html

2

**Expires: Date**

The date the information becomes invalid. It is used by the browser to decide when a page needs to be refreshed. A valid date string is in the format 01 Jan 1998 12:00:00 GMT.

3

**Location: URL**

The URL that is returned instead of the URL requested. You can use this field to redirect a request to any file.

4

**Last-modified: Date**

The date of last modification of the resource.

5

**Content-length: N**

The length, in bytes, of the data being returned. The browser uses this value to report the estimated download time for a file.

6

**Set-Cookie: String**

Set the cookie passed through the  _string_

## CGI Environment Variables

All the CGI programs have access to the following environment variables. These variables play an important role while writing any CGI program.

Sr.No.

Variable Name & Description

1

**CONTENT_TYPE**

The data type of the content. Used when the client is sending attached content to the server. For example, file upload.

2

**CONTENT_LENGTH**

The length of the query information. It is available only for POST requests.

3

**HTTP_COOKIE**

Returns the set cookies in the form of key & value pair.

4

**HTTP_USER_AGENT**

The User-Agent request-header field contains information about the user agent originating the request. It is name of the web browser.

5

**PATH_INFO**

The path for the CGI script.

6

**QUERY_STRING**

The URL-encoded information that is sent with GET method request.

7

**REMOTE_ADDR**

The IP address of the remote host making the request. This is useful logging or for authentication.

8

**REMOTE_HOST**

The fully qualified name of the host making the request. If this information is not available, then REMOTE_ADDR can be used to get IR address.

9

**REQUEST_METHOD**

The method used to make the request. The most common methods are GET and POST.

10

**SCRIPT_FILENAME**

The full path to the CGI script.

11

**SCRIPT_NAME**

The name of the CGI script.

12

**SERVER_NAME**

The server's hostname or IP Address

13

**SERVER_SOFTWARE**

The name and version of the software the server is running.

Here is small CGI program to list out all the CGI variables. Click this link to see the result  [Get Environment](http://www.tutorialspoint.com/cgi-bin/get_env.py)

[Live Demo](http://tpcg.io/2otJ04)

#!/usr/bin/python  import os print  ("Content-type: text/html\r\n\r\n");  print  ("<font size=+1>Environment</font><\br>");  for param in os.environ.keys():  print  ("<b>%20s</b>: %s<\br>"  %  (param, os.environ[param]))

## GET and POST Methods

You must have come across many situations when you need to pass some information from your browser to web server and ultimately to your CGI Program. Most frequently, browser uses two methods two pass this information to web server. These methods are GET Method and POST Method.

## Passing Information using GET method

The GET method sends the encoded user information appended to the page request. The page and the encoded information are separated by the ? character as follows −

http://www.test.com/cgi-bin/hello.py?key1=value1&key2=value2

The GET method is the default method to pass information from browser to web server and it produces a long string that appears in your browser's Location:box. Never use GET method if you have password or other sensitive information to pass to the server. The GET method has size limitation: only 1024 characters can be sent in a request string. The GET method sends information using QUERY_STRING header and will be accessible in your CGI Program through QUERY_STRING environment variable.

You can pass information by simply concatenating key and value pairs along with any URL or you can use HTML <FORM> tags to pass information using GET method.

## Simple URL Example:Get Method

Here is a simple URL, which passes two values to hello_get.py program using GET method.

[/cgi-bin/hello_get.py?first_name=ZARA&last_name=ALI](https://www.tutorialspoint.com/cgi-bin/hello_get.py?first_name=ZARA&last_name=ALI)

Below is  **hello_get.py**  script to handle input given by web browser. We are going to use  **cgi**  module, which makes it very easy to access passed information −

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields first_name = form.getvalue('first_name') last_name = form.getvalue('last_name')  print  ("Content-type:text/html\r\n\r\n")  print  ("<html>")  print  ("<head>")  print  ("<title>Hello - Second CGI Program</title>")  print  ("</head>")  print  ("<body>")  print  ("<h2>Hello %s %s</h2>"  %  (first_name, last_name))  print  ("</body>")  print  ("</html>")

This would generate the following result −

## Hello ZARA ALI

## Simple FORM Example:GET Method

This example passes two values using HTML FORM and submit button. We use same CGI script hello_get.py to handle this input.

<form  action  =  "/cgi-bin/hello_get.py"  method  =  "get"> First Name: <input  type  =  "text"  name  =  "first_name">  <br  /> Last Name: <input  type  =  "text"  name  =  "last_name"  />  <input  type  =  "submit"  value  =  "Submit"  />  </form>

Here is the actual output of the above form, you enter First and Last Name and then click submit button to see the result.

First Name:  
Last Name:

## Passing Information Using POST Method

A generally more reliable method of passing information to a CGI program is the POST method. This packages the information in exactly the same way as GET methods, but instead of sending it as a text string after a ? in the URL it sends it as a separate message. This message comes into the CGI script in the form of the standard input.

Below is same hello_get.py script which handles GET as well as POST method.

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields first_name = form.getvalue('first_name') last_name = form.getvalue('last_name')  print  "Content-type:text/html\r\n\r\n"  print  "<html>"  print  "<head>"  print  "<title>Hello - Second CGI Program</title>"  print  "</head>"  print  "<body>"  print  "<h2>Hello %s %s</h2>"  %  (first_name, last_name)  print  "</body>"  print  "</html>"

Let us take again same example as above which passes two values using HTML FORM and submit button. We use same CGI script hello_get.py to handle this input.

<form  action  =  "/cgi-bin/hello_get.py"  method  =  "post"> First Name: <input  type  =  "text"  name  =  "first_name"><br  /> Last Name: <input  type  =  "text"  name  =  "last_name"  />  <input  type  =  "submit"  value  =  "Submit"  />  </form>

Here is the actual output of the above form. You enter First and Last Name and then click submit button to see the result.

First Name:  
Last Name:

## Passing Checkbox Data to CGI Program

Checkboxes are used when more than one option is required to be selected.

Here is example HTML code for a form with two checkboxes −

<form  action  =  "/cgi-bin/checkbox.cgi"  method  =  "POST"  target  =  "_blank">  <input  type  =  "checkbox"  name  =  "maths"  value  =  "on"  /> Maths <input  type  =  "checkbox"  name  =  "physics"  value  =  "on"  /> Physics <input  type  =  "submit"  value  =  "Select Subject"  />  </form>

The result of this code is the following form −

Maths  Physics

Below is checkbox.cgi script to handle input given by web browser for checkbox button.

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields  if form.getvalue('maths'): math_flag =  "ON"  else: math_flag =  "OFF"  if form.getvalue('physics'): physics_flag =  "ON"  else: physics_flag =  "OFF"  print  "Content-type:text/html\r\n\r\n"  print  "<html>"  print  "<head>"  print  "<title>Checkbox - Third CGI Program</title>"  print  "</head>"  print  "<body>"  print  "<h2> CheckBox Maths is : %s</h2>"  % math_flag print  "<h2> CheckBox Physics is : %s</h2>"  % physics_flag print  "</body>"  print  "</html>"

## Passing Radio Button Data to CGI Program

Radio Buttons are used when only one option is required to be selected.

Here is example HTML code for a form with two radio buttons −

<form  action  =  "/cgi-bin/radiobutton.py"  method  =  "post"  target  =  "_blank">  <input  type  =  "radio"  name  =  "subject"  value  =  "maths"  /> Maths <input  type  =  "radio"  name  =  "subject"  value  =  "physics"  /> Physics <input  type  =  "submit"  value  =  "Select Subject"  />  </form>

The result of this code is the following form −

Maths  Physics

Below is radiobutton.py script to handle input given by web browser for radio button −

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields  if form.getvalue('subject'): subject = form.getvalue('subject')  else: subject =  "Not set"  print  "Content-type:text/html\r\n\r\n"  print  "<html>"  print  "<head>"  print  "<title>Radio - Fourth CGI Program</title>"  print  "</head>"  print  "<body>"  print  "<h2> Selected Subject is %s</h2>"  % subject print  "</body>"  print  "</html>"

## Passing Text Area Data to CGI Program

TEXTAREA element is used when multiline text has to be passed to the CGI Program.

Here is example HTML code for a form with a TEXTAREA box −

<form  action  =  "/cgi-bin/textarea.py"  method  =  "post"  target  =  "_blank">  <textarea  name  =  "textcontent"  cols  =  "40"  rows  =  "4"> Type your text here... </textarea>  <input  type  =  "submit"  value  =  "Submit"  />  </form>

The result of this code is the following form −

Below is textarea.cgi script to handle input given by web browser −

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields  if form.getvalue('textcontent'): text_content = form.getvalue('textcontent')  else: text_content =  "Not entered"  print  "Content-type:text/html\r\n\r\n"  print  "<html>"  print  "<head>";  print  "<title>Text Area - Fifth CGI Program</title>"  print  "</head>"  print  "<body>"  print  "<h2> Entered Text Content is %s</h2>"  % text_content print  "</body>"

## Passing Drop Down Box Data to CGI Program

Drop Down Box is used when we have many options available but only one or two will be selected.

Here is example HTML code for a form with one drop down box −

<form  action  =  "/cgi-bin/dropdown.py"  method  =  "post"  target  =  "_blank">  <select  name  =  "dropdown">  <option  value  =  "Maths"  selected>Maths</option>  <option  value  =  "Physics">Physics</option>  </select>  <input  type  =  "submit"  value  =  "Submit"/>  </form>

The result of this code is the following form −

Maths  Physics

Below is dropdown.py script to handle input given by web browser.

#!/usr/bin/python  # Import modules for CGI handling  import cgi, cgitb # Create instance of FieldStorage form = cgi.FieldStorage()  # Get data from fields  if form.getvalue('dropdown'): subject = form.getvalue('dropdown')  else: subject =  "Not entered"  print  "Content-type:text/html\r\n\r\n"  print  "<html>"  print  "<head>"  print  "<title>Dropdown Box - Sixth CGI Program</title>"  print  "</head>"  print  "<body>"  print  "<h2> Selected Subject is %s</h2>"  % subject print  "</body>"  print  "</html>"

## Using Cookies in CGI

HTTP protocol is a stateless protocol. For a commercial website, it is required to maintain session information among different pages. For example, one user registration ends after completing many pages. How to maintain user's session information across all the web pages?

In many situations, using cookies is the most efficient method of remembering and tracking preferences, purchases, commissions, and other information required for better visitor experience or site statistics.

## How It Works?

Your server sends some data to the visitor's browser in the form of a cookie. The browser may accept the cookie. If it does, it is stored as a plain text record on the visitor's hard drive. Now, when the visitor arrives at another page on your site, the cookie is available for retrieval. Once retrieved, your server knows/remembers what was stored.

Cookies are a plain text data record of 5 variable-length fields −

-   **Expires**  − The date the cookie will expire. If this is blank, the cookie will expire when the visitor quits the browser.
    
-   **Domain**  − The domain name of your site.
    
-   **Path**  − The path to the directory or web page that sets the cookie. This may be blank if you want to retrieve the cookie from any directory or page.
    
-   **Secure**  − If this field contains the word "secure", then the cookie may only be retrieved with a secure server. If this field is blank, no such restriction exists.
    
-   **Name=Value**  − Cookies are set and retrieved in the form of key and value pairs.
    

## Setting up Cookies

It is very easy to send cookies to browser. These cookies are sent along with HTTP Header before to Content-type field. Assuming you want to set UserID and Password as cookies. Setting the cookies is done as follows −

#!/usr/bin/python  print  "Set-Cookie:UserID = XYZ;\r\n"  print  "Set-Cookie:Password = XYZ123;\r\n"  print  "Set-Cookie:Expires = Tuesday, 31-Dec-2007 23:12:40 GMT;\r\n"  print  "Set-Cookie:Domain = www.tutorialspoint.com;\r\n"  print  "Set-Cookie:Path = /perl;\n"  print  "Content-type:text/html\r\n\r\n"  ...........Rest  of the HTML Content....

From this example, you must have understood how to set cookies. We use  **Set-Cookie**  HTTP header to set cookies.

It is optional to set cookies attributes like Expires, Domain, and Path. It is notable that cookies are set before sending magic line  **"Content-type:text/html\r\n\r\n**.

## Retrieving Cookies

It is very easy to retrieve all the set cookies. Cookies are stored in CGI environment variable HTTP_COOKIE and they will have following form −

key1 = value1;key2 = value2;key3 = value3....

Here is an example of how to retrieve cookies.

#!/usr/bin/python  # Import modules for CGI handling  from os import environ import cgi, cgitb if environ.has_key('HTTP_COOKIE'):  for cookie in map(strip, split(environ['HTTP_COOKIE'],  ';')):  (key,  value  )  = split(cookie,  '=');  if key ==  "UserID": user_id =  value  if key ==  "Password": password =  value  print  "User ID  = %s"  % user_id print  "Password = %s"  % password

This produces the following result for the cookies set by above script −

User ID = XYZ
Password = XYZ123

## File Upload Example

To upload a file, the HTML form must have the enctype attribute set to  **multipart/form-data**. The input tag with the file type creates a "Browse" button.

<html>  <body>  <form  enctype  =  "multipart/form-data"  action  =  "save_file.py"  method  =  "post">  <p>File: <input  type  =  "file"  name  =  "filename"  /></p>  <p><input  type  =  "submit"  value  =  "Upload"  /></p>  </form>  </body>  </html>

The result of this code is the following form −

File:

Above example has been disabled intentionally to save people uploading file on our server, but you can try above code with your server.

Here is the script  **save_file.py**  to handle file upload −

#!/usr/bin/python  import cgi, os import cgitb; cgitb.enable() form = cgi.FieldStorage()  # Get filename here. fileitem = form['filename']  # Test if the file was uploaded  if fileitem.filename:  # strip leading path from file name to avoid  # directory traversal attacks fn = os.path.basename(fileitem.filename) open('/tmp/'  + fn,  'wb').write(fileitem.file.read()) message =  'The file "'  + fn +  '" was uploaded successfully'  else: message =  'No file was uploaded'  print  """\
Content-Type: text/html\n
<html>
<body>
   <p>%s</p>
</body>
</html>
"""  %  (message,)

If you run the above script on Unix/Linux, then you need to take care of replacing file separator as follows, otherwise on your windows machine above open() statement should work fine.

fn = os.path.basename(fileitem.filename.replace("\\", "/" ))

## How To Raise a "File Download" Dialog Box?

Sometimes, it is desired that you want to give option where a user can click a link and it will pop up a "File Download" dialogue box to the user instead of displaying actual content. This is very easy and can be achieved through HTTP header. This HTTP header is be different from the header mentioned in previous section.

For example, if you want make a  **FileName**  file downloadable from a given link, then its syntax is as follows −

#!/usr/bin/python  # HTTP Header  print  "**Content-Type:**application/octet-stream; name = \"FileName\"\r\n";  print  "**Content-Disposition:** attachment; filename = \"FileName\"\r\n\n";  # Actual File Content will go here. fo = open("foo.txt",  "rb") str = fo.read();  print str # Close opend file fo.close()

Hope you enjoyed this tutorial. If yes, please send me your feedback at:  [Contact Us](https://www.tutorialspoint.com/about/contact_us.htm)

# Python 3 - MySQL Database Access

The Python standard for database interfaces is the Python DB-API. Most Python database interfaces adhere to this standard.

You can choose the right database for your application. Python Database API supports a wide range of database servers such as −

-   GadFly
-   mSQL
-   MySQL
-   PostgreSQL
-   Microsoft SQL Server 2000
-   Informix
-   Interbase
-   Oracle
-   Sybase
-   SQLite

Here is the list of available Python database interfaces −  [Python Database Interfaces and APIs](https://wiki.python.org/moin/DatabaseInterfaces). You must download a separate DB API module for each database you need to access. For example, if you need to access an Oracle database as well as a MySQL database, you must download both the Oracle and the MySQL database modules.

The DB API provides a minimal standard for working with databases using Python structures and syntax wherever possible. This API includes the following −

-   Importing the API module.
-   Acquiring a connection with the database.
-   Issuing SQL statements and stored procedures.
-   Closing the connection

Python has an in-built support for SQLite. In this section, we would learn all the concepts using MySQL. MySQLdb module, a popular interface with MySQL is not compatible with Python 3. Instead, we shall use  [PyMySQL](http://www.pymysql.org/)  module.

## What is PyMySQL ?

PyMySQL is an interface for connecting to a MySQL database server from Python. It implements the Python Database API v2.0 and contains a pure-Python MySQL client library. The goal of PyMySQL is to be a drop-in replacement for MySQLdb.

## How do I Install PyMySQL?

Before proceeding further, you make sure you have PyMySQL installed on your machine. Just type the following in your Python script and execute it −

#!/usr/bin/python3  import pymysql

If it produces the following result, then it means MySQLdb module is not installed −

Traceback (most recent call last):
   File "test.py", line 3, in <module>
      Import pymysql
ImportError: No module named pymysql

The last stable release is available on PyPI and can be installed with pip −

pip install pymysql

Alternatively (e.g. if pip is not available), a tarball can be downloaded from  [GitHub](https://github.com/PyMySQL/PyMySQL)  and installed with Setuptools as follows −

$ # X.X is the desired pymysql version (e.g. 0.5 or 0.6). $ curl -L https://github.com/PyMySQL/PyMySQL/tarball/pymysql-X.X | tar xz $ cd PyMySQL* $ python setup.py install
$ # The folder PyMySQL* can be safely removed now.

**Note**  − Make sure you have root privilege to install the above module.

## Database Connection

Before connecting to a MySQL database, make sure of the following points −

-   You have created a database TESTDB.
    
-   You have created a table EMPLOYEE in TESTDB.
    
-   This table has fields FIRST_NAME, LAST_NAME, AGE, SEX and INCOME.
    
-   User ID "testuser" and password "test123" are set to access TESTDB.
    
-   Python module PyMySQL is installed properly on your machine.
    
-   You have gone through MySQL tutorial to understand  [MySQL Basics.](https://www.tutorialspoint.com/mysql/index.htm)
    

### Example

Following is an example of connecting with MySQL database "TESTDB" −

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using _cursor()_ method cursor = db.cursor()  # execute SQL query using _execute()_ method. cursor.execute("SELECT VERSION()")  # Fetch a single row using _fetchone()_ method. data = cursor.fetchone()  print  ("Database version : %s "  % data)  # disconnect from server db.close()

While running this script, it produces the following result.

Database version : 5.5.20-log

If a connection is established with the datasource, then a Connection Object is returned and saved into  **db**  for further use, otherwise  **db**  is set to None. Next,  **db**  object is used to create a  **cursor**  object, which in turn is used to execute SQL queries. Finally, before coming out, it ensures that the database connection is closed and resources are released.

## Creating Database Table

Once a database connection is established, we are ready to create tables or records into the database tables using  **execute**  method of the created cursor.

### Example

Let us create a Database table EMPLOYEE −

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using _cursor()_ method cursor = db.cursor()  # Drop table if it already exist using _execute()_ method. cursor.execute("DROP TABLE IF EXISTS EMPLOYEE")  # Create table as per requirement sql =  """CREATE TABLE EMPLOYEE (
   FIRST_NAME  CHAR(20) NOT NULL,
   LAST_NAME  CHAR(20),
   AGE INT,  
   SEX CHAR(1),
   INCOME FLOAT )""" cursor.execute(sql)  # disconnect from server db.close()

## INSERT Operation

The INSERT Operation is required when you want to create your records into a database table.

### Example

The following example, executes SQL  _INSERT_  statement to create a record in the EMPLOYEE table −

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using cursor() method cursor = db.cursor()  # Prepare SQL query to INSERT a record into the database. sql =  """INSERT INTO EMPLOYEE(FIRST_NAME,
   LAST_NAME, AGE, SEX, INCOME)
   VALUES ('Mac', 'Mohan', 20, 'M', 2000)"""  try:  # Execute the SQL command cursor.execute(sql)  # Commit your changes in the database db.commit()  except:  # Rollback in case there is any error db.rollback()  # disconnect from server db.close()

The above example can be written as follows to create SQL queries dynamically −

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using cursor() method cursor = db.cursor()  # Prepare SQL query to INSERT a record into the database. sql =  "INSERT INTO EMPLOYEE(FIRST_NAME, \
   LAST_NAME, AGE, SEX, INCOME) \
   VALUES ('%s', '%s', '%d', '%c', '%d' )"  % \ ('Mac',  'Mohan',  20,  'M',  2000)  try:  # Execute the SQL command cursor.execute(sql)  # Commit your changes in the database db.commit()  except:  # Rollback in case there is any error db.rollback()  # disconnect from server db.close()

### Example

The following code segment is another form of execution where you can pass parameters directly −

..................................
user_id = "test123"
password = "password"

con.execute('insert into Login values("%s", "%s")' % \
             (user_id, password))
..................................

## READ Operation

READ Operation on any database means to fetch some useful information from the database.

Once the database connection is established, you are ready to make a query into this database. You can use either  **fetchone()**  method to fetch a single record or  **fetchall()**  method to fetch multiple values from a database table.

-   **fetchone()**  − It fetches the next row of a query result set. A result set is an object that is returned when a cursor object is used to query a table.
    
-   **fetchall()**  − It fetches all the rows in a result set. If some rows have already been extracted from the result set, then it retrieves the remaining rows from the result set.
    
-   **rowcount**  − This is a read-only attribute and returns the number of rows that were affected by an execute() method.
    

### Example

The following procedure queries all the records from EMPLOYEE table having salary more than 1000 −

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using cursor() method cursor = db.cursor()  # Prepare SQL query to INSERT a record into the database. sql =  "SELECT * FROM EMPLOYEE \
      WHERE INCOME > '%d'"  %  (1000)  try:  # Execute the SQL command cursor.execute(sql)  # Fetch all the rows in a list of lists. results = cursor.fetchall()  for row in results: fname = row[0] lname = row[1] age = row[2] sex = row[3] income = row[4]  # Now print fetched result  print  ("fname = %s,lname = %s,age = %d,sex = %s,income = %d"  % \ (fname, lname, age, sex, income ))  except:  print  ("Error: unable to fetch data")  # disconnect from server db.close()

### Output

This will produce the following result −

fname = Mac, lname = Mohan, age = 20, sex = M, income = 2000

## Update Operation

UPDATE Operation on any database means to update one or more records, which are already available in the database.

The following procedure updates all the records having SEX as  **'M'**. Here, we increase the AGE of all the males by one year.

### Example

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using _cursor()_ method cursor = db.cursor()  # Prepare SQL query to UPDATE required records sql =  "UPDATE EMPLOYEE SET AGE = AGE + 1
                          WHERE SEX = '%c'"  %  ('M')  try:  # Execute the SQL command cursor.execute(sql)  # Commit your changes in the database db.commit()  except:  # Rollback in case there is any error db.rollback()  # disconnect from server db.close()

## DELETE Operation

DELETE operation is required when you want to delete some records from your database. Following is the procedure to delete all the records from EMPLOYEE where AGE is more than 20 −

### Example

#!/usr/bin/python3  import pymysql # Open database connection db = pymysql.connect("localhost","testuser","test123","TESTDB"  )  # prepare a cursor object using _cursor()_ method cursor = db.cursor()  # Prepare SQL query to DELETE required records sql =  "DELETE FROM EMPLOYEE WHERE AGE > '%d'"  %  (20)  try:  # Execute the SQL command cursor.execute(sql)  # Commit your changes in the database db.commit()  except:  # Rollback in case there is any error db.rollback()  # disconnect from server db.close()

## Performing Transactions

Transactions are a mechanism that ensures data consistency. Transactions have the following four properties −

-   **Atomicity**  − Either a transaction completes or nothing happens at all.
    
-   **Consistency**  − A transaction must start in a consistent state and leave the system in a consistent state.
    
-   **Isolation**  − Intermediate results of a transaction are not visible outside the current transaction.
    
-   **Durability**  − Once a transaction was committed, the effects are persistent, even after a system failure.
    

The Python DB API 2.0 provides two methods to either  _commit_  or  _rollback_  a transaction.

### Example

You already know how to implement transactions. Here is a similar example −

# Prepare SQL query to DELETE required records sql =  "DELETE FROM EMPLOYEE WHERE AGE > '%d'"  %  (20)  try:  # Execute the SQL command cursor.execute(sql)  # Commit your changes in the database db.commit()  except:  # Rollback in case there is any error db.rollback()

## COMMIT Operation

Commit is an operation, which gives a green signal to the database to finalize the changes, and after this operation, no change can be reverted back.

Here is a simple example to call the  **commit**  method.

db.commit()

## ROLLBACK Operation

If you are not satisfied with one or more of the changes and you want to revert back those changes completely, then use the  **rollback()**  method.

Here is a simple example to call the  **rollback()**  method.

db.rollback()

## Disconnecting Database

To disconnect the Database connection, use the close() method.

db.close()

If the connection to a database is closed by the user with the close() method, any outstanding transactions are rolled back by the DB. However, instead of depending on any of the DB lower level implementation details, your application would be better off calling commit or rollback explicitly.

## Handling Errors

There are many sources of errors. A few examples are a syntax error in an executed SQL statement, a connection failure, or calling the fetch method for an already canceled or finished statement handle.

The DB API defines a number of errors that must exist in each database module. The following table lists these exceptions.

Sr.No.

Exception & Description

1

**Warning**

Used for non-fatal issues. Must subclass StandardError.

2

**Error**

Base class for errors. Must subclass StandardError.

3

**InterfaceError**

Used for errors in the database module, not the database itself. Must subclass Error.

4

**DatabaseError**

Used for errors in the database. Must subclass Error.

5

**DataError**

Subclass of DatabaseError that refers to errors in the data.

6

**OperationalError**

Subclass of DatabaseError that refers to errors such as the loss of a connection to the database. These errors are generally outside of the control of the Python scripter.

7

**IntegrityError**

Subclass of DatabaseError for situations that would damage the relational integrity, such as uniqueness constraints or foreign keys.

8

**InternalError**

Subclass of DatabaseError that refers to errors internal to the database module, such as a cursor no longer being active.

9

**ProgrammingError**

Subclass of DatabaseError that refers to errors such as a bad table name and other things that can safely be blamed on you.

10

**NotSupportedError**

Subclass of DatabaseError that refers to trying to call unsupported functionality.

Your Python scripts should handle these errors, but before using any of the above exceptions, make sure your MySQLdb has support for that exception. You can get more information about them by reading the DB API 2.0 specification.

# Python 3 - Network Programming

Python provides two levels of access to the network services. At a low level, you can access the basic socket support in the underlying operating system, which allows you to implement clients and servers for both connection-oriented and connectionless protocols.

Python also has libraries that provide higher-level access to specific application-level network protocols, such as FTP, HTTP, and so on.

This chapter gives you an understanding on the most famous concept in Networking - Socket Programming.

## What is Sockets?

Sockets are the endpoints of a bidirectional communications channel. Sockets may communicate within a process, between processes on the same machine, or between processes on different continents.

Sockets may be implemented over a number of different channel types: Unix domain sockets, TCP, UDP, and so on. The  _socket_  library provides specific classes for handling the common transports as well as a generic interface for handling the rest.

Sockets have their own vocabulary −

Sr.No.

Term & Description

1

**domain**

The family of protocols that is used as the transport mechanism. These values are constants such as AF_INET, PF_INET, PF_UNIX, PF_X25, and so on.

2

**type**

The type of communications between the two endpoints, typically SOCK_STREAM for connection-oriented protocols and SOCK_DGRAM for connectionless protocols.

3

**protocol**

Typically zero, this may be used to identify a variant of a protocol within a domain and type.

4

**hostname**

The identifier of a network interface −

-   A string, which can be a host name, a dotted-quad address, or an IPV6 address in colon (and possibly dot) notation
    
-   A string "<broadcast>", which specifies an INADDR_BROADCAST address.
    
-   A zero-length string, which specifies INADDR_ANY, or
    
-   An Integer, interpreted as a binary address in host byte order.
    

5

**port**

Each server listens for clients calling on one or more ports. A port may be a Fixnum port number, a string containing a port number, or the name of a service.

## The socket Module

To create a socket, you must use the  _socket.socket()_  function available in the socket module, which has the general syntax −

s = socket.socket (socket_family, socket_type, protocol = 0)

Here is the description of the parameters −

-   **socket_family**  − This is either AF_UNIX or AF_INET, as explained earlier.
    
-   **socket_type**  − This is either SOCK_STREAM or SOCK_DGRAM.
    
-   **protocol**  − This is usually left out, defaulting to 0.
    

Once you have  _socket_  object, then you can use the required functions to create your client or server program. Following is the list of functions required −

## Server Socket Methods

Sr.No.

Method & Description

1

**s.bind()**

This method binds address (hostname, port number pair) to socket.

2

**s.listen()**

This method sets up and start TCP listener.

3

**s.accept()**

This passively accept TCP client connection, waiting until connection arrives (blocking).

## Client Socket Methods

Sr.No.

Method & Description

1

**s.connect()**

This method actively initiates TCP server connection.

## General Socket Methods

Sr.No.

Method & Description

1

**s.recv()**

This method receives TCP message

2

**s.send()**

This method transmits TCP message

3

**s.recvfrom()**

This method receives UDP message

4

**s.sendto()**

This method transmits UDP message

5

**s.close()**

This method closes socket

6

**socket.gethostname()**

Returns the hostname.

## A Simple Server

To write Internet servers, we use the  **socket**  function available in socket module to create a socket object. A socket object is then used to call other functions to setup a socket server.

Now call the  **bind(hostname, port)**  function to specify a  _port_  for your service on the given host.

Next, call the  _accept_  method of the returned object. This method waits until a client connects to the port you specified, and then returns a  _connection_  object that represents the connection to that client.

#!/usr/bin/python3           # This is server.py file  import socket # create a socket object serversocket = socket.socket( socket.AF_INET, socket.SOCK_STREAM)  # get local machine name host = socket.gethostname() port =  9999  # bind to the port serversocket.bind((host, port))  # queue up to 5 requests serversocket.listen(5)  while  True:  # establish a connection clientsocket,addr = serversocket.accept()  print("Got a connection from %s"  % str(addr)) msg =  'Thank you for connecting'+  "\r\n" clientsocket.send(msg.encode('ascii')) clientsocket.close()

## A Simple Client

Let us write a very simple client program which opens a connection to a given port 12345 and a given host. It is very simple to create a socket client using the Python's  _socket_  module function.

The  **socket.connect(hosname, port )**  opens a TCP connection to  _hostname_  on the  _port_. Once you have a socket open, you can read from it like any IO object. When done, remember to close it, as you would close a file.

### Example

The following code is a very simple client that connects to a given host and port, reads any available data from the socket, and then exits −

#!/usr/bin/python3           # This is client.py file  import socket # create a socket object s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  # get local machine name host = socket.gethostname() port =  9999  # connection to hostname on the port. s.connect((host, port))  # Receive no more than 1024 bytes msg = s.recv(1024) s.close()  print  (msg.decode('ascii'))

Now run this server.py in the background and then run the above client.py to see the result.

# Following would start a server in background. $ python server.py &  # Once server is started run client as follows: $ python client.py

### Output

This would produce following result −

on server terminal
Got a connection from ('192.168.1.10', 3747)
On client terminal
Thank you for connecting

## Python Internet Modules

A list of some important modules in Python Network/Internet programming are given below −

Protocol

Common function

Port No

Python module

HTTP

Web pages

80

httplib, urllib, xmlrpclib

NNTP

Usenet news

119

nntplib

FTP

File transfers

20

ftplib, urllib

SMTP

Sending email

25

smtplib

POP3

Fetching email

110

poplib

IMAP4

Fetching email

143

imaplib

Telnet

Command lines

23

telnetlib

Gopher

Document transfers

70

gopherlib, urllib

Please check all the libraries mentioned above to work with FTP, SMTP, POP, and IMAP protocols.

## Further Readings

This was a quick start with the Socket Programming. It is a vast subject. It is recommended to go through the following link to find more detail −

-   [Unix Socket Programming](https://www.tutorialspoint.com/unix_sockets/index.htm "Unix Socket Programming").
    
-   [Python Socket Library and Modules](http://docs.python.org/3.0/library/socket.html "Python Socket Library").
    

# Python 3 - Sending Email using SMTP

Simple Mail Transfer Protocol (SMTP) is a protocol, which handles sending an e-mail and routing e-mail between mail servers.

Python provides  **smtplib**  module, which defines an SMTP client session object that can be used to send mails to any Internet machine with an SMTP or ESMTP listener daemon.

Here is a simple syntax to create one SMTP object, which can later be used to send an e-mail −

import smtplib

smtpObj = smtplib.SMTP(  [host [, port [, local_hostname]]]  )

Here is the detail of the parameters −

-   **host**  − This is the host running your SMTP server. You can specifiy IP address of the host or a domain name like tutorialspoint.com. This is an optional argument.
    
-   **port**  − If you are providing  _host_  argument, then you need to specify a port, where SMTP server is listening. Usually this port would be 25.
    
-   **local_hostname**  − If your SMTP server is running on your local machine, then you can specify just  _localhost_  the option.
    

An SMTP object has an instance method called  **sendmail**, which is typically used to do the work of mailing a message. It takes three parameters −

-   The  _sender_  − A string with the address of the sender.
    
-   The  _receivers_  − A list of strings, one for each recipient.
    
-   The  _message_  − A message as a string formatted as specified in the various RFCs.
    

### Example

Here is a simple way to send one e-mail using Python script. Try it once −

#!/usr/bin/python3  import smtplib

sender =  'from@fromdomain.com' receivers =  ['to@todomain.com'] message =  """From: From Person <from@fromdomain.com>
To: To Person <to@todomain.com>
Subject: SMTP e-mail test

This is a test e-mail message.
"""  try: smtpObj = smtplib.SMTP('localhost') smtpObj.sendmail(sender, receivers, message)  print  "Successfully sent email"  except  SMTPException:  print  "Error: unable to send email"

Here, you have placed a basic e-mail in message, using a triple quote, taking care to format the headers correctly. An e-mail requires a  **From**,  **To**, and a  **Subject**  header, separated from the body of the e-mail with a blank line.

To send the mail you use  _smtpObj_  to connect to the SMTP server on the local machine. Then use the  _sendmail_  method along with the message, the from address, and the destination address as parameters (even though the from and to addresses are within the e-mail itself, these are not always used to route the mail).

If you are not running an SMTP server on your local machine, you can the use  _smtplib_  client to communicate with a remote SMTP server. Unless you are using a webmail service (such as gmail or Yahoo! Mail), your e-mail provider must have provided you with the outgoing mail server details that you can supply them, as follows −

mail = smtplib.SMTP('smtp.gmail.com',  587)

## Sending an HTML e-mail using Python

When you send a text message using Python, then all the content is treated as simple text. Even if you include HTML tags in a text message, it is displayed as simple text and HTML tags will not be formatted according to the HTML syntax. However, Python provides an option to send an HTML message as actual HTML message.

While sending an e-mail message, you can specify a Mime version, content type and the character set to send an HTML e-mail.

### Example

Following is an example to send the HTML content as an e-mail. Try it once −

#!/usr/bin/python3  import smtplib

message =  """From: From Person <from@fromdomain.com>
To: To Person <to@todomain.com>
MIME-Version: 1.0
Content-type: text/html
Subject: SMTP HTML e-mail test

This is an e-mail message to be sent in HTML format

<b>This is HTML message.</b>
<h1>This is headline.</h1>
"""  try: smtpObj = smtplib.SMTP('localhost') smtpObj.sendmail(sender, receivers, message)  print  "Successfully sent email"  except  SMTPException:  print  "Error: unable to send email"

## Sending Attachments as an E-mail

To send an e-mail with mixed content requires setting the  **Content-type**  header to  **multipart/mixed**. Then, the text and the attachment sections can be specified within  **boundaries**.

A boundary is started with two hyphens followed by a unique number, which cannot appear in the message part of the e-mail. A final boundary denoting the e-mail's final section must also end with two hyphens.

The attached files should be encoded with the  **pack("m")**  function to have base 64 encoding before transmission.

### Example

Following is an example, which sends a file  **/tmp/test.txt**  as an attachment. Try it once −

#!/usr/bin/python3  import smtplib import base64

filename =  "/tmp/test.txt"  # Read a file and encode it into base64 format fo = open(filename,  "rb") filecontent = fo.read() encodedcontent = base64.b64encode(filecontent)  # base64 sender =  'webmaster@tutorialpoint.com' reciever =  'amrood.admin@gmail.com' marker =  "AUNIQUEMARKER" body ="""
This is a test email to send an attachement.
"""  # Define the main headers. part1 =  """From: From Person <me@fromdomain.net>
To: To Person <amrood.admin@gmail.com>
Subject: Sending Attachement
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary=%s
--%s
"""  %  (marker, marker)  # Define the message action part2 =  """Content-Type: text/plain
Content-Transfer-Encoding:8bit

%s
--%s
"""  %  (body,marker)  # Define the attachment section part3 =  """Content-Type: multipart/mixed; name=\"%s\"
Content-Transfer-Encoding:base64
Content-Disposition: attachment; filename=%s

%s
--%s--
"""  %(filename, filename, encodedcontent, marker) message = part1 + part2 + part3 try: smtpObj = smtplib.SMTP('localhost') smtpObj.sendmail(sender, reciever, message)  print  "Successfully sent email"  except  Exception:  print  ("Error: unable to send email")

# Python 3 - Multithreaded Programming

Running several threads is similar to running several different programs concurrently, but with the following benefits −

-   Multiple threads within a process share the same data space with the main thread and can therefore share information or communicate with each other more easily than if they were separate processes.
    
-   Threads are sometimes called light-weight processes and they do not require much memory overhead; they are cheaper than processes.
    

A thread has a beginning, an execution sequence, and a conclusion. It has an instruction pointer that keeps track of where within its context is it currently running.

-   It can be pre-empted (interrupted).
    
-   It can temporarily be put on hold (also known as sleeping) while other threads are running - this is called yielding.
    

There are two different kind of threads −

-   kernel thread
-   user thread

Kernel Threads are a part of the operating system, while the User-space threads are not implemented in the kernel.

There are two modules which support the usage of threads in Python3 −

-   _thread
-   threading

The thread module has been "deprecated" for quite a long time. Users are encouraged to use the threading module instead. Hence, in Python 3, the module "thread" is not available anymore. However, it has been renamed to "_thread" for backwards compatibilities in Python3.

## Starting a New Thread

To spawn another thread, you need to call the following method available in the  _thread_  module −

_thread.start_new_thread (  function, args[, kwargs]  )

This method call enables a fast and efficient way to create new threads in both Linux and Windows.

The method call returns immediately and the child thread starts and calls function with the passed list of  _args_. When the function returns, the thread terminates.

Here,  _args_  is a tuple of arguments; use an empty tuple to call function without passing any arguments.  _kwargs_ is an optional dictionary of keyword arguments.

### Example

#!/usr/bin/python3  import _thread import time # Define a function for the thread  def print_time( threadName, delay): count =  0  while count <  5: time.sleep(delay) count +=  1  print  ("%s: %s"  %  ( threadName, time.ctime(time.time())  ))  # Create two threads as follows  try: _thread.start_new_thread( print_time,  ("Thread-1",  2,  )  ) _thread.start_new_thread( print_time,  ("Thread-2",  4,  )  )  except:  print  ("Error: unable to start thread")  while  1:  pass

### Output

When the above code is executed, it produces the following result −

Thread-1: Fri Feb 19 09:41:39 2016
Thread-2: Fri Feb 19 09:41:41 2016
Thread-1: Fri Feb 19 09:41:41 2016
Thread-1: Fri Feb 19 09:41:43 2016
Thread-2: Fri Feb 19 09:41:45 2016
Thread-1: Fri Feb 19 09:41:45 2016
Thread-1: Fri Feb 19 09:41:47 2016
Thread-2: Fri Feb 19 09:41:49 2016
Thread-2: Fri Feb 19 09:41:53 2016

Program goes in an infinite loop. You will have to press ctrl-c to stop

Although it is very effective for low-level threading, the  _thread_  module is very limited compared to the newer threading module.

## The Threading Module

The newer threading module included with Python 2.4 provides much more powerful, high-level support for threads than the thread module discussed in the previous section.

The  _threading_  module exposes all the methods of the  _thread_  module and provides some additional methods −

-   **threading.activeCount()**  − Returns the number of thread objects that are active.
    
-   **threading.currentThread()**  − Returns the number of thread objects in the caller's thread control.
    
-   **threading.enumerate()**  − Returns a list of all thread objects that are currently active.
    

In addition to the methods, the threading module has the  _Thread_  class that implements threading. The methods provided by the  _Thread_  class are as follows −

-   **run()**  − The run() method is the entry point for a thread.
    
-   **start()**  − The start() method starts a thread by calling the run method.
    
-   **join([time])**  − The join() waits for threads to terminate.
    
-   **isAlive()**  − The isAlive() method checks whether a thread is still executing.
    
-   **getName()**  − The getName() method returns the name of a thread.
    
-   **setName()**  − The setName() method sets the name of a thread.
    

## Creating Thread Using Threading Module

To implement a new thread using the threading module, you have to do the following −

-   Define a new subclass of the  _Thread_  class.
    
-   Override the  ___init__(self [,args])_  method to add additional arguments.
    
-   Then, override the run(self [,args]) method to implement what the thread should do when started.
    

Once you have created the new  _Thread_  subclass, you can create an instance of it and then start a new thread by invoking the  _start()_, which in turn calls the  _run()_  method.

### Example

#!/usr/bin/python3  import threading import time

exitFlag =  0  class myThread (threading.Thread):  def __init__(self, threadID, name, counter): threading.Thread.__init__(self)  self.threadID = threadID self.name = name self.counter = counter def run(self):  print  ("Starting "  +  self.name) print_time(self.name,  self.counter,  5)  print  ("Exiting "  +  self.name)  def print_time(threadName, delay, counter):  while counter:  if exitFlag: threadName.exit() time.sleep(delay)  print  ("%s: %s"  %  (threadName, time.ctime(time.time()))) counter -=  1  # Create new threads thread1 = myThread(1,  "Thread-1",  1) thread2 = myThread(2,  "Thread-2",  2)  # Start new Threads thread1.start() thread2.start() thread1.join() thread2.join()  print  ("Exiting Main Thread")

### Result

When we run the above program, it produces the following result −

Starting Thread-1
Starting Thread-2
Thread-1: Fri Feb 19 10:00:21 2016
Thread-2: Fri Feb 19 10:00:22 2016
Thread-1: Fri Feb 19 10:00:22 2016
Thread-1: Fri Feb 19 10:00:23 2016
Thread-2: Fri Feb 19 10:00:24 2016
Thread-1: Fri Feb 19 10:00:24 2016
Thread-1: Fri Feb 19 10:00:25 2016
Exiting Thread-1
Thread-2: Fri Feb 19 10:00:26 2016
Thread-2: Fri Feb 19 10:00:28 2016
Thread-2: Fri Feb 19 10:00:30 2016
Exiting Thread-2
Exiting Main Thread

## Synchronizing Threads

The threading module provided with Python includes a simple-to-implement locking mechanism that allows you to synchronize threads. A new lock is created by calling the  _Lock()_  method, which returns the new lock.

The  _acquire(blocking)_  method of the new lock object is used to force the threads to run synchronously. The optional  _blocking_  parameter enables you to control whether the thread waits to acquire the lock.

If  _blocking_  is set to 0, the thread returns immediately with a 0 value if the lock cannot be acquired and with a 1 if the lock was acquired. If blocking is set to 1, the thread blocks and wait for the lock to be released.

The  _release()_  method of the new lock object is used to release the lock when it is no longer required.

### Example

#!/usr/bin/python3  import threading import time class myThread (threading.Thread):  def __init__(self, threadID, name, counter): threading.Thread.__init__(self)  self.threadID = threadID self.name = name self.counter = counter def run(self):  print  ("Starting "  +  self.name)  # Get lock to synchronize threads threadLock.acquire() print_time(self.name,  self.counter,  3)  # Free lock to release next thread threadLock.release()  def print_time(threadName, delay, counter):  while counter: time.sleep(delay)  print  ("%s: %s"  %  (threadName, time.ctime(time.time()))) counter -=  1 threadLock = threading.Lock() threads =  []  # Create new threads thread1 = myThread(1,  "Thread-1",  1) thread2 = myThread(2,  "Thread-2",  2)  # Start new Threads thread1.start() thread2.start()  # Add threads to thread list threads.append(thread1) threads.append(thread2)  # Wait for all threads to complete  for t in threads: t.join()  print  ("Exiting Main Thread")

### Output

When the above code is executed, it produces the following result −

Starting  Thread-1  Starting  Thread-2  Thread-1:  Fri  Feb  19  10:04:14  2016  Thread-1:  Fri  Feb  19  10:04:15  2016  Thread-1:  Fri  Feb  19  10:04:16  2016  Thread-2:  Fri  Feb  19  10:04:18  2016  Thread-2:  Fri  Feb  19  10:04:20  2016  Thread-2:  Fri  Feb  19  10:04:22  2016  Exiting  Main  Thread

## Multithreaded Priority Queue

The  _Queue_  module allows you to create a new queue object that can hold a specific number of items. There are following methods to control the Queue −

-   **get()**  − The get() removes and returns an item from the queue.
    
-   **put()**  − The put adds item to a queue.
    
-   **qsize()** − The qsize() returns the number of items that are currently in the queue.
    
-   **empty()**  − The empty( ) returns True if queue is empty; otherwise, False.
    
-   **full()**  − the full() returns True if queue is full; otherwise, False.
    

### Example

#!/usr/bin/python3  import queue import threading import time

exitFlag =  0  class myThread (threading.Thread):  def __init__(self, threadID, name, q): threading.Thread.__init__(self)  self.threadID = threadID self.name = name self.q = q def run(self):  print  ("Starting "  +  self.name) process_data(self.name,  self.q)  print  ("Exiting "  +  self.name)  def process_data(threadName, q):  while  not exitFlag: queueLock.acquire()  if  not workQueue.empty(): data = q.get() queueLock.release()  print  ("%s processing %s"  %  (threadName, data))  else: queueLock.release() time.sleep(1) threadList =  ["Thread-1",  "Thread-2",  "Thread-3"] nameList =  ["One",  "Two",  "Three",  "Four",  "Five"] queueLock = threading.Lock() workQueue = queue.Queue(10) threads =  [] threadID =  1  # Create new threads  for tName in threadList: thread = myThread(threadID, tName, workQueue) thread.start() threads.append(thread) threadID +=  1  # Fill the queue queueLock.acquire()  for word in nameList: workQueue.put(word) queueLock.release()  # Wait for queue to empty  while  not workQueue.empty():  pass  # Notify threads it's time to exit exitFlag =  1  # Wait for all threads to complete  for t in threads: t.join()  print  ("Exiting Main Thread")

### Output

When the above code is executed, it produces the following result −

Starting Thread-1
Starting Thread-2
Starting Thread-3
Thread-1 processing One
Thread-2 processing Two
Thread-3 processing Three
Thread-1 processing Four
Thread-2 processing Five
Exiting Thread-3
Exiting Thread-1
Exiting Thread-2
Exiting Main Thread

# Python 3 - XML Processing

XML is a portable, open source language that allows programmers to develop applications that can be read by other applications, regardless of operating system and/or developmental language.

## What is XML?

The Extensible Markup Language (XML) is a markup language much like HTML or SGML. This is recommended by the World Wide Web Consortium and available as an open standard.

XML is extremely useful for keeping track of small to medium amounts of data without requiring an SQL-based backbone.

## XML Parser Architectures and APIs

The Python standard library provides a minimal but useful set of interfaces to work with XML.

The two most basic and broadly used APIs to XML data are the SAX and DOM interfaces.

-   **Simple API for XML (SAX)**  − Here, you register callbacks for events of interest and then let the parser proceed through the document. This is useful when your documents are large or you have memory limitations, it parses the file as it reads it from the disk and the entire file is never stored in the memory.
    
-   **Document Object Model (DOM) API**  − This is a World Wide Web Consortium recommendation wherein the entire file is read into the memory and stored in a hierarchical (tree-based) form to represent all the features of an XML document.
    

SAX obviously cannot process information as fast as DOM, when working with large files. On the other hand, using DOM exclusively can really kill your resources, especially if used on many small files.

SAX is read-only, while DOM allows changes to the XML file. Since these two different APIs literally complement each other, there is no reason why you cannot use them both for large projects.

For all our XML code examples, let us use a simple XML file  _movies.xml_  as an input −

<collection  shelf  =  "New Arrivals">  <movie  title  =  "Enemy Behind">  <type>War, Thriller</type>  <format>DVD</format>  <year>2003</year>  <rating>PG</rating>  <stars>10</stars>  <description>Talk about a US-Japan war</description>  </movie>  <movie  title  =  "Transformers">  <type>Anime, Science Fiction</type>  <format>DVD</format>  <year>1989</year>  <rating>R</rating>  <stars>8</stars>  <description>A schientific fiction</description>  </movie>  <movie  title  =  "Trigun">  <type>Anime, Action</type>  <format>DVD</format>  <episodes>4</episodes>  <rating>PG</rating>  <stars>10</stars>  <description>Vash the Stampede!</description>  </movie>  <movie  title  =  "Ishtar">  <type>Comedy</type>  <format>VHS</format>  <rating>PG</rating>  <stars>2</stars>  <description>Viewable boredom</description>  </movie>  </collection>

## Parsing XML with SAX APIs

SAX is a standard interface for event-driven XML parsing. Parsing XML with SAX generally requires you to create your own ContentHandler by subclassing xml.sax.ContentHandler.

Your  _ContentHandler_  handles the particular tags and attributes of your flavor(s) of XML. A ContentHandler object provides methods to handle various parsing events. Its owning parser calls ContentHandler methods as it parses the XML file.

The methods  _startDocument_  and  _endDocument_  are called at the start and the end of the XML file. The method  _characters(text)_  is passed the character data of the XML file via the parameter text.

The ContentHandler is called at the start and end of each element. If the parser is not in namespace mode, the methods  _startElement(tag, attributes)_  and  _endElement(tag)_  are called; otherwise, the corresponding methods  _startElementNS_  and  _endElementNS_  are called. Here, tag is the element tag, and attributes is an Attributes object.

Here are other important methods to understand before proceeding −

## The make_parser Method

The following method creates a new parser object and returns it. The parser object created will be of the first parser type, the system finds.

xml.sax.make_parser(  [parser_list]  )

Here are the details of the parameters −

-   **parser_list**  − The optional argument consisting of a list of parsers to use which must all implement the make_parser method.
    

## The parse Method

The following method creates a SAX parser and uses it to parse a document.

xml.sax.parse( xmlfile, contenthandler[, errorhandler])

Here are the details of the parameters −

-   **xmlfile**  − This is the name of the XML file to read from.
    
-   **contenthandler**  − This must be a ContentHandler object.
    
-   **errorhandler**  − If specified, errorhandler must be a SAX ErrorHandler object.
    

## The parseString Method

There is one more method to create a SAX parser and to parse the specified  **XML string**.

xml.sax.parseString(xmlstring, contenthandler[, errorhandler])

Here are the details of the parameters −

-   **xmlstring**  − This is the name of the XML string to read from.
    
-   **contenthandler**  − This must be a ContentHandler object.
    
-   **errorhandler**  − If specified, errorhandler must be a SAX ErrorHandler object.
    

### Example

#!/usr/bin/python3  import xml.sax class  MovieHandler( xml.sax.ContentHandler  ):  def __init__(self):  self.CurrentData  =  ""  self.type =  ""  self.format =  ""  self.year =  ""  self.rating =  ""  self.stars =  ""  self.description =  ""  # Call when an element starts  def startElement(self, tag, attributes):  self.CurrentData  = tag if tag ==  "movie":  print  ("*****Movie*****") title = attributes["title"]  print  ("Title:", title)  # Call when an elements ends  def endElement(self, tag):  if  self.CurrentData  ==  "type":  print  ("Type:",  self.type)  elif  self.CurrentData  ==  "format":  print  ("Format:",  self.format)  elif  self.CurrentData  ==  "year":  print  ("Year:",  self.year)  elif  self.CurrentData  ==  "rating":  print  ("Rating:",  self.rating)  elif  self.CurrentData  ==  "stars":  print  ("Stars:",  self.stars)  elif  self.CurrentData  ==  "description":  print  ("Description:",  self.description)  self.CurrentData  =  ""  # Call when a character is read  def characters(self, content):  if  self.CurrentData  ==  "type":  self.type = content elif  self.CurrentData  ==  "format":  self.format = content elif  self.CurrentData  ==  "year":  self.year = content elif  self.CurrentData  ==  "rating":  self.rating = content elif  self.CurrentData  ==  "stars":  self.stars = content elif  self.CurrentData  ==  "description":  self.description = content if  ( __name__ ==  "__main__"):  # create an XMLReader parser = xml.sax.make_parser()  # turn off namepsaces parser.setFeature(xml.sax.handler.feature_namespaces,  0)  # override the default ContextHandler  Handler  =  MovieHandler() parser.setContentHandler(  Handler  ) parser.parse("movies.xml")

### Output

This would produce the following result −

*****Movie*****
Title: Enemy Behind
Type: War, Thriller
Format: DVD
Year: 2003
Rating: PG
Stars: 10
Description: Talk about a US-Japan war
*****Movie*****
Title: Transformers
Type: Anime, Science Fiction
Format: DVD
Year: 1989
Rating: R
Stars: 8
Description: A scientific fiction
*****Movie*****
Title: Trigun
Type: Anime, Action
Format: DVD
Rating: PG
Stars: 10
Description: Vash the Stampede!
*****Movie*****
Title: Ishtar
Type: Comedy
Format: VHS
Rating: PG
Stars: 2
Description: Viewable boredom

For a complete detail on SAX API documentation, please refer to the standard  [Python SAX APIs](https://docs.python.org/library/xml.sax.html).

## Parsing XML with DOM APIs

The Document Object Model ("DOM") is a cross-language API from the World Wide Web Consortium (W3C) for accessing and modifying the XML documents.

The DOM is extremely useful for random-access applications. SAX only allows you a view of one bit of the document at a time. If you are looking at one SAX element, you have no access to another.

Here is the easiest way to load an XML document quickly and to create a minidom object using the xml.dom module. The minidom object provides a simple parser method that quickly creates a DOM tree from the XML file.

The sample phrase calls the parse( file [,parser] ) function of the minidom object to parse the XML file, designated by file into a DOM tree object.

### Example

#!/usr/bin/python3  from xml.dom.minidom import parse import xml.dom.minidom # Open XML document using minidom parser  DOMTree  = xml.dom.minidom.parse("movies.xml") collection =  DOMTree.documentElement if collection.hasAttribute("shelf"):  print  ("Root element : %s"  % collection.getAttribute("shelf"))  # Get all the movies in the collection movies = collection.getElementsByTagName("movie")  # Print detail of each movie.  for movie in movies:  print  ("*****Movie*****")  if movie.hasAttribute("title"):  print  ("Title: %s"  % movie.getAttribute("title")) type = movie.getElementsByTagName('type')[0]  print  ("Type: %s"  % type.childNodes[0].data) format = movie.getElementsByTagName('format')[0]  print  ("Format: %s"  % format.childNodes[0].data) rating = movie.getElementsByTagName('rating')[0]  print  ("Rating: %s"  % rating.childNodes[0].data) description = movie.getElementsByTagName('description')[0]  print  ("Description: %s"  % description.childNodes[0].data)

### Output

This would produce the following result −

Root element : New Arrivals
*****Movie*****
Title: Enemy Behind
Type: War, Thriller
Format: DVD
Rating: PG
Description: Talk about a US-Japan war
*****Movie*****
Title: Transformers
Type: Anime, Science Fiction
Format: DVD
Rating: R
Description: A scientific fiction
*****Movie*****
Title: Trigun
Type: Anime, Action
Format: DVD
Rating: PG
Description: Vash the Stampede!
*****Movie*****
Title: Ishtar
Type: Comedy
Format: VHS
Rating: PG
Description: Viewable boredom

For a complete detail on DOM API documentation, please refer to the standard  [Python DOM APIs](https://docs.python.org/library/xml.dom.html).

# Python 3 - GUI Programming (Tkinter)

Python provides various options for developing graphical user interfaces (GUIs). The most important features are listed below.

-   **Tkinter**  − Tkinter is the Python interface to the Tk GUI toolkit shipped with Python. We would look this option in this chapter.
    
-   **wxPython**  − This is an open-source Python interface for wxWidgets GUI toolkit. You can find a complete tutorial on WxPython  [here](https://www.tutorialspoint.com/wxpython/index.htm).
    
-   **PyQt**  −This is also a Python interface for a popular cross-platform Qt GUI library. TutorialsPoint has a very good tutorial on PyQt  [here](https://www.tutorialspoint.com/pyqt/index.htm).
    
-   **JPython**  − JPython is a Python port for Java which gives Python scripts seamless access to the Java class libraries on the local machine  [http://www.jython.org](http://www.jython.org/).
    

There are many other interfaces available, which you can find them on the net.

## Tkinter Programming

Tkinter is the standard GUI library for Python. Python when combined with Tkinter provides a fast and easy way to create GUI applications. Tkinter provides a powerful object-oriented interface to the Tk GUI toolkit.

Creating a GUI application using Tkinter is an easy task. All you need to do is perform the following steps −

-   Import the  _Tkinter_  module.
    
-   Create the GUI application main window.
    
-   Add one or more of the above-mentioned widgets to the GUI application.
    
-   Enter the main event loop to take action against each event triggered by the user.
    

## Example

#!/usr/bin/python3  import tkinter # note that module name has changed from Tkinter in Python 2 to tkinter in Python 3 top = tkinter.Tk()  # Code to add widgets will go here... top.mainloop()

This would create a following window −

![TK Window](https://www.tutorialspoint.com/python3/images/tkwindow.jpg)

## Tkinter Widgets

Tkinter provides various controls, such as buttons, labels and text boxes used in a GUI application. These controls are commonly called widgets.

There are currently 15 types of widgets in Tkinter. We present these widgets as well as a brief description in the following table −

Sr.No.

Operator & Description

1

[Button](https://www.tutorialspoint.com/python3/tk_button.htm)

The Button widget is used to display buttons in your application.

2

[Canvas](https://www.tutorialspoint.com/python3/tk_canvas.htm)

The Canvas widget is used to draw shapes, such as lines, ovals, polygons and rectangles, in your application.

3

[Checkbutton](https://www.tutorialspoint.com/python3/tk_checkbutton.htm)

The Checkbutton widget is used to display a number of options as checkboxes. The user can select multiple options at a time.

4

[Entry](https://www.tutorialspoint.com/python3/tk_entry.htm)

The Entry widget is used to display a single-line text field for accepting values from a user.

5

[Frame](https://www.tutorialspoint.com/python3/tk_frame.htm)

The Frame widget is used as a container widget to organize other widgets.

6

[Label](https://www.tutorialspoint.com/python3/tk_label.htm)

The Label widget is used to provide a single-line caption for other widgets. It can also contain images.

7

[Listbox](https://www.tutorialspoint.com/python3/tk_listbox.htm)

The Listbox widget is used to provide a list of options to a user.

8

[Menubutton](https://www.tutorialspoint.com/python3/tk_menubutton.htm)

The Menubutton widget is used to display menus in your application.

9

[Menu](https://www.tutorialspoint.com/python3/tk_menu.htm)

The Menu widget is used to provide various commands to a user. These commands are contained inside Menubutton.

10

[Message](https://www.tutorialspoint.com/python3/tk_message.htm)

The Message widget is used to display multiline text fields for accepting values from a user.

11

[Radiobutton](https://www.tutorialspoint.com/python3/tk_radiobutton.htm)

The Radiobutton widget is used to display a number of options as radio buttons. The user can select only one option at a time.

12

[Scale](https://www.tutorialspoint.com/python3/tk_scale.htm)

The Scale widget is used to provide a slider widget.

13

[Scrollbar](https://www.tutorialspoint.com/python3/tk_scrollbar.htm)

The Scrollbar widget is used to add scrolling capability to various widgets, such as list boxes.

14

[Text](https://www.tutorialspoint.com/python3/tk_text.htm)

The Text widget is used to display text in multiple lines.

15

[Toplevel](https://www.tutorialspoint.com/python3/tk_toplevel.htm)

The Toplevel widget is used to provide a separate window container.

16

[Spinbox](https://www.tutorialspoint.com/python3/tk_spinbox.htm)

The Spinbox widget is a variant of the standard Tkinter Entry widget, which can be used to select from a fixed number of values.

17

[PanedWindow](https://www.tutorialspoint.com/python3/tk_panedwindow.htm)

A PanedWindow is a container widget that may contain any number of panes, arranged horizontally or vertically.

18

[LabelFrame](https://www.tutorialspoint.com/python3/tk_labelframe.htm)

A labelframe is a simple container widget. Its primary purpose is to act as a spacer or container for complex window layouts.

19

[tkMessageBox](https://www.tutorialspoint.com/python3/tk_messagebox.htm)

This module is used to display message boxes in your applications.

## Standard attributes

Let us look at how some of their common attributes, such as sizes, colors and fonts are specified.

-   [Dimensions](https://www.tutorialspoint.com/python3/tk_dimensions.htm)
    
-   [Colors](https://www.tutorialspoint.com/python3/tk_colors.htm)
    
-   [Fonts](https://www.tutorialspoint.com/python3/tk_fonts.htm)
    
-   [Anchors](https://www.tutorialspoint.com/python3/tk_anchors.htm)
    
-   [Relief styles](https://www.tutorialspoint.com/python3/tk_relief.htm)
    
-   [Bitmaps](https://www.tutorialspoint.com/python3/tk_bitmaps.htm)
    
-   [Cursors](https://www.tutorialspoint.com/python3/tk_cursors.htm)
    

## Geometry Management

All Tkinter widgets have access to the specific geometry management methods, which have the purpose of organizing widgets throughout the parent widget area. Tkinter exposes the following geometry manager classes: pack, grid, and place.

-   [The pack() Method](https://www.tutorialspoint.com/python3/tk_pack.htm)  − This geometry manager organizes widgets in blocks before placing them in the parent widget.
    
-   [The grid() Method](https://www.tutorialspoint.com/python3/tk_grid.htm)  − This geometry manager organizes widgets in a table-like structure in the parent widget.
    
-   [The place() Method](https://www.tutorialspoint.com/python3/tk_place.htm)  − This geometry manager organizes widgets by placing them in a specific position in the parent widget.
    

# Python 3 - Extension Programming with C


Any code that you write using any compiled language like C, C++, or Java can be integrated or imported into another Python script. This code is considered as an "extension."

A Python extension module is nothing more than a normal C library. On Unix machines, these libraries usually end in  **.so**  (for shared object). On Windows machines, you typically see  **.dll**  (for dynamically linked library).

## Pre-Requisites for Writing Extensions

To start writing your extension, you are going to need the Python header files.

-   On Unix machines, this usually requires installing a developer-specific package such as  python2.5-dev.
    
-   Windows users get these headers as part of the package when they use the binary Python installer.
    

Additionally, it is assumed that you have a good knowledge of C or C++ to write any Python Extension using C programming.

## First look at a Python Extension

For your first look at a Python extension module, you need to group your code into four part −

-   The header file  _Python.h_.
    
-   The C functions you want to expose as the interface from your module.
    
-   A table mapping the names of your functions as Python developers see them as C functions inside the extension module.
    
-   An initialization function.
    

## The Header File Python.h

You need to include  _Python.h_  header file in your C source file, which gives you the access to the internal Python API used to hook your module into the interpreter.

Make sure to include Python.h before any other headers you might need. You need to follow the includes with the functions you want to call from Python.

## The C Functions

The signatures of the C implementation of your functions always takes one of the following three forms −

static  PyObject  *MyFunction(  PyObject  *self,  PyObject  *args );  static  PyObject  *MyFunctionWithKeywords(PyObject  *self,  PyObject  *args,  PyObject  *kw);  static  PyObject  *MyFunctionWithNoArgs(  PyObject  *self  );

Each one of the preceding declarations returns a Python object. There is no such thing as a  _void_ function in Python as there is in C. If you do not want your functions to return a value, return the C equivalent of Python's  **None**  value. The Python headers define a macro, Py_RETURN_NONE, that does this for us.

The names of your C functions can be whatever you like as they are never seen outside of the extension module. They are defined as  _static_  function.

Your C functions usually are named by combining the Python module and function names together, as shown here −

static  PyObject  *module_func(PyObject  *self,  PyObject  *args)  {  /* Do your stuff here. */  Py_RETURN_NONE;  }

This is a Python function called  _func_  inside the module  _module_. You will be putting pointers to your C functions into the method table for the module that usually comes next in your source code.

## The Method Mapping Table

This method table is a simple array of PyMethodDef structures. That structure looks something like this −

struct  PyMethodDef  {  char  *ml_name;  PyCFunction ml_meth;  int ml_flags;  char  *ml_doc;  };

Here is the description of the members of this structure −

-   **ml_name**  − This is the name of the function as the Python interpreter presents when it is used in Python programs.
    
-   **ml_meth**  − This is the address of a function that has any one of the signatures described in the previous section.
    
-   **ml_flags**  − This tells the interpreter which of the three signatures ml_meth is using.
    
    -   This flag usually has a value of METH_VARARGS.
        
    -   This flag can be bitwise OR'ed with METH_KEYWORDS if you want to allow keyword arguments into your function.
        
    -   This can also have a value of METH_NOARGS that indicates you do not want to accept any arguments.
        
-   **ml_doc**  − This is the docstring for the function, which could be NULL if you do not feel like writing one.
    

This table needs to be terminated with a sentinel that consists of NULL and 0 values for the appropriate members.

### Example

For the above-defined function, we have the following method mapping table −

static  PyMethodDef module_methods[]  =  {  {  "func",  (PyCFunction)module_func, METH_NOARGS, NULL },  { NULL, NULL,  0, NULL }  };

## The Initialization Function

The last part of your extension module is the initialization function. This function is called by the Python interpreter when the module is loaded. It is required that the function be named  **init_Module_**, where  _Module_  is the name of the module.

The initialization function needs to be exported from the library you will be building. The Python headers define PyMODINIT_FUNC to include the appropriate incantations for that to happen for the particular environment in which we are compiling. All you have to do is use it when defining the function.

Your C initialization function generally has the following overall structure −

PyMODINIT_FUNC initModule()  {  Py_InitModule3(func, module_methods,  "docstring...");  }

Here is the description of  **Py_InitModule3**  function −

-   **func**  − This is the function to be exported.
    
-   **module_methods**  − This is the mapping table name defined above.
    
-   **docstring**  − This is the comment you want to give in your extension.
    

Putting all this together, it looks like the following −

#include  <Python.h>  static  PyObject  *module_func(PyObject  *self,  PyObject  *args)  {  /* Do your stuff here. */  Py_RETURN_NONE;  }  static  PyMethodDef module_methods[]  =  {  {  "func",  (PyCFunction)module_func, METH_NOARGS, NULL },  { NULL, NULL,  0, NULL }  };  PyMODINIT_FUNC initModule()  {  Py_InitModule3(func, module_methods,  "docstring...");  }

### Example

A simple example that makes use of all the above concepts −

#include  <Python.h>  static  PyObject* helloworld(PyObject*  self)  {  return  Py_BuildValue("s",  "Hello, Python extensions!!");  }  static  char helloworld_docs[]  =  "helloworld( ): Any message you want to put here!!\n";  static  PyMethodDef helloworld_funcs[]  =  {  {"helloworld",  (PyCFunction)helloworld, METH_NOARGS, helloworld_docs},  {NULL}  };  void inithelloworld(void)  {  Py_InitModule3("helloworld", helloworld_funcs,  "Extension module example!");  }

Here the  _Py_BuildValue_  function is used to build a Python value. Save above code in hello.c file. We would see how to compile and install this module to be called from Python script.

## Building and Installing Extensions

The  _distutils_  package makes it very easy to distribute Python modules, both pure Python and extension modules, in a standard way. Modules are distributed in the source form, built and installed via a setup script usually called  _setup.py_  as.

For the above module, you need to prepare the following setup.py script −

from distutils.core import setup,  Extension setup(name =  'helloworld', version =  '1.0', \
   ext_modules =  [Extension('helloworld',  ['hello.c'])])

Now, use the following command, which would perform all needed compilation and linking steps, with the right compiler and linker commands and flags, and copies the resulting dynamic library into an appropriate directory −

$ python setup.py install

On Unix-based systems, you will most likely need to run this command as root in order to have permissions to write to the site-packages directory. This usually is not a problem on Windows.

## Importing Extensions

Once you install your extensions, you would be able to import and call that extension in your Python script as follows −

### Example

#!/usr/bin/python3  import helloworld print helloworld.helloworld()

### Output

This would produce the following result −

Hello, Python extensions!!

## Passing Function Parameters

As you will most likely want to define functions that accept arguments, you can use one of the other signatures for your C functions. For example, the following function, that accepts some number of parameters, would be defined like this −

static  PyObject  *module_func(PyObject  *self,  PyObject  *args)  {  /* Parse args and do something interesting here. */  Py_RETURN_NONE;  }

The method table containing an entry for the new function would look like this −

static  PyMethodDef module_methods[]  =  {  {  "func",  (PyCFunction)module_func, METH_NOARGS, NULL },  {  "func", module_func, METH_VARARGS, NULL },  { NULL, NULL,  0, NULL }  };

You can use the API  _PyArg_ParseTuple_  function to extract the arguments from the one PyObject pointer passed into your C function.

The first argument to PyArg_ParseTuple is the args argument. This is the object you will be  _parsing_. The second argument is a format string describing the arguments as you expect them to appear. Each argument is represented by one or more characters in the format string as follows.

static  PyObject  *module_func(PyObject  *self,  PyObject  *args)  {  int i;  double d;  char  *s;  if  (!PyArg_ParseTuple(args,  "ids",  &i,  &d,  &s))  {  return NULL;  }  /* Do something interesting here. */  Py_RETURN_NONE;  }

### Output

Compiling the new version of your module and importing it enables you to invoke the new function with any number of arguments of any type −

module.func(1, s = "three", d = 2.0)
module.func(i = 1, d = 2.0, s = "three")
module.func(s = "three", d = 2.0, i = 1)

You can probably come up with even more variations.

## The PyArg_ParseTuple Function

Here is the standard signature for the  **PyArg_ParseTuple**  function −

int  PyArg_ParseTuple(PyObject* tuple,char* format,...)

This function returns 0 for errors, and a value not equal to 0 for success. Tuple is the PyObject* that was the C function's second argument. Here  _format_  is a C string that describes mandatory and optional arguments.

Here is a list of format codes for the  **PyArg_ParseTuple**  function −

Code

C type

Meaning

c

char

A Python string of length 1 becomes a C char.

d

double

A Python float becomes a C double.

f

float

A Python float becomes a C float.

i

int

A Python int becomes a C int.

l

long

A Python int becomes a C long.

L

long long

A Python int becomes a C long long

O

PyObject*

Gets non-NULL borrowed reference to Python argument.

s

char*

Python string without embedded nulls to C char*.

s#

char*+int

Any Python string to C address and length.

t#

char*+int

Read-only single-segment buffer to C address and length.

u

Py_UNICODE*

Python Unicode without embedded nulls to C.

u#

Py_UNICODE*+int

Any Python Unicode C address and length.

w#

char*+int

Read/write single-segment buffer to C address and length.

z

char*

Like s, also accepts None (sets C char* to NULL).

z#

char*+int

Like s#, also accepts None (sets C char* to NULL).

(...)

as per ...

A Python sequence is treated as one argument per item.

|

The following arguments are optional.

:

Format end, followed by function name for error messages.

;

Format end, followed by entire error message text.

## Returning Values

_Py_BuildValue_  takes in a format string much like  _PyArg_ParseTuple_  does. Instead of passing in the addresses of the values you are building, you pass in the actual values. Here is an example showing how to implement an add function −

static  PyObject  *foo_add(PyObject  *self,  PyObject  *args)  {  int a;  int b;  if  (!PyArg_ParseTuple(args,  "ii",  &a,  &b))  {  return NULL;  }  return  Py_BuildValue("i", a + b);  }

This is what it would look like if implemented in Python −

def  add(a, b):  return  (a + b)

You can return two values from your function as follows. This would be captured using a list in Python.

static  PyObject  *foo_add_subtract(PyObject  *self,  PyObject  *args)  {  int a;  int b;  if  (!PyArg_ParseTuple(args,  "ii",  &a,  &b))  {  return NULL;  }  return  Py_BuildValue("ii", a + b, a - b);  }

This is what it would look like if implemented in Python −

def add_subtract(a, b):  return  (a + b, a - b)

## The  _Py_BuildValue_  Function

Here is the standard signature for  **Py_BuildValue**  function −

PyObject*  Py_BuildValue(char* format,...)

Here  _format_  is a C string that describes the Python object to build. The following arguments of  _Py_BuildValue_  are C values from which the result is built. The  _PyObject*_  result is a new reference.

The following table lists the commonly used code strings, of which zero or more are joined into a string format.

Code

C type

Meaning

c

char

A C char becomes a Python string of length 1.

d

double

A C double becomes a Python float.

f

float

A C float becomes a Python float.

i

int

A C int becomes a Python int.

l

long

A C long becomes a Python int.

N

PyObject*

Passes a Python object and steals a reference.

O

PyObject*

Passes a Python object and INCREFs it as normal.

O&

convert+void*

Arbitrary conversion

s

char*

C 0-terminated char* to Python string, or NULL to None.

s#

char*+int

C char* and length to Python string, or NULL to None.

u

Py_UNICODE*

C-wide, null-terminated string to Python Unicode, or NULL to None.

u#

Py_UNICODE*+int

C-wide string and length to Python Unicode, or NULL to None.

w#

char*+int

Read/write single-segment buffer to C address and length.

z

char*

Like s, also accepts None (sets C char* to NULL).

z#

char*+int

Like s#, also accepts None (sets C char* to NULL).

(...)

as per ...

Builds Python tuple from C values.

[...]

as per ...

Builds Python list from C values.

{...}

as per ...

Builds Python dictionary from C values, alternating keys and values.

Code {...} builds dictionaries from an even number of C values, alternately keys and values. For example, Py_BuildValue("{issi}",23,"zig","zag",42) returns a dictionary like Python's {23:'zig','zag':42}.

> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMjIxNDY2OV19
-->