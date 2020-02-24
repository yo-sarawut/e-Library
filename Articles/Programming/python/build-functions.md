
# Build Functions to Easily Perform Repeated Operations

-   February 18, 2018 • 19 min read
-   Key Terms: functions, lists, loops, math

**Functions**  allow you to store reusable logic.

### Function Terminology[¶](https://dfrieds.com/python/functions.html#Function-Terminology)
```py
type(32)

# int
```
The  **name**  of the function is the words that precede the parentheses.

The expression in parentheses is the  **argument**  of the function. Functions don't  _need_  arguments; functions can contain  _multiple_  arguments.

The result for this function is outputted below the function and called the  **return**  value. Every function returns a value.

In the statement above, our  **function**  named  `type`  takes in an  **argument**  of  `32`  and returns  `int`  - an integer.  [`type`](https://docs.python.org/3/library/functions.html#type)  is a function built into the Python standard library. So, the function has already been defined for us.

In the statement above, we  **call**  the function  `type`  to perform the function's computation and  **return**  the result.

Execution of the  **return**  statement inside a function exits the function.

### Bike Trips Example[](https://dfrieds.com/python/functions.html#Bike-Trips-Example)

Below is a sample of data for bike trips as a list of lists. Each inner list holds the data for a trip formatted as  _[duration in seconds, date]_.
```py
bike_trips = [[475, '2018-02-18'],
              [825, '2018-02-18'],
              [1034, '2018-02-18'],
              [980, '2018-02-18'],
              [1350, '2018-02-19'],
              [1880, '2018-02-19'],
              [1950, '2018-02-19'],
              [1530, '2018-02-19']
             ]
```
We want to answer these questions:

-   What is the average trip duration on any given day?
-   How many trips were taken on any given day?

In terms of Python, there's 3 componenents we want to create:

1.  Sum of trip durations on a day
2.  Count of trips on a day
3.  Averge trip duration on a day

We can create our  _own_  functions with logic for each component.

#### Sum of trip durations on a day[](https://dfrieds.com/python/functions.html#Sum-of-trip-durations-on-a-day)

`def`  is a Python keyword that indicates the start of a function definition.

The name preceding  `def`  is the function name. Python recommends lowercase letters and underscores between words - similar to naming variables.

An argument passed to  `sum_seconds_biked_day`  is assigned to a variable called a  **parameter**. We use this  **parameter**  in the body of our function.

Inside our functions, you'll see text in triple quotes. These triple quotes are docstrings - plain text as comments to document the logic of our function.
```py
# global variables below can be used in any function
index_trip_duration_seconds = 0
index_trip_date = 1

def sum_seconds_biked_day(ride_date):
    """
 Find the sum of seconds biked on a given day
  
 :param ride_date: string in format year-month-day
 :returns sum_trips_seconds: sum of seconds biked on a single day
 """
    sum_trips_seconds = 0
    for trip in bike_trips:
        if trip[index_trip_date] == ride_date:
            sum_trips_seconds += trip[index_trip_duration_seconds]
        
    return sum_trips_seconds
```
#### Count of trips on a day[](https://dfrieds.com/python/functions.html#Count-of-trips-on-a-day)
```py
def count_bike_trips_day(ride_date):
    """
 Count bike trips on a given day
  
 :param ride_date: string in format year-month-day
 :returns count: count of unique bike trips in a day
 """
    count = 0
    for trip in bike_trips:
        if trip[index_trip_date] == ride_date:
            count += 1
    return count
```
#### Average trip duration on a day[](https://dfrieds.com/python/functions.html#Average-trip-duration-on-a-day)

An  _average_  computation is the sum of events divided by the count of events.

We can  **call**  our two previously created functions inside a new function.
```py
def average_trip_duration_seconds_day(ride_date):
    """
 Compute average trip duration in seconds 
  
 :param ride_date: string in format year-month-day
 :returns average_trip_duration_in_seconds: average duration of trips in a day - units are seconds
 """
    average_trip_duration_in_seconds = sum_seconds_biked_day(ride_date) / count_bike_trips_day(ride_date)
    return average_trip_duration_in_seconds
```
In  `average_trip_duration_seconds_day`, the  _flow of execution_  is to call the function  `sum_seconds_biked_day`  and divide the  **return**  value by the  **return**  value of  `count_bike_trips_day`.

#### Answer questions for February 18th, 2018[](https://dfrieds.com/python/functions.html#Answer-questions-for-February-18th,-2018)
```py
sum_seconds_biked_day('2018-02-18')

# 3314
```
```py
count_bike_trips_day('2018-02-18')
```p
4

average_trip_duration_seconds_day('2018-02-18')

828.5

#### Present data in better readable format[](https://dfrieds.com/python/functions.html#Present-data-in-better-readable-format)

It's weird to say the average trip duration for February 18th, 2018 is 825.5 seconds. You should pronounce it in days.

Let's design a function to present the average trip durations in a more typical format such as 38 minutes and 40 seconds.

I'll use Python operations for  [floor division](https://docs.python.org/3.1/tutorial/introduction.html#numbers)  and  [modulo](https://docs.python.org/3/reference/expressions.html#binary-arithmetic-operations).

seconds_in_a_minute = 60

def convert_seconds_to_minutes_seconds_readable_format(total_seconds):
    """
 Convert a seconds value into a clean human readable format of X minutes and Y seconds
  
 :param total_seconds: seconds value
 :returns readable_statement: human readable string of minutes and seconds
 """
    minutes = total_seconds // seconds_in_a_minute
    seconds = total_seconds % seconds_in_a_minute
    readable_statement = str(minutes) + " minutes and " + str(seconds) + " seconds"
    return readable_statement

We pass a function call as an argument to a function too.

convert_seconds_to_minutes_seconds_readable_format(average_trip_duration_seconds_day('2018-02-18'))

'13.0 minutes and 48.5 seconds'

### Why are Functions Important[](https://dfrieds.com/python/functions.html#Why-are-Functions-Important)

Creating a new function gives you an opportunity to coordinate similar statements together, which makes your code easier to read and debug. Our seconds conversion definition utilizes similar concepts with seconds, minutes and math logic around time conversions.

Functions can make a program smaller by eliminating repetitive code. You'll often hear in programming the acronym DRY - do not repeat yourself. We wrapped  `count_bike_trips_day`  in a function and can utilize it to calculate  _just_  the count of trips in a day as well as the average trip duration of rides in a day. We  _reuse_  our counting logic. It is  _much_  more concise to call a function twice than to copy and paste the body!

Using multiple functions in a program allows you to easily write logic in components - step by step - just as we did with our sum, count and average functions. I find it's quicker to get to the final solution by writing out small functions and utilize them together.

Well-designed functions can be used in multiple programs. Our  `convert_seconds_to_minutes_seconds_readable_format`  can used to analyze the time it takes to repair bikes, the amount of time people spend in a bike store and more.

> [Source : ](https://dfrieds.com/python/functions.html).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0MDg5NjIzOV19
-->