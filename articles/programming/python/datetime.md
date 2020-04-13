# Datetime

```python
import datetime

x = datetime.datetime.now()
print(x)
```

```python
2019-09-26 00:21:06.668559
```

## Date Output

```python
import datetime

x = datetime.datetime.now()

print(x.year)
print(x.strftime("%A"))
```

```python
2019
Thursday
```

## Creating Date Objects

```python
import datetime

x = datetime.datetime(2020, 5, 17)
print(x)
```

```python
2020-05-17 00:00:00
```

## The strftime\(\) Method

```python
import datetime

x = datetime.datetime(2018, 6, 1)
print(x.strftime("%B"))
```

```python
June
```

## A reference of all the legal format codes:

| Directive | Description | Example |
| :--- | :--- | :--- |
| %a | Weekday, short version | Wed |
| %A | Weekday, full version | Wednesday |
| %w | Weekday as a number 0-6, 0 is Sunday | 3 |
| %d | Day of month 01-31 | 31 |
| %b | Month name, short version | Dec |
| %B | Month name, full version | December |
| %m | Month as a number 01-12 | 12 |
| %y | Year, short version, without century | 18 |
| %Y | Year, full version | 2018 |
| %H | Hour 00-23 | 17 |
| %I | Hour 00-12 | 05 |
| %p | AM/PM | PM |
| %M | Minute 00-59 | 41 |
| %S | Second 00-59 | 08 |
| %f | Microsecond 000000-999999 | 548513 |
| %z | UTC offset | +0100 |
| %Z | Timezone | CST |
| %j | Day number of year 001-366 | 365 |
| %U | Week number of year, Sunday as the first day of week, 00-53 | 52 |
| %W | Week number of year, Monday as the first day of week, 00-53 | 52 |
| %c | Local version of date and time | Mon Dec 31 17:41:00 2018 |
| %x | Local version of date | 12/31/18 |
| %X | Local version of time | 17:41:00 |
| %% | A % character | % |

## timedelta

**ตัวอย่างการหาผลต่างของวันที่**

```python
import datetime
import pytz

my_birthday = datetime.datetime(1985, 10, 20, 17, 55)
brothers_birthday = datetime.datetime(1992, 6, 25, 18, 30)

indy = pytz.timezone("America/Indianapolis")
my_birthday = indy.localize(my_birthday)
brothers_birthday = indy.localize(brothers_birthday)

diff = brothers_birthday - my_birthday
print(diff)
```

```python
2440 days, 0:35:00
```

**หาวัน โดยบวกจากวันปัจจุบันไปอีก 90 วัน**

```python
import datetime

today = datetime.datetime.now()
ninety_days = datetime.timedelta(days=90)

target_date = today + ninety_days

target_date.strftime("%A")
```

```python
'Wednesday'
```

