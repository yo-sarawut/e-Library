
# Time Series


```python
import numpy as np
import pandas as pd
np.random.seed(12345)
import matplotlib.pyplot as plt
plt.rc('figure', figsize=(10, 6))
PREVIOUS_MAX_ROWS = pd.options.display.max_rows
pd.options.display.max_rows = 20
np.set_printoptions(precision=4, suppress=True)
```

## Date and Time Data Types and Tools


```python
from datetime import datetime
now = datetime.now()
now
now.year, now.month, now.day
```



```py
(2019, 10, 17)
```



```python
delta = datetime(2011, 1, 7) - datetime(2008, 6, 24, 8, 15)
delta
delta.days
delta.seconds
```



```py
56700
```



```python
from datetime import timedelta
start = datetime(2011, 1, 7)
start + timedelta(12)
start - 2 * timedelta(12)
```



```py
datetime.datetime(2010, 12, 14, 0, 0)
```


### Converting Between String and Datetime


```python
stamp = datetime(2011, 1, 3)
str(stamp)
stamp.strftime('%Y-%m-%d')
```



```py
'2011-01-03'
```



```python
value = '2011-01-03'
datetime.strptime(value, '%Y-%m-%d')
datestrs = ['7/6/2011', '8/6/2011']
[datetime.strptime(x, '%m/%d/%Y') for x in datestrs]
```



```py
[datetime.datetime(2011, 7, 6, 0, 0), 
datetime.datetime(2011, 8, 6, 0, 0)]
```



```python
from dateutil.parser import parse
parse('2011-01-03')
```



```py
datetime.datetime(2011, 1, 3, 0, 0)
```



```python
parse('Jan 31, 1997 10:45 PM')
```



```py
datetime.datetime(1997, 1, 31, 22, 45)
```



```bush
parse('6/12/2011', dayfirst=True)
```



```bush
datetime.datetime(2011, 12, 6, 0, 0)
```



```python
datestrs = ['2011-07-06 12:00:00', '2011-08-06 00:00:00']
pd.to_datetime(datestrs)
```



```bush
DatetimeIndex(['2011-07-06 12:00:00', '2011-08-06 00:00:00'], dtype='datetime64[ns]', freq=None)
```



```py
idx = pd.to_datetime(datestrs + [None])
idx
idx[2]
pd.isnull(idx)
```



```bush
array([False, False,  True])
```


## Time Series Basics


```python
from datetime import datetime
dates = [datetime(2011, 1, 2), datetime(2011, 1, 5),
         datetime(2011, 1, 7), datetime(2011, 1, 8),
         datetime(2011, 1, 10), datetime(2011, 1, 12)]
ts = pd.Series(np.random.randn(6), index=dates)
ts
```



```bush
    2011-01-02   -0.204708
    2011-01-05    0.478943
    2011-01-07   -0.519439
    2011-01-08   -0.555730
    2011-01-10    1.965781
    2011-01-12    1.393406
    dtype: float64
```



```python
ts.index
```



```bush
DatetimeIndex(['2011-01-02', '2011-01-05', '2011-01-07', '2011-01-08',
                   '2011-01-10', '2011-01-12'],
                  dtype='datetime64[ns]', freq=None)
```



```python
ts + ts[::2]
```



```bush
    2011-01-02   -0.409415
    2011-01-05         NaN
    2011-01-07   -1.038877
    2011-01-08         NaN
    2011-01-10    3.931561
    2011-01-12         NaN
    dtype: float64
```



```py
ts.index.dtype
```



```bush
dtype('<M8[ns]')
```



```py
stamp = ts.index[0]
stamp
```



```bush
Timestamp('2011-01-02 00:00:00')
```


### Indexing, Selection, Subsetting


```python
stamp = ts.index[2]
ts[stamp]
```



```bush
-0.5194387150567381
```



```python
ts['1/10/2011']
ts['20110110']
```



```bush
 1.9657805725027142
```



```python
longer_ts = pd.Series(np.random.randn(1000),
                      index=pd.date_range('1/1/2000', periods=1000))
longer_ts
longer_ts['2001']
```



```bush
    2001-01-01    1.599534
    2001-01-02    0.474071
    2001-01-03    0.151326
    2001-01-04   -0.542173
    2001-01-05   -0.475496
    2001-01-06    0.106403
    2001-01-07   -1.308228
    2001-01-08    2.173185
    2001-01-09    0.564561
    2001-01-10   -0.190481
                    ...   
    2001-12-22    0.000369
    2001-12-23    0.900885
    2001-12-24   -0.454869
    2001-12-25   -0.864547
    2001-12-26    1.129120
    2001-12-27    0.057874
    2001-12-28   -0.433739
    2001-12-29    0.092698
    2001-12-30   -1.397820
    2001-12-31    1.457823
    Freq: D, Length: 365, dtype: float64
```



```python
longer_ts['2001-05']
```

