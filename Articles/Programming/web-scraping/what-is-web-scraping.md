
What Is Web Scraping?
===

![What Is Web Scraping?](https://i2.wp.com/therenegadecoder.com/wp-content/uploads/2019/09/what-is-web-scraping-featured-image.jpeg?fit=800%2C500&ssl=1)

Last Updated on  January 8, 2020

Jeremy here! Once again, I decided to share this space with the kind people of Kite. This time,  [they’ve brought you an article by Zac Clancy on web scraping](https://kite.com/blog/python/what-is-web-scraping/). Check it out!

If you are enjoying these guest posts, let me know! I’ll be happy to work with Kite and other sources to get more. For instance,  [here’s an article on Data Science by Kirit Thadaka](https://therenegadecoder.com/code/data-science-the-good-the-bad-and-the-future/).

## Table of Contents

-   [Table of Contents](https://therenegadecoder.com/code/what-is-web-scraping/#table-of-contents "Table of Contents")
-   [Introducing Web Scraping](https://therenegadecoder.com/code/what-is-web-scraping/#introducing-web-scraping "Introducing Web Scraping")
-   [Some Use Cases of Web Scraping](https://therenegadecoder.com/code/what-is-web-scraping/#some-use-cases-of-web-scraping "Some Use Cases of Web Scraping")
-   [So How Does It Work?](https://therenegadecoder.com/code/what-is-web-scraping/#so-how-does-it-work "So How Does It Work?")
-   [Robots.txt](https://therenegadecoder.com/code/what-is-web-scraping/#robotstxt "Robots.txt")
-   [A Simple Example](https://therenegadecoder.com/code/what-is-web-scraping/#a-simple-example "A Simple Example")
-   [Working with HTML](https://therenegadecoder.com/code/what-is-web-scraping/#working-with-html "Working with HTML")
-   [Data Processing](https://therenegadecoder.com/code/what-is-web-scraping/#data-processing "Data Processing")
-   [Next steps](https://therenegadecoder.com/code/what-is-web-scraping/#next-steps "Next steps")

## Introducing Web Scraping

Simply put, web scraping is one of the tools developers use to gather and analyze information from the Internet.

Some websites and platforms offer application programming interfaces (APIs) which we can use to access information in a structured way, but others might not. While APIs are certainly becoming the standard way of interacting with today’s popular platforms, we don’t always have this luxury when interacting with most of the websites on the internet.

Rather than reading data from standard API responses, we’ll need to find the data ourselves by reading the website’s pages and feeds.

## Some Use Cases of Web Scraping

The World Wide Web was born in 1989 and web scraping and crawling entered the conversation not long after in 1993.

Before scraping, search engines were compiled lists of links collected by the website administrator, and arranged into a long list of links somewhere on their website. The first web scraper and crawler, the  _World Wide Web Wanderer_, were created to follow all these indexes and links to try and determine how big the internet was.

It wasn’t long after this that developers started using crawlers and scrapers to create  _crawler-based search engines_  that didn’t require human assistance. These crawlers would simply follow links that would come across each page and save information about the page. Since the web is a collaborative effort, the crawler could easily and infinitely follow embedded links on websites to other platforms, and the process would continue forever.

Nowadays, web scraping has its place in nearly every industry. In newsrooms, web scrapers are used to pull in information and trends from thousands of different internet platforms in real time.

Spending a little too much on Amazon this month? Websites exist that will let you know, and, in most cases, will do so by using web scraping to access that specific information on your behalf.

Machine learning and artificial intelligence companies are scraping  **billions**  of social media posts to better learn how we communicate online.

## So How Does It Work?

The process a developer builds for web scraping looks a lot like the process a user takes with a browser:

A URL is given to the program.

1.  The program downloads the response from the URL.
2.  The program processes the downloaded file depending on data required.
3.  The program starts over at with a new URL
4.  The nitty gritty comes in steps 3 and, in which data is processed and the

program determines how to continue (or if it should at all). For Google’s crawlers, step 3 likely includes collecting all URL links on the page so that the web scraper has a list of places to begin checking next. This is recursiveby design and allows Google to efficiently follow paths and discover new content.

There are many heavily used, well built libraries for reading and working with the downloaded HTML response. In the Ruby ecosystem  [Nokogiri](https://nokogiri.org/)  is the standard for parsing HTML. For Python,  [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/)  has been the standard for 15 years. These libraries provide simple ways for us to interact with the HTML from our own programs.

These code libraries will accept the page source as text, and a parser for handling the content of the text. They’ll return helper functions and attributes which we can use to navigate through our HTML structure in predictable ways and find the values we’re looking to extract.

Scraping projects involve a good amount of time spent analyzing a web site’s HTML for classes or identifiers, which we can use to find information on the page. Using the HTML below we can begin to imagine a strategy to extract product information from the table below using the HTML elements with the classes  `products`  and  `product`.
```html
<table class="products">
  <tr class="product">...</tr>
  <tr class="product">...</tr>
</table>
```
In the wild, HTML isn’t always as pretty and predictable. Part of the web scraping process is learning about your data and where it lives on the pages as you go along. Some websites go to great lengths to prevent web scraping, some aren’t built with scraping in mind, and others just have complicated user interfaces which our crawlers will need to navigate through.

## Robots.txt

While not an enforced standard, it’s been common since the early days of web scraping to check for the existence and contents of a robots.txt file on each site before scraping its content. This file can be used to define inclusion and exclusion rules that web scrapers and crawlers should follow while crawling the site. You can check out  [Facebook’s robots.txt](https://facebook.com/robots.txt)  file for a robust example: this file is always located at /robots.txt so that scrapers and crawlers can always look for it in the same spot. Additionally,  [GitHub’s robots.txt](https://github.com/robots.txt), and  [Twitter’s](https://twitter.com/robots.txt)  are good examples.

An example robots.txt file prohibits web scraping and crawling would look like the below:

User-agent: *
Disallow: /

The  `User-agent: *`  section is for all web scrapers and crawlers. In Facebook’s, we see that they set  `User-agent`  to be more explicit and have sections for  _Googlebot_,  _Applebot_, and others.

The  `Disallow: /`  line informs web scrapers and crawlers who observe the robots.txt file that they aren’t permitted to visit any pages on this site. Conversely, if this line read  `Allow: /`, web scrapers and crawlers would be allowed to visit any page on the website.

The robots.txt file can also be a good place to learn information about the website’s architecture and structure. Reading where our scraping tools are allowed to go – and not allowed to go – can help inform us on sections of the website we perhaps didn’t know existed, or may not have thought to look at.

If you’re running a website or platform it’s important to know that this file isn’t always respected by  **every**  web crawler and scraper. Larger properties like Google, Facebook, and Twitter respect these guidelines with their crawlers and information scrapers, but since robots.txt is considered a best practice rather than an enforceable standard, you may see different results from different parties. It’s also important not to disclose private information which you wouldn’t want to become public knowledge, like an admin panel on  `/admin`  or something like that.

## A Simple Example

To illustrate this, we’ll use Python plus the  `BeautifulSoup`  and  [Requests](https://2.python-requests.org//en/master/)  libraries.
```py
1.  import requests
2.  from bs4 import  BeautifulSoup

4.  page = requests.get('https://google.com')
5.  soup = BeautifulSoup(page.text, 'html.parser')
```
We’ll go through this line-by-line:
```py
page = requests.get('https://google.com')
```
This uses the  `requests`  library to make a request to  `https://google.com`  and return the response.
```py
soup = BeautifulSoup(page.text, 'html.parser')
```
The  `requests`  library assigns the text of our response to an attribute called  `text`  which we use to give  `BeautifulSoup`  our HTML content. We also tell  `BeautifulSoup`  to use Python 3’s built-in HTML parser  `html.parser`.

Now that  `BeautifulSoup`  has parsed our HTML text into an object that we can interact with, we can begin to see how information may be extracted.
```py
paragraphs = soup.find_all('p')
```
Using  `find_all`  we can tell  `BeautifulSoup`  to only return HTML paragraphs  `<p>`  from the document.

If we were looking for a div with a specific ID (`#content`) in the HTML we could do that in a few different ways:
```py
1.  element = soup.select('#content')
2.  # or
3.  element = soup.find_all('div', id='content')
4.  # or
5.  element = soup.find(id='content')
```
In the Google scenario from above, we can imagine that they have a function that does something similar to grab all the links off of the page for further processing:
```py
links = soup.find_all('a', href=True)
```
The above snippet will return all of the  `<a>`  elements from the HTML which are acting as links to other pages or websites. Most large-scale web scraping implementations will use a function like this to capture local links on the page, outbound links off the page, and then determine some priority for the links’ further processing.

## Working with HTML

The most difficult aspect of web scraping is analyzing and learning the underlying HTML of the sites you’ll be scraping. If an HTML element has a consistent ID or set of classes, then we should be able to work with it fairly easily, we can just select it using our HTML parsing library (Nokogiri,  `BeautifulSoup`, etc). If the element on the page  _doesn’t have consistent classes or identifiers_, we’ll need to access it using a different selector.

Imagine our HTML page contains the following table which we’d like to extract product information from:

|NAME	|CATEGORY|	PRICE|
|-------|--------|------|
|Shirt	|Athletic|	$19.99|
|Jacket	|Outdoor|	$124.99|

`BeautifulSoup`  allows us to parse tables and other complex elements fairly simply. Let’s look at how we’d read the table’s rows in Python:
```py
1.  # Find all the HTML tables on the page
2.  tables = soup.find_all('table')

4.  # Loop through all of the tables
5.  for table in tables:
6.  # Access the table's body
7.  table_body = table.find('tbody')
8.  # Grab the rows from the table body
9.  rows = table_body.find_all('tr')

11.  # Loop through the rows
12.  for row in rows:
13.  # Extract each HTML column from the row
14.  columns = row.find_all('td')

16.  # Loop through the columns
17.  for column in columns:
18.  # Print the column value
19.  print(column.text)
```
The above code snippet would print  `Shirt`, followed by  `Athletic`, and then  `$19.99`  before continuing on to the next table row. While simple, this example illustrates one of the many strategies a developer might take for retrieving data from different HTML elements on a page.

## Data Processing

Researching and inspecting the websites you’ll be scraping for data is a crucial component to each project. We’ll generally have a model that we’re trying to fill with data for each page. If we were scraping restaurant websites we’d probably want to make sure we’re collecting the name, address, and the hours of operation at least, with other fields being added as we’re able to find the information. You’ll begin to notice that some websites are much easier to scrape for data than others – some are even defensive against it!

Once you’ve got your data in hand there are a number of different options for handling, presenting, and accessing that data. In many cases you’ll probably want to handle the data yourself, but there’s a slew of services offered for many use cases by various platforms and companies.

-   **Search indexing**: Looking to store the text contents of websites and easily search?  [Algolia](https://www.algolia.com/)  and  [Elasticsearch](https://github.com/elastic/elasticsearch)  are good for that.
-   **Text analysis**: Want to extract people, places, money and other entities from the text? Maybe  [spaCy](https://spacy.io/)  or  [Google’s Natural Language API](https://cloud.google.com/natural-language/)  are for you.
-   **Maps and location data**: If you’ve collected some addresses or landmarks, you can use  [OpenStreetMap](https://www.openstreetmap.org/)  or  [MapBox](https://www.mapbox.com/)  to bring that location data to life.
-   **Push notifications**: If you want to get a text message when your web crawler finds a specific result, check out  [Twilio](https://www.twilio.com/sms)  or  [Pusher](https://pusher.com/beams).

## Next steps

In this post, we learned about the basics of web scraping and looked at some simplistic crawling examples which helped demonstrate how we can interact with HTML pages from our own code. Ruby’s Nokogiri, Python’s  `BeautifulSoup`, and JavaScript’s  [Nightmare](http://www.nightmarejs.org/)  are powerful tools to begin learning web scraping with. These libraries are relatively simple to start with, but offer powerful interfaces to begin to extend in more advanced use cases.

Moving forward from this post, try to create a simple web scraper of your own! You could potentially write a simple script that reads a tweet from a URL and prints the tweet text into your terminal. With some practice, you’ll be analyzing HTML on all the websites you visit, learning its structure, and understanding how you’d navigate its elements with a web scraper.


> [Source : ](https://therenegadecoder.com/code/what-is-web-scraping/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE1NDM3MjczXX0=
-->