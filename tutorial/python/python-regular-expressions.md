---
bookFlatSection: true
title: Regular Expressions
bookToc: true
---

# Tutorial: Python Regex \(Regular Expressions\) for Data Scientists

![enter image description here](https://www.dataquest.io/wp-content/uploads/2017/11/books-regex2.jpg)

Diving headlong into data sets is a part of the mission for anyone working in data science. Often, this means number-crunching, but what do we do when our data set is primarily text-based? We can use regular expressions. In this tutorial, we’re going to take a closer look at how to use regular expressions \(regex\) in Python.

Regular expressions \(regex\) are essentially text patterns that you can use to automate searching through and replacing elements within strings of text. This can make cleaning and working with text-based data sets much easier, saving you the trouble of having to search through mountains of text by hand.

Regular expressions can be used across a variety of programming languages, and they’ve been around for [a very long time!](http://aishack.in/tutorials/artificial-neurons-mccullochpitts-model/)

In this tutorial, though, we’ll learning about regular expressions in Python, so basic familiarity with key Python concepts like if-else statements, while and for loops, etc., is required. \(If you need a refresher on any of this stuff, [our introductory Python courses](https://www.dataquest.io/path/data-scientist/) cover all of the relevant topics interactively, right in your browser, and they’re free!\)

By the end of the tutorial, you’ll be familiar with how Python regex works, and be able to use the basic patterns and functions in Python’s regex module, `re`, for to analyze text strings. You’ll also get an introduction to how regex can be used in concert with pandas to work with large text corpuses \(_corpus_ means a data set of text\).

\(To work through the pandas section of this tutorial, you will need to have the pandas library installed. The easiest way to do this is to download [Anaconda](https://docs.continuum.io/anaconda/) and work through this tutorial in a Jupyter notebook. For other options, check out the [pandas installation guide](http://pandas.pydata.org/pandas-docs/stable/install.html).\)

![spam-email-python-regex](https://www.dataquest.io/wp-content/uploads/2020/01/spam-email-python-regex-scaled.jpg)

Let's dig into some data about everyone's least favorite types of email: spam and scams.

## Our Task: Analyze Spam Emails

In this tutorial, we’ll use the Fraudulent Email Corpus from Kaggle. It contains thousands of phishing emails sent between 1998 and 2007. They’re pretty entertaining to read.

You can find the full corpus [here](https://www.kaggle.com/rtatman/fraudulent-email-corpus). But we’ll start by learning basic regex commands using a few emails. If you’d like, you can use our [test file](https://www.dataquest.io/wp-content/uploads/2020/01/test_emails.txt) as well, or you can try this with the full corpus.

## Introducing Python’s Regex Module

First, we’ll prepare the data set by opening the test file, setting it to read-only, and reading it. We’ll also assign it to a variable, `fh` \(for “file handle”\).

```python
fh = open(r"test_emails.txt", "r").read()
```

Notice that we precede the directory path with an `r`. This technique converts a string into a raw string, which helps to avoid conflicts caused by how some machines read characters, such as backslashes in directory paths on Windows.

Now, suppose we want to find out who the emails are from. We could try raw Python on its own:

```python
for line in fh.split("n"):
    if "From:" in line:
        print(line)
```

```text
der.com>
Message-Id: <200210311310.g9VDANt24674@bloodwork.mr.itd.UM>
From: "Mr. Be
g_715@epatra.com>
Message-Id: <200210312227.g9VMQvDj017948@bluewhale.cs.CU>
From: "PRINCE OBONG ELEME" <obo
```

But that’s not giving us exactly what we want. If you take a look at our test file, we could figure out why and fix it, but instead, let’s use Python’s `re` module and do it with regular expressions!

We’ll start by importing Python’s `re` module. Then, we’ll use a function called `re.findall()` that returns a list of all instances of a pattern we define in the string we’re looking at.

Here’s how it looks:

```python
import re

for line in re.findall("From:.*", fh):
    print(line)
```

```text
From: "Mr. Ben Suleman" <bensul2004nng@spinfinder.com>
From: "PRINCE OBONG ELEME" <obong_715@epatra.com>
```

This is essentially the same length as our raw Python, but that’s because it’s a very simple example. The more you’re trying to do, the more effort Python regex is likely to save you.

Before we move on, let’s take a closer look at `re.findall()`. This function takes two arguments in the form of `re.findall(pattern, string)`. Here, `pattern` represents the substring we want to find, and `string` represents the main string we want to find it in. The main string can consist of multiple lines. In this case, we’re having it search through all of `fh`, the file with our selected emails.

The `.*` is a shorthand for a string pattern. Regular expressions work by using these shorthand patterns to find specific patterns in text, so let’s take a look at some other common examples:

## Common Python Regex Patterns

The pattern we used with `re.findall()` above contains a fully spelled-out out string, `"From:"`. This is useful when we know precisely what we’re looking for, right down to the actual letters and whether or not they’re upper or lower case. If we don’t know the exact format of the strings we want, we’d be lost. Fortunately, regex has basic patterns that account for this scenario. Let’s look at the ones we use in this tutorial:

* `w`  matches alphanumeric characters, which means a-z, A-Z, and 0-9. It also matches the underscore, \_, and the dash, -.
* `d`  matches digits, which means 0-9.
* `s`  matches whitespace characters, which include the tab, new line, carriage return, and space characters.
* `S`  matches non-whitespace characters.
* `.`  matches any character except the new line character  `n`.

With these regex patterns in hand, you’ll quickly understand our code above as we go on to explain it.

## Working with Regex Patterns

We can now explain the use of `.*` in the line `re.findall("From:.*", text)` above. Let’s look at `.` first:

```python
for line in re.findall("From:.", fh):
    print(line)
```

```text
From:
From:
```

By adding a `.` next to `From:`, we look for one additional character next to it. Because `.` looks for any character except `n`, it captures the space character, which we cannot see. We can try more dots to verify this.

```python
for line in re.findall("From:...........", fh):
    print(line)
```

```text
From: "Mr. Ben S
From: "PRINCE OB
```

It looks like adding dots does acquire the rest of the line for us. But, it’s tedious and we don’t know how many dots to add. This is where the asterisk symbol, `*`, comes in.

`*` matches zero or more instances of a pattern on its left. This means it looks for repeating patterns. When we look for repeating patterns, we say that our search is “greedy.” If we don’t look for repeating patterns, we can call our search “non-greedy” or “lazy.”

Let’s construct a greedy search for `.` with `*`.

```python
for line in re.findall("From:.*", fh):
    print(line)
```

```text
From: "Mr. Ben Suleman" <bensul2004nng@spinfinder.com>
From: "PRINCE OBONG ELEME" <obong_715@epatra.com>
```

Because `*` matches zero or more instances of the pattern indicated on its left, and `.` is on its left here, we are able to acquire all the characters in the `From:` field until the end of the line. This prints out the full line with beautifully succinct code.

We might even go further and isolate only the name. Let’s use `re.findall()` to return a list of lines containing the pattern `"From:.*"` as we’ve done before. We’ll assign it to the variable `match` for neatness. Next, we’ll iterate through the list. In each cycle, we’ll execute `re.findall` again, matching the first quotation mark to pick out just the name:

```python
match = re.findall("From:.*", fh)

for line in match:
    print(re.findall('\".*\"', line))
```

```text
['"Mr. Ben Suleman"']
['"PRINCE OBONG ELEME"']
```

Notice that we use a backslash next to the first quotation mark. The backslash is a special character used for escaping other special characters. For instance, when we want to use a quotation mark as a string literal instead of a special character, we escape it with a backslash like this: `\"`. If we do not escape the pattern above with backslashes, it would become `"".*""`, which the Python interpreter would read as a period and an asterisk between two empty strings. It would produce an error and break the script. Hence, it’s crucial that we escape the quotation marks here with backslashes.

After the first quotation mark is matched, `.*` acquires all the characters in the line until the next quotation mark, also escaped in the pattern. This gets us just the name, within quotation marks. The name is also printed within square brackets because `re.findall` returns matches in a list.

What if we want the email address instead?

```python
match = re.findall("From:.*", fh)

for line in match:
    print(re.findall("\w\S*@*.\w", line))
```

```text
['bensul2004nng@spinfinder.com']
['obong_715@epatra.com']
```

Looks simple enough, doesn’t it? Only the pattern is different. Let’s walk through it.

Here’s how we match just the front part of the email address:

```python
for line in match:
    print(re.findall("\w\S*@", line))
```

```text
['bensul2004nng@']
['obong_715@']
```

Emails always contain an @ symbol, so we start with it. The part of the email before the @ symbol might contain alphanumeric characters, which means `w` is required. However, because some emails contain a period or a dash, that’s not enough. We add `S` to look for non-whitespace characters. But, `w\S` will get only two characters. Add `*` to look for repetitions. The front part of the pattern thus looks like this: `\w\S*@`.

Now for the pattern behind the @ symbol:

```python
for line in match:
    print(re.findall("@.*", line))
```

```text
['@spinfinder.com>']
['@epatra.com>']
```

The domain name usually contains alphanumeric characters, periods, and a dash sometimes, so a `.` will do. To make it greedy, we extend the search with a `*`. This allows us to match any character till the end of the line.

If we look at the line closely, we see that each email is encapsulated within angle brackets, &lt; and &gt;. Our pattern, `.*`, includes the closing bracket, &gt;. Let’s remedy it:

```python
for line in match:
    print(re.findall("@.*\w", line))
```

```text
['@spinfinder.com']
['@epatra.com']
```

Email addresses end with an alphanumeric character, so we cap the pattern with `w`. So, after the @ symbol we have `.*\w`, which means that the pattern we want is a group of any type of characters ending with an alphanumeric character. This excludes &gt;.

Our full email address pattern thus looks like this: `\w\S*@.*\w`.

Phew! That was quite a bit to work through. Next, we’ll run through some common `re` functions that will be useful when we start reorganizing our corpus.

## Common Python Regex Functions

`re.findall()` is undeniably useful, but it’s not the only built-in function that’s available to us in `re`:

* `re.search()`
* `re.split()`
* `re.sub()`

Let’s look at these one by one before using them to bring some order to our data set.

### re.search\(\)

While `re.findall()` matches all instances of a pattern in a string and returns them in a list, `re.search()` matches the first instance of a pattern in a string, and returns it as a `re` match object.

```python
match = re.search("From:.*", fh)
print(type(match))
print(type(match.group()))
print(match)
print(match.group())
```

```text
<class 're.Match'>
<class 'str'>
<re.Match object; span=(3590, 3644), match='From: "Mr. Ben Suleman" <bensul2004nng@spinfinder>
From: "Mr. Ben Suleman" <bensul2004nng@spinfinder.com>
```

Like `re.findall()`, `re.search()` also takes two arguments. The first is the pattern to match, and the second is the string to find it in. Here, we’ve assigned the results to the `match` variable for neatness.

Because `re.search()` returns a `re` match object, we can’t display the name and email address by printing it directly. Instead, we have to apply the `group()` function to it first. We’ve printed both their types out in the code above. As we can see, `group()` converts the match object into a string.

We can also see that printing `match` displays properties beyond the string itself, whereas printing `match.group()` displays only the string.

### re.split\(\)

Suppose we need a quick way to get the domain name of the email addresses. We could do it with three regex operations, like so:

```python
address = re.findall("From:.*", fh)
for item in address:
    for line in re.findall("\w\S*@.*\w", item):
        username, domain_name = re.split("@", line)
        print("{}, {}".format(username, domain_name))
```

```text
bensul2004nng, spinfinder.com
obong_715, epatra.com
```

The first line is familiar. We return a list of strings, each containing the contents of the `From:` field, and assign it to a variable. Next, we iterate through the list to find the email addresses. At the same time, we iterate through the email addresses and use the `re` module’s `split()` function to snip each address in half, with the @ symbol as the delimiter. Finally, we print it.

### re.sub\(\)

Another handy `re` function is `re.sub()`. As the function name suggests, it substitutes parts of a string. An example:

```python
sender = re.search("From:.*", fh)
address = sender.group()
email = re.sub("From", "Email", address)
print(address)
print(email)
```

```text
From: "Mr. Ben Suleman"
```

> [Source : ](https://www.dataquest.io/blog/regular-expressions-data-scientists/).