```bush
    2001-05-01   -0.622547
    2001-05-02    0.936289
    2001-05-03    0.750018
    2001-05-04   -0.056715
    2001-05-05    2.300675
    2001-05-06    0.569497
    2001-05-07    1.489410
    2001-05-08    1.264250
    2001-05-09   -0.761837
    2001-05-10   -0.331617
                    ...   
    2001-05-22    0.503699
    2001-05-23   -1.387874
    2001-05-24    0.204851
    2001-05-25    0.603705
    2001-05-26    0.545680
    2001-05-27    0.235477
    2001-05-28    0.111835
    2001-05-29   -1.251504
    2001-05-30   -2.949343
    2001-05-31    0.634634
    Freq: D, Length: 31, dtype: float64
```



```python
ts[datetime(2011, 1, 7):]
```



```py
    2011-01-07   -0.519439
    2011-01-08   -0.555730
    2011-01-10    1.965781
    2011-01-12    1.393406
    dtype: float64
```


```python
ts
ts['1/6/2011':'1/11/2011']
```



```py
    2011-01-07   -0.519439
    2011-01-08   -0.555730
    2011-01-10    1.965781
    dtype: float64
```



```python
ts.truncate(after='1/9/2011')
```



```py
    2011-01-02   -0.204708
    2011-01-05    0.478943
    2011-01-07   -0.519439
    2011-01-08   -0.555730
    dtype: float64
```



```python
dates = pd.date_range('1/1/2000', periods=100, freq='W-WED')
long_df = pd.DataFrame(np.random.randn(100, 4),
                       index=dates,
                       columns=['Colorado', 'Texas',
                                'New York', 'Ohio'])
long_df.loc['5-2001']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2001-05-02</th>
      <td>-0.006045</td>
      <td>0.490094</td>
      <td>-0.277186</td>
      <td>-0.707213</td>
    </tr>
    <tr>
      <th>2001-05-09</th>
      <td>-0.560107</td>
      <td>2.735527</td>
      <td>0.927335</td>
      <td>1.513906</td>
    </tr>
    <tr>
      <th>2001-05-16</th>
      <td>0.538600</td>
      <td>1.273768</td>
      <td>0.667876</td>
      <td>-0.969206</td>
    </tr>
    <tr>
      <th>2001-05-23</th>
      <td>1.676091</td>
      <td>-0.817649</td>
      <td>0.050188</td>
      <td>1.951312</td>
    </tr>
    <tr>
      <th>2001-05-30</th>
      <td>3.260383</td>
      <td>0.963301</td>
      <td>1.201206</td>
      <td>-1.852001</td>
    </tr>
  </tbody>
</table>
</div>



### Time Series with Duplicate Indices


```python
dates = pd.DatetimeIndex(['1/1/2000', '1/2/2000', '1/2/2000',
                          '1/2/2000', '1/3/2000'])
dup_ts = pd.Series(np.arange(5), index=dates)
dup_ts
```



```py
    2000-01-01    0
    2000-01-02    1
    2000-01-02    2
    2000-01-02    3
    2000-01-03    4
    dtype: int32
```



```python
dup_ts.index.is_unique
```



```py
    False
```



```python
dup_ts['1/3/2000']  # not duplicated
dup_ts['1/2/2000']  # duplicated
```



```py
    2000-01-02    1
    2000-01-02    2
    2000-01-02    3
    dtype: int32
```



```py
grouped = dup_ts.groupby(level=0)
grouped.mean()
grouped.count()
```



```py
    2000-01-01    1
    2000-01-02    3
    2000-01-03    1
    dtype: int64
```


## Date Ranges, Frequencies, and Shifting


```python
ts
resampler = ts.resample('D')
```

### Generating Date Ranges


```python
index = pd.date_range('2012-04-01', '2012-06-01')
index
```



```py
    DatetimeIndex(['2012-04-01', '2012-04-02', '2012-04-03', '2012-04-04',
                   '2012-04-05', '2012-04-06', '2012-04-07', '2012-04-08',
                   '2012-04-09', '2012-04-10', '2012-04-11', '2012-04-12',
                   '2012-04-13', '2012-04-14', '2012-04-15', '2012-04-16',
                   '2012-04-17', '2012-04-18', '2012-04-19', '2012-04-20',
                   '2012-04-21', '2012-04-22', '2012-04-23', '2012-04-24',
                   '2012-04-25', '2012-04-26', '2012-04-27', '2012-04-28',
                   '2012-04-29', '2012-04-30', '2012-05-01', '2012-05-02',
                   '2012-05-03', '2012-05-04', '2012-05-05', '2012-05-06',
                   '2012-05-07', '2012-05-08', '2012-05-09', '2012-05-10',
                   '2012-05-11', '2012-05-12', '2012-05-13', '2012-05-14',
                   '2012-05-15', '2012-05-16', '2012-05-17', '2012-05-18',
                   '2012-05-19', '2012-05-20', '2012-05-21', '2012-05-22',
                   '2012-05-23', '2012-05-24', '2012-05-25', '2012-05-26',
                   '2012-05-27', '2012-05-28', '2012-05-29', '2012-05-30',
                   '2012-05-31', '2012-06-01'],
                  dtype='datetime64[ns]', freq='D')
