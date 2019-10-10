Password Hashing with Flask Tutorial
===
<iframe width="622" height="350" src="https://www.youtube.com/embed/UtF58KqcHWU?list=PLQVvvaa0QuDc_owjTbIY4rbgXOFkUYOUB" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

While we have already incorporated the password hashing into our registration page, I wanted to take some time to go over what is actually happening. Maybe you end up working in another language, or maybe passlib doesn't support the version of Python you are using in the future. Because of this, you should know at least at a high level, how it works.

Not only is it important for security practices, it's also just pretty cool how it works!
To begin, you can probably understand why it is important to encrypt passwords to begin with. If your database stores plain-text passwords, at the very least, you are going to see the passwords yourself, and so will anyone who has access to your server. In a perfect world, no one would invade a user's privacy, but this world is not perfect. Not only might someone who works for you steal user passwords, a hacker might, or even the host to your server might, if you are using a virtual private server, or shared hosting.

So then how might we obscure passwords? Obscuring original text is easy enough, we can right a randomized algorithm that does this. The problem is, with passwords, we actually need to be able to validate what a user enters in the future as the original password.

One of the more primitive measures taken was simple password hashing. This was where a hash function was applied to what the user input, and that hash was what was stored as a password.

Here's a simple hashing script to illustrate this, which you can run:






> [Source: ](https://pythonprogramming.net/password-hashing-flask-tutorial/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzEyMDE5NDQ3XX0=
-->