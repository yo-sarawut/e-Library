
# Python for Finance, Part 2: Intro to Quantitative Trading Strategies

In  [Python for Finance, Part I](http://www.learndatasci.com/python-finance-part-yahoo-finance-api-pandas-matplotlib/), we focused on using Python and Pandas to

1.  retrieve financial time-series from free online sources (Yahoo),
2.  format the data by filling missing observations and aligning them,
3.  calculate some simple indicators such as rolling moving averages and
4.  visualise the final time-series.

As a reminder, the dataframe containing the three “cleaned” price timeseries has the following format:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style='darkgrid', context='talk', palette='Dark2')

data = pd.read_pickle('./data.pkl')
data.head(10)
```
| Date |AAPL |MSFT |^GSPC |
|-----|-----|-----|-----|
| 03/01/2000 |3.625643 |39.33463 |1455.219971 |
| 04/01/2000 |3.319964 |38.0059 |1399.420044 |
| 05/01/2000 |3.36854 |38.406628 |1402.109985 |
| 06/01/2000 |3.077039 |37.12008 |1403.449951 |
| 07/01/2000 |3.222794 |37.60517 |1441.469971 |
| 10/01/2000 |3.166112 |37.879354 |1457.599976 |
| 11/01/2000 |3.004162 |36.90917 |1438.560059 |
| 12/01/2000 |2.823993 |35.706986 |1432.25 |
| 13/01/2000 |3.133722 |36.381896 |1449.680054 |
| 14/01/2000 |3.253159 |37.879354 |1465.150024 |

has the following format:
```py
# Calculating the short-window moving average
short_rolling = data.rolling(window=20).mean()
short_rolling.head()
has the following format:
```
```py
# Calculating the short-window moving average
long_rolling = data.rolling(window=100).mean()
long_rolling.tail()
```
| Date |AAPL |MSFT |^GSPC |
|-----|-----|-----|-----|
| 26/12/2016 |110.958205 |58.41818 |2176.628791 |
| 27/12/2016 |111.047874 |58.476117 |2177.50018 |
| 28/12/2016 |111.1405889 |58.532936 |2178.24449 |
| 29/12/2016 |111.233698 |58.586112 |2178.879189 |
| 30/12/2016 |111.31527 |58.63526 |2179.42699 |

## General considerations about trading strategies

There are several ways one can go about when a trading strategy is to be developed. One approach would be to use the price time-series directly and work with numbers that correspond to some monetary value.

For example, a researcher could be working with time-series expressing the price of a given stock, like the time-series we used in the previous article. Similarly, if working with fixed income instruments, e.g. bonds, one could be using a time-series expressing the price of the bond as a percentage of a given reference value, in this case the par value of the bond. Working with this type of time-series can be more intuitive as people are used to thinking in terms of prices. However, price time-series have some drawbacks. Prices are usually only positive, which makes it harder to use models and approaches which require or produce negative numbers. In addition, price time-series are usually non-stationary, that is their statistical properties are less stable over time.

An alternative approach is to use time-series which correspond not to actual values but changes in the monetary value of the asset. These time-series can and do assume negative values and also, their statistical properties are usually more stable than the ones of price time-series. The most frequently used forms used are relative returns defined as

rrelative(t)=p(t)−p(t−1)p(t−1)rrelative(t)=p(t)−p(t−1)p(t−1)

and log-returns defined as

r(t)=log(p(t)p(t−1))r(t)=log⁡(p(t)p(t−1))

where  p(t)p(t)  is the price of the asset at time  tt. For example, if  p(t)=101p(t)=101  and  p(t−1)=100p(t−1)=100  then  rrelative(t)=101−100100=1%rrelative(t)=101−100100=1%.

There are several reasons why log-returns are being used in the industry and some of them are related to long-standing assumptions about the behaviour of asset returns and are out of our scope. However, what we need to point out are two quite interesting properties. Log-returns are additive and this facilitates treatment of our time-series, relative returns are not. We can see the additivity of log-returns in the following equation.

r(t1)+r(t2)=log(p(t1)p(t0))+log(p(t2)p(t1))=log(p(t2)p(t0))r(t1)+r(t2)=log⁡(p(t1)p(t0))+log⁡(p(t2)p(t1))=log⁡(p(t2)p(t0))

which is simply the log-return from  t0t0  to  t2t2. Secondly, log-returns are approximately equal to the relative returns for values of  p(t)p(t−1)p(t)p(t−1)  sufficiently close to  11. By taking the 1st order Taylor expansion of  log(p(t)p(t−1))log⁡(p(t)p(t−1))  around  11, we get

log(p(t)p(t−1))≃log(1)+p(t)p(t−1)−1=rrelative(t)log⁡(p(t)p(t−1))≃log⁡(1)+p(t)p(t−1)−1=rrelative(t)

Both of these are trivially calculated using Pandas:
```py
# Relative returns 
returns = data.pct_change(1) 
returns.head()
```

> Written with [StackEdit](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4ODYxNDM3MjZdfQ==
-->