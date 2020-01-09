
# Use Python to send email using SMTP

**Use Python to send emails**

In this tutorial, we will learn to use  [python](https://www.python.org/)  to send emails. If you are new to python, you can see our  [beginner’s series](https://saralgyaan.com/posts/chapter-1-introduction/). In case you are having trouble installing Python, you can see our posts on installing python on  [MacOS](https://saralgyaan.com/posts/how-to-install-python-3-on-macos-and-linux/)  and  [Windows](https://saralgyaan.com/posts/how-to-install-python-on-windows-pc/).

We will start with sending plain email using python and then learn to send advanced automated emails, HTML emails, emails with attachments etc. In this tutorial, we will be using  [gmail](https://mail.google.com/)  to send email via python, which is the most common email service used. However, you can use any other email service.(You will have to use slightly different setting in that case.)

Open your gmail account. If you are not using  [2-Step Verification](https://www.google.com/landing/2step/), you will have to allow less secure apps from this  [link](https://myaccount.google.com/lesssecureapps?pli=1).

![python send emails ...png](https://saralgyaan.com/media/images/uploads/2019/08/14/d9c92c1594-python-send-emails-...png)

However, if you are using  [2-Step Verification](https://www.google.com/landing/2step/)  (which I highly recommend), you need to create app password for your account for this project from  [here](https://myaccount.google.com/u/2/apppasswords). You can learn to create app passwords from google’s  [official documentation](https://support.google.com/accounts/answer/185833).

We do not want to hard code our username and password, so we will be using  [environment variable to set them](https://saralgyaan.com/posts/set-passwords-and-secret-keys-in-environment-variables-maclinuxwindows-python-quicktip/). Open the .bash_profile of your MacOS and save the email and password (or app password in case of 2-step verification) as under:-

```py
$ nano .bash_profile

```

```py
# .bash_profile
export EMAIL_USER="your_email"
export PASSWORD="your_password"

```

```py
$ source .bash_profile

```

**Sending simple email using python**

Now create a file called ‘python_send_email.py’ and import  [smtplib](https://docs.python.org/3/library/smtplib.html)  and write down the following code:-

```py
# python_send_email.py

import os
import smtplib

EMAIL = os.environ.get('EMAIL_USER')
PASSWORD = os.environ.get('PASSWORD')

with smtplib.SMTP('smtp.gmail.com', 587) as smtp:
    smtp.ehlo()
    smtp.starttls()
    smtp.ehlo()
    smtp.login(EMAIL, PASSWORD)
    subject = 'Python Send Email'
    body = 'This email is sent using python'
    message = f'Subject:{subject}\n\n{body}'
    smtp.sendmail(EMAIL, EMAIL, message)

```

Let me quickly go through each step.

We have used os to use  [environment variables](https://docs.python.org/3/library/os.html#os.environ,)  where we have saved our username and password.  
Then we have used the  [context manager](http://book.pythontips.com/en/latest/context_managers.html), so that the connection ends by itself after the script is complete.

Then we identified ourselves using  [smtp.ehlo()](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.ehlo), then we put it in the connection mode using  [smtp.starttls()](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.starttls)  and logged in using  [smtp.login()](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.login).

Finally, we will draft the email by adding subject, body, message and send it using  [smtp.sendmail(sender, receipient, message)](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail). Running the script will send the simple email to the user.

![python send emails _.png](https://saralgyaan.com/media/images/uploads/2019/08/14/1364822ec9-python-send-emails-_.png)

**Sending email using local debugging server**

While we are testing/learning, it could be frustrating to use real email, so we will start local debugging server using the following command. When we will run this, all the future emails which we will send using our script will be displayed on the terminal.

```py
$ python -m smtpd -c DebuggingServer -n localhost:1025

```

Now, we will have to make following changes to python_send_email.py :-

```py
# python_send_email.py

# with smtplib.SMTP('smtp.gmail.com', 587) as smtp:
with smtplib.SMTP('localhost', 1025) as smtp:    #add this and comment out the rest
    # smtp.ehlo()
    # smtp.starttls()
    # smtp.ehlo()
    # smtp.login(EMAIL, PASSWORD)

```

Now if we will run our python_send_email.py, it will be displayed in the terminal.

![python send email !.png](https://saralgyaan.com/media/images/uploads/2019/08/14/42f1b44e5a-python-send-email-!.png)

**Cleaning it up**

Instead of calling the server using  [smtp.ehlo()](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.ehlo)  we will be creating a SSL connection from the very beginning using  [smptlib.SMTP_SSL](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL)  and instead of port 587, we will use port 465. Now, we will be taking advantage of EmailMessage class of email.message to create a message and finally  [smtp.send_message()](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.send_message)  to send that message. The modified code is as under:-

```py
# python_send_email.py

import os
import smtplib
from email.message import EmailMessage #new

EMAIL = os.environ.get('EMAIL_USER')
PASSWORD = os.environ.get('PASSWORD')

message = EmailMessage()
message['Subject'] = 'Python Send Email'
message['From'] = EMAIL
message['To'] = EMAIL
message.set_content('This email is sent using python.')

with smtplib.SMTP_SSL('smtp.gmail.com', 465) as smtp:
    smtp.login(EMAIL, PASSWORD)
    smtp.send_message(message)

```

**Python - send email with attachment**

Now we will be sending the emails with attachment. In order to send an image we will be using  [imghdr](https://docs.python.org/3/library/imghdr.html#module-imghdr)  to find out the type of the image. Now place the image python_send_email.jpg in the same directory as the script python_send_email.py and change the code as under:

```py
# python_send_email.py

import imghdr # new


with open('python_send_email.jpg', 'rb') as f:
    file_data = f.read()
    file_type = imghdr.what(f.name)
    file_name = f.name

message.add_attachment(file_data, maintype='image', subtype=file_type, filename=file_name)


```





> Written with [StackEdit](https://saralgyaan.com/posts/use-python-to-send-email/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2MzU0ODIwOF19
-->