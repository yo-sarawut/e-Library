
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

So this simple investing strategy would yield a total return of more than 325% in the course of almost 16 years.

How does this translate to a yearly performance? Since we have kept all weekdays in our portfolio, there are 52×5=260 weekdays each year. There are 4435 days in our simulation which corresponds roughly to 16.92 years. We will be calculating the average geometric return, that is an average return r¯ which when compounded for 16.92 years will produce the total relative return of 325.14%. So we need to solve:

```py
# Calculating the time-related parameters of the simulation
days_per_year = 52 * 5
total_days_in_simulation = data.shape[0]
number_of_years = total_days_in_simulation / days_per_year

# The last data point will give us the total portfolio return
total_portfolio_return = total_relative_returns[-1]
# Average portfolio return assuming compunding of returns
average_yearly_return = (1 + total_portfolio_return)**(1 / number_of_years) - 1

print('Total portfolio return is: ' +
      '{:5.2f}'.format(100 * total_portfolio_return) + '%')
print('Average yearly return is: ' +
      '{:5.2f}'.format(100 * average_yearly_return) + '%')
```
Total portfolio return is: 325.14% Average yearly return is: **8.85%**

What next?
Our strategy is a very simple example of a buy-and-hold strategy. The investor simply splits up the available funds in the three assets and keeps the same position throughout the period under investigation. Although simple, the strategy does produce a healthy 8.85% per year.

However, the simulation is not completely accurate. Let us not forget that we have used ALL weekdays in our example, but we do know that on some days the markets are not trading. This will not affect the strategy we presented as the returns on the days the markets are closed are 0, but it may potentially affect other types of strategies. Furthermore, the weights here are constant over time. Ideally, we would like weights that change over time so that we can take advantage of price swings and other market events.

Also, we have said nothing at all about the risk of this strategy. Risk is the most important consideration in any investment strategy and is closely related to the expected returns. In what follows, we will start designing a more complex strategy, the weights of which will not be constant over time. At the same time we will start looking into the risk of the strategy and present appropriate metrics to measure it. Finally, we will look into the issue of optimizing the strategy parameters and how this can improve our return to risk profile.

See Part 3 of this series: Moving Average Trading Strategies.
> Written with [StackEdit](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTM3NjM1MTM4LDg0MzI4OTE1M119
-->