```



```python
pd.date_range(start='2012-04-01', periods=20)
pd.date_range(end='2012-06-01', periods=20)
```




    DatetimeIndex(['2012-05-13', '2012-05-14', '2012-05-15', '2012-05-16',
                   '2012-05-17', '2012-05-18', '2012-05-19', '2012-05-20',
                   '2012-05-21', '2012-05-22', '2012-05-23', '2012-05-24',
                   '2012-05-25', '2012-05-26', '2012-05-27', '2012-05-28',
                   '2012-05-29', '2012-05-30', '2012-05-31', '2012-06-01'],
                  dtype='datetime64[ns]', freq='D')




```python
pd.date_range('2000-01-01', '2000-12-01', freq='BM')
```



```py
    DatetimeIndex(['2000-01-31', '2000-02-29', '2000-03-31', '2000-04-28',
                   '2000-05-31', '2000-06-30', '2000-07-31', '2000-08-31',
                   '2000-09-29', '2000-10-31', '2000-11-30'],
                  dtype='datetime64[ns]', freq='BM')
```



```python
pd.date_range('2012-05-02 12:56:31', periods=5)
```



```py
    DatetimeIndex(['2012-05-02 12:56:31', '2012-05-03 12:56:31',
                   '2012-05-04 12:56:31', '2012-05-05 12:56:31',
                   '2012-05-06 12:56:31'],
                  dtype='datetime64[ns]', freq='D')
```



```python
pd.date_range('2012-05-02 12:56:31', periods=5, normalize=True)
```



```py
    DatetimeIndex(['2012-05-02', '2012-05-03', '2012-05-04', '2012-05-05',
                   '2012-05-06'],
                  dtype='datetime64[ns]', freq='D')
```


### Frequencies and Date Offsets


```python
from pandas.tseries.offsets import Hour, Minute
hour = Hour()
hour
```


```py
    <Hour>
```



```python
four_hours = Hour(4)
four_hours
```



```py
    <4 * Hours>
```



```python
pd.date_range('2000-01-01', '2000-01-03 23:59', freq='4h')
```



```py
    DatetimeIndex(['2000-01-01 00:00:00', '2000-01-01 04:00:00',
                   '2000-01-01 08:00:00', '2000-01-01 12:00:00',
                   '2000-01-01 16:00:00', '2000-01-01 20:00:00',
                   '2000-01-02 00:00:00', '2000-01-02 04:00:00',
                   '2000-01-02 08:00:00', '2000-01-02 12:00:00',
                   '2000-01-02 16:00:00', '2000-01-02 20:00:00',
                   '2000-01-03 00:00:00', '2000-01-03 04:00:00',
                   '2000-01-03 08:00:00', '2000-01-03 12:00:00',
                   '2000-01-03 16:00:00', '2000-01-03 20:00:00'],
                  dtype='datetime64[ns]', freq='4H')

```


```python
Hour(2) + Minute(30)
```



```py
    <150 * Minutes>
```



```python
pd.date_range('2000-01-01', periods=10, freq='1h30min')
```



```py
    DatetimeIndex(['2000-01-01 00:00:00', '2000-01-01 01:30:00',
                   '2000-01-01 03:00:00', '2000-01-01 04:30:00',
                   '2000-01-01 06:00:00', '2000-01-01 07:30:00',
                   '2000-01-01 09:00:00', '2000-01-01 10:30:00',
                   '2000-01-01 12:00:00', '2000-01-01 13:30:00'],
                  dtype='datetime64[ns]', freq='90T')
```


#### Week of month dates


```python
rng = pd.date_range('2012-01-01', '2012-09-01', freq='WOM-3FRI')
list(rng)
```



```py
    [Timestamp('2012-01-20 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-02-17 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-03-16 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-04-20 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-05-18 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-06-15 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-07-20 00:00:00', freq='WOM-3FRI'),
     Timestamp('2012-08-17 00:00:00', freq='WOM-3FRI')]
```


### Shifting (Leading and Lagging) Data


```python
ts = pd.Series(np.random.randn(4),
               index=pd.date_range('1/1/2000', periods=4, freq='M'))
ts
ts.shift(2)
ts.shift(-2)
```



```py
    2000-01-31   -0.117388
    2000-02-29   -0.517795
    2000-03-31         NaN
    2000-04-30         NaN
    Freq: M, dtype: float64
```

```py
ts / ts.shift(1) - 1
```

```python
ts.shift(2, freq='M')
```



```py
    2000-03-31   -0.066748
    2000-04-30    0.838639
    2000-05-31   -0.117388
    2000-06-30   -0.517795
    Freq: M, dtype: float64
```



```python
ts.shift(3, freq='D')
ts.shift(1, freq='90T')
```



```py
    2000-01-31 01:30:00   -0.066748
    2000-02-29 01:30:00    0.838639
    2000-03-31 01:30:00   -0.117388
    2000-04-30 01:30:00   -0.517795
    Freq: M, dtype: float64
