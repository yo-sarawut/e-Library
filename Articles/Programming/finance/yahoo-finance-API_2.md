
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




> Written with [StackEdit](https://www.learndatasci.com/tutorials/python-finance-part-2-intro-quantitative-trading-strategies/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMjk1NDY0N119
-->