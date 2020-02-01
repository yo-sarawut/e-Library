Introduction to the Financial Time Series Analysis using Pandas - Part 1
As defined in Investopedia A time series is a sequence of numerical data points in successive order. Generally, observation points are successively equally spaced in time. Most of the financial data is in the time series format and hence "Financial Time Series Analysis" is an important tool for anyone trying to understand the historical movements, predict the future movements or manage the risk associated with the future movements.

Through this tutorial, we are providing tools that are neccessary to get access to the financial data and perform a preliminary analysis and visualization to understand the data better.

By the end of this tutorial you will be capable of doing the following tasks:
1. Download and Know your data

Load data of any financial instrument using Quandl's Python package
Know your data
2. Plot Time Series data

Plot the stock price data
Plot subplot for price and volume traded
Normalize the time series to see how your investment grew
3. Returns Calculation

Calculate simple return
Calculate and plot the daily returns
Calculate the Compound Annual Growth Rate(CAGR)
4. Volatility Calculation

Calculate the annualized volatility
Calculate and plot the rolling volatilty
Relationship between Vol and returns
5. Correlation Calculation

Generate pair-wise plot and analyse
Generate correlation metrics
6. Returns Distribution and Analysis

Plot the return distribution
Normality test
7. Monthly plot

Comment on seasonality
8. Digging deep

Calculate and plot the moving average
Perform the drawdown analysis
1. Downloading and Knowing your data
There are multiple sources that provide APIs to download data into your python code directly.
In this tutorial we are using Quandl's free API for sourcing financial data. The pre-requisites for using Quandl API are:

Register on Quandl and generate API key.
Install Quandl package in python and import the same.
Note: For further information please refer to link Quandl for Python

Importing Packages
Before jumping into the actual code, the first step is to import all the packages that will be used in this tutorial.

Load live data of any financial instrument using Quandl's Python package.
The data can be downloaded by specifying following parameters to the get function of Quandl

Ticker for which the data is required
Start date for the time series
End date for the time series
Quandl API key for aunthentication
The data will be downloaded as a pandas DataFrame, which will have the dates as index and market data such as Open, High, Low, Close prices, Shares Traded and Turnover (Rs. Cr) as columns.

Lets start with downloading NIFTY50 Index data
To know more about NIFTY50 click here.

We can print first 5 rows of our data by using "head" function. This helps us to have a quick look at the structure of the data downloaded.

               Open     High      Low    Close  Shares Traded  \
Date                                                            
2010-01-04  5200.90  5238.45  5167.10  5232.20    148652424.0   
2010-01-05  5277.15  5288.35  5242.40  5277.90    240844424.0   
2010-01-06  5278.15  5310.85  5260.05  5281.80    216147837.0   
2010-01-07  5281.80  5302.55  5244.75  5263.10    181246734.0   
2010-01-08  5264.25  5276.75  5234.70  5244.75    201910800.0   

            Turnover (Rs. Cr)  
Date                           
2010-01-04            6531.61  
2010-01-05            7969.62  
2010-01-06            7892.60  
2010-01-07            6890.99  
2010-01-08            7777.04  
Printing basic information about about your data
info function gives list of column names in pandas dataframe, their data type and number of non 'NaN' values.
describe function provides basic statistics such as count, mean, std, min/max etc. for each column

***************Basic information about data downloaded***************
<class 'pandas.core.frame.DataFrame'>
DatetimeIndex: 2111 entries, 2010-01-04 to 2018-06-29
Data columns (total 6 columns):
Open                 2111 non-null float64
High                 2111 non-null float64
Low                  2111 non-null float64
Close                2111 non-null float64
Shares Traded        2093 non-null float64
Turnover (Rs. Cr)    2093 non-null float64
dtypes: float64(6)
memory usage: 115.4 KB
None
***************Data description***************
               Open          High           Low         Close  Shares Traded  \
count   2111.000000   2111.000000   2111.000000   2111.000000   2.093000e+03   
mean    7135.990881   7172.192492   7090.158361   7131.309332   1.727730e+08   
std     1779.522933   1779.082316   1775.820220   1777.239695   5.805946e+07   
min     4623.150000   4623.150000   4531.150000   4544.200000   6.555703e+06   
25%     5530.525000   5564.650000   5486.650000   5530.825000   1.353542e+08   
50%     6530.000000   6562.850000   6497.650000   6526.650000   1.628396e+08   
75%     8470.825000   8505.850000   8423.425000   8471.825000   1.989305e+08   
max    11120.850000  11171.550000  11075.950000  11130.400000   6.291986e+08   

       Turnover (Rs. Cr)  
