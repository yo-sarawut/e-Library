Password Hashing with Flask Tutorial
===
<iframe width="622" height="350" src="https://www.youtube.com/embed/UtF58KqcHWU?list=PLQVvvaa0QuDc_owjTbIY4rbgXOFkUYOUB" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

While we have already incorporated the password hashing into our registration page, I wanted to take some time to go over what is actually happening. Maybe you end up working in another language, or maybe passlib doesn't support the version of Python you are using in the future. Because of this, you should know at least at a high level, how it works.

Not only is it important for security practices, it's also just pretty cool how it works!
To begin, you can probably understand why it is important to encrypt passwords to begin with. If your database stores plain-text passwords, at the very least, you are going to see the passwords yourself, and so will anyone who has access to your server. In a perfect world, no one would invade a user's privacy, but this world is not perfect. Not only might someone who works for you steal user passwords, a hacker might, or even the host to your server might, if you are using a virtual private server, or shared hosting.

So then how might we obscure passwords? Obscuring original text is easy enough, we can right a randomized algorithm that does this. The problem is, with passwords, we actually need to be able to validate what a user enters in the future as the original password.

One of the more primitive measures taken was simple password hashing. This was where a hash function was applied to what the user input, and that hash was what was stored as a password.

Here's a simple hashing script to illustrate this, which you can run:
```py
import hashlib
password =  'pa$$w0rd' 
h = hashlib.md5(password.encode())  
print(h.hexdigest())
```
Import hashlib, set an example password, create the hash object, print the hash:
```py
`6c9b8b27dea1ddb845f96aa2567c6754`
```
o that works pretty well. If you just saw that hash in a database, you'd have no idea what it meant. The problem, however, arises with the following: Run the script two times, or five times. You will find that the output is the same every time. Initially, with validation in mind, you may think well isn't this a requirement anyway? How else can we achieve validation?

The problem here is that people created massive hash tables, notably referred to as hash-lookup tables, where you could just search for the hash, and then find the corresponding plain-text password. You could also create one yourself, by just generating hashes for combinations of characters. It takes a bit longer to generate the tables, . These tables are big, but not too big to store on your laptop or netbook.

What we need instead, is a way to generate unique hashes, yet find a way to validate that hash by asking merely if two hashes came from the same input, despite being very different hashes.

Before arriving there, however, people came up with an easier solution: Why not place a secret pattern of text into every entered password, that only we the server knew. This is what is known as "salting."

Salting, while still used, initially started out pretty simple. Here's an example of how salting works, building off our last example:
```py
import hashlib

user_entered_password =  'pa$$w0rd' 
salt =  "5gz" 
db_password = user_entered_password+salt
h = hashlib.md5(db_password.encode())  
print(h.hexdigest())  
```
Here, the only major difference is we just have a salt that we append to the very end. Then, any time the user enters their password, we append the salt, hash it, and then compare those hashes.
```py
de6e389819bdaa9e0ca60bb52cabccae
```
Now, the salt can be added anywhere. Maybe it's input right in the middle, maybe at the beginning, maybe at the end. May you have a salt at the beginning, another for the middle of the password, and one more at the end even.

This is pretty good, but there is inherent risk, still, and here's why:

The hash is always the same for the same password. This means if someone cracks how you generated your salt, then they have now cracked all passwords by generating a hash table. This, again, can take a lot of processing, but this is by no means out of reach by today's standards.

One of the adages for encryption is that you cannot depend on secrecy for security. A good test for your encryption is to ask yourself: "If someone discovers my encryption method, is my security compromised?" In many cases, like with a cipher for example, the answer to this is "yes!" That's a problem. Consider that many reasons why someone has access to your database also mean that they have access to your source code. This means someone can find out your salt. From here, it's relatively quick work to break the entire database of encrypted passwords.

What we want instead is a way to generate unique hashes, where their source can be validated easily, but brute forcing will require a brute forcing per password, not a brute forcing for the entire database. Let's bring in the big guns with passlib.

If you do not have passlib already, which you likely do not since it is not part of the standard library, do a quick:
```py
pip install passlib
```
or...
```
`sudo apt-get install python-passlib`
```
Once you have passlib, let's play!
```py
from passlib.hash import sha256_crypt

password = sha256_crypt.encrypt("password") 
password2 = sha256_crypt.encrypt("password")  
print(password)  
print(password2)  
print(sha256_crypt.verify("password", password))  
```
Here we're bringing in passlib's hashing ability, and using SHA256 as the algorithm. SHA256 is inherently better than md5, but you're free to replace "md5" with "sha256" in our above examples to see the hash that is output still remains the same, just a bit longer.