```


#### Shifting dates with offsets


```python
from pandas.tseries.offsets import Day, MonthEnd
now = datetime(2011, 11, 17)
now + 3 * Day()
```



```py
    Timestamp('2011-11-20 00:00:00')
```



```py
now + MonthEnd()
now + MonthEnd(2)
```



```py
    Timestamp('2011-12-31 00:00:00')
```



```python
offset = MonthEnd()
offset.rollforward(now)
offset.rollback(now)
```



```py
    Timestamp('2011-10-31 00:00:00')
```



```python
ts = pd.Series(np.random.randn(20),
               index=pd.date_range('1/15/2000', periods=20, freq='4d'))
ts
ts.groupby(offset.rollforward).mean()
```



```py
    2000-01-31   -0.005833
    2000-02-29    0.015894
    2000-03-31    0.150209
    dtype: float64
```



```python
ts.resample('M').mean()
```



```py
    2000-01-31   -0.005833
    2000-02-29    0.015894
    2000-03-31    0.150209
    Freq: M, dtype: float64
```


## Time Zone Handling


```python
import pytz
pytz.common_timezones[-5:]
```



```py
    ['US/Eastern', 'US/Hawaii', 'US/Mountain', 'US/Pacific', 'UTC']
```



```python
tz = pytz.timezone('America/New_York')
tz
```



```py
    <DstTzInfo 'America/New_York' LMT-1 day, 19:04:00 STD>
```


### Time Zone Localization and Conversion


```python
rng = pd.date_range('3/9/2012 9:30', periods=6, freq='D')
ts = pd.Series(np.random.randn(len(rng)), index=rng)
ts
```



```py
    2012-03-09 09:30:00   -0.202469
    2012-03-10 09:30:00    0.050718
    2012-03-11 09:30:00    0.639869
    2012-03-12 09:30:00    0.597594
    2012-03-13 09:30:00   -0.797246
    2012-03-14 09:30:00    0.472879
    Freq: D, dtype: float64
```



```python
print(ts.index.tz)
```
```py
None
 ```   


```py
pd.date_range('3/9/2012 9:30', periods=10, freq='D', tz='UTC')
```



```py
DatetimeIndex(['2012-03-09 09:30:00+00:00', '2012-03-10 09:30:00+00:00',
                   '2012-03-11 09:30:00+00:00', '2012-03-12 09:30:00+00:00',
                   '2012-03-13 09:30:00+00:00', '2012-03-14 09:30:00+00:00',
                   '2012-03-15 09:30:00+00:00', '2012-03-16 09:30:00+00:00',
                   '2012-03-17 09:30:00+00:00', '2012-03-18 09:30:00+00:00'],
                  dtype='datetime64[ns, UTC]', freq='D')
```



```python
ts
ts_utc = ts.tz_localize('UTC')
ts_utc
ts_utc.index
```



```py
DatetimeIndex(['2012-03-09 09:30:00+00:00', '2012-03-10 09:30:00+00:00',
                   '2012-03-11 09:30:00+00:00', '2012-03-12 09:30:00+00:00',
                   '2012-03-13 09:30:00+00:00', '2012-03-14 09:30:00+00:00'],
                  dtype='datetime64[ns, UTC]', freq='D')
```



```python
ts_utc.tz_convert('America/New_York')
```



```py
    2012-03-09 04:30:00-05:00   -0.202469
    2012-03-10 04:30:00-05:00    0.050718
    2012-03-11 05:30:00-04:00    0.639869
    2012-03-12 05:30:00-04:00    0.597594
    2012-03-13 05:30:00-04:00   -0.797246
    2012-03-14 05:30:00-04:00    0.472879
    Freq: D, dtype: float64
```



```python
ts_eastern = ts.tz_localize('America/New_York')
ts_eastern.tz_convert('UTC')
ts_eastern.tz_convert('Europe/Berlin')
```



```py
    2012-03-09 15:30:00+01:00   -0.202469
    2012-03-10 15:30:00+01:00    0.050718
    2012-03-11 14:30:00+01:00    0.639869
    2012-03-12 14:30:00+01:00    0.597594
    2012-03-13 14:30:00+01:00   -0.797246
    2012-03-14 14:30:00+01:00    0.472879
    Freq: D, dtype: float64
```



```python
ts.index.tz_localize('Asia/Shanghai')
```


```py

DatetimeIndex(['2012-03-09 09:30:00+08:00', '2012-03-10 09:30:00+08:00',
                   '2012-03-11 09:30:00+08:00', '2012-03-12 09:30:00+08:00',
                   '2012-03-13 09:30:00+08:00', '2012-03-14 09:30:00+08:00'],
                  dtype='datetime64[ns, Asia/Shanghai]', freq='D')
```

### Operations with Time Zone−Aware Timestamp Objects


```python
stamp = pd.Timestamp('2011-03-12 04:00')
stamp_utc = stamp.tz_localize('utc')
stamp_utc.tz_convert('America/New_York')
```



```py
    Timestamp('2011-03-11 23:00:00-0500', tz='America/New_York')