count        2093.000000  
mean         7656.236885  
std          2854.432124  
min           297.890000  
25%          5782.230000  
50%          7105.680000  
75%          8920.290000  
max         29479.770000  
2. Ploting Time Series data
The first step to understand and analyse financial data is through visualization. By simply ploting the financial timeseries we can get the understanding of how an investment has performed over the time period.

Plot the Stock Price data
The code given below uses the package matplotlib.pyplot to plot the 'Close', 'High' and 'Low' columns of the time series downloaded for NIFTY50 as a line graph. We can customize the chart to show its title, the label for the y axis and its legend.


Plot Subplot for Price and Volume traded
The code given below subsets the timeseries downloaded for NIFTY50 for dates greater than 2017-12-31 and handles the missing values by using the forward fill method. Then it creates 2 subplots, one of which is the line chart for 'Close', 'High' and 'Low', while the second is the line chart for the volume of 'Shares Traded'. Looking at these graphs adjacent to each other helps us in observing the relationship between price movement and volumen traded.


Normalize the Time Series
A financial time series is normalized to observe how an investment of x amount changes with time. It is useful for comparing the performance of multiple time series.

Normalization is done by using the formula given below:

p(t)p(0)∗xfor 0<=t<=T where T is period end date
 
The code given below normalizes and plots the sliced time series to see how an investment of 1000 made in NIFTY50 on 2017-12-31 changes over time.


We will try to repeat the above process but this time with multiple stocks

     ticker       date  adj_close
None                             
0      MSFT 2018-03-27      89.47
1      MSFT 2018-03-26      93.78
2      MSFT 2018-03-23      87.18
3      MSFT 2018-03-22      89.79
4      MSFT 2018-03-21      92.48
We need to process above dataframe further to get desired format

ticker	AAPL	F	GM	MSFT
date				
2012-01-03	52.848787	8.772734	18.035831	22.792249
2012-01-04	53.132802	8.906729	18.121512	23.332995
2012-01-05	53.722681	9.135309	18.995457	23.571435
2012-01-06	54.284287	9.229893	19.638064	23.933352
2012-01-09	54.198183	9.300832	19.569519	23.622529
This time we will try Plotly to plot interactive plots.


Its difficult to compare the performane of different underlying give they all are trading at different levels. Normalisation as discussed above will help to compare performance of these 4 stocks.


3. Returns Calculation
The return of a financial instrument is the profit/loss incurred on an investment over a period of time, expressed as a proportion of the original investment. It gives a complete, scale-free summary of the investment opportunity.

The simple single period return of financial instrument is calculated using the formula given below

R(t)=P(f)P(i)−1where P(i) and P(f) are the prices at the starting time point and ending time point of the period
The code given below calculates the simple return for the period between 2017-12-31 and 2018-06-30

Nifty returns for period starting from 2017-12-31 till 2018-06-30 is 2.67%
Simple Daily Return
The daily return is the day over day return.

The underlying formula for calculating simple daily return is

R(t)=(P(t)P(t−1)−1)for 0<=t<=T 
 
The code given below calculates the daily returns using the pandas dataframe function pct_change. We also calculated the mean daily simple return, which comes out to be close to zero. This tells the importance of compounding effect.

The return series hence obtained is first plotted as a line chart and then as a histogram to observe its underlying distribution. From histogram we can observe that return distribution is bell shaped and similar to famous normal distribution.

Avg daily return is 0.038790%


Logarithmic Return / Continuously Compounded Return
The logarithmic return or continuously compounded return, D(t), is calculated using the formula

D(t)=log(P(f)P(i))where P(i) and P(f) are the initial and the final prices of the instrumentD(t)=log(R(t)+1)where R(t) is the simple return during the period
The advantages of using log returns over simple returns are as follows:

The logarithmic returns are symmetric in nature, as opposed to simple returns.
In case the prices are distributed log-normally, log(1+R(t)) is distributed normally.
The log returns are additive in nature.
The code given below calculates the log returns using the log function from the numpy library. Instead of calculating log returns from scratch, we have used simple returns timeseries to calculate log returns.

