# 03\_variable-representing-univariate-data

## 3 Representing Univariate Data with the Series

## Configuring pandas

```python
# import numpy and pandas
import numpy as np
import pandas as pd

# used for dates
import datetime
from datetime import datetime, date

# Set some pandas options controlling output format
pd.set_option('display.notebook_repr_html', False)
pd.set_option('display.max_columns', 8)
pd.set_option('display.max_rows', 10)
pd.set_option('display.width', 80)

# bring in matplotlib for graphics
import matplotlib.pyplot as plt
%matplotlib inline
```

## Creating a Series using

Python lists and dictionaries

```python
# create a series of multiple values from a list
s = pd.Series([10, 11, 12, 13, 14])
s
```

```text
0    10
1    11
2    12
3    13
4    14
dtype: int64
```

```python
# value stored at index label 3
s[3]
```

```text
13
```

```python
# create a Series of alphas
pd.Series(['Mike', 'Marcia', 'Mikael', 'Bleu'])
```

```text
0      Mike
1    Marcia
2    Mikael
3      Bleu
dtype: object
```

```python
# a sequence of 5 values, all 2
pd.Series([2]*5)
```

```text
0    2
1    2
2    2
3    2
4    2
dtype: int64
```

```python
# use each character as a value
pd.Series(list('abcde'))
```

```text
0    a
1    b
2    c
3    d
4    e
dtype: object
```

```python
# create Series from dict
pd.Series({'Mike': 'Dad', 
           'Marcia': 'Mom', 
           'Mikael': 'Son', 
           'Bleu': 'Best doggie ever' })
```

```text
Bleu      Best doggie ever
Marcia                 Mom
Mikael                 Son
Mike                   Dad
dtype: object
```

## Creation using NumPy functions

```python
# 4 through 8
pd.Series(np.arange(4, 9))
```

```text
0    4
1    5
2    6
3    7
4    8
dtype: int64
```

```python
# 0 through 9
pd.Series(np.linspace(0, 9, 5))
```

```text
0    0.00
1    2.25
2    4.50
3    6.75
4    9.00
dtype: float64
```

```python
# random numbers
np.random.seed(12345) # always generate the same values
# 5 normally random numbers
pd.Series(np.random.normal(size=5))
```

```text
0   -0.204708
1    0.478943
2   -0.519439
3   -0.555730
4    1.965781
dtype: float64
```

## Creation using a scalar value

```python
# create a one item Series
s = pd.Series(2)
s
```

```text
0    2
dtype: int64
```

```python
# create the Series
s = pd.Series(np.arange(0, 5))
# multiple all values by 2
s * 2
```

```text
0    0
1    2
2    4
3    6
4    8
dtype: int64
```

## The .index and .values properties

```python
# get the values in the Series
s = pd.Series([1, 2, 3])
s.values
```

```text
array([1, 2, 3])
```

```python
# show that this is a numpy array
type(s.values)
```

```text
numpy.ndarray
```

```python
# get the index of the Series
s.index
```

```text
RangeIndex(start=0, stop=3, step=1)
```

## The size and shape of a Series

```python
# example series
s = pd.Series([0, 1, 2, 3])
len(s)
```

```text
4
```

```python
# .size is also the # of items in the Series
s.size
```

```text
4
```

```python
# .shape is a tuple with one value
s.shape
```

```text
(4,)
```

## Specifying an index at creation

```python
# explicitly create an index
labels = ['Mike', 'Marcia', 'Mikael', 'Bleu']
role = ['Dad', 'Mom', 'Son', 'Dog']
s = pd.Series(labels, index=role)
s
```

```text
Dad      Mike
Mom    Marcia
Son    Mikael
Dog      Bleu
dtype: object
```

```python
# examine the index
s.index
```

```text
Index(['Dad', 'Mom', 'Son', 'Dog'], dtype='object')
```

```python
# who is the Dad?
s['Dad']
```

```text
'Mike'
```

## Heads, tails and takes

```python
# a ten item Series
s = pd.Series(np.arange(1, 10), 
              index=list('abcdefghi'))
```

```python
# show the first five
s.head()
```

```text
a    1
b    2
c    3
d    4
e    5
dtype: int64
```

```python
# the first three
s.head(n = 3) # s.head(3) is equivalent
```

```text
a    1
b    2
c    3
dtype: int64
```

```python
# the last five
s.tail()
```

```text
e    5
f    6
g    7
h    8
i    9
dtype: int64
```

```python
# the last 3
s.tail(n = 3) # equivalent to s.tail(3)
```

```text
g    7
h    8
i    9
dtype: int64
```

```python
# only take specific items by position
s.take([1, 5, 8])
```

```text
b    2
f    6
i    9
dtype: int64
```

## Lookup by label using the \[\] and .ix\[\] operators

```python
# we will use this series to examine lookups
s1 = pd.Series(np.arange(10, 15), index=list('abcde'))
s1
```

```text
a    10
b    11
c    12
d    13
e    14
dtype: int64
```

