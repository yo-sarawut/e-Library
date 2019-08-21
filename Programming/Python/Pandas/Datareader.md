Pandas Datareader
===

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NTUwMTc5MzZdfQ==
-->