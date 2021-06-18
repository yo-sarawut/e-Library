Convert Python PY File to EXE File
===
![enter image description here](https://geekscoders.com/wp-content/uploads/2020/10/convert-py-to-exe-python.jpg)

In this article we are going to learn How to Convert Python PY File to EXE File, also we

will learn how you can create installer for your application. for converting PY to EXE we

are going to use pyinstaller library, and for making installer we want to use inno setup

application. pyinstaller is a library that you can use for you can use for converting of your

PY file to EXE file.

-   [Python Top 5 Game Libraries](https://geekscoders.com/python-top-5-game-libraries/)
-   [Python GUI Development Libraries](https://geekscoders.com/python-gui-development-libraries/)
-   [Web Development Libraries in Python](https://geekscoders.com/python-web-development-frameworks/)
-   [How to Download Youtube Videos in Python](https://geekscoders.com/how-to-download-youtube-videos-in-python/)
-   [Working with Python Pyglet Library](https://geekscoders.com/python-pyglet-working-with-pyglet-library/)
-   [Python Speech Recognition For Beginners](https://geekscoders.com/python-speech-recognition-tutorial-for-beginners/)

### **Installation**

First of all you need to install pyinstaller, you can use pip for the installation.
```
pip install pyinstaller
```
OK in this example we are going to create a GUI application using PyQt5,

so PyQt5 is a binding for [Qt5 C++](https://doc.qt.io/qt-5/qt5-intro.html) a GUI framework for C++ programming language,

PyQt5 is used to write all kinds of GUI applications, from accounting applications, to

visualization tools used by scientists and engineers. it is possible to write PyQt5 applications

that are just tens of lines long, and medium-size projects of 1000 to 10000 lines are very

common. if you are not using PyQt5 you can use another Python GUI Libraries like

TKinter, Kivy or wxPython.

basically this is a simple code for creating of a basic window in pyqt5, we want to first

convert this python PY file to EXE and after that we make an installer for our application

using InnoSetup.


```py
from PyQt5.QtWidgets import QApplication,  QWidget,  QVBoxLayout,  QLabel

import sys

from PyQt5.QtGui import QIcon,  QFont

class  WindowExample(QWidget):

def __init__(self):

super().__init__()

self.setGeometry(200,200,  400,300)

self.setWindowTitle("Codeloop.org")

self.setWindowIcon(QIcon('python.ico'))

self.setStyleSheet('background-color:red')

vbox  =  QVBoxLayout()

label  =  QLabel("Welcome to GeeksCoders.com")

label.setFont(QFont("Sanserif",  14))

label.setStyleSheet('color:white')

vbox.addWidget(label)

self.setLayout(vbox)

app  =  QApplication(sys.argv)

window  =  WindowExample()

window.show()

sys.exit(app.exec_())
```
Now let’s convert this PY file to EXE, first of all you need to copy this file in your

Scripts folder.

![Scripts Folder in Python ](https://geekscoders.com/wp-content/uploads/2020/10/script-folder-in-python.jpg)

Scripts Folder in Python

and after that run this command, make sure that you have also copied an icon

in the Scripts folder.

1

pyinstaller  --onefile  --windowed  --icon=python.ico window.py

### **What to generate Option**

-D, --onedir

Create a one-folder bundle containing an executable (default)

-F, --onefile

Create a one-file bundled executable.

--specpath DIR

Folder to store the generated spec file (default: current directory)

-n NAME, --name NAME

Name to assign to the bundled app and spec file (default: first script’s basename)

### **Windows and Mac OS X specific options**

-c, --console, --nowindowed

Open a console window for standard i/o (default). On Windows this option will have no effect if the first script is a ‘.pyw’ file.

-w, --windowed, --noconsole

Windows and Mac OS X: do not provide a console window for standard i/o. On Mac OS X this also triggers building an OS X .app bundle. On Windows this option will be set if the first script is a ‘.pyw’ file. This option is ignored in *NIX systems.

-i <FILE.ico or FILE.exe,ID or FILE.icns>, --icon <FILE.ico or FILE.exe,ID or FILE.icns>

FILE.ico: apply that icon to a Windows executable. FILE.exe,ID, extract the icon with ID from an exe. FILE.icns: apply the icon to the .app bundle on Mac OS X

After that you will have two directory in your Scripts folder.

![PyInstaller Convert PY to EXE](https://geekscoders.com/wp-content/uploads/2020/10/pinstaller-convert-py-exe.jpg)

PyInstaller Convert PY to EXE

Also you can find the exe file in the  _dist_ folder.

![How to Convert Python PY File to EXE File](https://geekscoders.com/wp-content/uploads/2020/10/python-exe-file.jpg)

How to Convert Python PY File to EXE File

### **How to Convert our EXE to Setup Installer**

OK sometimes you need to create an installer for your application, for example you

have created your application and you want to sell that application or you want to give

that for your friend, for this you want to create an installer that they can install your

application in their computers, for creating of installer we need to use  [InnoSetup](https://jrsoftware.org/isdl.php).

Now make two folders and copy your two directories of  _dist_ and _build_, paste  
that in your created second folder. also copy your icon in that folder like this.

![Python Make Installer Setup](https://geekscoders.com/wp-content/uploads/2020/10/python-inno-setup-example.jpg)

Python Make Installer Setup

Now open your InnoSetup, from _File_ choose _New_ and after that you need to

add your application information that you want to make setup installer.

![Python Inno Setup Application Info](https://geekscoders.com/wp-content/uploads/2020/10/python-inno-setup-geekscoders.jpg)

Python Inno Setup Application Info

After that click on next, there will be another page of Application Folder, you don’t need

to bring changes in their, just click on next.

Now we have Application Files page, in here in the Application main executable you need to

_Browse_ your exe file from the folder that you have already copied. after that click on the

_Add Folder_ and you need to add your main folder that includes the dist and build folders.

![Inno Setup Add Folder ](https://geekscoders.com/wp-content/uploads/2020/10/inno-setup-add-folders-geekscoders.jpg)

Inno Setup Add Folder

Than click on next you will see Application Shortcut page, you don’t need to bring

any changes in their, just click on next.

![Inno Setup Shortcut ](https://geekscoders.com/wp-content/uploads/2020/10/create-shortcut-inno-setup.jpg)

Inno Setup Shortcut

after that there will be Application Documentation, like you can add license

and before installation instructions for the application, iam not going to give any

documentation for the application so just click on next if you don’t want.

![Application Documentation Inno Setup](https://geekscoders.com/wp-content/uploads/2020/10/application-documentation-in-inno-setup.jpg)

Application Documentation Inno Setup

Don’t bring any change in the setup install mode page click on next.

![Setup Install Mode Inno Setup](https://geekscoders.com/wp-content/uploads/2020/10/setup-install-mode-pyinstaller-inno-setup.jpg)

Setup Install Mode Inno Setup

After that choose your language and click on next, now you need to give the

compiler output folder also add your icon in here.

![Inno Setup Compiler Setting ](https://geekscoders.com/wp-content/uploads/2020/10/compiler-setting-pyinstaller-inno-setup.jpg)

Inno Setup Compiler Setting

Click on next and finish, now you are done and you have a setup for your application,

you can install that on your computer and you can give the installer for your friends,

they install the application and use from that.

Thank you for visiting my website! If you enjoyed the free courses, please consider supporting my works on Patreon.
















> Reference : https://geekscoders.com/how-to-convert-python-py-file-to-exe-file/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5ODEzMjU5OF19
-->