```python
# get the value with label 'a'
s1['a']
```

```text
10
```

```python
# get multiple items
s1[['d', 'b']]
```

```text
d    13
b    11
dtype: int64
```

```python
# gets values based upon position
s1[[3, 1]]
```

```text
d    13
b    11
dtype: int64
```

```python
# to demo lookup by matching labels as integer values
s2 = pd.Series([1, 2, 3, 4], index=[10, 11, 12, 13])
s2
```

```text
10    1
11    2
12    3
13    4
dtype: int64
```

```python
# this is by label not position
s2[[13, 10]]
```

```text
13    4
10    1
dtype: int64
```

## Explicit position lookup with .iloc\[\]

```python
# explicitly  by position
s1.iloc[[0, 2]]
```

```text
a    10
c    12
dtype: int64
```

```python
# explicitly  by position
s2.iloc[[3, 2]]
```

```text
13    4
12    3
dtype: int64
```

## Explicit label lookup with .loc\[\]

```python
# explicit via labels
s1.loc[['a', 'd']]
```

```text
a    10
d    13
dtype: int64
```

```python
# get items at position 11 an d12
s2.loc[[11, 12]]
```

```text
11    2
12    3
dtype: int64
```

```python
# -1 and 15 will be NaN
s1.loc[['a', 'f']]
```

```text
a    10.0
f     NaN
dtype: float64
```

## Slicing a Series into subsets

```python
# a Series to use for slicing
# using index labels not starting at 0 to demonstrate 
# position based slicing
s = pd.Series(np.arange(100, 110), index=np.arange(10, 20))
s
```

```text
10    100
11    101
12    102
13    103
14    104
15    105
16    106
17    107
18    108
19    109
dtype: int64
```

```python
# slice showing items at position 1 thorugh 5
s[1:6]
```

```text
11    101
12    102
13    103
14    104
15    105
dtype: int64
```

```python
# lookup via list of positions
s.iloc[[1, 2, 3, 4, 5]]
```

```text
11    101
12    102
13    103
14    104
15    105
dtype: int64
```

```python
# items at position 1, 3, 5
s[1:6:2]
```

```text
11    101
13    103
15    105
dtype: int64
```

```python
# first five by slicing, same as .head(5)
s[:5]
```

```text
10    100
11    101
12    102
13    103
14    104
dtype: int64
```

```python
# fourth position to the end
s[4:]
```

```text
14    104
15    105
16    106
17    107
18    108
19    109
dtype: int64
```

```python
# every other item in the first five positions
s[:5:2]
```

```text
10    100
12    102
14    104
dtype: int64
```

```python
# every other item starting at the fourth position
s[4::2]
```

```text
14    104
16    106
18    108
dtype: int64
```

```python
# reverse the Series
s[::-1]
```

```text
19    109
18    108
17    107
16    106
15    105
14    104
13    103
12    102
11    101
10    100
dtype: int64
```

```python
# every other starting at position 4, in reverse
s[4::-2]
```

```text
14    104
12    102
10    100
dtype: int64
```

```python
# -4:, which means the last 4 rows
s[-4:]
```

```text
16    106
17    107
18    108
19    109
dtype: int64
```

```python
# :-4, all but the last 4
s[:-4]
```

```text
10    100
11    101
12    102
13    103
14    104
15    105
dtype: int64
```

```python
# equivalent to s.tail(4).head(3)
s[-4:-1]
```

```text
16    106
17    107
18    108
dtype: int64
```

```python
# used to demonstrate the next two slices
s = pd.Series(np.arange(0, 5), 
              index=['a', 'b', 'c', 'd', 'e'])
s
```

```text
a    0
b    1
c    2
d    3
e    4
dtype: int64
```

```python
# slices by position as the index is characters
s[1:3]
```

```text
b    1
c    2
dtype: int64
```

```python
# this slices by the strings in the index
s['b':'d']
```

```text
b    1
c    2
d    3
dtype: int64
```

## Alignment via index labels

```python
# First series for alignment
s1 = pd.Series([1, 2], index=['a', 'b'])
s1
```

```text
a    1
b    2
dtype: int64
```

```python
# Second series for alignment
s2 = pd.Series([4, 3], index=['b', 'a'])
s2
```

```text
b    4
a    3
dtype: int64
```

```python
# add them
s1 + s2
```

```text
a    4
b    6
dtype: int64
```

```python
# multiply all values in s3 by 2
s1 * 2
```

```text
a    2
b    4
dtype: int64
```

```python
# scalar series using s3's index
t = pd.Series(2, s1.index)
t
```

```text
a    2
b    2
dtype: int64
```

```python
# multiply s1 by t
s1 * t
```

```text
a    2
b    4
dtype: int64
```

```python
# we will add this to s1
s3 = pd.Series([5, 6], index=['b', 'c'])
s3
```

```text
b    5
c    6
dtype: int64
```

```python
# s1 and s3 have different sets of index labels
# NaN will result for a and c
s1 + s3
```

