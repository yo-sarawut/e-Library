
Pandas Groupby Tutorial
===

> [Source : ](http://www.pybloggers.com/2018/12/python-pandas-groupby-tutorial/).

In this Pandas group by we are going to learn how to organize  [Pandas](https://pandas.pydata.org/) dataframes by groups. More specifically, we are going to learn how to group by one and multiple columns. Furthermore, we are going to learn how calculate some basics summary statistics (e.g., mean, median), convert Pandas groupby to dataframe, calculate the percentage of observations in each group, and many more useful things.

-   More about working with Pandas:  [Pandas Dataframe Tutorial](https://www.marsja.se/pandas-dataframe-read-csv-excel-subset/)

First of all we are going to import pandas as pd, and read a CSV file, using the read_csv method, to a dataframe. In the example below, we use _index_col=0_  because the first row in the dataset is the index column.
```py
import pandas as pd

data_url = 'http://vincentarelbundock.github.io/Rdatasets/csv/carData/Salaries.csv'
df = pd.read_csv(data_url, index_col=0)

df.head()
```
## ![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepython-pandas-groupby-exp-25c8755367b765f276486f1e3690092de0afe3f2.jpg)

We used Pandas head to se the first 5 rows of our dataframe. In the image above we can see that we have, at least, three variables that we can group our data by. That is, we can group our data by “rank”, “discipline”, and “sex”. Of course, we could also group it by yrs.since.phd or yrs.service but it may be a lot of groups. As previously mentioned we are going to use Pandas groupby to group a dataframe based on one, two, three, or more columns.

Data can be loaded from other file formats as well (e.g., Excel, HTML, JSON):

-   [Pandas Excel Tutorial: How to Read and Write Excel Files](https://www.marsja.se/pandas-excel-tutorial-how-to-read-and-write-excel-files/)
-   [Explorative Data Analysis with Pandas, SciPy, and Seaborn](https://www.marsja.se/explorative-data-analysis-with-pandas-scipy-and-seaborn/) includes a short introduction to Pandas _read_html_

## Python Pandas Groupby Example

We are starting with the simplest example; grouping by one column. In the Pandas groupby example below we are going to group by the column “rank”.

There are many different methods that we can use on Pandas groupby objects (and Pandas dataframe objects). All available methods on a Python object can be found using this code:
```py
import IPython

# Grouping by one factor
df_rank = df.groupby('rank')

# Getting all methods from the groupby object:
meth = [method_name for method_name in dir(df_rank)
 if callable(getattr(df_rank, method_name)) & ~method_name.startswith('_')]

# Printing the result
print(IPython.utils.text.columnize(meth))
```
![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepython-pandas-groupby-obj-afd86d7b4d24cd44af18f6a77c46c876bf113fcc.jpg)

Note, that in the code example above we also import IPython to print the list in columns. In the following examples we are going to use some of these methods. First, we can print out the groups by using the _groups_  method to get a dictionary of groups:
```py
df_rank.groups
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-dictionary-53a1b4cb232a6c6215bc094e018a2a6783fc7555.jpg)](https://www.marsja.se/wp-content/uploads/2018/12/groupby-pandas-dictionary-of-groups.jpg)

We can also use the groupby method _get_group_  to filter the grouped data. In the next code example we are going to select the Assistant Professor group (i.e., “AsstProf”).
```py
# Get group
df_rank.get_group('AsstProf').head()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sehow-to-use-python-pandas-e95a6eebcdfb1fba6674fa3d26358d8b02ed7606.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sehow-to-use-python-pandas-e95a6eebcdfb1fba6674fa3d26358d8b02ed7606.jpg)

### Pandas Groupby Count

If we want to find out how big each group is (e.g., how many observations in each group), we can use use .size() to count the number of rows in each group:
```py
df_rank.size()
```
```py
# Output:
#
# rank
# AssocProf     64
# AsstProf      67
# Prof         266
# dtype: int64
```
Additionally, we can also use Pandas groupby count method to count by group(s) and get the entire dataframe. If we don’t have any missing values the number should be the same for each column and group. Thus, this is a way we can explore the dataset and see if there are any missing values in any column.
```py
df_rank.count()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-count-pyth-f374a61332609c0f0fd15361fbdfe0bc52d64edd.jpg)](https://www.marsja.se/wp-content/uploads/2018/12/pandas-groupby-count-python.jpg)

That was how to use Pandas size to count the number of rows in each group. We will return to this, later, when we are grouping by multiple columns. Now we are going to In some cases we may want to find out the number of unique values in each group. This can be done using the groupby method  _nunique_:

df_rank.nunique()

![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-one-column-0885722f4dd7578053af162ff7e0789cc3e482f4.jpg)

As can be seen in the the last column (salary) there are 63 Associate Professors, 53 Assistant Proffessors, and 261 Professors in the dataset. In this example we have a complete dataset and we can see that some have the same salary (e.g., there are 261 unique values in the column salary for Professors). As we will see if we have missing values in the dataframe we would get a different result. In the next example we are using Pandas  _mask_ method together with NumPy’s  [_random.random_](https://docs.scipy.org/doc/numpy-1.15.0/reference/generated/numpy.random.random.html)  to insert missing values (i.e., np.NaN) in 10% of the dataframe:
```py
df_null = df.mask(np.random.random(df.shape) < .1)
df_null.isnull().sum().reset_index(name='N Missing Values')
```
![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-count-missing-valu-ebba62184a9f628cae05cb36dae5cb0b6540f771.jpg)

Note, we used the  _reset_index_ method above to get the multi-level indexed grouped dataframe to become a single indexed. In the particular example, above, we used the parameter _name_  to name the count column (“N Missing Values”). This parameter, however, can only be used on Pandas series objects and not dataframe objects.

That said, let’s return to the example; if we run the same code as above (counting unique values by group) we can see that it will not count missing values:
```py
df_null.groupby('rank').nunique()
```
![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-grouping-b-9ecda6447f765eb8015d13b5b53592a3a8a1f5a9.jpg)

That is, we don’t get the same numbers in the two tables because of the missing values. In the following examples we are going to work with Pandas groupby to calculate the mean, median, and standard deviation by one group.

### Pandas Groupby Mean

If we want to calculate the mean salary grouped by one column (rank, in this case) it’s simple. We just use Pandas _mean_ method on the grouped dataframe:
```py
df_rank['salary'].mean().reset_index()
```
![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.secalculate-mean-by-categor-7890d4a672ffbae5208ab9da79e26ef85a9e10f6.jpg)

Having a column named salary may not be useful. For instance, if someone else are going to see the table they may not know that it’s the mean salary for each group. Luckily, we can add the _rename_  method to the above code to rename the columns of the grouped data:
```py
df_rank['salary'].mean().reset_index().rename(
    columns={'rank':'Rank','salary' : 'Mean Salary'})
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepython-groupby-mean-panda-a17ede4ce143264589e5a24bdb808e8a56fbb56b.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepython-groupby-mean-panda-a17ede4ce143264589e5a24bdb808e8a56fbb56b.jpg)

### **Median Score of a Group Using the groupby Method in Pandas**

Now lets group by disciplne of the academic and find the median salary in the next Pandas groupby example
```py
df.groupby('rank')['salary'].median().reset_index().rename(
    columns={'rank':'Rank','salary' : 'MedianSalary'})
```
[![](https://www.marsja.se/wp-content/uploads/2018/12/how-to-use-pandas-groupby-and-get-median.jpg)](https://www.marsja.se/wp-content/uploads/2018/12/how-to-use-pandas-groupby-and-get-median.jpg)

### Aggregate Data by Group using Pandas Groupby

Most of the time we want to have our summary statistics in the same table. We can calculate the mean and median salary, by groups, using the  _agg_  method. In this next Pandas groupby example we are also adding the minimum and maximum salary by group (rank):
```py
df_rank['salary'].agg(['mean', 'median', 
                                  'std', 'min', 'max']).reset_index()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-aggregate-bc5cd75d44f39d9379242ea66d0ea1b151ff32cf.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-aggregate-bc5cd75d44f39d9379242ea66d0ea1b151ff32cf.jpg)

A very neat thing with Pandas agg method is that we can write custom functions and pass them along. Let’s say that we wanted, instead of having one column for min salary and one column for max salary, to have a column with salary range:
```py
def salary_range(df):
    mini = df.min()
    maxi = df.max()
    rang = '%s - %s' % (mini, maxi)
    
    return rang

df_descriptive = df_rank['salary'].agg(['mean', 'median', 'std', salary_range]).reset_index()
```
Here, however, the output will have the name of the methods/functions used. That is, we will have a column named ‘salary_range’ and we are going to rename this column:
```py
# Renaming Pandas Dataframe Columns
```py
df_descriptive.rename(columns={'rank':'Rank', 'mean':'Mean', 'median':'Median', 
                               'std':'Standard Deviation', 'salary_range':'Range'})
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-custom-function-r-484aad53a46a29aaebe0ac6355dc1e4bb9b5573a.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-custom-function-r-484aad53a46a29aaebe0ac6355dc1e4bb9b5573a.jpg)

Furthermore, it’s possible to use methods from other Python packages such as SciPy and NumPy. For instance, if we wanted to calculate the harmonic and geometric mean we can use SciPy:

from scipy.stats.mstats import gmean, hmean

df_descriptive = df_rank['salary'].agg(['mean', 'median', hmean, gmean]).reset_index()
df_descriptive

More about doing descriptive statistics using Pyton:

-   [Descriptive Statistics using Python and Pandas](https://www.marsja.se/pandas-python-descriptive-statistics/)
-   [How to do Descriptive Statistics in Python using Numpy](https://www.marsja.se/how-to-python-descriptives-statistics-numpy/)

## Pandas Groupby Multiple Columns

In this section we are going to continue using Pandas groupby but grouping by many columns. In the first example we are going to group by two columns and the we will continue with grouping by two columns, ‘discipline’ and ‘rank’. To use Pandas groupby with multiple columns we add a list containing the column names. In the example below we also count the number of observations in each group:
```py
df_grp = df.groupby(['rank', 'discipline'])
df_grp.size().reset_index(name='count')
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-two-column-f11924c0311d2c68a71b529ee7510b4e0190bab5.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-two-column-f11924c0311d2c68a71b529ee7510b4e0190bab5.jpg)

Again, we can use the get_group method to select groups. However, in this case we have to input a tuple and select two groups:
```py
# Get two groups
df_grp.get_group(('AssocProf', 'A')).head()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segrouping-by-two-columns-p-e3079707f696dcb722acdb0ec23cc884f4fa0b09.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segrouping-by-two-columns-p-e3079707f696dcb722acdb0ec23cc884f4fa0b09.jpg)

## Pandas Groupby Count Multiple Groups

In the next groupby example we are going to calculate the number of observations in three groups (i.e., “n”). We have to start by grouping by “rank”, “discipline” and “sex” using groupby. As with the previous example (groupby one column) we use the method size to calculate the **n**  and reset_index, with the parameter _name=”n”_, to get the series to a dataframe:
```py
df_3grps = df.groupby(['rank', 'discipline', 'sex'])
df_n_per_group = df_3grps.size().reset_index(name='n')
```
Now we can continue and calculate the percentage of men and women in each rank and discipline. In this, and the next, Pandas groupby example we are going to use the _apply_  method together with the [_lambda_](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions)  function.
```py
perc = df.groupby(['rank', 'discipline', 'sex'])['salary'].size()

# Give the percentage on the level of Rank:
percbyrank = perc.groupby(level=0).apply(lambda x: 100 * x / float(x.sum()))

print(percbyrank)
print('Total percentage in group AssocProf. ',
      percbyrank.reset_index().query('rank == "AssocProf"')['salary'].sum())
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-percentage-bbead0c6a191c3400e244018e2ca82f2f794bd2f.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.segroupby-pandas-percentage-bbead0c6a191c3400e244018e2ca82f2f794bd2f.jpg)

Note, in the last line of code above we calculate the total of % for the group AssocProf and it’s 100, which is good. We are going to continue with calculating the percentage of men and women in each group (i.e., rank and discipline). In the next code we have to summarize the total **n** (n=397). We can, for instance, see that there are more male professors regardless of discipline.
```py
n = perc.reset_index()['salary'].sum()
totalperc =  perc.groupby(level=0).apply(lambda x: 100 * x / N).reset_index(name='% of total n')
totalperc.reset_index()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.secalculate-percentage-by-g-db241b5985ae299732a3b89f40a4d2142f67d304.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.secalculate-percentage-by-g-db241b5985ae299732a3b89f40a4d2142f67d304.jpg)

### How to convert a Pandas groupby to Dataframe

When dealing with multiple groups and Pandas groupby we get a GroupByDataFrame object. Let’s use _type_  to see what type a grouped object have:
```py
df_rn = df.groupby(['rank', 'discipline']).mean()
```
Furthermore, if we use the _index_  method we can see that it is MultiIndex:
```py
df_rn.index
```
[![](https://www.marsja.se/wp-content/uploads/2018/12/pandas-multiindex-grouped-by-gender.jpg)](https://www.marsja.se/wp-content/uploads/2018/12/pandas-multiindex-grouped-by-gender.jpg)

It’s easy to convert the Pandas groupby to dataframe; we have actually already done it. In this example, however, we are going to calculate the mean values per the three groups. Furthermore, we are going to add a suffix to each column and use reset_index to get a dataframe.
```py
df_rn = df_rn.add_suffix('_Mean').reset_index()
type(df_rn)

# Output: pandas.core.frame.DataFrame
```
## Pandas groupby agg with Multiple Groups

In this last section we are going use agg, again. We are not going into detail on how to use mean, median, and other methods to get summary statistics, however. This is because it’s basically the same as for grouping by n groups and it’s better to get all the summary statistics in one table.

That is, we are going to calculate mean, median, and standard deviation using the agg method. In this groupby example we are also adding the summary statistics (i.e., “mean”, “median”, and “std”) to each column. Otherwise we will get a multi-level indexed result like the image below:

[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-aggregate-ea0562c7abe98f927d9354b8b831e1b17bbf26f9.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-aggregate-ea0562c7abe98f927d9354b8b831e1b17bbf26f9.jpg)

If we use Pandas _columns_ and the method  _ravel_  together with list comprehension we can add the suffixes to our column name and get another table. Note, in the example code below we only print the first 7 columns. In fact, with many columns it may be better to keep the result multi-level indexed.
```py
df_stats = df.groupby(['rank', 'discipline', 'sex']).agg(['mean', 'median', 'std'])
df_stats.columns = ["_".join(x) for x in df_stats.columns.ravel()]

df_stats.iloc[:,0:6].reset_index()
```
[![](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-multiple-c-db167f775ed1497b33d98e9a1317b8d3a7f3f4f8.jpg)](http://www.pybloggers.com/wp-content/uploads/2018/12/www.marsja.sepandas-groupby-multiple-c-db167f775ed1497b33d98e9a1317b8d3a7f3f4f8.jpg)

Note, if we wanted an output as the first image we just remove the second line above (“df_stats.columns = …”). Additionally, as previous mentioned, we can also use custom functions, NumPy and SciPy methods when working with groupby agg. Just scroll back up and look at those examples, for grouping by one column, and apply them to the data grouped by multiple columns. More information of the different methods and objects used here can be found in the  [Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/).

## Conclusion:

In this Pandas groupby tutorial we have learned how to use Pandas groupby to:

-   group one or many columns
-   count observations using the methods count and size
-   calculate simple summary statistics using:
    -   groupby mean, median, std
    -   groupby agg (aggregate)
    -   agg with our own function
-   Calculate the percentage of observations in different groups

The post  [Python Pandas Groupby Tutorial](https://www.marsja.se/python-pandas-groupby-tutorial-examples/)  appeared first on  [Erik Marsja](https://www.marsja.se/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0Njk1MzA3NF19
-->