Pandas Datareader
===
[**Source**](https://riptutorial.com/pandas/topic/1912/pandas-datareader)

## Datareader basic example (Yahoo Finance)


from pandas_datareader import data
```python
# Only get the adjusted close.
aapl = data.DataReader("AAPL", 
                       start='2015-1-1', 
                       end='2015-12-31', 
                       data_source='yahoo')['Adj Close']

>>> aapl.plot(title='AAPL Adj. Closing Price')

```

[![enter image description here](http://i.stack.imgur.com/amLQD.png)](http://i.stack.imgur.com/amLQD.png)

```python
# Convert the adjusted closing prices to cumulative returns.
returns = aapl.pct_change()
>>> ((1 + returns).cumprod() - 1).plot(title='AAPL Cumulative Returns')

```

[![enter image description here](http://i.stack.imgur.com/JiPUS.png)](http://i.stack.imgur.com/JiPUS.png)

## Reading financial data (for multiple tickers) into pandas panel - demo

```python
from datetime import datetime
import pandas_datareader.data as wb

stocklist = ['AAPL','GOOG','FB','AMZN','COP']

start = datetime(2016,6,8)
end = datetime(2016,6,11)

p = wb.DataReader(stocklist, 'yahoo',start,end)

```

`p`  - is a pandas panel, with which we can do funny things:

let's see what do we have in our panel

```python
In [388]: p.axes
Out[388]:
[Index(['Open', 'High', 'Low', 'Close', 'Volume', 'Adj Close'], dtype='object'),
 DatetimeIndex(['2016-06-08', '2016-06-09', '2016-06-10'], dtype='datetime64[ns]', name='Date', freq='D'),
 Index(['AAPL', 'AMZN', 'COP', 'FB', 'GOOG'], dtype='object')]

In [389]: p.keys()
Out[389]: Index(['Open', 'High', 'Low', 'Close', 'Volume', 'Adj Close'], dtype='object')

```

selecting & slicing data

```python
In [390]: p['Adj Close']
Out[390]:
                 AAPL        AMZN        COP          FB        GOOG
Date
2016-06-08  98.940002  726.640015  47.490002  118.389999  728.280029
2016-06-09  99.650002  727.650024  46.570000  118.559998  728.580017
2016-06-10  98.830002  717.909973  44.509998  116.620003  719.409973

In [391]: p['Volume']
Out[391]:
                  AAPL       AMZN        COP          FB       GOOG
Date
2016-06-08  20812700.0  2200100.0  9596700.0  14368700.0  1582100.0
2016-06-09  26419600.0  2163100.0  5389300.0  13823400.0   985900.0
2016-06-10  31462100.0  3409500.0  8941200.0  18412700.0  1206000.0

In [394]: p[:,:,'AAPL']
Out[394]:
                 Open       High        Low      Close      Volume  Adj Close
Date
2016-06-08  99.019997  99.559998  98.680000  98.940002  20812700.0  98.940002
2016-06-09  98.500000  99.989998  98.459999  99.650002  26419600.0  99.650002
2016-06-10  98.529999  99.349998  98.480003  98.830002  31462100.0  98.830002

In [395]: p[:,'2016-06-10']
Out[395]:
            Open        High         Low       Close      Volume   Adj Close
AAPL   98.529999   99.349998   98.480003   98.830002  31462100.0   98.830002
AMZN  722.349976  724.979980  714.210022  717.909973   3409500.0  717.909973
COP    45.900002   46.119999   44.259998   44.509998   8941200.0   44.509998
FB    117.540001  118.110001  116.260002  116.620003  18412700.0  116.620003
GOOG  719.469971  725.890015  716.429993  719.409973   1206000.0  719.409973
```

# _Dividend_ (เงินปันผล)
```python
from pandas_datareader import data

df = data.DataReader('PTT.BK', 'yahoo-dividends')
df
```
```python
[actions, value])
2019-03-06	DIVIDEND	1.200
2018-10-11	DIVIDEND	0.800
2018-03-06	DIVIDEND	1.200
2017-08-31	DIVIDEND	0.800
2017-03-29	DIVIDEND	1.000
2016-08-31	DIVIDEND	0.600
2016-03-03	DIVIDEND	0.400
2015-09-10	DIVIDEND	0.600
2015-03-03	DIVIDEND	0.500
2014-09-15	DIVIDEND	0.600
2014-03-06	DIVIDEND	0.800
2013-09-18	DIVIDEND	0.500
2013-03-06	DIVIDEND	0.800
2012-09-05	DIVIDEND	0.500
2012-03-05	DIVIDEND	0.700
2011-09-06	DIVIDEND	0.500
2011-03-15	DIVIDEND	0.550
2010-09-07	DIVIDEND	0.475
2010-03-04	DIVIDEND	0.450
```




# Dividends and Stock Splits (_+Splits_)
```python
from pandas_datareader import data

df = data.DataReader('PTT.BK', 'yahoo-actions')
df
```
```python
[actions, splits])
2019-03-06	DIVIDEND	1.200
2018-10-11	DIVIDEND	0.800
2018-04-24	SPLIT	10.000
2018-03-06	DIVIDEND	1.200
2017-08-31	DIVIDEND	0.800
2017-03-29	DIVIDEND	1.000
2016-08-31	DIVIDEND	0.600
2016-03-03	DIVIDEND	0.400
2015-09-10	DIVIDEND	0.600
2015-03-03	DIVIDEND	0.500
2014-09-15	DIVIDEND	0.600
2014-03-06	DIVIDEND	0.800
2013-09-18	DIVIDEND	0.500
2013-03-06	DIVIDEND	0.800
2012-09-05	DIVIDEND	0.500
2012-03-05	DIVIDEND	0.700
2011-09-06	DIVIDEND	0.500
2011-03-15	DIVIDEND	0.550
2010-09-07	DIVIDEND	0.475
2010-03-04	DIVIDEND	0.450
```

- [**SIMPLE PYTHON SCRIPT TO RETRIEVE ALL STOCKS DATA FROM GOOGLE FINANCE SCREENER**](https://simply-python.com/2015/09/26/simple-python-script-to-retrieve-all-stocks-data-from-google-finance-screener/)
- [https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/)
- [https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054)
- [https://www.pydoc.io/pypi/pandas-datareader-0.4.0/autoapi/data/index.html](https://www.pydoc.io/pypi/pandas-datareader-0.4.0/autoapi/data/index.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwNDk2MTE4MV19
-->