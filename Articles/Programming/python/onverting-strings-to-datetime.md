
Converting Strings using datetime
===

The  [datetime](https://docs.python.org/3/library/datetime.html)  module consists of three different object types:  `date`,  `time`  and  `datetime`. As you may have guessed,  `date`  holds the date,  `time`  holds the time, and  `datetime`  holds both date and time.

For example, the following example will print the current date and time:

```python
import datetime

print ('Current date/time: {}'.format(datetime.datetime.now()))

```

Running this code will print an output similar to below:

```sh
$ python3 datetime-print-1.py
Current date/time: 2018-06-29 08:15:27.243860

```

When no custom formatting is given, the default string format is used, i.e. the format for "2018-06-29 08:15:27.243860" is in  [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)  format (YYYY-MM-DDTHH:MM:SS.mmmmmm). If our input string to create a  `datetime`  object is in the same ISO 8601 format, we can easily parse it to a  `datetime`  object.

Let's take a look at the code below:

```python
import datetime

date_time_str = '2018-06-29 08:15:27.243860'
date_time_obj = datetime.datetime.strptime(date_time_str, '%Y-%m-%d %H:%M:%S.%f')

print('Date:', date_time_obj.date())
print('Time:', date_time_obj.time())
print('Date-time:', date_time_obj)

```

Running it will print the below output:

```sh
$ python3 datetime-print-2.py
Date: 2018-06-29
Time: 08:15:27.243860
Date-time: 2018-06-29 08:15:27.243860

```

In this example, we are using a new method called  `strptime`. This method takes two arguments: the first one is the string representation of the date-time and the second one is the format of the input string. The return value is of the type  `datetime`. In our example,  `"2018-06-29 08:15:27.243860"`  is the input string and  `"%Y-%m-%d %H:%M:%S.%f"`  is the format of this date string. The returned  `datetime`  value is stored in  `date_time_obj`  variable. Since this is a  `datetime`  variable, we can call  `date()`  and  `time()`  methods directly on it. As you can see from the output, it prints the 'date' and 'time' part of the input string.

You might be wondering what is the meaning of the format  `"%Y-%m-%d %H:%M:%S.%f"`. These are known as  _format tokens_  with different meaning for each token. Check out the  [strptime documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior)  for the list of all different types of format code supported in Python.

So, if the format of a string is known, it can be easily parsed to a  `datetime`  object using  `strptime`. Let me show you one more non-trivial example:

```python
import datetime

date_time_str = 'Jun 28 2018  7:40AM'
date_time_obj = datetime.datetime.strptime(date_time_str, '%b %d %Y %I:%M%p')

print('Date:', date_time_obj.date())
print('Time:', date_time_obj.time())
print('Date-time:', date_time_obj)

```

From the following output you can see that the string was successfully parsed since it is being properly printed by the  `datetime`  object here.

```sh
$ python3 datetime-print-3.py
Date: 2018-06-28
Time: 07:40:00
Date-time: 2018-06-28 07:40:00

```

Here are a few more examples of commonly used time formats and the tokens used for parsing:

```
"Jun 28 2018 at 7:40AM" -> "%b %d %Y at %I:%M%p"
"September 18, 2017, 22:19:55" -> "%B %d, %Y, %H:%M:%S"
"Sun,05/12/99,12:30PM" -> "%a,%d/%m/%y,%I:%M%p"
"Mon, 21 March, 2015" -> "%a, %d %B, %Y"
"2018-03-12T10:12:45Z" -> "%Y-%m-%dT%H:%M:%SZ"

```

You can parse a date-time string of any format using the table mentioned in the  [strptime documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior).

### Dealing with Timezones and datetime

Handling date-times becomes more complex while dealing with timezones. All above examples we have discussed are naive  `datetime`  objects, i.e. these objects don't contain any timezone-related data. The  `datetime`  object has one variable  `tzinfo`, that holds the timezone information.

```python
import datetime as dt

dtime = dt.datetime.now()
print(dtime)
print(dtime.tzinfo)

```

This code will print:

```sh
$ python3 datetime-tzinfo-1.py
2018-06-29 22:16:36.132767
None

```

The output of  `tzinfo`  is  `None`  since it is a naive  `datetime`  object. For timezone conversion, one library called  `pytz`  is available for Python. You can install it as described in  [these instructions](http://pytz.sourceforge.net/). Now, let's use the  `pytz`  library to convert the above timestamp to  [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

```python
import datetime as dt
import pytz

dtime = dt.datetime.now(pytz.utc)
print(dtime)
print(dtime.tzinfo)

```

Output:

```sh
$ python3 datetime-tzinfo-2.py
2018-06-29 17:08:00.586525+00:00
UTC

```

`+00:00`  is the difference between the displayed time and the UTC time. In this example the value of  `tzinfo`  happens to be UTC as well, hence the  `00:00`  offset. In this case, the  `datetime`  object is a  _timezone-aware object_.

Similarly, we can convert date-time strings to any other timezone. For example, we can convert the string "2018-06-29 17:08:00.586525+00:00" to "America/New_York" timezone, as shown below:

```python
import datetime as dt
import pytz

date_time_str = '2018-06-29 17:08:00'
date_time_obj = dt.datetime.strptime(date_time_str, '%Y-%m-%d %H:%M:%S')

timezone = pytz.timezone('America/New_York')
timezone_date_time_obj = timezone.localize(date_time_obj)

print(timezone_date_time_obj)
print(timezone_date_time_obj.tzinfo)

```

Output:

```sh
$ python3 datetime-tzinfo-3.py
2018-06-29 17:08:00-04:00
America/New_York

```

First, we have converted the string to a  `datetime`  object,  `date_time_obj`. Then we converted it to a timezone-enabled  `datetime`  object,  `timezone_date_time_obj`. Since we have mentioned the timezone as "America/New_York", the output time shows that it is  _4 hours_  behind than UTC time. You can check  [this Wikipedia page](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)  to find the full list of available time zones.

### Converting Timezones

We can convert timezone of a  `datetime`  object from one region to another, as shown in the example below:

```python
import datetime as dt
import pytz

timezone_nw = pytz.timezone('America/New_York')
nw_datetime_obj = dt.datetime.now(timezone_nw)

timezone_london = pytz.timezone('Europe/London')
london_datetime_obj = nw_datetime_obj.astimezone(timezone_london)


print('America/New_York:', nw_datetime_obj)
print('Europe/London:', london_datetime_obj)

```

First, it created one datetime object with the current time on "America/New_York" timezone. Then using  `astimezone()`  method, we have converted this  `datetime`  to "Europe/London" timezone. Both  `datetime`s will print different values like:

```sh
$ python3 datetime-tzinfo-4.py
America/New_York: 2018-06-29 22:21:41.349491-04:00
Europe/London: 2018-06-30 03:21:41.349491+01:00

```

### Using Third Party Libraries

Python's  `datetime`  module can convert all different types of strings to a  `datetime`  object. But the main problem is that in order to do this you need to create the appropriate formatting code string that  `strptime`  can understand. Creating this string takes time and it makes the code harder to read. Instead, we can use other third-party libraries to make it easier.

In some cases these third party libraries also have better built-in support for manipulating and comparing date-times, and some even have timezones built-in, so you don't need to include an extra package.

Let's take a look at few of these libraries in the following sections.

#### dateutil

The  [dateutil module](https://dateutil.readthedocs.io/en/stable/)  is an extension to the  `datetime`  module. We don't need to pass any parsing code to parse a string. For example:

```python
from dateutil.parser import parse

datetime = parse('2018-06-29 22:21:41')

print(datetime)

```

This  `parse`  function will parse the string automatically and store it in the  `datetime`  variable. Parsing is done automatically. You don't have to mention any format string. Let's try to parse different types of strings using  `dateutil`:

```python
from dateutil.parser import parse

date_array = [
    '2018-06-29 08:15:27.243860',
    'Jun 28 2018  7:40AM',
    'Jun 28 2018 at 7:40AM',
    'September 18, 2017, 22:19:55',
    'Sun, 05/12/1999, 12:30PM',
    'Mon, 21 March, 2015',
    '2018-03-12T10:12:45Z',
    '2018-06-29 17:08:00.586525+00:00',
    '2018-06-29 17:08:00.586525+05:00',
    'Tuesday , 6th September, 2017 at 4:30pm'
]

for date in date_array:
    print('Parsing: ' + date)
    dt = parse(date)
    print(dt.date())
    print(dt.time())
    print(dt.tzinfo)
    print('\n')

```

Output:

```py
$ python3 dateutil-1.py
Parsing: 2018-06-29 08:15:27.243860
2018-06-29
08:15:27.243860
None

Parsing: Jun 28 2018  7:40AM
2018-06-28
07:40:00
None

Parsing: Jun 28 2018 at 7:40AM
2018-06-28
07:40:00
None

Parsing: September 18, 2017, 22:19:55
2017-09-18
22:19:55
None

Parsing: Sun, 05/12/1999, 12:30PM
1999-05-12
12:30:00
None

Parsing: Mon, 21 March, 2015
2015-03-21
00:00:00
None

Parsing: 2018-03-12T10:12:45Z
2018-03-12
10:12:45
tzutc()

Parsing: 2018-06-29 17:08:00.586525+00:00
2018-06-29
17:08:00.586525
tzutc()

Parsing: 2018-06-29 17:08:00.586525+05:00
2018-06-29
17:08:00.586525
tzoffset(None, 18000)

Parsing: Tuesday , 6th September, 2017 at 4:30pm
2017-09-06
16:30:00
None

```

You can see that almost any type of string can be parsed easily using the  `dateutil`  module.

#### Maya

[Maya](https://github.com/kennethreitz/maya)  also makes it very easy to parse a string and for changing timezones. Some simple examples are shown below:

```python
import maya

dt = maya.parse('2018-04-29T17:45:25Z').datetime()
print(dt.date())
print(dt.time())
print(dt.tzinfo)

```

Output:

```sh
$ python3 maya-1.py
2018-04-29
17:45:25
UTC

```

For converting the time to a different timezone:

```python
import maya

dt = maya.parse('2018-04-29T17:45:25Z').datetime(to_timezone='America/New_York', naive=False)
print(dt.date())
print(dt.time())
print(dt.tzinfo)

```

Output:

```sh
$ python3 maya-2.py
2018-04-29
13:45:25
America/New_York

```

Now isn't that easy to use? Let's try out  `maya`  with the same set of strings we have used with  `dateutil`:

```python
import maya

date_array = [
    '2018-06-29 08:15:27.243860',
    'Jun 28 2018  7:40AM',
    'Jun 28 2018 at 7:40AM',
    'September 18, 2017, 22:19:55',
    'Sun, 05/12/1999, 12:30PM',
    'Mon, 21 March, 2015',
    '2018-03-12T10:12:45Z',
    '2018-06-29 17:08:00.586525+00:00',
    '2018-06-29 17:08:00.586525+05:00',
    'Tuesday , 6th September, 2017 at 4:30pm'
]

for date in date_array:
    print('Parsing: ' + date)
    dt = maya.parse(date).datetime()
    print(dt)
    print(dt.date())
    print(dt.time())
    print(dt.tzinfo)

```

Output:

```py
$ python3 maya-3.py
Parsing: 2018-06-29 08:15:27.243860
2018-06-29 08:15:27.243860+00:00
2018-06-29
08:15:27.243860
UTC

Parsing: Jun 28 2018  7:40AM
2018-06-28 07:40:00+00:00
2018-06-28
07:40:00
UTC

Parsing: Jun 28 2018 at 7:40AM
2018-06-28 07:40:00+00:00
2018-06-28
07:40:00
UTC

Parsing: September 18, 2017, 22:19:55
2017-09-18 22:19:55+00:00
2017-09-18
22:19:55
UTC

Parsing: Sun, 05/12/1999, 12:30PM
1999-05-12 12:30:00+00:00
1999-05-12
12:30:00
UTC

Parsing: Mon, 21 March, 2015
2015-03-21 00:00:00+00:00
2015-03-21
00:00:00
UTC

Parsing: 2018-03-12T10:12:45Z
2018-03-12 10:12:45+00:00
2018-03-12
10:12:45
UTC

Parsing: 2018-06-29 17:08:00.586525+00:00
2018-06-29 17:08:00.586525+00:00
2018-06-29
17:08:00.586525
UTC

Parsing: 2018-06-29 17:08:00.586525+05:00
2018-06-29 12:08:00.586525+00:00
2018-06-29
12:08:00.586525
UTC

Parsing: Tuesday , 6th September, 2017 at 4:30pm
2017-09-06 16:30:00+00:00
2017-09-06
16:30:00
UTC

```

As you can see, all date formats were parsed, but did you notice the difference? If we are not providing the timezone info it automatically converts it to UTC. So, it is important to note that we need to provide  `to_timezone`  and  `naive`  parameters if the time is not in UTC.

#### Arrow

[Arrow](https://arrow.readthedocs.io/en/latest/)  is another library for dealing with datetime in Python. We can get the Python  `datetime`  object from an  `arrow`  object. Let's try this with the same example string we have used for  `maya`:

```python
import arrow

dt = arrow.get('2018-04-29T17:45:25Z')
print(dt.date())
print(dt.time())
print(dt.tzinfo)

```

Output:

```py
$ python3 arrow-1.py
2018-04-29
17:45:25
tzutc()

```

Timezone conversion:

```python
import arrow

dt = arrow.get('2018-04-29T17:45:25Z').to('America/New_York')
print(dt)
print(dt.date())
print(dt.time())

```

Output:

```sh
$ python3 arrow-2.py
2018-04-29T13:45:25-04:00
2018-04-29
13:45:25

```

As you can see the date-time string is converted to the "America/New_York" region.

Now, let's again use the same set of strings we have used above:

```python
import arrow

date_array = [
    '2018-06-29 08:15:27.243860',
    #'Jun 28 2018  7:40AM',
    #'Jun 28 2018 at 7:40AM',
    #'September 18, 2017, 22:19:55',
    #'Sun, 05/12/1999, 12:30PM',
    #'Mon, 21 March, 2015',
    '2018-03-12T10:12:45Z',
    '2018-06-29 17:08:00.586525+00:00',
    '2018-06-29 17:08:00.586525+05:00',
    #'Tuesday , 6th September, 2017 at 4:30pm'
]

for date in date_array:
    dt = arrow.get(date)
    print('Parsing: ' + date)
    print(dt)
    print(dt.date())
    print(dt.time())
    print(dt.tzinfo)
```

This code will fail for the date-time strings that have been commented out. The output for other strings will be:

```py
$ python3 arrow-3.py
Parsing: 2018-06-29 08:15:27.243860
2018-06-29T08:15:27.243860+00:00
2018-06-29
08:15:27.243860
tzutc()

Parsing: 2018-03-12T10:12:45Z
2018-03-12T10:12:45+00:00
2018-03-12
10:12:45
tzutc()

Parsing: 2018-06-29 17:08:00.586525+00:00
2018-06-29T17:08:00.586525+00:00
2018-06-29
17:08:00.586525
tzoffset(None, 0)

Parsing: 2018-06-29 17:08:00.586525+05:00
2018-06-29T17:08:00.586525+05:00
2018-06-29
17:08:00.586525
tzoffset(None, 18000)

```

In order to correctly parse the date-time strings that I have commented out, you'll need to pass the corresponding format tokens. For example, "MMM" for months name, like "Jan, Feb, Mar" etc. You can check  [this guide](https://arrow.readthedocs.io/en/latest/)  for all available tokens.

### Conclusion

We have checked different ways to parse a string to a  `datetime`  object in Python. You can either opt for the default Python  `datetime`  library or any of the third party library mentioned in this article, among many others. The main problem with default  `datetime`  package is that we need to specify the parsing code manually for almost all date-time string formats. So, if your string format changes in the future, you will likely have to change your code as well. But many third-party libraries, like the ones mentioned here, handle it automatically.

One more problem we face is dealing with timezones. The best way to handle them is always to store the time in UTC format on the server and convert it to the user's local timezone while parsing. Not only for parsing string, these libraries can be used for a lot of different types of date-time related operations. I'd encourage you to go through the documents to learn the functionalities in detail.




> Source [stackabuse.com](https://stackabuse.com/converting-strings-to-datetime-in-python/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyNjI0MjMxNSwtMTgzNjA2OTAyM119
-->