The returns hence obtained are plotted as a histogram to observe the distribution of these returns. As we can observe the log returns distribution is also bell shaped and similar to normal distibution.


Compound Annual Growth Rate (CAGR)
The Compound Annual Growth Rate (CAGR) is the mean annual growth rate of an investment over a specified period of time longer than one year. It describes the rate at which an investment would have grown, if it had grown at a steady rate, which doesn't ususally happen in reality. CAGR can be essentially viewed as a way to smooth out an investment’s returns so that they may be more easily understood.

The formula for calculating CAGR is

R(t)=(P(f)P(i))(1n)−1where P(f) and P(i) are the final and the initial values for a period and n is the time in years 
CAGR is a relatively simple metric and hence has a variety of uses.

CAGR can be used to calculate the average growth of a single investment
It can be used to compare investments of different types with one another. For example it can be used to compare an investment in risk free instrument with an investment in a portfolio with varying growth rate
It can also be used to track the performance of various business measures of one or multiple companies alongside one another
The code given below illustrates how CAGR can be calculated.

Compound annual growth rate from 2010-01-04 to 2018-06-29 for NSE/NIFTY_50 is 8.81%
4. Volatility Calculation
Annualized Volatility
Annualised volatility is the degree of variation observed in the prices of a financial instrument over a period of one year. It can be calculated by scaling the daily volatility, which is measured as the standard deviation of the returns of the stock prices, to 1 year. The daily volatility can be scaled to annual by simply multiplying with  252−−−√  (considering that there are 252 business days in a year) in case it is calculated as the standard deviation of the log returns.

The code given below calcluates annualised volatility by calculating the standard deviation of log returns of NIFTY50 using pandas dataframe function std and then multiplying it by  252−−−√ .

Annualized daily volatility from 2010-01-04 to 2018-06-29 for NSE/NIFTY_50 is 15.58%
N-days Rolling Volatility
N-days rolling volatility is calculated by rolling the dates for a window of N days and using the corresponding data for calculating the volatility.

The code given below calculates the rolling annualized volatility for NIFTY50 for a window of 252 days using pandas function rolling. The series of rolling volatility hence obtained is plotted on the secondary y-axis, along with index levels plotted on the primary y-axis.


Studying correlation between two stocks

5. Correlation Calculation
ticker	AAPL	F	GM	MSFT
date				
2012-01-04	0.005360	0.015159	0.004739	0.023448
2012-01-05	0.011041	0.025340	0.047100	0.010167
2012-01-06	0.010400	0.010301	0.033270	0.015237
2012-01-09	-0.001587	0.007656	-0.003497	-0.013072
2012-01-10	0.003574	0.000000	0.017362	0.003598

ticker	AAPL	F	GM	MSFT
ticker				
AAPL	1.000000	0.295965	0.282291	0.356120
F	0.295965	1.000000	0.692737	0.329482
GM	0.282291	0.692737	1.000000	0.323293
MSFT	0.356120	0.329482	0.323293	1.000000
6. Return Distribution Analysis
Through below excercises we are comparing NIFTY50 log returns ditribution with Normal distribution using various methods.

Many simple models assume underlying distribution to be normal and hence it is very important for us to understand the distribution of our data to develop an understanding about the challenges posed when the data is run on models having Normality as an assumption.

Read more about Normal distribution here

Quantile-Quantile Plot (Q-Q Plot)
The quantile-quantile (q-q) plot is a graphical technique for determining if two data sets come from populations with a common distribution, such as Normal, Exponential,etc. It is created by plotting two sets of quantiles against one another. If both sets of quantiles came from the same distribution, we should see the points forming a line that’s roughly straight. Normal q-q plot is used more frequently in practice due to so many statistical methods assuming normality. For creating the plot, the quantile of our sample data is plotted against the quantile calculated from a theoretical distribution. A 45-degree reference line is also plotted to see the alignment.

The normal q-q plot for sample data belonging to a skewed distribution will from a curve instead of a straight line. On the other hand, the normal q-q plot for a distribution with heavy tails will have points fall along a line in the middle of the graph, but curved off in the extremities.

The code given below calculates the z-score for the daily log returns and then plots its quantile against that of a theoretical normal distribution to generate the Normal Q-Q Plot.


The above Normal Q-Q plot indicates that the distribution of the log returns is heavy tailed.