```



```python
stamp_moscow = pd.Timestamp('2011-03-12 04:00', tz='Europe/Moscow')
stamp_moscow
```



```py
    Timestamp('2011-03-12 04:00:00+0300', tz='Europe/Moscow')
```



```python
stamp_utc.value
stamp_utc.tz_convert('America/New_York').value
```



```py
    1299902400000000000
```


```python
from pandas.tseries.offsets import Hour
stamp = pd.Timestamp('2012-03-12 01:30', tz='US/Eastern')
stamp
stamp + Hour()
```



```py
    Timestamp('2012-03-12 02:30:00-0400', tz='US/Eastern')
```



```python
stamp = pd.Timestamp('2012-11-04 00:30', tz='US/Eastern')
stamp
stamp + 2 * Hour()
```




    Timestamp('2012-11-04 01:30:00-0500', tz='US/Eastern')



### Operations Between Different Time Zones


```python
rng = pd.date_range('3/7/2012 9:30', periods=10, freq='B')
ts = pd.Series(np.random.randn(len(rng)), index=rng)
ts
ts1 = ts[:7].tz_localize('Europe/London')
ts2 = ts1[2:].tz_convert('Europe/Moscow')
result = ts1 + ts2
result.index
```



```py
DatetimeIndex(['2012-03-07 09:30:00+00:00', '2012-03-08 09:30:00+00:00',
                   '2012-03-09 09:30:00+00:00', '2012-03-12 09:30:00+00:00',
                   '2012-03-13 09:30:00+00:00', '2012-03-14 09:30:00+00:00',
                   '2012-03-15 09:30:00+00:00'],
                  dtype='datetime64[ns, UTC]', freq='B')
```


## Periods and Period Arithmetic


```python
p = pd.Period(2007, freq='A-DEC')
p
```



```py
    Period('2007', 'A-DEC')
```



```python
p + 5
p - 2
```



```py
Period('2005', 'A-DEC')
```



```python
pd.Period('2014', freq='A-DEC') - p
```



```py
    <7 * YearEnds: month=12>
```



```python
rng = pd.period_range('2000-01-01', '2000-06-30', freq='M')
rng
```



```py
PeriodIndex(['2000-01', '2000-02', '2000-03', '2000-04', '2000-05', '2000-06'], dtype='period[M]', freq='M')
```



```python
pd.Series(np.random.randn(6), index=rng)
```



```py
    2000-01   -0.514551
    2000-02   -0.559782
    2000-03   -0.783408
    2000-04   -1.797685
    2000-05   -0.172670
    2000-06    0.680215
    Freq: M, dtype: float64
```



```python
values = ['2001Q3', '2002Q2', '2003Q1']
index = pd.PeriodIndex(values, freq='Q-DEC')
index
```



```py
PeriodIndex(['2001Q3', '2002Q2', '2003Q1'], 
dtype='period[Q-DEC]', freq='Q-DEC')
```


### Period Frequency Conversion


```python
p = pd.Period('2007', freq='A-DEC')
p
p.asfreq('M', how='start')
p.asfreq('M', how='end')
```



```py
    Period('2007-12', 'M')
```



```python
p = pd.Period('2007', freq='A-JUN')
p
p.asfreq('M', 'start')
p.asfreq('M', 'end')
```



```py
    Period('2007-06', 'M')
```



```python
p = pd.Period('Aug-2007', 'M')
p.asfreq('A-JUN')
```



```py
    Period('2008', 'A-JUN')
```



```python
rng = pd.period_range('2006', '2009', freq='A-DEC')
ts = pd.Series(np.random.randn(len(rng)), index=rng)
ts
ts.asfreq('M', how='start')
```



```py
    2006-01    1.607578
    2007-01    0.200381
    2008-01   -0.834068
    2009-01   -0.302988
    Freq: M, dtype: float64
```



```python
ts.asfreq('B', how='end')
```



```py
    2006-12-29    1.607578
    2007-12-31    0.200381
    2008-12-31   -0.834068
    2009-12-31   -0.302988
    Freq: B, dtype: float64
```

### Quarterly Period Frequencies


```python
p = pd.Period('2012Q4', freq='Q-JAN')
p
```



```py
Period('2012Q4', 'Q-JAN')
```



```python
p.asfreq('D', 'start')
p.asfreq('D', 'end')
```



```py
Period('2012-01-31', 'D')
```



```python
p4pm = (p.asfreq('B', 'e') - 1).asfreq('T', 's') + 16 * 60
p4pm
p4pm.to_timestamp()
```


```py

Timestamp('2012-01-30 16:00:00')
```



```python
rng = pd.period_range('2011Q3', '2012Q4', freq='Q-JAN')
ts = pd.Series(np.arange(len(rng)), index=rng)
ts
new_rng = (rng.asfreq('B', 'e') - 1).asfreq('T', 's') + 16 * 60
ts.index = new_rng.to_timestamp()
ts
```



```py
    2010-10-28 16:00:00    0
    2011-01-28 16:00:00    1
    2011-04-28 16:00:00    2
    2011-07-28 16:00:00    3
    2011-10-28 16:00:00    4
    2012-01-30 16:00:00    5
    dtype: int32
