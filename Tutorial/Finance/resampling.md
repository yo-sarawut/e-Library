Resample
===
```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
```
```
df = pd.read_csv('walmart_stock.csv')
```
```
df.head()
```
```
         Date       Open       High        Low      Close    Volume  Adj Close
0  2012-01-03  59.970001  61.060001  59.869999  60.330002  12668800  52.619235
1  2012-01-04  60.209999  60.349998  59.470001  59.709999   9593300  52.078475
2  2012-01-05  59.349998  59.619999  58.369999  59.419998  12768200  51.825539
3  2012-01-06  59.419998  59.450001  58.869999  59.000000   8069400  51.459220
4  2012-01-09  59.029999  59.549999  58.919998  59.180000   6679300  51.616215
```
```
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1258 entries, 0 to 1257
Data columns (total 7 columns):
Date         1258 non-null object
Open         1258 non-null float64
High         1258 non-null float64
Low          1258 non-null float64
Close        1258 non-null float64
Volume       1258 non-null int64
Adj Close    1258 non-null float64
dtypes: float64(5), int64(1), object(1)
memory usage: 63.9+ KB
```
## Create a date index from the date column
```
df['Date'] = df['Date'].apply(pd.to_datetime)
```
```
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1258 entries, 0 to 1257
Data columns (total 7 columns):
Date         1258 non-null datetime64[ns]
Open         1258 non-null float64
High         1258 non-null float64
Low          1258 non-null float64
Close        1258 non-null float64
Volume       1258 non-null int64
Adj Close    1258 non-null float64
dtypes: datetime64[ns](1), float64(5), int64(1)
memory usage: 68.8 KB
```
```
df.head()
```
```
         Date       Open       High        Low      Close    Volume  Adj Close
0  2012-01-03  59.970001  61.060001  59.869999  60.330002  12668800  52.619235
1  2012-01-04  60.209999  60.349998  59.470001  59.709999   9593300  52.078475
2  2012-01-05  59.349998  59.619999  58.369999  59.419998  12768200  51.825539
3  2012-01-06  59.419998  59.450001  58.869999  59.000000   8069400  51.459220
4  2012-01-09  59.029999  59.549999  58.919998  59.180000   6679300  51.616215
```
```
df.set_index('Date',inplace=True)
df.head()
```
```py
                 Open       High        Low      Close    Volume  Adj Close
Date                                                                       
2012-01-03  59.970001  61.060001  59.869999  60.330002  12668800  52.619235
2012-01-04  60.209999  60.349998  59.470001  59.709999   9593300  52.078475
2012-01-05  59.349998  59.619999  58.369999  59.419998  12768200  51.825539
2012-01-06  59.419998  59.450001  58.869999  59.000000   8069400  51.459220
2012-01-09  59.029999  59.549999  58.919998  59.180000   6679300  51.616215
```

<table border="1" class="docutils">
<colgroup>
<col width="13%" />
<col width="87%" />
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Alias</th>
<th class="head">Description</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td>B</td>
<td>business day frequency</td>
</tr>
<tr class="row-odd"><td>C</td>
<td>custom business day frequency (experimental)</td>
</tr>
<tr class="row-even"><td>D</td>
<td>calendar day frequency</td>
</tr>
<tr class="row-odd"><td>W</td>
<td>weekly frequency</td>
</tr>
<tr class="row-even"><td>M</td>
<td>month end frequency</td>
</tr>
<tr class="row-odd"><td>SM</td>
<td>semi-month end frequency (15th and end of month)</td>
</tr>
<tr class="row-even"><td>BM</td>
<td>business month end frequency</td>
</tr>
<tr class="row-odd"><td>CBM</td>
<td>custom business month end frequency</td>
</tr>
<tr class="row-even"><td>MS</td>
<td>month start frequency</td>
</tr>
<tr class="row-odd"><td>SMS</td>
<td>semi-month start frequency (1st and 15th)</td>
</tr>
<tr class="row-even"><td>BMS</td>
<td>business month start frequency</td>
</tr>
<tr class="row-odd"><td>CBMS</td>
<td>custom business month start frequency</td>
</tr>
<tr class="row-even"><td>Q</td>
<td>quarter end frequency</td>
</tr>
<tr class="row-odd"><td>BQ</td>
<td>business quarter endfrequency</td>
</tr>
<tr class="row-even"><td>QS</td>
<td>quarter start frequency</td>
</tr>
<tr class="row-odd"><td>BQS</td>
<td>business quarter start frequency</td>
</tr>
<tr class="row-even"><td>A</td>
<td>year end frequency</td>
</tr>
<tr class="row-odd"><td>BA</td>
<td>business year end frequency</td>
</tr>
<tr class="row-even"><td>AS</td>
<td>year start frequency</td>
</tr>
<tr class="row-odd"><td>BAS</td>
<td>business year start frequency</td>
</tr>
<tr class="row-even"><td>BH</td>
<td>business hour frequency</td>
</tr>
<tr class="row-odd"><td>H</td>
<td>hourly frequency</td>
</tr>
<tr class="row-even"><td>T, min</td>
<td>minutely frequency</td>
</tr>
<tr class="row-odd"><td>S</td>
<td>secondly frequency</td>
</tr>
<tr class="row-even"><td>L, ms</td>
<td>milliseconds</td>
</tr>
<tr class="row-odd"><td>U, us</td>
<td>microseconds</td>
</tr>
<tr class="row-even"><td>N</td>
<td>nanoseconds</td>
</tr>
</tbody>
</table>