Kurtosis and Skewness
Kurtosis — Kurtosis is a measure of the combined weight of a distribution's tails relative to the center of the distribution. It esssentially tells us whether the data is heavy-tailed or light-tailed relative to a normal distribution. The kurtosis of any univariate normal distribution is 3. Distributions with kurtosis less than 3 are said to be platykurtic, while those with kurtosis greater than 3 are said to be leptokurtic. In python, the kurtosis can be calculated using the kurtosis function of pandas. This, however, calculates the excess Kurtosis(Kurtosis expressed as above or below 3), as it assumes the Fisher's definition of Kurtosis, whereby Kurtosis of Normal distribution is equal to 0.

Skewness — Skewness is a measure of symmetricity of the distribution and can be mathematically defined as the averaged cubed deviation from the mean divided by the standard deviation cubed. If the result of the computation is greater than zero, the distribution is positively skewed. If it's less than zero, it's negatively skewed. If equal to zero, it's roughly symmetric. Normal distrbution has a skewness measure of zero. The funtion skew of pandas can be used to calculate the skewness of a distribution.

Excess Kurtosis of distribution of NSE/NIFTY_50 daily returns is 1.756
Skewness of distribution of NSE/NIFTY_50 daily returns is -0.195
JB Test for Normality
The Jarque-Bera Test (JB Test) is a test for Normality. Specifically, the test matches the skewness and kurtosis of data to see if it matches a Normal distribution.

The JB test tests the hypothesis

Ho : Data is Normal

Ha : Data is NOT Normal

using the test statistic

JBTestStat=n(Skewness^26+ExcessKurtosis^224)where n is the sample size
If data came from a Normal distriubtion, the test statistic would assume the value zero.

Note that this test only works for a large enough number of data samples (>2000) as the test statistic asymptotically has a Chi-squared distribution with 2 degrees of freedom.

The code given below calculates the JB test statistic and its corresponding p-value for the distribution using the function jarque_bera from scipy.stats

JB test statistic calculated for NSE/NIFTY_50 daily returns is 284.384
JB test statistic for NSE/NIFTY_50 daily returns is 282.208
p-value for JB test for NSE/NIFTY_50 daily returns is 0.000
The p-value of 0.0 implies that we reject the null hypothesis of distribution of log returns of NSE/NIFTY_50 being normal with 95% confidence level
7. Heatmap and Seasonality
Monthly Returns as a Heatmap
A heatmap is a graphical representation of matrix data where the individual values contained are represented as colors.

The code given below plots the monthly returns against their respective years in the form of a heatmap. It is done by first resampling the daily data as monthly, by taking the last published value of the month. Using these end of month levels, we calculate the monthly return, which is then grouped by 'Year' and 'Month'. The matrix hence obtained is plotted as a heatmap using the function heatmap of the library seaborn.

The colour scheme of the map highlights the high positive returns towards the green side of the spectrum, while high negative returns are towards the red side.


Value
Date		
2010	Jan	NaN
Feb	0.094303
Mar	0.046789
Apr	0.031396
May	-0.140235
8. Digging deep
N-days Moving Average
N-days moving average is calculated by rolling the dates for a window of N days at a time and using the corresponding data for calculating the volatility.

The code given below calculates and plots the 20-day and 120-day moving average for NIFTY50 using the pandas rolling function.


Drawdown Analysis
A drawdown is the peak-to-trough decline during a specific recorded period of an investment, fund or commodity security. It is usually quoted as the percentage between the peak and the subsequent trough and it respresents the downside risk. Drawdowns help determine an investment's financial risk by evaluating recovery-period, which is the time taken for the investment to recover from a decline in its net asset value back to the peak.

The code given below calculates the Maximum Rolling Drawdown for a window of 250 days, which is essentially the largest percentage loss a hypothetical investor could have incurred on the investment over a period of 250 days. It also calculates the recovery period and finally highlights the maximum drawdown period and recovery period, along with the plots for maximum rolling drawdown and index closing levels.


The code given below calculates the Max Drawdown dates and the period start and end date. It also evaluates the Max Drawdown percentage, and the recovery period and completion time.

Max Drawdown period for NSE/NIFTY_50 was between 2010-11-05 to 2011-12-20
Recovery was completed at 2013-11-03 post drawdown
Max Drawdown Percentage  = -28.012103%
Max Drawdown period = 410 days
Max Drawdown recovery period = 684 days

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwNDkyNDg5XX0=
-->