```text
a    NaN
b    7.0
c    NaN
dtype: float64
```

```python
# 2 'a' labels
s1 = pd.Series([1.0, 2.0, 3.0], index=['a', 'a', 'b'])
s1
```

```text
a    1.0
a    2.0
b    3.0
dtype: float64
```

```python
# 3 a labels
s2 = pd.Series([4.0, 5.0, 6.0, 7.0], index=['a', 'a', 'c', 'a'])
s2
```

```text
a    4.0
a    5.0
c    6.0
a    7.0
dtype: float64
```

```python
# will result in 6 'a' index labels, and NaN for b and c
s1 + s2
```

```text
a    5.0
a    6.0
a    8.0
a    6.0
a    7.0
a    9.0
b    NaN
c    NaN
dtype: float64
```

## Boolean selection

```python
# which rows have values that are > 5?
s = pd.Series(np.arange(0, 5), index=list('abcde'))
logical_results = s >= 3
logical_results
```

```text
a    False
b    False
c    False
d     True
e     True
dtype: bool
```

```python
# select where True
s[logical_results]
```

```text
d    3
e    4
dtype: int64
```

```python
# a little shorter version
s[s > 5]
```

```text
Series([], dtype: int64)
```

```python
# commented as it throws an exception
# s[s >= 2 and s < 5]
```

```python
# correct syntax
s[(s >=2) & (s < 5)]
```

```text
c    2
d    3
e    4
dtype: int64
```

```python
# are all items >= 0?
(s >= 0).all()
```

```text
True
```

```python
# any items < 2?
s[s < 2].any()
```

```text
True
```

```python
# how many values < 2?
(s < 2).sum()
```

```text
2
```

## Reindexing a Series

```python
# sample series of five items
np.random.seed(123456)
s = pd.Series(np.random.randn(5))
s
```

```text
0    0.469112
1   -0.282863
2   -1.509059
3   -1.135632
4    1.212112
dtype: float64
```

```python
# change the index
s.index = ['a', 'b', 'c', 'd', 'e']
s
```

```text
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
e    1.212112
dtype: float64
```

```python
# a series that we will reindex
np.random.seed(123456)
s1 = pd.Series(np.random.randn(4), ['a', 'b', 'c', 'd'])
s1
```

```text
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
dtype: float64
```

```python
# reindex with different number of labels
# results in dropped rows and/or NaN's
s2 = s1.reindex(['a', 'c', 'g'])
s2
```

```text
a    0.469112
c   -1.509059
g         NaN
dtype: float64
```

```python
# different types for the same values of labels
# causes big trouble
s1 = pd.Series([0, 1, 2], index=[0, 1, 2])
s2 = pd.Series([3, 4, 5], index=['0', '1', '2'])
s1 + s2
```

```text
0   NaN
1   NaN
2   NaN
0   NaN
1   NaN
2   NaN
dtype: float64
```

```python
# reindex by casting the label types
# and we will get the desired result
s2.index = s2.index.values.astype(int)
s1 + s2
```

```text
0    3
1    5
2    7
dtype: int64
```

```python
# fill with 0 instead of NaN
s2 = s.copy()
s2.reindex(['a', 'f'], fill_value=0)
```

```text
a    0.469112
f    0.000000
dtype: float64
```

```python
# create example to demonstrate fills
s3 = pd.Series(['red', 'green', 'blue'], index=[0, 3, 5])
s3
```

```text
0      red
3    green
5     blue
dtype: object
```

```python
# forward fill example
s3.reindex(np.arange(0,7), method='ffill')
```

```text
0      red
1      red
2      red
3    green
4    green
5     blue
6     blue
dtype: object
```

```python
# backwards fill example
s3.reindex(np.arange(0,7), method='bfill')
```

```text
0      red
1    green
2    green
3    green
4     blue
5     blue
6      NaN
dtype: object
```

## Modifying a Series in-place

```python
# generate a Series to play with
np.random.seed(123456)
s = pd.Series(np.random.randn(3), index=['a', 'b', 'c'])
s
```

```text
a    0.469112
b   -0.282863
c   -1.509059
dtype: float64
```

```python
# change a value in the Series
# this is done in-place
# a new Series is not returned that has a modified value
s['d'] = 100
s
```

```text
a      0.469112
b     -0.282863
c     -1.509059
d    100.000000
dtype: float64
```

```python
# modify the value at 'd' in-place
s['d'] = -100
s
```

```text
a      0.469112
b     -0.282863
c     -1.509059
d   -100.000000
dtype: float64
```

```python
# remove a row / item
del(s['a'])
s
```

```text
b     -0.282863
c     -1.509059
d   -100.000000
dtype: float64
```

```python
copy = s.copy() # preserve s
slice = copy[:2] # slice with first two rows
slice
```

```text
b   -0.282863
c   -1.509059
dtype: float64
```

```python
# change item with label 10 to 1000
slice['b'] = 0
# and see it in the source
copy
```

```text
b      0.000000
c     -1.509059
d   -100.000000
dtype: float64
```