```


### Converting Timestamps to Periods (and Back)


```python
rng = pd.date_range('2000-01-01', periods=3, freq='M')
ts = pd.Series(np.random.randn(3), index=rng)
ts
pts = ts.to_period()
pts
```



```py
    2000-01    1.663261
    2000-02   -0.996206
    2000-03    1.521760
    Freq: M, dtype: float64
```



```python
rng = pd.date_range('1/29/2000', periods=6, freq='D')
ts2 = pd.Series(np.random.randn(6), index=rng)
ts2
ts2.to_period('M')
```



```py
    2000-01    0.244175
    2000-01    0.423331
    2000-01   -0.654040
    2000-02    2.089154
    2000-02   -0.060220
    2000-02   -0.167933
    Freq: M, dtype: float64
```



```py
pts = ts2.to_period()
pts
pts.to_timestamp(how='end')
```



```py
    2000-01-29 23:59:59.999999999    0.244175
    2000-01-30 23:59:59.999999999    0.423331
    2000-01-31 23:59:59.999999999   -0.654040
    2000-02-01 23:59:59.999999999    2.089154
    2000-02-02 23:59:59.999999999   -0.060220
    2000-02-03 23:59:59.999999999   -0.167933
    Freq: D, dtype: float64
```


### Creating a PeriodIndex from Arrays


```python
data = pd.read_csv('examples/macrodata.csv')
data.head(5)
data.year
data.quarter
```



```py
    0      1.0
    1      2.0
    2      3.0
    3      4.0
    4      1.0
    5      2.0
    6      3.0
    7      4.0
    8      1.0
    9      2.0
          ... 
    193    2.0
    194    3.0
    195    4.0
    196    1.0
    197    2.0
    198    3.0
    199    4.0
    200    1.0
    201    2.0
    202    3.0
    Name: quarter, Length: 203, dtype: float64
```



```py
index = pd.PeriodIndex(year=data.year, quarter=data.quarter,
                       freq='Q-DEC')
index
data.index = index
data.infl
```



```py
    1959Q1    0.00
    1959Q2    2.34
    1959Q3    2.74
    1959Q4    0.27
    1960Q1    2.31
    1960Q2    0.14
    1960Q3    2.70
    1960Q4    1.21
    1961Q1   -0.40
    1961Q2    1.47
              ... 
    2007Q2    2.75
    2007Q3    3.45
    2007Q4    6.38
    2008Q1    2.82
    2008Q2    8.53
    2008Q3   -3.16
    2008Q4   -8.79
    2009Q1    0.94
    2009Q2    3.37
    2009Q3    3.56
    Freq: Q-DEC, Name: infl, Length: 203, dtype: float64
```


## Resampling and Frequency Conversion


```python
rng = pd.date_range('2000-01-01', periods=100, freq='D')
ts = pd.Series(np.random.randn(len(rng)), index=rng)
ts
ts.resample('M').mean()
ts.resample('M', kind='period').mean()
```




    2000-01   -0.165893
    2000-02    0.078606
    2000-03    0.223811
    2000-04   -0.063643
    Freq: M, dtype: float64



### Downsampling


```python
rng = pd.date_range('2000-01-01', periods=12, freq='T')
ts = pd.Series(np.arange(12), index=rng)
ts
```



```py
    2000-01-01 00:00:00     0
    2000-01-01 00:01:00     1
    2000-01-01 00:02:00     2
    2000-01-01 00:03:00     3
    2000-01-01 00:04:00     4
    2000-01-01 00:05:00     5
    2000-01-01 00:06:00     6
    2000-01-01 00:07:00     7
    2000-01-01 00:08:00     8
    2000-01-01 00:09:00     9
    2000-01-01 00:10:00    10
    2000-01-01 00:11:00    11
    Freq: T, dtype: int32
```



```python
ts.resample('5min', closed='right').sum()
```



```py
    1999-12-31 23:55:00     0
    2000-01-01 00:00:00    15
    2000-01-01 00:05:00    40
    2000-01-01 00:10:00    11
    Freq: 5T, dtype: int32
```



```python
ts.resample('5min', closed='right').sum()
```



```py
    1999-12-31 23:55:00     0
    2000-01-01 00:00:00    15
    2000-01-01 00:05:00    40
    2000-01-01 00:10:00    11
    Freq: 5T, dtype: int32
```



```python
ts.resample('5min', closed='right', label='right').sum()
```


```py
    2000-01-01 00:00:00     0
    2000-01-01 00:05:00    15
    2000-01-01 00:10:00    40
    2000-01-01 00:15:00    11
    Freq: 5T, dtype: int32
```



```python
ts.resample('5min', closed='right',
            label='right', loffset='-1s').sum()
```


```py
    1999-12-31 23:59:59     0
    2000-01-01 00:04:59    15
    2000-01-01 00:09:59    40
    2000-01-01 00:14:59    11
    Freq: 5T, dtype: int32
