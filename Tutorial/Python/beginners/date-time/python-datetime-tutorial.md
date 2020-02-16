---
bookFlatSection: true
title: Datetime Tutorial
bookToc: true

---
Python Datetime Tutorial: Manipulate Times, Dates, and Time Spans
===

![enter image description here](https://www.dataquest.io/wp-content/uploads/2019/10/python-datetime-tutorial-960x520.jpg)


Dealing with dates and times in Python can be a hassle. Thankfully, there’s a built-in way of making it easier: the Python datetime module.

`datetime`  helps us identify and process time-related elements like dates, hours, minutes, seconds, days of the week, months, years, etc. It offers various services like managing time zones and daylight savings time. It can work with timestamp data. It can extract the day of the week, day of the month, and other date and time formats from strings.

In short, it’s a really powerful way of handling anything date and time related in Python. So let’s get into it!

In this tutorial, we’ll learn about python datetime functions in detail, including:

-   Creating Date Objects
-   Getting year and month from the date
-   Getting month day and Weekday from date
-   Getting hour and minutes from the date
-   Getting Week number of the year from date
-   Converting date object into timestamp
-   Converting UNIX timestamp string to date object
-   Handling timedelta objects
-   Getting the difference between two dates and times
-   Formatting dates: strftime() and strptime()
-   Handling timezones
-   Working with Pandas datetime objects
    
    -   Getting year, month, day, hour, and minute
    -   Getting weekday and day of year
    -   Converting date objects into a DataFrame index

As you work through this tutorial, we’d encourage you to run the code on your own machine. Alternatively, if you’d like to run code in your browser and learn in an interactive fashion with answer-checking to be sure you’re getting it right, our  [free Python intermediate course](https://www.dataquest.io/course/python-for-data-science-intermediate/)  has  [a lesson on datetime in Python](https://www.dataquest.io/m/353-working-with-dates-and-times-in-python/)  that we recommend. All it requires is  [signing up for a free user account](https://app.dataquest.io/signup).

## Python  `datetime`  Classes  

Before jumping into writing code, it’s worth looking at the five main object classes that are used in the  `datetime`  module. Depending on what we’re trying to do, we’ll likely need to make use of one or more of these distinct classes:

-   **datetime**  – Allows us to manipulate times and dates together (month, day, year, hour, second, microsecond).
    
-   **date**  – Allows us to manipulate dates independent of time (month, day, year).
    
-   **time**  – Allows us to manipulate time independent of date (hour, minute, second, microsecond).
    
-   **timedelta**— A  _duration_  of time used for manipulating dates and measuring.
    
-   **tzinfo**— An abstract class for dealing with time zones.
    

If those distinctions don’t make sense yet, don’t worry! Let’s dive into  `datetime`  and start working with it to better understand how these are applied.

## Creating Date Objects  

First, let’s take a closer look at a  `datetime`  object. Since  `datetime`  is both a module and a class within that module, we’ll start by importing the  `datetime`  class from the  `datetime`  module.

Then, we’ll print the current date and time to take a closer look at what’s contained in a  `datetime`  object. We can do this using  `datetime`‘s  `.now()`  function. We’ll print our datetime object, and then also print its type using  `type()`  so we can take a closer look.

```python
# import datetime class from datetime module
from datetime import datetime

# get current date
datetime_object = datetime.now()
print(datetime_object)
print('Type :- ',type(datetime_object))
```
```
2019-10-25 10:24:01.521881
Type :-  <class 'datetime.datetime'>
```
We can see from the results above that  `datetime_object`  is indeed a  `datetime`  object of the  `datetime`  class. This includes the year, month, day, hour, minute, second, and microsecond.

## Extract Year and Month from the Date  

Now we’ve seen what makes up a  `datetime`  object, we can probably guess how  `date`  and  `time`  objects look, because we know that  `date`  objects are just like  `datetime`  without the time data, and  `time`  objects are just like  `datetime`  without the date data.

We can also antipate some problems. For example, in most data sets, date and time information is stored in string format! Also, we may not  _want_  all of this date and time data — if we’re doing something like a monthly sales analysis, breaking things down by microsecond isn’t going to be very useful.

So now, let’s start digging into a common task in data science: extracting only the elements that we actually want from a string using  `datetime`.

To do this, we need to do a few things.

#### Handling Date and Time Strings with  `strptime()`  and  `strftime()`[](https://www.dataquest.io/blog/python-datetime-tutorial/#Handling-Date-and-Time-Strings-with-strptime()-and-strftime())  

Thankfully,  `datetime`  includes two methods,  `strptime()`  and  `strftime()`, for converting objects from strings to  `datetime`  objects and vice versa.  `strptime()`  can read strings with date and time information and convert them to  `datetime`  objects, and  `strftime()`  converts datetime objects back into strings.

Of course,  `strptime()`  isn’t magic — it can’t turn  _any_  string into a date and time, and it will need a little help from us to interpret what it’s seeing! But it’s capable of reading most conventional string formats for date and time data (see  [the documentation for more details](https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior)). Let’s give it a date string in YYYY-MM-DD format and see what it can do!

```python
my_string = '2019-10-31'

# Create date object in given time format yyyy-mm-dd
my_date = datetime.strptime(my_string, "%Y-%m-%d")

print(my_date)
print('Type: ',type(my_date))
```
```
2019-10-31 00:00:00
Type:  <class 'datetime.datetime'>
```
Note that  `strptime()`  took two arguments: the string (`my_string`) and  `"%Y-%m-%d"`, another string that tells  `strptime()`  how to interpret the input string  `my_string`.  `%Y`, for example, tells it to expect the first four characters of the string to be the year.

A full list of these patterns is available in  [the documentation](https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior), and we’ll go into these methods in more depth later in this tutorial.

You may also have noticed that a time of  `00:00:00`  has been added to the date. That’s because we created a  `datetime`  object, which must include a date  _and_  a time.  `00:00:00`  is the default time that will be assigned if no time is designated in the string we’re inputting.

Anyway, we were hoping to separate out specific elements of the date for our analysis. One way can do that using the built-in class attributes of a datetime object, like  `.month`  or  `.year`:

```python
print('Month: ', my_date.month) # To Get month from date
print('Year: ', my_date.year) # To Get month from year
```
```
Month:  10
Year:  2019
```
## Getting Day of the Month and Day of the Week from a Date  

Let’s do some more extraction, because that’s a really common task. This time, we’ll try to get the day of the month and the day of the week from  `my_date`. Datetime will give us the day of the week as a number using its  `.weekday()`  function, but we can convert this to a text format (i.e. Monday, Tuesday, Wednesday…) using the  `calendar`  module and a method called  `day_name`.

We’ll start by importing  `calendar`, and then using  `.day`  and  `.weekday()`  on  `my_date`. From there, we can get the day of the week in text format like so:

```python
# import calendar module
import calendar

print('Day of Month:', my_date.day)

# to get name of day(in number) from date
print('Day of Week (number): ', my_date.weekday())

# to get name of day from date
print('Day of Week (name): ', calendar.day_name[my_date.weekday()])
```
```
Day of Month: 31
Day of Week (number):  3
Day of Week (name):  Thursday
```
Wait a minute, that looks a bit odd! The third day of the week should be Wednesday, not Thursday, right?

Let’s take a closer look at that  `day_name`  variable using a for loop:

```python
j = 0
for i in calendar.day_name:
    print(j,'-',i)
    j+=1
```
```
0 - Monday
1 - Tuesday
2 - Wednesday
3 - Thursday
4 - Friday
5 - Saturday
6 - Sunday
```

Now we can see that Python starts weeks on Monday and counts from the index 0 rather than starting at 1. So it makes sense that the number 3 is converted to “Thursday” as we saw above.

## Getting Hours and Minutes From a Python Datetime Object[](https://www.dataquest.io/blog/python-datetime-tutorial/#Getting-Hours-and-Minutes-From-a-Datetime-Object)  

Now let’s dig into time and extract the hours and minutes from datetime object. Much like what we did above with month and year, we can use class attributes  `.hour`  and  `.minute`  to get the hours and minutes of the day.

Let’s set a new date and time using the  `.now()`  function. As of this writing, it’s October 25, 2019 at 10:25 AM. You’ll get different results depending on when you choose to run this code, of course!

```python
from datetime import datetime
todays_date = datetime.now()

# to get hour from datetime
print('Hour: ', todays_date.hour)

# to get minute from datetime
print('Minute: ', todays_date.minute)
```
```
Hour:  10
Minute:  25
```
## Getting Week of the Year from a Datetime Object[](https://www.dataquest.io/blog/python-datetime-tutorial/#Getting-Week-of-the-Year-from-a-Datetime-Object)  

We can also do fancier things with  `datetime`. For example, what if we want to know what week of the year it is?

We can get the year, week of the year, and day of the week from a  `datetime`  object with the  `.isocalendar()`  function.

Specifically,  `isocalendar()`  returns a tuple with ISO year, week number and weekday. The  [ISO calendar](https://en.wikipedia.org/wiki/ISO_week_date)  is a widely-used standard calendar based on the Gregorian calendar. You can read about it in more detail at that link, but for our purposes, all we need to know is that it works as a regular calendar, starting each week on Monday.

```python
# Return a 3-tuple, (ISO year, ISO week number, ISO weekday).
todays_date.isocalendar()
```
```
(2019, 43, 5)
```
Note that in the ISO calendar, the week starts counting from 1, so here 5 represents the correct day of the week: Friday.

We can see from the above that this is the 43rd week of the year, but if we wanted to isolate that number, we could do so with indexing just as we might for any other Python list or tuple:

```python
todays_date.isocalendar()[1]
```
```
43
```
## Converting a Date Object into Unix Timestamp and Vice Versa[](https://www.dataquest.io/blog/python-datetime-tutorial/#Converting-a-Date-Object-into-Unix-Timestamp-and-Vice-Versa)  

In programming, it’s not uncommon to encounter time and date data that’s stored as a timestamp, or to want to store your own data in  [Unix timestamp format](https://en.wikipedia.org/wiki/Unix_time).

We can do that using datetime’s built-in  `timestamp()`  function, which takes a  `datetime`  object as an argument and returns that date and time in timestamp format:

```python
#import datetime
from datetime import datetime

# get current date
now = datetime.now()

# convert current date into timestamp
timestamp = datetime.timestamp(now)

print("Date and Time :", now)
print("Timestamp:", timestamp)
```
```
Date and Time : 2019-10-25 10:36:32.827300
Timestamp: 1572014192.8273
```
Similarly, we can do the reverse conversion using  `fromtimestamp()`. This is a  `datetime`  function that takes a timestamp (in float format) as an argument and returns a  `datetime`  object, as below:

```python
#import datetime
from datetime import datetime

timestamp = 1572014192.8273

#convert timestamp to datetime object
dt_object = datetime.fromtimestamp(timestamp)

print("dt_object:", dt_object)
print("type(dt_object): ", type(dt_object))
```
```
dt_object: 2019-10-25 10:36:32.827300
type(dt_object):  <class 'datetime.datetime'>
```
![python datetime tutorial - timedelta and time span](https://www.dataquest.io/wp-content/uploads/2019/10/measure-time-span-python-timedelta.jpg)

## Measuring Time Span with Timedelta Objects[](https://www.dataquest.io/blog/python-datetime-tutorial/#Measuring-Time-Span-with-Timedelta-Objects)  

Often, we may want to measure a span of time, or a duration, using Python datetime. We can do this with its built-in  `timedelta`  class. A  `timedelta`  object represents the amount of time between two dates or times. We can use this to measure time spans, or manipulate dates or times by adding and subtracting from them, etc.

By default a timedelta object has all parameters set to zero. Let’s create a new timedelta object that’s two weeks long and see how that looks:

```python
#import datetime
from datetime import timedelta

# create timedelta object with difference of 2 weeks
d = timedelta(weeks=2)

print(d)
print(type(d))
print(d.days)
```
```
14 days, 0:00:00
<class 'datetime.timedelta'>
14
```
Note that we can get our time duration in days by using the  `timedelta`  class attribute  `.days`. As we can see in  [its documentation](https://docs.python.org/2/library/datetime.html#timedelta-objects), we can also get this time duration in seconds or microseconds.

Let’s create another timedelta duration to get a bit more practice:

```python
year = timedelta(days=365)
print(year)
```
```
365 days, 0:00:00
```
Now let’s start doing using timedelta objects together with datetime objects to do some math! Specifically, let’s add a few diffeent time durations to the current time and date to see what date it will be after 15 days, what date it was two weeks ago.

To do this, we can use the  `+`  or  `-`  operators to add or subtract the timedelta object to/from a datetime object. The result will be the datetime object plus or minus the duration of time specified in our timedelta object. Cool, right?

(Note: in the code below, it’s October 25 at 11:12 AM; your results will differ depending on when you run the code since we’re getting our  `datetime`  object using the  `.now()`  function).

```python
#import datetime
from datetime import datetime, timedelta

# get current time
now = datetime.now()
print ("Today's date: ", str(now))

#add 15 days to current date
future_date_after_15days = now + timedelta(days = 15)
print('Date after 15 days: ', future_date_after_15days)

#subtract 2 weeks from current date
two_weeks_ago = now - timedelta(weeks = 2)
print('Date two weeks ago: ', two_weeks_ago)
print('two_weeks_ago object type: ', type(two_weeks_ago))
```
```
Today's date:  2019-10-25 11:12:24.863308
Date after 15 days:  2019-11-09 11:12:24.863308
Date two weeks ago:  2019-10-11 11:12:24.863308
two_weeks_ago object type:  <class 'datetime.datetime'>
```
Note that the output of these mathematical operations is still a  `datetime`  object.

## Find the Difference Between Two Dates and Times[](https://www.dataquest.io/blog/python-datetime-tutorial/#Find-the-Difference-Between-Two-Dates-and-Times)  

Similar to what we did above, we can also subtract one date from another date to find the timespan between them using datetime.

Because the result of this math is a  _duration_, the object produced when we subtract one date from another will be a  `timedelta`  object.

Here, we’ll create two  `date`  objects (remeber, these work the same as  `datetime`  objects, they just don’t include time data) and subtract one from the other to find the duration:

```python
# import datetime
from datetime import date

# Create two dates
date1 = date(2008, 8, 18)
date2 = date(2008, 8, 10)

# Difference between two dates
delta = date2 - date1

print("Difference: ", delta.days)
print('delta object type: ', type(delta))
```
```
Difference:  -8
delta object type:  <class 'datetime.timedelta'>
```
Above, we used only dates for the sake of clarity, but we can do the same thing with  `datetime`  objects to get a more precise measurement that includes hours, minutes, and seconds as well:

```python
# import datetime
from datetime import datetime

# create two dates with year, month, day, hour, minute, and second
date1 = datetime(2017, 6, 21, 18, 25, 30)
date2 = datetime(2017, 5, 16, 8, 21, 10)

# Difference between two dates
diff = date1-date2

print("Difference: ", diff)
```
```
Difference:  36 days, 10:04:20
```
![python datetime tutorial formatting dates strftime](https://www.dataquest.io/wp-content/uploads/2019/10/python-datetime-formatting-dates.jpg)

## Formatting Dates: More on strftime() and strptime()[](https://www.dataquest.io/blog/python-datetime-tutorial/#Formatting-Dates:-More-on-strftime()-and-strptime())  

We touched briefly on  `strftime()`  and  `strptime()`  earlier, but let’s take a closer look at these methods, as they’re often important for data analysis work in Python.

`strptime()`  is the method we used before, and you’ll recall that it can turn a date and time that’s formatted as a text string into a datetime object, in the following format:

`time.strptime(string, format)`

Note that it takes two arguments:

-   string − the time in string format that we want to convert
    
-   format − the specific formatting of the time in the string, so that strptime() can parse it correctly
    

Let’s try converting a different kind of date string this time.  [This site](http://strftime.org/)  is a really useful reference for finding the formatting codes needed to help  `strptime()`  interpret our string input.

```python
# import datetime
from datetime import datetime

date_string = "1 August, 2019"

# format date
date_object = datetime.strptime(date_string, "%d %B, %Y")

print("date_object: ", date_object)
```
```
date_object:  2019-08-01 00:00:00
```
Now let’s do something a bit more advanced to practice everything we’ve learned so far! We’ll start with a date in string format, convert it to a datetime object, and look at a couple different ways of formatting it (dd/mm and mm/dd).

Then, sticking with the mm/dd formatting, we’ll convert it into a Unix timestamp. Then we’ll convert it back into a  `datetime`  object, and convert  _that_  back into strings using a few different  [strftime patterns](http://strftime.org/)  to control the output:

```python
# import datetime
from datetime import datetime

dt_string = "12/11/2018 09:15:32"
# Considering date is in dd/mm/yyyy format
dt_object1 = datetime.strptime(dt_string, "%d/%m/%Y %H:%M:%S")
print("dt_object1:", dt_object1)
# Considering date is in mm/dd/yyyy format
dt_object2 = datetime.strptime(dt_string, "%m/%d/%Y %H:%M:%S")
print("dt_object2:", dt_object2)

# Convert dt_object2 to Unix Timestamp
timestamp = datetime.timestamp(dt_object2)
print('Unix Timestamp: ', timestamp)

# Convert back into datetime
date_time = datetime.fromtimestamp(timestamp)
d = date_time.strftime("%c")
print("Output 1:", d)
d = date_time.strftime("%x")
print("Output 2:", d)
d = date_time.strftime("%X")
print("Output 3:", d)
```
```
dt_object1: 2018-11-12 09:15:32
dt_object2: 2018-12-11 09:15:32
Unix Timestamp:  1544537732.0
Output 1: Tue Dec 11 09:15:32 2018
Output 2: 12/11/18
Output 3: 09:15:32
```
Here’s an image you can save with a cheat sheet for common, useful strptime and strftime patterns:

![Screenshot%20Capture%20-%202019-10-12%20-%2011-05-58.png](data:image/png;base64,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)

Let’s get a little more practice using these:

```python
# current date and time
now = datetime.now()

# get year from date
year = now.strftime("%Y")
print("Year:", year)

# get month from date
month = now.strftime("%m")
print("Month;", month)

# get day from date
day = now.strftime("%d")
print("Day:", day)

# format time in HH:MM:SS
time = now.strftime("%H:%M:%S")
print("Time:", time)

# format date
date_time = now.strftime("%m/%d/%Y, %H:%M:%S")
print("Date and Time:",date_time)
```

Year: 2019
Month; 10
Day: 25
Time: 11:56:41
Date and Time: 10/25/2019, 11:56:41

## Handling Timezones[](https://www.dataquest.io/blog/python-datetime-tutorial/#Handling-Timezones)  

Working with dates and times in Pythin can get even more complicated when timezones get involved. Thankfully, the  `pytz`  module exists to help us deal with cross-timezone conversions. It also handles the daylight savings time in locations that use that.

We can use the  `localize`  function to add a time zone location to a Python datetime object. Then we can use the function  `astimezone()`  to convert the existing local time zone into any other time zone we specify (it takes the time zone we want to convert into as an argument).

For example:

```python
# import timezone from pytz module
from pytz import timezone

# Create timezone US/Eastern
east = timezone('US/Eastern')
# Localize date
loc_dt = east.localize(datetime(2011, 11, 2, 7, 27, 0))
print(loc_dt)

# Convert localized date into Asia/Kolkata timezone
kolkata = timezone("Asia/Kolkata")
print(loc_dt.astimezone(kolkata))

# Convert localized date into Australia/Sydney timezone
au_tz = timezone('Australia/Sydney')
print(loc_dt.astimezone(au_tz))
```
```
2011-11-02 07:27:00-04:00
2011-11-02 16:57:00+05:30
2011-11-02 22:27:00+11:00
```
This module can help make life simpler when working with data sets that include multiple different time zones.

## Working with  `pandas`  Datetime Objects[](https://www.dataquest.io/blog/python-datetime-tutorial/#Working-with-pandas-Datetime-Objects)  

Data scientists love  `pandas`  for many reasons. One of them is that it contains extensive capabilities and features for working with time series data. Much like  `datetime`  itself, pandas has both  `datetime`  and  `timedelta`  objects for specifying dates and times and durations, respectively.

We can convert date, time, and duration text strings into pandas Datetime objects using these functions:

-   **to_datetime()**: Converts string dates and times into Python datetime objects.
-   **to_timedelta()**: Finds differences in times in terms of days, hours, minutes, and seconds.

And as we’ll see, these functions are actually quite good at converting strings to Python datetime objects by detecting their format automatically, without needing us to define it using strftime patterns.

Let’s look at a quick example:

```python
# import pandas module as pd
import pandas as pd

# create date object using to_datetime() function
date = pd.to_datetime("8th of sep, 2019")
print(date)
```
```
2019-09-08 00:00:00
```
Note that even though we gave it a string with some complicating factors like a “th” and “sep” rather than “Sep.” or “September”, pandas was able to correctly parse the string and return a formatted date.

We can also use pandas (and some of its affiliated numpy functionality) to create date ranges automatically as pandas Series. Below, for example, we create a series of twelve dates starting from the day we defined above. Then we create a different series of dates starting from a predefined date using  `pd.date_range()`:

```python
# Create date series using numpy and to_timedelta() function
date_series = date + pd.to_timedelta(np.arange(12), 'D')
print(date_series)

#  Create date series using date_range() function
date_series = pd.date_range('08/10/2019', periods = 12, freq ='D')
print(date_series)
```
```
DatetimeIndex(['2019-09-08', '2019-09-09', '2019-09-10', '2019-09-11',
               '2019-09-12', '2019-09-13', '2019-09-14', '2019-09-15',
               '2019-09-16', '2019-09-17', '2019-09-18', '2019-09-19'],
              dtype='datetime64[ns]', freq=None)
DatetimeIndex(['2019-08-10', '2019-08-11', '2019-08-12', '2019-08-13',
               '2019-08-14', '2019-08-15', '2019-08-16', '2019-08-17',
               '2019-08-18', '2019-08-19', '2019-08-20', '2019-08-21'],
              dtype='datetime64[ns]', freq='D')
```
#### Get Year, Month, Day, Hour, Minute in pandas[](https://www.dataquest.io/blog/python-datetime-tutorial/#Get-Year,-Month,-Day,-Hour,-Minute-in-pandas)  

We can easily get year, month, day, hour, or minute from dates in a column of a pandas dataframe using  `dt`  attributes for all columns. For example, we can use  `df['date'].dt.year`  to extract only the year from a pandas column that includes the full date.

To explore this, let’s make a quick DataFrame using one of the Series we created above:

```python
# Create a DataFrame with one column date
df = pd.DataFrame()
df['date'] = date_series
df.head()
```
	date
0	2019-08-10
1	2019-08-11
2	2019-08-12
3	2019-08-13
4	2019-08-14

Now, let’s create separate columns for each element of the date by using the relevant Python datetime (accessed with  `dt`) attributes:

```python
# Extract year, month, day, hour, and minute. Assign all these date component to new column.
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['hour'] = df['date'].dt.hour
df['minute'] = df['date'].dt.minute
df.head()
```

date

year

month

day

hour

minute

0

2019-08-10

2019

8

10

0

0

1

2019-08-11

2019

8

11

0

0

2

2019-08-12

2019

8

12

0

0

3

2019-08-13

2019

8

13

0

0

4

2019-08-14

2019

8

14

0

0

#### Get Weekday and Day of Year[](https://www.dataquest.io/blog/python-datetime-tutorial/#Get-Weekday-and-Day-of-Year)  

Pandas is also capable of getting other elements, like the day of the week and the day of the year, from its datetime objects. Again, we can use  `dt`  attributes to do this. Note that here, as in Python generally, the week starts on Monday at index 0, so day of the week 5 is  _Saturday_.

```python
# get Weekday and Day of Year. Assign all these date component to new column.
df['weekday'] = df['date'].dt.weekday
df['day_name'] = df['date'].dt.weekday_name
df['dayofyear'] = df['date'].dt.dayofyear
df.head()
```

date

year

month

day

hour

minute

weekday

day_name

dayofyear

0

2019-08-10

2019

8

10

0

0

5

Saturday

222

1

2019-08-11

2019

8

11

0

0

6

Sunday

223

2

2019-08-12

2019

8

12

0

0

0

Monday

224

3

2019-08-13

2019

8

13

0

0

1

Tuesday

225

4

2019-08-14

2019

8

14

0

0

2

Wednesday

226

### Convert Date Object into DataFrame Index[](https://www.dataquest.io/blog/python-datetime-tutorial/#Convert-Date-Object-into-DataFrame-Index)  

We can also use pandas to make a datetime column into the index of our DataFrame. This can be very helpful for tasks like exploratory data visualization, because matplotlib will recognize that the DataFrame index is a time series and plot the data accordingly.

To do this, all we have to do is redefine  `df.index`:

```python
# Assign date column to dataframe index
df.index = df.date
df.head()
```

date

year

month

day

hour

minute

weekday

day_name

dayofyear

date

2019-08-10

2019-08-10

2019

8

10

0

0

5

Saturday

222

2019-08-11

2019-08-11

2019

8

11

0

0

6

Sunday

223

2019-08-12

2019-08-12

2019

8

12

0

0

0

Monday

224

2019-08-13

2019-08-13

2019

8

13

0

0

1

Tuesday

225

2019-08-14

2019-08-14

2019

8

14

0

0

2

Wednesday

226

## Conclusion[](https://www.dataquest.io/blog/python-datetime-tutorial/#Conclusion)  

In this tutorial, we’ve taken a deep dive into Python datetime, and also done some work with pandas and the calendar module. We’ve covered a lot, but remember: the best way to learn something is by actually writing code yourself! If you’d like to practice writing  `datetime`  code with interactive answer-checking, check out our  [free Python intermediate course](https://www.dataquest.io/course/python-for-data-science-intermediate/)  for  [a lesson on datetime in Python](https://www.dataquest.io/m/353-working-with-dates-and-times-in-python/)  with interative answer-checking and in-browser code-running.


> [Source : ](https://www.dataquest.io/blog/python-datetime-tutorial/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxMTEyMTQ0NV19
-->