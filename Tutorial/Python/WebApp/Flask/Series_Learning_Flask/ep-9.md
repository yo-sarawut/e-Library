
# Working with JSON data | Learning Flask Ep. 9

Handle incoming, parsing and returning JSON data with Flask!

In this part of the "Learning Flask" series, we're going to be working with JSON data.

JSON is an extremely popular format for sending and receiving data over the web. Flask provides us with some great tools to make light work of handling JSON data.

In this guide, we're going to quickly cover how to handle incoming JSON data and return JSON data to the client.

### Handling JSON

Let's start out with a new route. This route will receive some JSON, parse the data, do some validation and return a new JSON response.

**app/app/views.py**
```py
@app.route("/json")
def json_example():
    return "Thanks!"
```

We're going to be POSTing data to the server so we need to pass the  `methods`  argument to the  `@app.route()`  decorator, along with the HTTP methods we want to allow for this route:

**app/app/views.py**
```py
@app.route("/json", methods=["POST"])
def json_example():
    return "Thanks!" 
```
Working with any kind of request in Flask requires importing the  `request`  object. Go ahead and import it:

**app/app/views.py**
```py
from flask import request
```
Now we need a method to handle the incoming JSON. Flask provides the handy  `request.get_json()`  method, which parses any incoming JSON data into a Python dictionary.

Let's store our incoming JSON data in a variable called  `req`  and print it out to the terminal:

**app/app/views.py**
```py
@app.route("/json", methods=["POST"])
def json_example():

    req = request.get_json()

    print(req)

    return "Thanks!"
```
Whilst we're here, let's explicitly set an HTTP response by passing it to  `return`:

**app/app/views.py**
```py
@app.route("/json", methods=["POST"])
def json_example():

    req = request.get_json()

    print(req)

    return "Thanks!", 200
```
### POSTing JSON

Let's post some data to our route!

> Tip - We're going to use the free  [Postman](https://www.getpostman.com/downloads/)  app to make our requests, however, feel free to use an alternative such as curl or write a JavaScript function and call it from the browser (You'll learn how to do this in the next episode!)

Go ahead and create a new  `POST`  request to the following URL:

**Postman URL**

`http://127.0.0.1:5000/json` 

We need to create some JSON data in the body of our request. Go ahead and click the  `raw`  tab and select  `JSON (application/json)`  from the dropdown list on the right.

Let's just create a simple JSON object with 2 fields for now:

**Postman body**

`{
    "name": "Julian",
    "message": "Posting JSON data to Flask!"
}` 

If you're using  [cURL](https://curl.haxx.se/):

**cURL request**

`curl --header "Content-Type: application/json" --request POST --data '{"name":"Julian","message":"Posting JSON data to Flask!"}' http://127.0.0.1:5000/json` 

Go ahead and click the Send button and look at the bottom of the app for the response body.

You'll see:

**Postman response body**

`Thanks!` 

Now take a look in your terminal, you'll see:

**Terminal**

`{'name': 'Julian', 'message': 'Posting JSON data to Flask!'}` 

Awesome, We've posted some JSON data to Flask and received a response. You'll also notice the response  `status`  at the bottom of the Postman app with  `200 OK`. Just as we told our route to do!

### Parsing incoming JSON

We know using the  `get_json()`  method on the  `request`  object will return a Python dictionary with our JSON fields serielized into key/value pairs.

We can also validate and perform some conditional testing on our incoming request to determine if the body contains JSON data or not using the  `is_json`  check provided by Flask.

Let's check that our response is JSON and return a response depending on what we receive:

**app/app/views.py**
```py
@app.route("/json", methods=["POST"])
def json_example():

    # Validate the request body contains JSON
    if request.is_json:

        # Parse the JSON into a Python dictionary
        req = request.get_json()

        # Print the dictionary
        print(req)

        # Return a string along with an HTTP status code
        return "JSON received!", 200

    else:

        # The request body wasn't JSON so return a 400 HTTP status code
        return "Request was not JSON", 400 
```
We perform a conditional check using the  `if`  statement on the incoming request object to determine if the request body contains JSON or not.

If the request contains JSON, we're printing it and returning the  `JSON received!`  string along with a  `200`  status code to indicate a successful transaction.

If the request body doesn't contain JSON, we're returning  `Request was not JSON`  along with a  `400`  HTTP status code to let the client know there was a bad request.

Go ahead and make another POST request in the Postman app to see the updates  `JSON received!`  response.

**Postman response body**

`JSON received!` 

Now, change the dropdown menu in the Postman app from  `JSON (applicationjson)`  to  `text`  and click send to see the  `Request was not JSON`  message in the response, along with the  `400 BAD REQUEST`  error.

**Postman response body**

`Request was not JSON` 

Alright! So now you know how to handle incoming JSON. Let's go ahead and return some!

### Returning JSON

Again, Flask makes returning JSON a breeze using the the built in  `jsonify`  and  `make_response`  functions.

Let's go ahead and import them:

**app/app/views.py**

`from flask import jsonify, make_response` 

Let's refactor our  `/json`  route to use  `jsonify`  and  `make_response`. We'll discuss them after:

**app/app/views.py**
```py
@app.route("/json", methods=["POST"])
def json_example():

    if request.is_json:

        req = request.get_json()

        response_body = {
            "message": "JSON received!",
            "sender": req.get("name")
        }

        res = make_response(jsonify(response_body), 200)

        return res

    else:

        return make_response(jsonify({"message": "Request body must be JSON"}), 400)` 
```
We've created a new  `response_body`  object using a dictionary and passed it some values.

We then use the  `make_response()`  function to prepare a response, to which we've provided 2 arguments:

-   `jsonify(*args, **kwargs)`  wraps Python's own  `json.dumps()`  method and will serialize Python strings, lists or dicts as a JSON string.
-   `200`  is the HTTP status code we want to return.

> Tip -  `jsonify(1, 2, 3)`  and  `jsonify([1, 2, 3])`  will both serialize to  `[1, 2, 3]`

By passing both of these arguments to the  `make_response()`  function, we can create our response ahead of returning it by storing it as a variable. In our case, the  `res`  variable.

We've also done the same under the  `else`  conditional, just with it all on one line to save some space.

Go ahead and repeat the same process in the Postman app or cURL to see the newly formatted responses.

Posting  `JSON (application/json)`  will return:

**Postman response body**

`{
    "message": "JSON received!",
    "sender": "Julian"
}` 

Changing the dropdown to  `Text`  and posting will return:

**Postman response body**

`{
    "message": "Request body must be JSON"
}` 

### Wrapping up

Flask makes working with JSON easy, providing many useful functions and methods such as  `is_json`,  `get_json()`  and  `jsonify()`, along with helpful functions such as  `make_response()`. Creating API's, webhooks and handling JSON is only a few lines of code away!

Last modified  ·  28 Feb 2019






> Written with [StackEdit](https://pythonise.com/series/learning-flask/working-with-json-in-flask).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODA3MDg2MjZdfQ==
-->