```


#### Open-High-Low-Close (OHLC) resampling


```python
ts.resample('5min').ohlc()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01 00:00:00</th>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2000-01-01 00:05:00</th>
      <td>5</td>
      <td>9</td>
      <td>5</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2000-01-01 00:10:00</th>
      <td>10</td>
      <td>11</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



### Upsampling and Interpolation


```python
frame = pd.DataFrame(np.random.randn(2, 4),
                     index=pd.date_range('1/1/2000', periods=2,
                                         freq='W-WED'),
                     columns=['Colorado', 'Texas', 'New York', 'Ohio'])
frame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-05</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-0.046662</td>
      <td>0.927238</td>
      <td>0.482284</td>
      <td>-0.867130</td>
    </tr>
  </tbody>
</table>
</div>




```py
df_daily = frame.resample('D').asfreq()
df_daily
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-05</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-0.046662</td>
      <td>0.927238</td>
      <td>0.482284</td>
      <td>-0.867130</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.resample('D').ffill()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-05</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-0.046662</td>
      <td>0.927238</td>
      <td>0.482284</td>
      <td>-0.867130</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.resample('D').ffill(limit=2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-05</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-0.046662</td>
      <td>0.927238</td>
      <td>0.482284</td>
      <td>-0.867130</td>
    </tr>
  </tbody>
</table>
</div>




```python
frame.resample('W-THU').ffill()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-06</th>
      <td>-0.896431</td>
      <td>0.677263</td>
      <td>0.036503</td>
      <td>0.087102</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>-0.046662</td>
      <td>0.927238</td>
      <td>0.482284</td>
      <td>-0.867130</td>
    </tr>
  </tbody>
</table>
</div>



### Resampling with Periods


```python
frame = pd.DataFrame(np.random.randn(24, 4),
                     index=pd.period_range('1-2000', '12-2001',
                                           freq='M'),
                     columns=['Colorado', 'Texas', 'New York', 'Ohio'])
frame[:5]
annual_frame = frame.resample('A-DEC').mean()
annual_frame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Q-DEC: Quarterly, year ending in December
annual_frame.resample('Q-DEC').ffill()
annual_frame.resample('Q-DEC', convention='end').ffill()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000Q4</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q1</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q2</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q3</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q4</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
  </tbody>
</table>
</div>




```python
annual_frame.resample('Q-MAR').ffill()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Colorado</th>
      <th>Texas</th>
      <th>New York</th>
      <th>Ohio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000Q4</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q1</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q2</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q3</th>
      <td>0.556703</td>
      <td>0.016631</td>
      <td>0.111873</td>
      <td>-0.027445</td>
    </tr>
    <tr>
      <th>2001Q4</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
    <tr>
      <th>2002Q1</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
    <tr>
      <th>2002Q2</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
    <tr>
      <th>2002Q3</th>
      <td>0.046303</td>
      <td>0.163344</td>
      <td>0.251503</td>
      <td>-0.157276</td>
    </tr>
  </tbody>
</table>
</div>



## Moving Window Functions


```python
close_px_all = pd.read_csv('examples/stock_px_2.csv',
                           parse_dates=True, index_col=0)
close_px = close_px_all[['AAPL', 'MSFT', 'XOM']]
close_px = close_px.resample('B').ffill()
```


```python
close_px.AAPL.plot()
close_px.AAPL.rolling(250).mean().plot()
```


    <matplotlib.axes._subplots.AxesSubplot at 0x22fac2bcc88>


![png](https://github.com/yosarawut/e-Library/raw/master/img/output_127_1.png)



```python
plt.figure()
```



```py
    <Figure size 432x288 with 0 Axes>

    <Figure size 432x288 with 0 Axes>
```


```python
appl_std250 = close_px.AAPL.rolling(250, min_periods=10).std()
appl_std250[5:12]
appl_std250.plot()
```



```py
    <matplotlib.axes._subplots.AxesSubplot at 0x22faf3d2470>
```



![png](https://github.com/yosarawut/e-Library/raw/master/img/output_129_1.png)



```python
expanding_mean = appl_std250.expanding().mean()
```


```python
plt.figure()
```




    <Figure size 432x288 with 0 Axes>

    <Figure size 432x288 with 0 Axes>



```python
close_px.rolling(60).mean().plot(logy=True)
```
    <matplotlib.axes._subplots.AxesSubplot at 0x22faf4f1748>




![png](https://github.com/yosarawut/e-Library/raw/master/img/output_132_1.png)



```python
close_px.rolling('20D').mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>MSFT</th>
      <th>XOM</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2003-01-02</th>
      <td>7.400000</td>
      <td>21.110000</td>
      <td>29.220000</td>
    </tr>
    <tr>
      <th>2003-01-03</th>
      <td>7.425000</td>
      <td>21.125000</td>
      <td>29.230000</td>
    </tr>
    <tr>
      <th>2003-01-06</th>
      <td>7.433333</td>
      <td>21.256667</td>
      <td>29.473333</td>
    </tr>
    <tr>
      <th>2003-01-07</th>
      <td>7.432500</td>
      <td>21.425000</td>
      <td>29.342500</td>
    </tr>
    <tr>
      <th>2003-01-08</th>
      <td>7.402000</td>
      <td>21.402000</td>
      <td>29.240000</td>
    </tr>
    <tr>
      <th>2003-01-09</th>
      <td>7.391667</td>
      <td>21.490000</td>
      <td>29.273333</td>
    </tr>
    <tr>
      <th>2003-01-10</th>
      <td>7.387143</td>
      <td>21.558571</td>
      <td>29.238571</td>
    </tr>
    <tr>
      <th>2003-01-13</th>
      <td>7.378750</td>
      <td>21.633750</td>
      <td>29.197500</td>
    </tr>
    <tr>
      <th>2003-01-14</th>
      <td>7.370000</td>
      <td>21.717778</td>
      <td>29.194444</td>
    </tr>
    <tr>
      <th>2003-01-15</th>
      <td>7.355000</td>
      <td>21.757000</td>
      <td>29.152000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2011-10-03</th>
      <td>398.002143</td>
      <td>25.890714</td>
      <td>72.413571</td>
    </tr>
    <tr>
      <th>2011-10-04</th>
      <td>396.802143</td>
      <td>25.807857</td>
      <td>72.427143</td>
    </tr>
    <tr>
      <th>2011-10-05</th>
      <td>395.751429</td>
      <td>25.729286</td>
      <td>72.422857</td>
    </tr>
    <tr>
      <th>2011-10-06</th>
      <td>394.099286</td>
      <td>25.673571</td>
      <td>72.375714</td>
    </tr>
    <tr>
      <th>2011-10-07</th>
      <td>392.479333</td>
      <td>25.712000</td>
      <td>72.454667</td>
    </tr>
    <tr>
      <th>2011-10-10</th>
      <td>389.351429</td>
      <td>25.602143</td>
      <td>72.527857</td>
    </tr>
    <tr>
      <th>2011-10-11</th>
      <td>388.505000</td>
      <td>25.674286</td>
      <td>72.835000</td>
    </tr>
    <tr>
      <th>2011-10-12</th>
      <td>388.531429</td>
      <td>25.810000</td>
      <td>73.400714</td>
    </tr>
    <tr>
      <th>2011-10-13</th>
      <td>388.826429</td>
      <td>25.961429</td>
      <td>73.905000</td>
    </tr>
    <tr>
      <th>2011-10-14</th>
      <td>391.038000</td>
      <td>26.048667</td>
      <td>74.185333</td>
    </tr>
  </tbody>
</table>
<p>2292 rows × 3 columns</p>
</div>



### Exponentially Weighted Functions


```python
plt.figure()
```




    <Figure size 432x288 with 0 Axes>

    <Figure size 432x288 with 0 Axes>



```python
aapl_px = close_px.AAPL['2006':'2007']
ma60 = aapl_px.rolling(30, min_periods=20).mean()
ewma60 = aapl_px.ewm(span=30).mean()
ma60.plot(style='k--', label='Simple MA')
ewma60.plot(style='k-', label='EW MA')
plt.legend()
```




    <matplotlib.legend.Legend at 0x22faf6b9710>




![png](https://github.com/yosarawut/e-Library/raw/master/img/output_136_1.png)


### Binary Moving Window Functions


```python
plt.figure()
```



```py
<Figure size 432x288 with 0 Axes>
<Figure size 432x288 with 0 Axes>
```


```python
spx_px = close_px_all['SPX']
spx_rets = spx_px.pct_change()
returns = close_px.pct_change()
```


```python
corr = returns.AAPL.rolling(125, min_periods=100).corr(spx_rets)
corr.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x22faf7f5550>




![png](https://github.com/yosarawut/e-Library/raw/master/img/output_140_1.png)



```python
plt.figure()
```



```py
<Figure size 432x288 with 0 Axes>

<Figure size 432x288 with 0 Axes>
```


```python
corr = returns.rolling(125, min_periods=100).corr(spx_rets)
corr.plot()
```



```py
<matplotlib.axes._subplots.AxesSubplot at 0x22faf7fe358>
```



![png](https://github.com/yosarawut/e-Library/raw/master/img/output_142_1.png)


### User-Defined Moving Window Functions


```python
plt.figure()
```



```py
<Figure size 432x288 with 0 Axes>

<Figure size 432x288 with 0 Axes>

```

```python
from scipy.stats import percentileofscore
score_at_2percent = lambda x: percentileofscore(x, 0.02)
result = returns.AAPL.rolling(250).apply(score_at_2percent)
result.plot()
```

   
    




    <matplotlib.axes._subplots.AxesSubplot at 0x22fb1406c88>




![png](https://github.com/yosarawut/e-Library/raw/master/img/output_145_2.png)



```python
pd.options.display.max_rows = PREVIOUS_MAX_ROWS
```

## Conclusion

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMDcyNjgxNzAsMTg2MDI1OTM3OSwtNz
k0ODgwNTI3XX0=
-->