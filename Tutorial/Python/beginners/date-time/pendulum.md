

Installing  `pendulum`  is quite simple:
```py
$ pip install pendulum
```
or, if you are using  [poetry](https://poetry.eustace.io/):
```
$ poetry add pendulum
```
# Introduction[](https://pendulum.eustace.io/docs/#introduction "Permanent link")

Pendulum is a Python package to ease datetimes manipulation.

It provides classes that are drop-in replacements for the native ones (they inherit from them).

Special care has been taken to ensure timezones are handled correctly, and are based on the underlying  `tzinfo`  implementation. For example all comparisons are done in  `UTC`  or in the timezone of the datetime being used.
```py
 import pendulum

 dt_toronto = pendulum.datetime(2012, 1, 1, tz='America/Toronto')
 dt_vancouver = pendulum.datetime(2012, 1, 1, tz='America/Vancouver')

 print(dt_vancouver.diff(dt_toronto).in_hours())

#3
```
The default timezone, except when using the  `now()`, method will always be  `UTC`.

# Instantiation[](https://pendulum.eustace.io/docs/#instantiation "Permanent link")

There are several different methods available to create a new  `DateTime`  instance.

First there is the main  `datetime()`  helper.
```py
 import pendulum

 dt = pendulum.datetime(2015, 2, 5)
 isinstance(dt, datetime)

#True
```
```py
 dt.timezone.name

#'UTC'
```
`datetime()`  sets the time to  `00:00:00`  if it's not specified, and the timezone (the  `tz`  keyword argument) to  `UTC`. It otherwise can be a  `Timezone`  instance or simply a string timezone value.
```py
 import pendulum

 pendulum.datetime(2015, 2, 5, tz='Europe/Paris')
 tz = pendulum.timezone('Europe/Paris')
 pendulum.datetime(2015, 2, 5, tz=tz)
```
Supported strings for timezones are the one provided by the  [IANA time zone database](https://www.iana.org/time-zones%3E).

The special  `local`  string is also supported and will return your current timezone.

The  `tz`  argument is keyword-only, unlike in version  `1.x`

The  `local()`  helper is similar to  `datetime()`  but automatically sets the timezone to the local timezone.
```py
 import pendulum

 dt = pendulum.local(2015, 2, 5)
 print(dt.timezone.name)

#'America/Toronto'
```
`local()`  is just an alias for  `datetime(..., tz='local')`.

There is also the  `now()`  method.
```py
 import pendulum

 now = pendulum.now()

 now_in_london_tz = pendulum.now('Europe/London')
 now_in_london_tz.timezone_name

#'Europe/London'
 ```
To accompany  `now()`, a few other static instantiation helpers exist to create known instances. The only thing to really notice here is that  `today()`,  `tomorrow()`  and  `yesterday()`, besides behaving as expected, all accept a timezone parameter and each has their time value set to  `00:00:00`.
 ```py
 now = pendulum.now()
 print(now)

#2016-06-28T16:51:45.978473-05:00
```
  ```py
 today = pendulum.today()
 print(today)

#'2016-06-28T00:00:00-05:00'
 ```
  ```py
 tomorrow = pendulum.tomorrow('Europe/London')
 print(tomorrow)
 
#'2016-06-29T00:00:00+01:00'
 ```
  ```py
 yesterday = pendulum.yesterday()
 print(yesterday)
 
#'2016-06-27T00:00:00-05:00'
  ```
Pendulum enforces timezone aware datetimes, and using them is the preferred and recommended way of using the library, however is you really need a  **naive**  `DateTime`  object, the  `naive()`  helper is there for you.
```
 import pendulum

 naive = pendulum.naive(2015, 2, 5)
 naive.timezone

#None
```
The next helper,  `from_format()`, is similar to the native  `datetime.strptime()`  function but uses custom tokens to create a  `DateTime`  instance.
```py
 dt = pendulum.from_format('1975-05-21 22', 'YYYY-MM-DD HH')
 print(dt)
 
#'1975-05-21T22:00:00+00:00'
```
To see all the available tokens, you can check the  [Formatter](https://pendulum.eustace.io/docs/#formatter)  section.

It also accepts a  `tz`  keyword argument to specify the timezone:
```py
 dt = pendulum.from_format('1975-05-21 22', 'YYYY-MM-DD HH', tz='Europe/London')
 
#'1975-05-21T22:00:00+01:00'
```
The final helper is for working with unix timestamps.  `from_timestamp()`  will create a  `DateTime`  instance equal to the given timestamp and will set the timezone as well or default it to  `UTC`.
```py
 dt = pendulum.from_timestamp(-1)
 print(dt)
 
#'1969-12-31T23:59:59+00:00'
```
```py
 dt  = pendulum.from_timestamp(-1, tz='Europe/London')
 print(dt)
 
#'1970-01-01T00:59:59+01:00'
```
Finally, if you find yourself inheriting a  `DateTime`  instance, you can create a  `DateTime`  instance via the  `instance()`  function.
```py
 dt = datetime(2008, 1, 1)
 p = pendulum.instance(dt)
 print(p)
 
#'2008-01-01T00:00:00+00:00'
```
# Parsing[](https://pendulum.eustace.io/docs/#parsing "Permanent link")

The library natively supports the RFC 3339 format, most ISO 8601 formats and some other common formats.
```py
 import pendulum

 dt = pendulum.parse('1975-05-21T22:00:00')
 print(dt)
 
#'1975-05-21T22:00:00+00:00

# You can pass a tz keyword to specify the timezone
 dt = pendulum.parse('1975-05-21T22:00:00', tz='Europe/Paris')
 print(dt)
#'1975-05-21T22:00:00+01:00'

# Not ISO 8601 compliant but common
 dt = pendulum.parse('1975-05-21 22:00:00')
```
If you pass a non-standard or more complicated string, it will raise an exception so it is advised to use the  `from_format()`  helper instead.

However, if you want the library to fallback on the  [dateutil](https://dateutil.readthedocs.io/)  parser, you have to pass  `strict=False`.
```py
 import pendulum

 dt = pendulum.parse('31-01-01')
Traceback (most recent call last):
...
#ParserError: Unable to parse string [31-01-01]
```
```py
 dt = pendulum.parse('31-01-01', strict=False)
 print(dt)
 
#'2031-01-01T00:00:00+00:00'
```
## RFC 3339[](https://pendulum.eustace.io/docs/#rfc-3339 "Permanent link")

STRING

OUTPUT

1996-12-19T16:39:57-08:00

1996-12-19T16:39:57-08:00

1990-12-31T23:59:59Z

1990-12-31T23:59:59+00:00

## ISO 8601[](https://pendulum.eustace.io/docs/#iso-8601 "Permanent link")

### Datetime[](https://pendulum.eustace.io/docs/#datetime "Permanent link")

STRING

OUTPUT

20161001T143028+0530

2016-10-01T14:30:28+05:30

20161001T14

2016-10-01T14:00:00+00:00

### Date[](https://pendulum.eustace.io/docs/#date "Permanent link")

STRING

OUTPUT

2012

2012-01-01T00:00:00+00:00

2012-05-03

2012-05-03T00:00:00+00:00

20120503

2012-05-03T00:00:00+00:00

2012-05

2012-05-01T00:00:00+00:00

### Ordinal day[](https://pendulum.eustace.io/docs/#ordinal-day "Permanent link")

STRING

OUTPUT

2012-007

2012-01-07T00:00:00+00:00

2012007

2012-01-07T00:00:00+00:00

### Week number[](https://pendulum.eustace.io/docs/#week-number "Permanent link")

STRING

OUTPUT

2012-W05

2012-01-30T00:00:00+00:00

2012W05

2012-01-30T00:00:00+00:00

2012-W05-5

2012-02-03T00:00:00+00:00

2012W055

2012-02-03T00:00:00+00:00

### Time[](https://pendulum.eustace.io/docs/#time "Permanent link")

When passing only time information the date will default to today.

STRING

OUTPUT

00:00

2016-12-17T00:00:00+00:00

12:04:23

2016-12-17T12:04:23+00:00

120423

2016-12-17T12:04:23+00:00

12:04:23.45

2016-12-17T12:04:23.450000+00:00

### Intervals[](https://pendulum.eustace.io/docs/#intervals "Permanent link")

STRING

OUTPUT

2007-03-01T13:00:00Z/2008-05-11T15:30:00Z

2007-03-01T13:00:00+00:00 -> 2008-05-11T15:30:00+00:00

2008-05-11T15:30:00Z/P1Y2M10DT2H30M

2008-05-11T15:30:00+00:00 -> 2009-07-21T18:00:00+00:00

P1Y2M10DT2H30M/2008-05-11T15:30:00Z

2007-03-01T13:00:00+00:00 -> 2008-05-11T15:30:00+00:00

You can pass the  `exact`  keyword argument to  `parse()`  to get the exact type that the string represents:

 import pendulum

 pendulum.parse('2012-05-03', exact=True)
Date(2012, 05, 03)

 pendulum.parse('12:04:23', exact=True)
Time(12, 04, 23)

# Localization[](https://pendulum.eustace.io/docs/#localization "Permanent link")

Localization occurs when using the  `format()`  method which accepts a  `locale`  keyword.
```py
 import pendulum

 dt = pendulum.datetime(1975, 5, 21)
 dt.format('dddd DD MMMM YYYY', locale='de')

#'Mittwoch 21 Mai 1975'

 dt.format('dddd DD MMMM YYYY')

#'Wednesday 21 May 1975'
```
`diff_for_humans()`  is also localized, you can set the locale by using  `pendulum.set_locale()`.
```py
 import pendulum

 pendulum.set_locale('de')
 pendulum.now().add(years=1).diff_for_humans()
#'in 1 Jahr'
 pendulum.set_locale('en')
```
However, you might not want to set the locale globally. The  `diff_for_humans()`  method accept a  `locale`  keyword argument to use a locale for a specific call.
```py
 pendulum.set_locale('de')
 dt = pendulum.now().add(years=1)
 dt.diff_for_humans(locale='fr')
#'dans 1 an'
```
# Attributes and Properties[](https://pendulum.eustace.io/docs/#attributes-and-properties "Permanent link")

Pendulum gives access to more attributes and properties than the default  `datetime`  class.
```py
 import pendulum

 dt = pendulum.parse('2012-09-05T23:26:11.123789')

# These properties specifically return integers
```py
 dt.year
2012
 dt.month
9
 dt.day
5
 dt.hour
23
 dt.minute
26
 dt.second
11
 dt.microsecond
123789
 dt.day_of_week
3
 dt.day_of_year
248
 dt.week_of_month
1
 dt.week_of_year
36
 dt.days_in_month
30
 dt.timestamp()
1346887571.123789
 dt.float_timestamp
1346887571.123789
 dt.int_timestamp
1346887571

 pendulum.datetime(1975, 5, 21).age
41  # calculated vs now in the same tz
 dt.quarter
3

# Returns an int of seconds difference from UTC (+/- sign included)
 pendulum.from_timestamp(0).offset
0
 pendulum.from_timestamp(0, 'America/Toronto').offset
-18000

# Returns a float of hours difference from UTC (+/- sign included)
 pendulum.from_timestamp(0, 'America/Toronto').offset_hours
-5.0
 pendulum.from_timestamp(0, 'Australia/Adelaide').offset_hours
9.5

# Gets the timezone instance
 pendulum.now().timezone
 pendulum.now().tz

# Gets the timezone name
 pendulum.now().timezone_name

# Indicates if daylight savings time is on
 dt = pendulum.datetime(2012, 1, 1, tz='America/Toronto')
 dt.is_dst()
False
 dt = pendulum.datetime(2012, 9, 1, tz='America/Toronto')
 dt.is_dst()
True

# Indicates if the instance is in the same timezone as the local timezone
 pendulum.now().is_local()
True
 pendulum.now('Europe/London').is_local()
False

# Indicates if the instance is in the UTC timezone
 pendulum.now().is_utc()
False
 pendulum.now('Europe/London').is_local()
False
 pendulum.now('UTC').is_utc()
True

# Fluent helpers[](https://pendulum.eustace.io/docs/#fluent-helpers "Permanent link")

Pendulum provides helpers that returns a new instance with some attributes modified compared to the original instance. However, none of these helpers, with the exception of explicitely setting the timezone, will change the timezone of the instance. Specifically, setting the timestamp will not set the corresponding timezone to UTC.

 import pendulum

 dt = pendulum.now()

 dt.set(year=1975, month=5, day=21).to_datetime_string()
'1975-05-21 13:45:18'

 dt.set(hour=22, minute=32, second=5).to_datetime_string()
'2016-11-16 22:32:05'

You can also use the  `on()`  and  `at()`  methods to change the date and the time respectively

 dt.on(1975, 5, 21).at(22, 32, 5).to_datetime_string()
'1975-05-21 22:32:05'

 dt.at(10).to_datetime_string()
'2016-11-16 10:00:00'

 dt.at(10, 30).to_datetime_string()
'2016-11-16 10:30:00'

You can also modify the timezone.

 dt.set(tz='Europe/London')

Setting the timezone just modify the timezone information without making any conversion while  `in_timezone()`  (or  `in_tz()`) converts the time in the appropriate timezone.

 import pendulum

 dt = pendulum.datetime(2013, 3, 31, 2, 30)
 print(dt)
'2013-03-31T02:30:00+00:00'

 dt = dt.set(tz='Europe/Paris')
 print(dt)
'2013-03-31T03:30:00+02:00'

 dt = dt.in_tz('Europe/Paris')
 print(dt)
'2013-03-31T04:30:00+02:00'

 dt = dt.set(tz='Europe/Paris').set(tz='UTC')
 print(dt)
'2013-03-31T03:30:00+00:00'

 dt = dt.in_tz('Europe/Paris').in_tz('UTC')
 print(dt)
'2013-03-31T02:30:00+00:00'

# String formatting[](https://pendulum.eustace.io/docs/#string-formatting "Permanent link")

The  `__str__`  magic method is defined which allows  `DateTime`  instances to be printed as a pretty date string when used in a string context.

The default string representation is the same as the one returned by the  `isoformat()`  method.

 import pendulum

 dt = pendulum.datetime(1975, 12, 25, 14, 15, 16)
 print(dt)
'1975-12-25T14:15:16+00:00'

 dt.to_date_string()
'1975-12-25'

 dt.to_formatted_date_string()
'Dec 25, 1975'

 dt.to_time_string()
'14:15:16'

 dt.to_datetime_string()
'1975-12-25 14:15:16'

 dt.to_day_datetime_string()
'Thu, Dec 25, 1975 2:15 PM'

# You can also use the format() method
 dt.format('dddd Do [of] MMMM YYYY HH:mm:ss A')
'Thursday 25th of December 1975 02:15:16 PM'

# Of course, the strftime method is still available
 dt.strftime('%A %-d%t of %B %Y %I:%M:%S %p')
'Thursday 25th of December 1975 02:15:16 PM'

For localization support see the  [Localization](https://pendulum.eustace.io/docs/#localization)  section.

## Common Formats[](https://pendulum.eustace.io/docs/#common-formats "Permanent link")

The following are methods to display a  `DateTime`  instance as a common format:

 import pendulum

 dt = pendulum.now()

 dt.to_atom_string()
'1975-12-25T14:15:16-05:00'

 dt.to_cookie_string()
'Thursday, 25-Dec-1975 14:15:16 EST'

 dt.to_iso8601_string()
'1975-12-25T14:15:16-0500'

 dt.to_rfc822_string()
'Thu, 25 Dec 75 14:15:16 -0500'

 dt.to_rfc850_string()
'Thursday, 25-Dec-75 14:15:16 EST'

 dt.to_rfc1036_string()
'Thu, 25 Dec 75 14:15:16 -0500'

 dt.to_rfc1123_string()
'Thu, 25 Dec 1975 14:15:16 -0500'

 dt.to_rfc2822_string()
'Thu, 25 Dec 1975 14:15:16 -0500'

 dt.to_rfc3339_string()
'1975-12-25T14:15:16-05:00'

 dt.to_rss_string()
'Thu, 25 Dec 1975 14:15:16 -0500'

 dt.to_w3c_string()
'1975-12-25T14:15:16-05:00'

## Formatter[](https://pendulum.eustace.io/docs/#formatter "Permanent link")

Pendulum uses its own formatter when using the  `format()`  method.

This format is more intuitive to use than the one used with  `strftime()`  and supports more directives.

 import pendulum

 dt = pendulum.datetime(1975, 12, 25, 14, 15, 16)
 dt.format('YYYY-MM-DD HH:mm:ss')
'1975-12-25 14:15:16'

### Tokens[](https://pendulum.eustace.io/docs/#tokens "Permanent link")

The following tokens are currently supported:

TOKEN

OUTPUT

**YEAR**

YYYY

2000, 2001, 2002 ... 2012, 2013

YY

00, 01, 02 ... 12, 13

**QUARTER**

Q

1 2 3 4

Qo

1st 2nd 3rd 4th

**MONTH**

MMMM

January, February, March ...

MMM

Jan, Feb, Mar ...

MM

01, 02, 03 ... 11, 12

M

1, 2, 3 ... 11, 12

Mo

1st 2nd ... 11th 12th

**DAY OF YEAR**

DDDD

001, 002, 003 ... 364, 365

DDD

1, 2, 3 ... 4, 5

**DAY OF MONTH**

DD

01, 02, 03 ... 30, 31

D

1, 2, 3 ... 30, 31

Do

1st, 2nd, 3rd ... 30th, 31st

**DAY OF WEEK**

dddd

Monday, Tuesday, Wednesday ...

ddd

Mon, Tue, Wed ...

dd

Mo, Tu, We ...

d

0, 1, 2 ... 6

**DAYS OF ISO WEEK**

E

1, 2, 3 ... 7

**HOUR**

HH

00, 01, 02 ... 23, 24

H

0, 1, 2 ... 23, 24

hh

01, 02, 03 ... 11, 12

h

1, 2, 3 ... 11, 12

**MINUTE**

mm

00, 01, 02 ... 58, 59

m

0, 1, 2 ... 58, 59

**SECOND**

ss

00, 01, 02 ... 58, 59

s

0, 1, 2 ... 58, 59

**FRACTIONAL SECOND**

S

0 1 ... 8 9

SS

00, 01, 02 ... 98, 99

SSS

000 001 ... 998 999

SSSS ...

000[0..] 001[0..] ... 998[0..] 999[0..]

SSSSSS

**AM / PM**

A

AM, PM

**TIMEZONE**

Z

-07:00, -06:00 ... +06:00, +07:00

ZZ

-0700, -0600 ... +0600, +0700

z

Asia/Baku, Europe/Warsaw, GMT ...

zz

EST CST ... MST PST

**SECONDS TIMESTAMP**

X

1381685817, 1234567890.123

**MICROSECONDS TIMESTAMP**

x

1234567890123

### Localized Formats[](https://pendulum.eustace.io/docs/#localized-formats "Permanent link")

Because preferred formatting differs based on locale, there are a few tokens that can be used to format an instance based on its locale.

**TIME**

LT

8:30 PM

**TIME WITH SECONDS**

LTS

8:30:25 PM

**MONTH NUMERAL, DAY OF MONTH, YEAR**

L

09/04/1986

**MONTH NAME, DAY OF MONTH, YEAR**

LL

September 4 1986

**MONTH NAME, DAY OF MONTH, YEAR, TIME**

LLL

September 4 1986 8:30 PM

**MONTH NAME, DAY OF MONTH, DAY OF WEEK, YEAR, TIME**

LLLL

Thursday, September 4 1986 8:30 PM

### Escaping Characters[](https://pendulum.eustace.io/docs/#escaping-characters "Permanent link")

To escape characters in format strings, you can wrap the characters in square brackets.

 import pendulum

 dt = pendulum.now()
 dt.format('[today] dddd', formatter='alternative')
'today Sunday'

# Comparison[](https://pendulum.eustace.io/docs/#comparison "Permanent link")

Simple comparison is offered up via the basic operators. Remember that the comparison is done in the UTC timezone so things aren't always as they seem.

 import pendulum

 first = pendulum.datetime(2012, 9, 5, 23, 26, 11, 0, tz='America/Toronto')
 second = pendulum.datetime(2012, 9, 5, 20, 26, 11, 0, tz='America/Vancouver')

 first.to_datetime_string()
'2012-09-05 23:26:11'
 first.timezone_name
'America/Toronto'
 second.to_datetime_string()
'2012-09-05 20:26:11'
 second.timezone_name
'America/Vancouver'

 first == second
True
 first != second
False
 first > second
False
 first >= second
True
 first < second
False
 first <= second
True

 first = first.on(2012, 1, 1).at(0, 0, 0)
 second = second.on(2012, 1, 1).at(0, 0, 0)
# tz is still America/Vancouver for second

 first == second
False
 first != second
True
 first > second
False
 first >= second
False
 first < second
True
 first <= second
True

To handle the most used cases there are some simple helper functions. For the methods that compare to  `now()`  (ex.  `is_today()`) in some manner the  `now()`  is created in the same timezone as the instance.

 import pendulum

 dt = pendulum.now()

 dt.is_past()
 dt.is_leap_year()

 born = pendulum.datetime(1987, 4, 23)
 not_birthday = pendulum.datetime(2014, 9, 26)
 birthday = pendulum.datetime(2014, 2, 23)
 past_birthday = pendulum.now().subtract(years=50)

 born.is_birthday(not_birthday)
False
 born.is_birthday(birthday)
True
 past_birthday.is_birthday()
# Compares to now by default
True

# Addition and Subtraction[](https://pendulum.eustace.io/docs/#addition-and-subtraction "Permanent link")

To easily adding and subtracting time, you can use the  `add()`  and  `subtract()`  methods. Each method returns a new  `DateTime`  instance.

 import pendulum

 dt = pendulum.datetime(2012, 1, 31)

 dt.to_datetime_string()
'2012-01-31 00:00:00'

 dt = dt.add(years=5)
'2017-01-31 00:00:00'
 dt = dt.add(years=1)
'2018-01-31 00:00:00'
 dt = dt.subtract(years=1)
'2017-01-31 00:00:00'
 dt = dt.subtract(years=5)
'2012-01-31 00:00:00'

 dt = dt.add(months=60)
'2017-01-31 00:00:00'
 dt = dt.add(months=1)
'2017-02-28 00:00:00'
 dt = dt.subtract(months=1)
'2017-01-28 00:00:00'
 dt = dt.subtract(months=60)
'2012-01-28 00:00:00'

 dt = dt.add(days=29)
'2012-02-26 00:00:00'
 dt = dt.add(days=1)
'2012-02-27 00:00:00'
 dt = dt.subtract(days=1)
'2012-02-26 00:00:00'
 dt = dt.subtract(days=29)
'2012-01-28 00:00:00'

 dt = dt.add(weeks=3)
'2012-02-18 00:00:00'
 dt = dt.add(weeks=1)
'2012-02-25 00:00:00'
 dt = dt.subtract(weeks=1)
'2012-02-18 00:00:00'
 dt = dt.subtract(weeks=3)
'2012-01-28 00:00:00'

 dt = dt.add(hours=24)
'2012-01-29 00:00:00'
 dt = dt.add(hours=1)
'2012-02-25 01:00:00'
 dt = dt.subtract(hours=1)
'2012-02-29 00:00:00'
 dt = dt.subtract(hours=24)
'2012-01-28 00:00:00'

 dt = dt.add(minutes=61)
'2012-01-28 01:01:00'
 dt = dt.add(minutes=1)
'2012-01-28 01:02:00'
 dt = dt.subtract(minutes=1)
'2012-01-28 01:01:00'
 dt = dt.subtract(minutes=24)
'2012-01-28 00:00:00'

 dt = dt.add(seconds=61)
'2012-01-28 00:01:01'
 dt = dt.add(seconds=1)
'2012-01-28 00:01:02'
 dt = dt.subtract(seconds=1)
'2012-01-28 00:01:01'
 dt = dt.subtract(seconds=61)
'2012-01-28 00:00:00'

 dt = dt.add(years=3, months=2, days=6, hours=12, minutes=31, seconds=43)
'2015-04-03 12:31:43'
 dt = dt.subtract(years=3, months=2, days=6, hours=12, minutes=31, seconds=43)
'2012-01-28 00:00:00'

# You can also add or remove a timedelta
 dt.add_timedelta(timedelta(hours=3, minutes=4, seconds=5))
'2012-01-28 03:04:05'
 dt.sub_timedelta(timedelta(hours=3, minutes=4, seconds=5))
'2012-01-28 00:00:00'

Passing negative values to  `add()`  is also possible and will act exactly like  `subtract()`

# Difference[](https://pendulum.eustace.io/docs/#difference "Permanent link")

The  `diff()`  method returns a  [Period](https://pendulum.eustace.io/docs/#period)  instance that represents the total duration between two  `DateTime`  instances. This interval can be then expressed in various units. These interval methods always return  _the total difference expressed_  in the specified time requested. All values are truncated and not rounded.

The  `diff()`  method has a default first parameter which is the  `DateTime`  instance to compare to, or  `None`  if you want to use  `now()`. The 2nd parameter is optional and indicates if you want the return value to be the absolute value or a relative value that might have a  `-`  (negative) sign if the passed in date is less than the current instance. This will default to  `True`, return the absolute value.

 import pendulum

 dt_ottawa = pendulum.datetime(2000, 1, 1, tz='America/Toronto')
 dt_vancouver = pendulum.datetime(2000, 1, 1, tz='America/Vancouver')

 dt_ottawa.diff(dt_vancouver).in_hours()
3
 dt_ottawa.diff(dt_vancouver, False).in_hours()
3
 dt_vancouver.diff(dt_ottawa, False).in_hours()
-3

 dt = pendulum.datetime(2012, 1, 31, 0)
 dt.diff(dt.add(months=1)).in_days()
29
 dt.diff(dt.subtract(months=1), False).in_days()
-31

 dt = pendulum.datetime(2012, 4, 30, 0)
 dt.diff(dt.add(months=1)).in_days()
30
 dt.diff(dt.add(weeks=1)).in_days()
7

 dt = pendulum.datetime(2012, 1, 1, 0)
 dt.diff(dt.add(seconds=59)).in_minutes()
0
 dt.diff(dt.add(seconds=60)).in_minutes()
1
 dt.diff(dt.add(seconds=119)).in_minutes()
1
 dt.diff(dt.add(seconds=120)).in_minutes()
2

## Difference for Humans[](https://pendulum.eustace.io/docs/#difference-for-humans "Permanent link")

The  `diff_for_humans()`  method will add a phrase after the difference value relative to the instance and the passed in instance. There are 4 possibilities:

-   When comparing a value in the past to default now:
    
    -   1 hour ago
    -   5 months ago
-   When comparing a value in the future to default now:
    
    -   1 hour from now
    -   5 months from now
-   When comparing a value in the past to another value:
    
    -   1 hour before
    -   5 months before
-   When comparing a value in the future to another value:
    
    -   1 hour after
    -   5 months after

You may also pass  `True`  as a 2nd parameter to remove the modifiers  `ago`,  `from now`, etc.

 import pendulum

# The most typical usage is for comments
# The instance is the date the comment was created
# and its being compared to default now()
 pendulum.now().subtract(days=1).diff_for_humans()
'5 days ago'

 pendulum.now().diff_for_humans(pendulum.now().subtract(years=1))
'1 year after'

 dt = pendulum.datetime(2011, 8, 1)
 dt.diff_for_humans(dt.add(months=1))
'1 month before'
 dt.diff_for_humans(dt.subtract(months=1))
'1 month after'

 pendulum.now().add(seconds=5).diff_for_humans()
'5 seconds from now'

 pendulum.now().subtract(days=24).diff_for_humans()
'3 weeks ago'

 pendulum.now().subtract(days=24).diff_for_humans(absolute=True)
'3 weeks'

You can also change the locale of the string either globally by using  `pendulum.set_locale('fr')`  before the  `diff_for_humans()`  call or specifically for the call by passing the  `locale`  keyword argument. See the  [Localization](https://pendulum.eustace.io/docs/#localization)  section for more detail.

 import pendulum

 pendulum.set_locale('de')
 pendulum.now().add(years=1).diff_for_humans()
'in 1 Jahr'
 pendulum.now().add(years=1).diff_for_humans(locale='fr')
'dans 1 an'

# Modifiers[](https://pendulum.eustace.io/docs/#modifiers "Permanent link")

These group of methods perform helpful modifications to a copy of the current instance. You'll notice that the  `start_of()`,  `next()`  and  `previous()`  methods set the time to  `00:00:00`  and the  `end_of()`  methods set the time to  `23:59:59.999999`.

The only one slightly different is the  `average()`  method. It returns the middle date between itself and the provided  `DateTime`  argument.

 import pendulum

 dt = pendulum.datetime(2012, 1, 31, 12, 0, 0)

 dt.start_of('day')
'2012-01-31 00:00:00'

 dt.end_of('day')
'2012-01-31 23:59:59'

 dt.start_of('month')
'2012-01-01 00:00:00'

 dt.end_of('month')
'2012-01-31 23:59:59'

 dt.start_of('year')
'2012-01-01 00:00:00'

 dt.end_of('year')
'2012-01-31 23:59:59'

 dt.start_of('decade')
'2010-01-01 00:00:00'

 dt.end_of('decade')
'2019-01-31 23:59:59'

 dt.start_of('century')
'2000-01-01 00:00:00'

 dt.end_of('century')
'2099-12-31 23:59:59'

 dt.start_of('week')
'2012-01-30 00:00:00'
 dt.day_of_week == pendulum.MONDAY
True # ISO8601 week starts on Monday

 dt.end_of('week')
'2012-02-05 23:59:59'
 dt.day_of_week == pendulum.SUNDAY
True # ISO8601 week ends on SUNDAY

 dt.next(pendulum.WEDNESDAY)
'2012-02-01 00:00:00'
 dt.day_of_week == pendulum.WEDNESDAY
True

 dt = pendulum.datetime(2012, 1, 1, 12, 0, 0)
dt.next()
'2012-01-08 00:00:00'
 dt.next(keep_time=True)
'2012-01-08T12:00:00+00:00'

 dt = pendulum.datetime(2012, 1, 31, 12, 0, 0)
 dt.previous(pendulum.WEDNESDAY)
'2012-01-25 00:00:00'
 dt.day_of_week == pendulum.WEDNESDAY
True

 dt = pendulum.datetime(2012, 1, 1, 12, 0, 0)
 dt.previous()
'2011-12-25 00:00:00'
 dt.previous(keep_time=True)
'2011-12-25 12:00:00'

 start = pendulum.datetime(2014, 1, 1)
 end = pendulum.datetime(2014, 1, 30)
 start.average(end)
'2014-01-15 12:00:00'

# others that are defined that are similar
# and tha accept month, quarter and year units
# first_of(), last_of(), nth_of()

# Timezones[](https://pendulum.eustace.io/docs/#timezones "Permanent link")

Timezones are an important part of every datetime library and  `pendulum`  tries to provide an easy and accurate system to handle them properly.

The timezone system works best inside the  `pendulum`  ecosystem but can also be used with the standard  `datetime`  library with a few limitations. See  [Using the timezone library directly](https://pendulum.eustace.io/docs/#using-the-timezone-library-directly).

## Normalization[](https://pendulum.eustace.io/docs/#normalization "Permanent link")

When you create a  `DateTime`  instance, the library will normalize it for the given timezone to properly handle any transition that might have occurred.

 import pendulum

 pendulum.datetime(2013, 3, 31, 2, 30, tz='Europe/Paris')
# 2:30 for the 31th of March 2013 does not exist
# so pendulum will return the actual time which is 3:30+02:00
'2013-03-31T03:30:00+02:00'

 pendulum.datetime(2013, 10, 27, 2, 30, tz='Europe/Paris')
# Here, 2:30 exists twice in the day so pendulum will
# assume that the transition already occurred
'2013-10-27T02:30:00+01:00'

You can, however, control the normalization behavior:

 import pendulum

 pendulum.datetime(2013, 3, 31, 2, 30, 0, 0, tz='Europe/Paris',
                      dst_rule=pendulum.PRE_TRANSITION)
'2013-03-31T01:30:00+01:00'
 pendulum.datetime(2013, 10, 27, 2, 30, 0, 0, tz='Europe/Paris',
                      dst_rule=pendulum.PRE_TRANSITION)
'2013-10-27T02:30:00+02:00'

 pendulum.datetime(2013, 3, 31, 2, 30, 0, 0, tz='Europe/Paris',
                      dst_rule=pendulum.TRANSITION_ERROR)
# NonExistingTime: The datetime 2013-03-31 02:30:00 does not exist
 pendulum.datetime(2013, 10, 27, 2, 30, 0, 0, tz='Europe/Paris',
                      dst_rule=pendulum.TRANSITION_ERROR)
# AmbiguousTime: The datetime 2013-10-27 02:30:00 is ambiguous.

Note that it only affects instances at creation time. Shifting time around transition times still behaves the same.

## Shifting time to transition[](https://pendulum.eustace.io/docs/#shifting-time-to-transition "Permanent link")

So, what happens when you add time to a  `DateTime`  instance and stumble upon a transition time? Well  `pendulum`, provided with the context of the previous instance, will adopt the proper behavior and apply the transition accordingly.

 import pendulum

 dt = pendulum.datetime(2013, 3, 31, 1, 59, 59, 999999,
                           tz='Europe/Paris')
'2013-03-31T01:59:59.999999+01:00'
 dt = dt.add(microseconds=1)
'2013-03-31T03:00:00+02:00'
 dt.subtract(microseconds=1)
'2013-03-31T01:59:59.999998+01:00'

 dt = pendulum.datetime(2013, 10, 27, 2, 59, 59, 999999,
                           tz='Europe/Paris',
                           dst_rule=pendulum.PRE_TRANSITION)
'2013-10-27T02:59:59.999999+02:00'
 dt = dt.add(microseconds=1)
'2013-10-27T02:00:00+01:00'
 dt = dt.subtract(microseconds=1)
'2013-10-27T02:59:59.999999+02:00'

## Switching timezones[](https://pendulum.eustace.io/docs/#switching-timezones "Permanent link")

You can easily change the timezone of a  `DateTime`  instance with the  `in_timezone()`  method.

You can also use the more concise  `in_tz()`

 in_paris = pendulum.datetime(2016, 8, 7, 22, 24, 30, tz='Europe/Paris')
'2016-08-07T22:24:30+02:00'
 in_paris.in_timezone('America/New_York')
'2016-08-07T16:24:30-04:00'
 in_paris.in_tz('Asia/Tokyo')
'2016-08-08T05:24:30+09:00'

## Using the timezone library directly[](https://pendulum.eustace.io/docs/#using-the-timezone-library-directly "Permanent link")

**You should avoid using the timezone library in Python < 3.6.**

This is due to the fact that Pendulum relies heavily on the presence of the  `fold`  attribute which was introduced in Python 3.6.

The reason it works inside the Pendulum ecosystem is that it backported the  `fold`  attribute in the  `DateTime`  class.

Like said in the introduction, you can use the timezone library directly with standard  `datetime`  objects but with limitations, especially when adding and subtracting time around transition times.

The value of the  `fold`  attribute will be used by default to determine the transition rule.

 from datetime import datetime
 from pendulum import timezone

 paris = timezone('Europe/Paris')
 dt = datetime(2013, 3, 31, 2, 30)
# By default, fold is set to 0
 dt = paris.convert(dt)
 dt.isoformat()
'2013-03-31T01:30:00+01:00'

 dt = datetime(2013, 3, 31, 2, 30, fold=1)
 dt = paris.convert(dt)
 dt.isoformat()
'2013-03-31T03:30:00+02:00'

Instead of relying on the  `fold`  attribute, you can use the  `dst_rule`  keyword argument, this is especially useful if you want to raise errors on non-existing and ambiguous times.

 import pendulum

 dt = datetime(2013, 3, 31, 2, 30)
# By default, fold is set to 0
 dt = paris.convert(dt, dst_rule=pendulum.PRE_TRANSITION)
 dt.isoformat()
'2013-03-31T01:30:00+01:00'

 dt = paris.convert(dt, dst_rule=pendulum.POST_TRANSITION)
 dt.isoformat()
'2013-03-31T03:30:00+02:00'

 paris.convert(dt, dst_rule=pendulum.TRANSITION_ERROR)
# NonExistingTime: The datetime 2013-03-31 02:30:00 does not exist

This works as expected. However, whenever we add or subtract a  `timedelta`  object, things get tricky.

 from datetime import datetime, timedelta
 from pendulum import timezone

 dt = datetime(2013, 3, 31, 1, 59, 59, 999999)
 dt = paris.convert(dt)
 dt.isoformat()
'2013-03-31T01:59:59.999999+01:00'
 dt = dt + timedelta(microseconds=1)
 dt.isoformat()
'2013-03-31T02:00:00+01:00'

This is not what we expect, it should be  `2013-03-31T03:00:00+02:00`. This is actually easy to retrieve the proper datetime by using  `convert()`  again.

 dt = tz.convert(dt)
 dt.isoformat()
'2013-03-31T03:00:00+02:00'

You can also get a normalized  `datetime`  object from a  `Timezone`  by using the  `datetime()`  method:

 import pendulum

 tz = pendulum.timezone('Europe/Paris')
 dt = tz.datetime(2013, 3, 31, 2, 30)
 dt.isoformat()
'2013-03-31T03:30:00+02:00'

# Duration[](https://pendulum.eustace.io/docs/#duration "Permanent link")

The  `Duration`  class is inherited from the native  `timedelta`  class. It has many improvements over the base class.

Even though, it inherits from the  `timedelta`  class, its behavior is slightly different. The more important to notice is that the native normalization does not happen, this is so that it feels more intuitive.

 import pendulum
 from datetime import datetime

 d1 = datetime(2012, 1, 1, 1, 2, 3, tzinfo=pytz.UTC)
 d2 = datetime(2011, 12, 31, 22, 2, 3, tzinfo=pytz.UTC)
 delta = d2 - d1
 delta.days
-1
 delta.seconds
75600

 d1 = pendulum.datetime(2012, 1, 1, 1, 2, 3)
 d2 = pendulum.datetime(2011, 12, 31, 22, 2, 3)
 delta = d2 - d1
 delta.days
0
 delta.hours
-3

## Instantiation[](https://pendulum.eustace.io/docs/#instantiation_1 "Permanent link")

To create a  `Duration`  instance, you can use the  `duration()`  helper:

 import pendulum

 it = pendulum.duration(days=1177, seconds=7284, microseconds=1234)

Unlike the native  `timedelta`  class, durations support specifying years and months.

 import pendulum

 it = pendulum.duration(years=2, months=3)

However, to maintain compatibility, native methods and properties will make approximations:

 it.days
820

 it.total_seconds()
70848000.0

## Properties and Duration Methods[](https://pendulum.eustace.io/docs/#properties-and-duration-methods "Permanent link")

The  `Duration`  class brings more properties than the default  `days`,  `seconds`  and  `microseconds`.

 import pendulum

 it = pendulum.duration(
...     years=2, months=3,
...     days=1177, seconds=7284, microseconds=1234
... )

 it.years
2
 it.months
3

# Weeks are based on the total of days
# It does not take into account years and months
 it.weeks
168

# Days, just like in timedelta, represents the total of days
# in the duration. If years and/or months are specified
# it will use an approximation
 it.days
1997

# If you want the remaining days not included in full weeks
 it.remaining_days
1

 # The remaining number in each unit
 it.hours
2
 it.minutes
1

# Seconds are, like days, a special case and the default
# property will return the whole value of remaining
# seconds just like the timedelta class for compatibility
 it.seconds
7284

# If you want the number of seconds not included
# in hours and minutes
 it.remaining_seconds
24

 it.microseconds
1234

If you want to get the duration in each supported unit you can use the appropriate methods.

# Each method returns a float like the native
# total_seconds() method
 it.total_weeks()
168.15490079569113

 it.total_days()
1177.0843055698379

 it.total_hours()
28250.02333367611

 it.total_minutes()
1695001.4000205665

 it.total_seconds()
101700084.001234

Similarly, the  `in_xxx()`  methods return the total duration in each supported unit as a truncated integer.

 it.in_weeks()
168

 it.in_days()
1997

 it.in_hours()
28250

 it.in_minutes()
1695001

 it.in_seconds()
101700084

It also has a handy  `in_words()`  method, which determines the duration representation when printed.

 import pendulum

 pendulum.set_locale('fr')

 it = pendulum.duration(days=1177, seconds=7284, microseconds=1234)
 it.in_words()
'168 semaines 1 jour 2 heures 1 minute 24 secondes'

 print(it)
'168 semaines 1 jour 2 heures 1 minute 24 secondes'

 it.in_words(locale='de')
'168 Wochen 1 Tag 2 Stunden 1 Minute 24 Sekunden'

# Period[](https://pendulum.eustace.io/docs/#period "Permanent link")

When you subtract a  `DateTime`  instance to another, or use the  `diff()`  method, it will return a  `Period`  instance. It inherits from the  [Duration](https://pendulum.eustace.io/docs/#duration)  class with the added benefit that it is aware of the instances that generated it, so that it can give access to more methods and properties:

 import pendulum

 start = pendulum.datetime(2000, 11, 20)
 end = pendulum.datetime(2016, 11, 5)

 period = end - start

 period.years
15
 period.months
11
 period.in_years()
15
 period.in_months()
191

# Note that the weeks property
# will change compared to the Duration class
 period.weeks
2 # 832 for the duration

# However the days property will still remain the same
# to keep the compatiblity with the timedelta class
 period.days
5829

Be aware that a period, just like an interval, is compatible with the  `timedelta`  class regarding its attributes. However, its custom attributes (like  `remaining_days`) will be aware of any DST transitions that might have occurred and adjust accordingly. Let's take an example:

 import pendulum

 start = pendulum.datetime(2017, 3, 7, tz='America/Toronto')
 end = start.add(days=6)

 period = end - start

# timedelta properties
 period.days
5
 period.seconds
82800

# period properties
 period.remaining_days
6
 period.hours
0
 period.remaining_seconds
0

Due to its nature (fixed duration between two datetimes), most arithmetic operations will return a  `Duration`  instead of a  `Period`.

 import pendulum

 dt1 = pendulum.datetime(2016, 8, 7, 12, 34, 56)
 dt2 = dt1.add(days=6, seconds=34)
 period = pendulum.period(dt1, dt2)
 period * 2
Duration(weeks=1, days=5, minutes=1, seconds=8)

## Instantiation[](https://pendulum.eustace.io/docs/#instantiation_2 "Permanent link")

You can create an instance by using the  `period()`  helper:

 import pendulum

 start = pendulum.datetime(2000, 1, 1)
 end = pendulum.datetime(2000, 1, 31)

 period = pendulum.period(start, end)

You can also make an inverted period:

 period = pendulum.period(end, start)
 period.remaining_days
-2

If you have inverted dates but want to make sure that the period is positive, you set the  `absolute`  keyword argument to  `True`:

 period = pendulum.period(end, start, absolute=True)
 period.remaining_days
2

## Range[](https://pendulum.eustace.io/docs/#range "Permanent link")

If you want to iterate over a period, you can use the  `range()`  method:

 import pendulum

 start = pendulum.datetime(2000, 1, 1)
 end = pendulum.datetime(2000, 1, 10)

 period = pendulum.period(start, end)

 for dt in period.range('days'):
     print(dt)

'2000-01-01T00:00:00+00:00'
'2000-01-02T00:00:00+00:00'
'2000-01-03T00:00:00+00:00'
'2000-01-04T00:00:00+00:00'
'2000-01-05T00:00:00+00:00'
'2000-01-06T00:00:00+00:00'
'2000-01-07T00:00:00+00:00'
'2000-01-08T00:00:00+00:00'
'2000-01-09T00:00:00+00:00'
'2000-01-10T00:00:00+00:00'

Supported units for  `range()`  are:  `years`,  `months`,  `weeks`,  `days`,  `hours`,  `minutes`  and  `seconds`

You can pass an amount for the passed unit to control the length of the gap:

 for dt in period.range('days', 2):
     print(dt)

'2000-01-01T00:00:00+00:00'
'2000-01-03T00:00:00+00:00'
'2000-01-05T00:00:00+00:00'
'2000-01-07T00:00:00+00:00'
'2000-01-09T00:00:00+00:00'

You can also directly iterate over the  `Period`  instance, the unit will be  `days`  in this case:

 for dt in period:
     print(dt)

You can check if a  `DateTime`  instance is inside a period using the  `in`  keyword:

 dt = pendulum.datetime(2000, 1, 4)
 dt in period
True

# Testing[](https://pendulum.eustace.io/docs/#testing "Permanent link")

The testing methods allow you to set a  `DateTime`  instance (real or mock) to be returned when a "now" instance is created. The provided instance will be returned specifically under the following conditions:

-   A call to the  `now()`  method, ex.  `pendulum.now()`.
-   When the string "now" is passed to the  `parse()`  method, ex.  `pendulum.parse('now')`

 import pendulum

# Create testing datetime
 known = pendulum.datetime(2001, 5, 21, 12)

# Set the mock
 pendulum.set_test_now(known)

 print(pendulum.now())
'2001-05-21T12:00:00+00:00'

 print(pendulum.parse('now'))
'2001-05-21T12:00:00+00:00'

# Clear the mock
 pendulum.set_test_now()

 print(pendulum.now())
'2016-07-10T22:10:33.954851-05:00'

Related methods will also returned values mocked according to the **now** instance.

```python
 print(pendulum.today())
'2001-05-21T00:00:00+00:00'

 print(pendulum.tomorrow())
'2001-05-22T00:00:00+00:00'

 print(pendulum.yesterday())
'2001-05-20T00:00:00+00:00'

If you don't want to manually clear the mock (or you are afraid of forgetting), you can use the provided  `test()`  contextmanager.

 import pendulum

 known = pendulum.datetime(2001, 5, 21, 12)

 with pendulum.test(known):
     print(pendulum.now())
'2001-05-21T12:00:00+00:00'

 print(pendulum.now())
'2016-07-10T22:10:33.954851-05:00'

# Limitations[](https://pendulum.eustace.io/docs/#limitations "Permanent link")

Even though the  `DateTime`  class is a subclass of  `datetime`, there are some rare cases where it can't replace the native class directly. Here is a list (non-exhaustive) of the reported cases with a possible solution, if any:

-   `sqlite3`  will use the the  `type()`  function to determine the type of the object by default. To work around it you can register a new adapter:
    
    import pendulum
    from sqlite3 import register_adapter
    
    register_adapter(pendulum.DateTime, lambda val: val.isoformat(' '))
    
-   `mysqlclient`  (former  `MySQLdb`) and  `PyMySQL`  will use the the  `type()`  function to determine the type of the object by default. To work around it you can register a new adapter:
    
    import pendulum
    import MySQLdb.converters
    import pymysql.converters
    
    MySQLdb.converters.conversions[pendulum.DateTime] = MySQLdb.converters.DateTime2literal
    pymysql.converters.conversions[pendulum.DateTime] = pymysql.converters.escape_datetime
    
-   `django`  will use the  `isoformat()`  method to store datetimes in the database. However since  `pendulum`  is always timezone aware the offset information will always be returned by  `isoformat()`  raising an error, at least for MySQL databases. To work around it you can either create your own  `DateTimeField`  or use the previous workaround for  `MySQLdb`:
    
    import pendulum
    from django.db.models import DateTimeField as BaseDateTimeField
    
    class DateTimeField(BaseDateTimeField):
    
        def value_to_string(self, obj):
            val = self.value_from_object(obj)
    
            if isinstance(value, pendulum.DateTime):
                return value.format('YYYY-MM-DD HH:mm:ss')
    
            return '' if val is None else val.isoformat()

> [Source : ](https://pendulum.eustace.io/docs/.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDg4OTM0MjVdfQ==
-->