# Set Passwords and Secret Keys in Environment Variables (Mac/Linux/Windows)

**Hide Passwords and Secret Keys in Environment Variables**

If you are into  [python](https://python.org/)  , there is a fair chance that you would have contributed to open-source or had your code snippets/projects on  [Github](https://github.com/)  or  [BitBucket](https://bitbucket.org/).Some time your code involves some important credentials like passwords or secret keys etc. like the code for our post on  [how to send emails using python](https://saralgyaan.com/posts/use-python-to-send-email/)  uses google/app password. You surely do not want to hard code the password in your code and accidentaly push it to a remote repository. Hence, the safest way is to do so is saving your secret keys/password in envirnoment variables. In this post we will learn how to save/hide the passwords, secret keys in  [environment variables](https://docs.python.org/3/using/windows.html#excursus-setting-environment-variables)  for MacOS, Linux and Windows.

**The wrong way**

Hard coding your username, passwords or secret keys in your code is wrong way and it exposes you to vulnerability. Have a look at the code below:-

```
# The wrong way 

user_name = 'my_user_name'
password = 'my_password'

print(user_name, password)

# output

my_user_name my_password

```

**Set Passwords and Secret Keys in Environment Variables on Mac/Linux**

To set password and secret keys in environment variable on Mac and Linux. You will need to open and modify  [.bash_profile](https://www.thegeekdiary.com/what-is-the-purpose-of-bash_profile-file-under-user-home-directory-in-linux/)  . To do that open the  [terminal](https://support.apple.com/en-in/guide/terminal/welcome/mac)  on your Mac or Linux and cd to the home directory. (You can read about useful terminal commands of mac  [here](https://medium.com/@uditvashisht/10-basic-terminal-commands-every-macos-user-must-know-1052cdb6add))

```c
user desktop $ cd
user ~ $

```

Now open the .bash_profile using your favorite editor like  [nano](https://www.nano-editor.org/)  ,  [vim](https://www.vim.org/)  ,  [sublime text](https://www.sublimetext.com/)  ,  [atom](https://atom.io/)  etc. You can read a bit more about the text editors  [here](https://saralgyaan.com/posts/chapter-2-quick-setup/)

```PY
user ~ $ nano .bash_profile

```

The following file will open . You may not have the same text like mine there.

![set password secret key in environment variable python.png](https://saralgyaan.com/media/images/uploads/2019/08/14/02c9160539-set-password-secret-key-in-environment-variable-python.png)

Now we need to add our environment variables. For that we will have to write the following code. Remember that there is  **no whitespace**  on either side of =.

```PY
export USER="my_user_name"
export PASSWORD="my_password"

```

Press ctrl + x and Y to save the nano file.

Now either restart the terminal or use the following command to effect the changes.

```PY
user ~ $ source .bash_profile

```

Now to use these variables in our python script, we will be needing  [os](https://docs.python.org/3/library/os.html)  module. Have a look at the following code. Here instead of hard coding the username and password like the example above, we have used the environment variables and still the result is same.

```PY
import os 

user_name = os.environ.get('USER')
password = os.environ.get('password')

print(user_name, password)

# output

my_user_name my_password

```

**Set Passwords and Secret Keys in Environment Variables on Windows**

To set the passwords and secret keys in environment variables on Windows, you will have to open Advance System Setting. You can either type ‘Advanced System Setting’ in search bar or browse to it by right clicking My Computer on desktop-> properties -> Advanced System Setting

![set password and secret keys in environment variables python.PNG](https://saralgyaan.com/media/images/uploads/2019/08/14/444338f2c2-set-password-and-secret-keys-in-environment-variables-python.PNG)

Now in Advance System Setting you will have to click on Environment Variables and the following screen will appear.

![set password and secret keys in environment variables python -.PNG](https://saralgyaan.com/media/images/uploads/2019/08/14/92c72da7f6-set-password-and-secret-keys-in-environment-variables-python--.PNG)

Now, here we need to add new user variable. So click on new and add both the variables.

![set password and secret keys in environment variables python -!.PNG](https://saralgyaan.com/media/images/uploads/2019/08/14/6b83d7e2ea-set-password-and-secret-keys-in-environment-variables-python--!.PNG)

Now using the same code as above, we can access the environmental variables.

```
import os 

user_name = os.environ.get('USER')
password = os.environ.get('password')

print(user_name, password)

# output

my_user_name my_password
```






> Written with [StackEdit](https://saralgyaan.com/posts/set-passwords-and-secret-keys-in-environment-variables-maclinuxwindows-python-quicktip/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODY5NDQzMjBdfQ==
-->