
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



> Written with [StackEdit](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzA3ODgxMDVdfQ==
-->