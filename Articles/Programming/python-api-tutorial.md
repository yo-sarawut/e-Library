Python API Tutorial: Getting Started with APIs
==

![enter image description here](https://www.dataquest.io/wp-content/uploads/2015/09/iss056e201262.jpg)

In this Python API tutorial, we’ll learn how to retrieve data for data science projects. There are millions of APIs online which provide access to data. Websites like  [Reddit](https://www.reddit.com/dev/api/),  [Twitter](https://developer.twitter.com/en/docs.html), and  [Facebook](https://developers.facebook.com/)  all offer certain data through their APIs.

To use an API, you make a request to a remote web server, and retrieve the data you need.

But why use an API instead of a static CSV dataset you can download from the web? APIs are useful in the following cases:

-   **The data is changing quickly**. An example of this is stock price data. It doesn’t really make sense to regenerate a dataset and download it every minute — this will take a lot of bandwidth, and be pretty slow.
-   **You want a small piece of a much larger set of data**. Reddit comments are one example. What if you want to just pull your own comments on Reddit? It doesn’t make much sense to download the entire Reddit database, then filter just your own comments.
-   **There is repeated computation involved**. Spotify has an API that can tell you the genre of a piece of music. You could theoretically create your own classifier, and use it to compute music categories, but you’ll never have as much data as Spotify does.

In cases like the ones above, an API is the right solution. In this blog post, we’ll be querying a simple API to retrieve data about the  [International Space Station](https://en.wikipedia.org/wiki/International_Space_Station)  (ISS).

## About this Python API Tutorial[](https://www.dataquest.io/blog/python-api-tutorial/#About-this-Python-API-Tutorial)  

This tutorial is based on part of our interactive course on APIs and Webscraping in Python, which you can  [start for free](https://www.dataquest.io/course/apis-and-scraping/).

For this tutorial, we assume that you know some of the fundamentals of working with data in Python. If you don’t, you might like to try our  [free Python Fundamentals course](https://www.dataquest.io/course/python-for-data-science-fundamentals/).

## What is an API?[](https://www.dataquest.io/blog/python-api-tutorial/#What-is-an-API?)  

An API, or Application Programming Interface, is a server that you can use to retrieve and send data to using code. APIs are most commonly used to retrieve data, and that will be the focus of this beginner tutorial.

When we want to receive data from an API, we need to make a  **request**. Requests are used all over the web. For instance, when you visited this blog post, your web browser made a request to the Dataquest web server, which responded with the content of this web page

![python api tutorial - page requests](https://www.dataquest.io/wp-content/uploads/2019/09/page-request.svg)

API requests work in exactly the same way – you make a request to an API server for data, and it responds to your request.

## Making API Requests in Python[](https://www.dataquest.io/blog/python-api-tutorial/#Making-API-Requests-in-Python)  

In order to work with APIs in Python, we need tools that will make those requests. In Python, the most common library for making requests and working with APIs is the  [**requests**  library](https://2.python-requests.org/en/master/). The requests library isn’t part of the standard Python library, so you’ll need to install it to get started.

If you use pip to manage your Python packages, you can install requests using the following command:

```py
pip install requests
```

If you use conda, the command you’ll need is:

```py
conda install requests
```

Once you’ve installed the library, you’ll need to import it. Let’s start with that important step:

```python
import requests
```

Now that we’ve installed and imported the requests library, let’s start using it.

## Making Our First API Request[](https://www.dataquest.io/blog/python-api-tutorial/#Making-Our-First-API-Request)  

There are many different types of requests. The most commonly used one, a  **GET**  request, is used to retrieve data. Because we’ll just be working with retrieving data, our focus will be on making ‘get’ requests.

When we make a request, the response from the API comes with a  **response code**  which tells us whether our request was successful. Response codes are important because they immediately tell us if something went wrong.

![](https://www.dataquest.io/wp-content/uploads/2019/09/api-request.svg)

To make a ‘GET’ request, we’ll use the  [`requests.get()`  function](https://2.python-requests.org/en/master/user/quickstart/#make-a-request), which requires one argument — the URL we want to make the request to. We’ll start by making a request to an API endpoint that doesn’t exist, so we can see what that response code looks like.

```python
response = requests.get("http://api.open-notify.org/this-api-doesnt-exist")
```

The  `get()`  function returns a  [`response`  object](https://2.python-requests.org/en/master/user/advanced/#request-and-response-objects). We can use the  [`response.status_code`](https://2.python-requests.org/en/master/user/quickstart/#response-status-codes)  attribute to receive the status code for our request:

```python
print(response.status_code)
```

```vim
404
```

The ‘404’ status code might be familiar to you — it’s the status code that a server returns if it can’t find the file we requested. In this case, we asked for  `this-api-doesnt-exist`  which (surprise, surprise) didn’t exist!

Let’s learn a little more about common status codes.

## API Status Codes[](https://www.dataquest.io/blog/python-api-tutorial/#API-Status-Codes)  

Status codes are returned with every request that is made to a web server. Status codes indicate information about what happened with a request. Here are some codes that are relevant to  _GET_  requests:

-   `200`: Everything went okay, and the result has been returned (if any).
-   `301`: The server is redirecting you to a different endpoint. This can happen when a company switches domain names, or an endpoint name is changed.
-   `400`: The server thinks you made a bad request. This can happen when you don’t send along the right data, among other things.
-   `401`: The server thinks you’re not authenticated. Many APIs require login ccredentials, so this happens when you don’t send the right credentials to access an API.
-   `403`: The resource you’re trying to access is forbidden: you don’t have the right permissions to see it.
-   `404`: The resource you tried to access wasn’t found on the server.
-   `503`: The server is not ready to handle the request.

You might notice that all of the status codes that begin with a ‘4’ indicate some sort of error. The first number of status codes indicate their categorization. This is useful — you can know that if your status code starts with a ‘2’ it was successful and if it starts with a ‘4’ or ‘5’ there was an error. If you’re interested you can  [read more about status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

## API Documentation[](https://www.dataquest.io/blog/python-api-tutorial/#API-Documentation)  

In order to ensure we make a succesful request, when we work with APIs it’s important to consult the documentation. Documentation can seem scary at first, but as you use documentation more and more you’ll find it gets easier.

We’ll be working with the  [Open Notify](http://open-notify.org/)  API, which gives access to data about the international space station. It’s a great API for learning because it has a very simple design, and doesn’t require authentication. We’ll teach you how to use an API that requires authentication in a later post.

Often there will be multiple APIs available on a particular server. Each of these APIs are commonly called  **endpoints**. The first endpoint we’ll use is  [`http://api.open-notify.org/astros.json`](http://open-notify.org/Open-Notify-API/People-In-Space/), which returns data about astronauts currently in space.

If you click the link above to look at the documentation for this endpoint, you’ll see that it says  _This API takes no inputs._  This makes it a simple API for us to get started with. We’ll start by making a GET request to the endpoint using the requests library:

```python
response = requests.get("http://api.open-notify.org/astros.json")
print(response.status_code)
```

```vim
200
```

We received a ‘200’ code which tells us our request was successful. The documentation tells us that the API response we’ll get is in JSON format. In the next section we’ll learn about JSON, but first let’s use the  [`response.json()`  method](https://2.python-requests.org/en/master/user/quickstart/#json-response-content)  to see the data we received back from the API:

```python
print(response.json())
```

```vim
{'message': 'success', 'people': [{'name': 'Alexey Ovchinin', 'craft': 'ISS'}, {'name': 'Nick Hague', 'craft': 'ISS'}, {'name': 'Christina Koch', 'craft': 'ISS'}, {'name': 'Alexander Skvortsov', 'craft': 'ISS'}, {'name': 'Luca Parmitano', 'craft': 'ISS'}, {'name': 'Andrew Morgan', 'craft': 'ISS'}], 'number': 6}
```

## Working with JSON Data in Python[](https://www.dataquest.io/blog/python-api-tutorial/#Working-with-JSON-Data-in-Python)  

[JSON](http://json.org/)  (JavaScript Object Notation) is the language of APIs. JSON is a way to encode data structures that ensures that they are easily readable by machines. JSON is the primary format in which data is passed back and forth to APIs, and most API servers will send their responses in JSON format.

You might have noticed that the JSON output we received from the API looked like it contained Python dictionaries, lists, strings and integers. You can think of JSON as being a combination of these objects represented as strings. Let’s look at a simple example:

![](https://www.dataquest.io/wp-content/uploads/2019/09/json.svg)

Python has great JSON support with the  [`json`  package](https://docs.python.org/3/library/json.html). The  `json`  package is part of the standard library, so we don’t have to install anything to use it. We can both convert  _lists_  and  _dictionaries_  to JSON, and convert strings to  _lists_  and  _dictionaries_. In the case of our ISS Pass data, it is a dictionary encoded to a string in JSON format.

The json library has two main functions:

-   [`json.dumps()`](https://docs.python.org/3/library/json.html#json.dumps)  — Takes in a Python object, and converts (dumps) it to a string.
-   [`json.loads()`](https://docs.python.org/3/library/json.html#json.loads)  — Takes a JSON string, and converts (loads) it to a Python object.

The  `dumps()`  function is particularly useful as we can use it to print a formatted string which makes it easier to understand the JSON output, like in the diagram we saw above:

```python
import json

def jprint(obj):
    # create a formatted string of the Python JSON object
    text = json.dumps(obj, sort_keys=True, indent=4)
    print(text)

jprint(response.json())
```

```vim
{
    "message": "success",
    "number": 6,
    "people": [
        {
            "craft": "ISS",
            "name": "Alexey Ovchinin"
        },
        {
            "craft": "ISS",
            "name": "Nick Hague"
        },
        {
            "craft": "ISS",
            "name": "Christina Koch"
        },
        {
            "craft": "ISS",
            "name": "Alexander Skvortsov"
        },
        {
            "craft": "ISS",
            "name": "Luca Parmitano"
        },
        {
            "craft": "ISS",
            "name": "Andrew Morgan"
        }
    ]
}
```

Immediately we can understand the structure of the data more easily – we can see that their are six people currently in space, with their names existing as dictionaries inside a list.

If we compare this to  [the documentation for the endpoint](http://open-notify.org/Open-Notify-API/People-In-Space/#json)  we’ll see that this matches the specified output for the endpoint.

## Using an API with Query Parameters[](https://www.dataquest.io/blog/python-api-tutorial/#Using-an-API-with-Query-Parameters)  

The  `http://api.open-notify.org/astros.json`  endpoint we used earlier does not take any parameters. We just send a GET request and the API sends back data about the number of people currently in space.

It’s very common, however, to have an API endpoint that requires us to specify parameters. An example of this the  [`http://api.open-notify.org/iss-pass.json`  endpoint](http://open-notify.org/Open-Notify-API/ISS-Pass-Times/). This endpoint tells us the next times that the international space station will pass over a given location on the earth.

If we look at the documentation, it specifies required  `lat`  (latitude) and  `long`  (longitude) parameters.

We can do this by adding an optional keyword argument,  `params`, to our request. We can make a dictionary with these parameters, and then pass them into the  `requests.get`  function. Here’s what our dictionary would look like, using coordinates for New York City:

```python
parameters = {
    "lat": 40.71,
    "lon": -74
}
```

We can also do the same thing directly by adding the parameters directly to the URL. like this:  `http://api.open-notify.org/iss-pass.json?lat=40.71&lon=-74`.

It’s almost always preferable to setup the parameters as a dictionary, because  `requests`  takes care of some things that come up, like properly formatting the query parameters, and we don’t need to worry about inserting the values into the URL string.

Let’s make a request using these coordinates and see what response we get.

```python
response = requests.get("http://api.open-notify.org/iss-pass.json", params=parameters)

jprint(response.json())
```

```vim
{
    "message": "success",
    "request": {
        "altitude": 100,
        "datetime": 1568062811,
        "latitude": 40.71,
        "longitude": -74.0,
        "passes": 5
    },
    "response": [
        {
            "duration": 395,
            "risetime": 1568082479
        },
        {
            "duration": 640,
            "risetime": 1568088118
        },
        {
            "duration": 614,
            "risetime": 1568093944
        },
        {
            "duration": 555,
            "risetime": 1568099831
        },
        {
            "duration": 595,
            "risetime": 1568105674
        }
    ]
}
```

## Understanding the Pass Times[](https://www.dataquest.io/blog/python-api-tutorial/#Understanding-the-Pass-Times)  

The JSON response matches what the documentation specified:

-   A dictionary with three keys
-   The third key,  `response`, contains a list of pass times
-   Each pass time is a dictionary with  `risetime`  (pass start time) and  `duration`  keys.

Let’s extract the pass times from our JSON object:

```python
pass_times = response.json()['response']
jprint(pass_times)
```

```vim
[
    {
        "duration": 395,
        "risetime": 1568082479
    },
    {
        "duration": 640,
        "risetime": 1568088118
    },
    {
        "duration": 614,
        "risetime": 1568093944
    },
    {
        "duration": 555,
        "risetime": 1568099831
    },
    {
        "duration": 595,
        "risetime": 1568105674
    }
]
```

Next we’ll usea loop to extract just the five  `risetime`  values:

```python
risetimes = []

for d in pass_times:
    time = d['risetime']
    risetimes.append(time)

print(risetimes)
```

```vim
[1568082479, 1568088118, 1568093944, 1568099831, 1568105674]
```

These times are difficult to understand – they are in a format known as timestamp or  [epoch](https://en.wikipedia.org/wiki/Unix_time). Essentially the time is measured in the number of seconds since January 1st 1970. We can use the Python  [`datetime.fromtimestamp()`  method](https://docs.python.org/3/library/datetime.html#datetime.date.fromtimestamp)  to convert these into easier to understand times:

```python
from datetime import datetime

times = []

for rt in risetimes:
    time = datetime.fromtimestamp(rt)
    times.append(time)
    print(time)
```

```vim
2019-09-09 21:27:59
2019-09-09 23:01:58
2019-09-10 00:39:04
2019-09-10 02:17:11
2019-09-10 03:54:34
```

It looks like the ISS passes over New York City often – the next five times happen within a seven hour period!

## Python API Tutorial: Next Steps[](https://www.dataquest.io/blog/python-api-tutorial/#Python-API-Tutorial:-Next-Steps)  

In this tutorial, we learned:

-   What an API is
-   Types of requests and response codes
-   How to make a get request
-   How to make a request with parameters
-   How to display and extract JSON data from an API

These fundamental steps will help you to start working with APIs. Remember that key to each time we used the API was to carefully read the API documentation and use that to understand what request to make and what parameters to provide.

Now you’ve completed our Python API tutorial, you might like to:

-   Complete our interactive Dataquest APIs and scraping course,  [which you can start for free](https://www.dataquest.io/course/apis-and-scraping).
-   Try working with some data from this list of  [Free Public APIs](https://github.com/public-apis/public-apis)  — we recommend selecting an API that doesn’t require authentication as a good first step.

Ref : [https://www.dataquest.io/blog/python-api-tutorial/](https://www.dataquest.io/blog/python-api-tutorial/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzkyNTkxODI2XX0=
-->