
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


Both of these are trivially calculated using Pandas:
```py
# Relative returns 
returns = data.pct_change(1) 
returns.head()
```
```py
# Log returns - First the logarithm of the prices is taken and the the difference of consecutive (log) observations
log_returns = np.log(data).diff()
log_returns.head()
```
```py
fig, (ax1, ax2) = plt.subplots(2, 1, figsize=(16,12))

for c in log_returns:
    ax1.plot(log_returns.index, log_returns[c].cumsum(), label=str(c))

ax1.set_ylabel('Cumulative log returns')
ax1.legend(loc='best')

for c in log_returns:
    ax2.plot(log_returns.index, 100*(np.exp(log_returns[c].cumsum()) - 1), label=str(c))

ax2.set_ylabel('Total relative returns (%)')
ax2.legend(loc='best')

plt.show()
```
![enter image description here](https://storage.googleapis.com/lds-media/images/aapl_msft_gspc_returns.width-1200.png)


> Written with [StackEdit](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODQzMjg5MTUzXX0=
-->