```
df.resample(rule='A')
```
```
DatetimeIndexResampler [freq=<YearEnd: month=12>, axis=0, closed=right, label=right, convention=start, base=0]
```
## To find the yearly mean
```
df.resample(rule='A').mean()
```
```
                 Open       High        Low      Close        Volume  \
Date                                                                   
2012-12-31  67.158680  67.602120  66.786520  67.215120  9.239015e+06   
2013-12-31  75.264048  75.729405  74.843055  75.320516  6.951496e+06   
2014-12-31  77.274524  77.740040  76.864405  77.327381  6.515612e+06   
2015-12-31  72.569405  73.064167  72.034802  72.491111  9.040769e+06   
2016-12-31  69.481349  70.019643  69.023492  69.547063  9.371645e+06   

            Adj Close  
Date                   
2012-12-31  59.389349  
2013-12-31  68.147179  
2014-12-31  71.709712  
2015-12-31  68.831426  
2016-12-31  68.054229  
```
**Weekly frequency Means**

df.resample(rule='W').mean().head()

                 Open    High      Low      Close      Volume  Adj Close
Date                                                                    
2012-01-08  59.737499  60.120  59.1450  59.615000  10774925.0  51.995617
2012-01-15  59.298000  59.680  59.0700  59.332001   6983580.0  51.748788
2012-01-22  60.085000  60.530  59.8975  60.369999   8506200.0  52.654120
2012-01-29  61.080000  61.510  60.7220  61.090000   6827240.0  53.282098
2012-02-05  61.702001  62.084  61.2480  61.762000   8693500.0  53.868209

**Calendar day frequency Means**

df.resample(rule='D').mean().head()

                 Open       High        Low      Close      Volume  Adj Close
Date                                                                         
2012-01-03  59.970001  61.060001  59.869999  60.330002  12668800.0  52.619235
2012-01-04  60.209999  60.349998  59.470001  59.709999   9593300.0  52.078475
2012-01-05  59.349998  59.619999  58.369999  59.419998  12768200.0  51.825539
2012-01-06  59.419998  59.450001  58.869999  59.000000   8069400.0  51.459220
2012-01-07        NaN        NaN        NaN        NaN         NaN        NaN

**Business month end frequency Means**

df.resample(rule='BM').mean().head()

                 Open       High        Low      Close        Volume  \
Date                                                                   
2012-01-31  60.159000  60.572000  59.803000  60.235500  8.178850e+06   
2012-02-29  60.935500  61.224000  60.582500  60.898000  9.965725e+06   
2012-03-30  60.309546  60.642273  60.101818  60.433637  8.446464e+06   
2012-04-30  60.073000  60.553000  59.727000  60.149000  1.258940e+07   
2012-05-31  61.173182  61.771819  60.985455  61.456363  1.123173e+07   

            Adj Close  
Date                   
2012-01-31  52.536811  
2012-02-29  53.114637  
2012-03-30  52.983866  
2012-04-30  52.812508  
2012-05-31  54.230701  

**yearly frequency max**

df.resample(rule='A').max().head()

                 Open       High        Low      Close    Volume  Adj Close
Date                                                                       
2012-12-31  77.599998  77.599998  76.690002  77.150002  38007300  68.568371
2013-12-31  81.209999  81.370003  80.820000  81.209999  25683700  73.929868
2014-12-31  87.080002  88.089996  86.480003  87.540001  22812400  81.707680
2015-12-31  90.800003  90.970001  89.250000  90.470001  80898100  84.914216
2016-12-31  74.500000  75.190002  73.629997  74.300003  35076700  73.233524

**yearly frequency min**

df.resample(rule='A').min().head()

                 Open       High        Low      Close   Volume  Adj Close
Date                                                                      
2012-12-31  57.590000  58.430000  57.180000  57.360001  2904800  50.363689
2013-12-31  68.190002  68.669998  67.720001  68.300003  2094900  61.039636
2014-12-31  72.269997  73.099998  72.269997  72.660004  2491800  66.531393
2015-12-31  56.389999  57.060001  56.299999  56.419998  2482800  53.975581
2016-12-31  60.500000  61.490002  60.200001  60.840000  4234400  58.691607

**yearly frequency standard deviation**

df.resample(rule='A').std().head()

               Open      High       Low     Close        Volume  Adj Close
Date                                                                       
2012-12-31  6.089182  6.108822  6.017926  6.043120  4.668863e+06   5.697610
2013-12-31  3.204078  3.181319  3.190823  3.189005  2.784862e+06   3.204453
2014-12-31  3.314478  3.377809  3.275304  3.324339  2.605779e+06   3.411498
2015-12-31  9.702563  9.730657  9.674375  9.724255  6.314777e+06   8.707636
2016-12-31  3.033227  2.884394  3.088522  2.955446  4.322518e+06   3.303628
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2Njg2NDY2NjBdfQ==
-->