Unsupervised Learning to Market Behavior Forecasting
===
[Source:](https://towardsdatascience.com/unsupervised-learning-to-market-behavior-forecasting-ee8f78650415)

![enter image description here](https://miro.medium.com/max/4000/1*WqRCG-RXEM3y2jkG-q-9ug.jpeg)

# Introduction

The market data is a sequence called time series. Usually, researchers use only price data (or asset returns) to create a model that forecasts the next price value, movement direction, or other output. I think the better way is to use more data for that. The idea is try to combine versatile market conditions (volatility, volumes, price changes, and etc.)

The first type of potential features are the various derivatives of price data. The second type is the set of the volume derivatives.

> These features will describe the current market condition more complex than raw market data or simple returns.

You will see these features in the next part of the article. As for the modeling, we will use Hidden Markov Model.

Hidden Markov Model (HMM) is a statistical Markov model in which the system being modeled is assumed to be a Markov process with unobserved (i.e. hidden) states. Observed data is our market features, hidden states are our market behavior.

> Our goal is to interpret the hidden state after the modeling, and create the trading strategy based on this knowledge.

The basic figure of Hidden Markov Model looks like this

![](https://miro.medium.com/max/30/1*QEaCiq4SqBVaOrowmT67bw.png?q=20)

![](https://miro.medium.com/max/850/1*QEaCiq4SqBVaOrowmT67bw.png)

Hidden Markov Model

This article is practice-oriented. For more information you read the introduction to Hidden Markov Model in  [this](https://towardsdatascience.com/introduction-to-hidden-markov-models-cd2c93e6b781)  article by  [Tomer Amit](https://medium.com/u/d520265687a?source=post_page-----ee8f78650415----------------------). Also, I recommend to start with this video

----------

# Feature Engineering and Modeling

I think combing of code and explanation is a good approach to dive into the research. Let’s start coding.

Our libraries
``` py
import quandl
import numpy as np
import pandas as pd
import statsmodels.api as sm
from scipy import stats
from matplotlib import cm, pyplot as plt
from hmmlearn.hmm import GaussianHMM
import scipy
import datetime
import json
import seaborn as sns
from sklearn.externals import joblib
``` 
This code downloads data for BTC/USD from Quandl
```py 
start_date_string = '2014-04-01'
asset = 'BITFINEX/BTCUSD'
column_price = 'Last'
column_high = 'High'
column_low = 'Low'
column_volume = 'Volume'

quandl.ApiConfig.api_key = YOUR_QUANDL_API
dataset = quandl.get(asset, collapse = 'daily',
                     trim_start = start_date_string)
dataset = dataset.shift(1)
``` 
Then we can to plot the price and volume data
```py
plt.figure(figsize=(20,10))
plt.plot(dataset[column_price])
plt.title(asset)
plt.show()
```
After that we are getting this figure

![](https://miro.medium.com/max/30/1*-hgGZirH5rZwRqUxOKUaPA.png?q=20)

![](https://miro.medium.com/max/1176/1*-hgGZirH5rZwRqUxOKUaPA.png)

Price for BTC/USD from 01/01/2014

![](https://miro.medium.com/max/30/1*AkOqj7YYmt8icrVu6VSdzQ.png?q=20)

![](https://miro.medium.com/max/1182/1*AkOqj7YYmt8icrVu6VSdzQ.png)

Volume for BTC/USD from 01/01/2014

Now we are ready for coding the feature engineering and modeling functions.
```py
# Brute force modelling
def get_best_hmm_model(X, max_states, max_iter = 10000):
    best_score = -(10 ** 10)
    best_state = 0
    
    for state in range(1, max_states + 1):
        hmm_model = GaussianHMM(n_components = state, random_state = 100,
                                covariance_type = "diag", n_iter = max_iter).fit(X)
      if hmm_model.score(X) > best_score:
            best_score = hmm_model.score(X)
            best_state = state
    
best_model = GaussianHMM(n_components = best_state, random_state = 100,
   covariance_type = "diag", n_iter = max_iter).fit(X)
    return best_model
# Normalized st. deviation
def std_normalized(vals):
return np.std(vals) / np.mean(vals)
# Ratio of diff between last price and mean value to last price
def ma_ratio(vals):
    return (vals[-1] - np.mean(vals)) / vals[-1]

# z-score for volumes and price
def values_deviation(vals):
    return (vals[-1] - np.mean(vals)) / np.std(vals)
 ```   
Let’s split off the train period as a period before 01/01/2018. The next code runs the feature engineering and visualizes it.


After that, we are getting the five new time series and the trained model.

![](https://miro.medium.com/max/30/1*fUCr4UMHMgBAp3E201yg1Q.png?q=20)

![](https://miro.medium.com/max/1072/1*fUCr4UMHMgBAp3E201yg1Q.png)

Feature sequences

In the code above, we also created the  _future_return_ column that shifted by one lag for  _last_return_. This is the  **first key**  to understand the hidden states. Let’s plot this value as a cumulative sum by each state.

![](https://miro.medium.com/max/30/1*MkHCesyIRh3fil1wChwoFg.png?q=20)

![](https://miro.medium.com/max/1072/1*MkHCesyIRh3fil1wChwoFg.png)

Future return cumulative sum for each state

As we see, state #0 has the tendency to downside direction. State #1 doesn’t have a clear tendency. The last state #2 has a strong tendency to upside direction. This simple trick with a cumulative sum  _future_return_ allows us to understand how each state corresponds to the next price movement.

The  **second key**  is to research each state by features. After that, we can relate these two events (future movement and current condition). Let’s code simulation and visualization for features of each state.

![](https://miro.medium.com/max/30/1*RRcLqdr-PPxwMLz6Ncf-aA.png?q=20)

![](https://miro.medium.com/max/1075/1*RRcLqdr-PPxwMLz6Ncf-aA.png)

Feature distributions for each state

Now you can see how each state describes the current state. E.g., states #0 and #2 have a high volume deviation, it means that these states often presented on high volume, and state #1 on low one. Also, states #0 and #2 often presented on high volatility.

The interesting fact is state #0 has the low values for  _last_return_  and  _ma_ratio._ Probably_, the state #0_ corresponds to downside current condition (at the present). The backward situation is for state #2.

The interpretation of that two conclusions is

> If the market has the current state #0 we have mostly downside market condition (second key) at the current situation, and this tendency will go on (first key).
> 
> If the market has the current state #1 we have the uncertainty for the tendency.
> 
> If the market has the current state #2 we have mostly upside market condition (second key) at the current situation, and this tendency will go on (first key).

The next line of code saves the trained model into the file.

----------

# Application

Let’s try to create the trading strategy based on this knowledge. The strategy we should test since 01/01/2018, because this period out of the sample.

> The logic is simple: short when state #0, no position when state #1, long when state #2.

Our strategy will be implemented using  [Catalyst](https://enigma.co/catalyst/)  framework. In this  [post](https://medium.com/@sermal/adaptive-trend-following-trading-strategy-based-on-renko-9248bf83554), I demonstrated a quick introduction to Catalyst. The strategy will be contained in separated py-file. Let’s code basic functions and include the libraries

The main parameters, model loading are contained in the  _initialize_  function

The basic logic contained in handle_data function. This function runs every minute. The main activities are getting data, feature creating, market behavior estimating, and position management.

The last function is additional. We plot the figures and print the result.

Let’s run the strategy

As we see, the suggested algorithm straight beats the benchmark. It seems the strategy tries to catch the trend and following it. The bad condition for the strategy is no trend period.

![](https://miro.medium.com/max/30/1*jUweaRcpb13ykHbuXeSExA.png?q=20)

![](https://miro.medium.com/max/868/1*jUweaRcpb13ykHbuXeSExA.png)

Backtesting result
``` py
> Total return: 1.4889661611137708
> 
> Sortino coef: 1.8800527725096972
> 
> Max drawdown: -0.30508556497453887
> 
> alpha: 0.5672854146797404
> 
> beta: -0.1541654082608784
``` 
Alpha is positive, beta is very close to 0 (see this  [post](https://medium.com/@sermal/how-to-develop-a-stock-market-analytical-tool-using-shiny-and-r-c2385e0d2f89)  for the definition of these criteria). The drawdown is too high, but it much lower than drawdown of the benchmark.

----------

# Conclusion

1.  Suggested the approach based on the versatile price and volume features as sequences.
2.  Carried out the interpretation of hidden states of the model.
3.  Built the model using Hidden Markov Model on data for 4 years.
4.  Created the simple trading strategy that tested on out of the sample data (1.5 years) without retraining, commission and slippage included.
5.  The strategy beats the buy & hold benchmark, and it has positive alpha and beta is close to 0.
6.  The research artifacts are uploaded to GitHub
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzQ3NzkzMTVdfQ==
-->