Next, we show that we use the sha256_crypt from passlib to hash "password" twice. Once to the variable of password and once more to password2.

Then we output the hashes of both, noticing they are different.

Finally, we validate that the two separate hashes came from the same source.

Sure enough, the boolean rings True, and we have a match!

Now, we have a great way to protect user passwords, while still being able to validate the user when they login.

Now, consider the requirements of the hacker who breaches our server and gains access to both our source code and our database. They can see everything, but now what?

Now, they will have to crack passwords by brute force, the same as before, only now it is one measily password at a time. Yikes. What they can do is take their password-dictionary (usually a massive list of possible passwords), generate a hash, then attempt to validate this hash against all passwords in the database by iterating through each one and running the sha256_crypt.verify against them for the True/False response. This process, however, is exceptionally cumbersome, and the results are slow. This is going to take a long time, and there's no way to pre-prepare here. You might think, well cannot they prepare by generating the SHA256 hashes in advanced? Nope, because sha256_crypt also uses a unique salt.

At the time of my writing this, there are no known weaknesses to this  **method**.

Now, I would like to stress the use of "method" above. There exists a major difference between a method, and the application of the method.

Another adage for encryption and security in general goes something like:

"You can have the strongest, most impenetrable, reinforced door on the planet protecting a room, but that does no good if the walls are still weak."

It's really simple to forget about the walls, the ceiling, or even the ground.

Consider how many times you have written a program's logic, thought it was solid, then hit a bug and went "of course!" You're going to make mistakes constantly, and you probably know that you make them a lot. With security, these bugs often go unchecked, untested. Try your best to think like a hacker, but always remember that *every* system, connected to the world wide web, is hack-able. Just accept it, and work on that premise.

Accept that passlib might be flawed, and that, one day, or already, someone knows a flaw in SHA256. Also, plenty of password encryption systems are bypassed by hackers with server access extremely simply:

If a hacker gains access to your server, and finds that your database is encrypted securely, they can do something as simple as creating a logging function on your login form, where it just simply saves what the users typed into the field, before hashing, to a text file, or transmits the data elsewhere. This obviously isn't as great as getting the entire database at once, but this sort of thing happens.

A lot of people also put a lot of trust in things like 2FA (two factor authentication). I hate to burst your bubble, but, while this  **method**  makes a lot of sense, the application of this method by both you, the client, and the website you use matters greatly.

As a developer myself, I have set up 2FA a few times. There are many options you can select when installing 2FA that can increase, or hinder, security. One particular, very popular, bitcoin wallet website, for example, re-uses the public key for your 2FA. I discovered this when I changed phones. The result here is that someone could get access to your phone temporarily, get access to your account, revalidate 2FA, and you'd notice no change at all on your device. They are recycling the public keys that generate the code. Now they just wait for you to deposit a large sum, and then they take you. You'd never know you were even vulnerable. If the hackers could also fake your session cookie, this is another way they could do this, and they wouldn't even need your code. Faking sessions is pretty hard, but still possible. This is why websites usually require you to re-enter your password when making security changes on your account. This popular bitcoin wallet website? Nope, no need to re-enter your password.

Nice secure door, but weak walls.

Another great example of 2FA mistakes is when people use 2FA via something like Google. Great, but if the gmail account that you have your 2FA set up on with Google Authenicator is not also protected with 2FA, well you're screwed.

Great door, weak walls.

Finally, before leaving you feeling vulnerable, I will address the weakest point to all businesses and servers:

The people running them.

The weakest link is always the people. Whether it's because they make mistakes or it is because they can be easily social engineered, the people are usually the main target, or at least the reason for the vulnerabilities.

I cannot even count how many websites I have seen hacked, because someone posed as one of the admins, and was able to gain access. It sounds stupid, but this scam is easy to fall for, especially considering the world we live in today where developers are dispersed and usually not all local. I've personally been the victim of a successful version of this, I've had developers for the website be the hacker, and I've had endless attempts. That's what hackers do, they hack. They keep trying, and eventually they can get through. Your job is to just make it as challenging as possible.

It's like most crime. Most crimes are crimes of opportunity, your job is to not be the slowest, fattest, juiciest kid running from the bear.


> [Source: ](https://pythonprogramming.net/password-hashing-flask-tutorial/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxMDU1MzQ3OF19
-->