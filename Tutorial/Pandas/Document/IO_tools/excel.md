---
bookFlatSection: true
title: CSV & Text files
bookToc: true
weight: 3

---
## Excel files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#excel-files "Permalink to this headline")

The  [`read_excel()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html#pandas.read_excel "pandas.read_excel")  method can read Excel 2003 (`.xls`) files using the  `xlrd`  Python module. Excel 2007+ (`.xlsx`) files can be read using either  `xlrd`  or  `openpyxl`. Binary Excel (`.xlsb`) files can be read using  `pyxlsb`. The  [`to_excel()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_excel.html#pandas.DataFrame.to_excel "pandas.DataFrame.to_excel")  instance method is used for saving a  `DataFrame`  to Excel. Generally the semantics are similar to working with  [csv](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-read-csv-table)  data. See the  [cookbook](https://pandas.pydata.org/pandas-docs/stable/user_guide/cookbook.html#cookbook-excel)  for some advanced strategies.

### Reading Excel files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-excel-files "Permalink to this headline")

In the most basic use-case,  `read_excel`  takes a path to an Excel file, and the  `sheet_name`  indicating which sheet to parse.
```py
# Returns a DataFrame
pd.read_excel('path_to_file.xls', sheet_name='Sheet1')
```
#### `ExcelFile`  class[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#excelfile-class "Permalink to this headline")

To facilitate working with multiple sheets from the same file, the  `ExcelFile`  class can be used to wrap the file and can be passed into  `read_excel`  There will be a performance benefit for reading multiple sheets as the file is read into memory only once.
```py
xlsx = pd.ExcelFile('path_to_file.xls')
df = pd.read_excel(xlsx, 'Sheet1')
```
The  `ExcelFile`  class can also be used as a context manager.
```py
with pd.ExcelFile('path_to_file.xls') as xls:
    df1 = pd.read_excel(xls, 'Sheet1')
    df2 = pd.read_excel(xls, 'Sheet2')
```
The  `sheet_names`  property will generate a list of the sheet names in the file.

The primary use-case for an  `ExcelFile`  is parsing multiple sheets with different parameters:
```py
data = {}
# For when Sheet1's format differs from Sheet2
with pd.ExcelFile('path_to_file.xls') as xls:
    data['Sheet1'] = pd.read_excel(xls, 'Sheet1', index_col=None,
                                   na_values=['NA'])
    data['Sheet2'] = pd.read_excel(xls, 'Sheet2', index_col=1)
```
Note that if the same parsing parameters are used for all sheets, a list of sheet names can simply be passed to  `read_excel`  with no loss in performance.
```py
# using the ExcelFile class
data = {}
with pd.ExcelFile('path_to_file.xls') as xls:
    data['Sheet1'] = pd.read_excel(xls, 'Sheet1', index_col=None,
                                   na_values=['NA'])
    data['Sheet2'] = pd.read_excel(xls, 'Sheet2', index_col=None,
                                   na_values=['NA'])

# equivalent using the read_excel function
data = pd.read_excel('path_to_file.xls', ['Sheet1', 'Sheet2'],
                     index_col=None, na_values=['NA'])
```
`ExcelFile`  can also be called with a  `xlrd.book.Book`  object as a parameter. This allows the user to control how the excel file is read. For example, sheets can be loaded on demand by calling  `xlrd.open_workbook()`  with  `on_demand=True`.
```py
import xlrd
xlrd_book = xlrd.open_workbook('path_to_file.xls', on_demand=True)
with pd.ExcelFile(xlrd_book) as xls:
    df1 = pd.read_excel(xls, 'Sheet1')
    df2 = pd.read_excel(xls, 'Sheet2')
```
#### Specifying sheets[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-sheets "Permalink to this headline")

> **Note**
The second argument is  `sheet_name`, not to be confused with  `ExcelFile.sheet_names`.

**Note**
An ExcelFile’s attribute  `sheet_names`  provides access to a list of sheets.

-   The arguments  `sheet_name`  allows specifying the sheet or sheets to read.    
-   The default value for  `sheet_name`  is 0, indicating to read the first sheet    
-   Pass a string to refer to the name of a particular sheet in the workbook.    
-   Pass an integer to refer to the index of a sheet. Indices follow Python convention, beginning at 0.    
-   Pass a list of either strings or integers, to return a dictionary of specified sheets.    
-   Pass a  `None`  to return a dictionary of all available sheets.
    

# Returns a DataFrame
pd.read_excel('path_to_file.xls', 'Sheet1', index_col=None, na_values=['NA'])

Using the sheet index:

# Returns a DataFrame
pd.read_excel('path_to_file.xls', 0, index_col=None, na_values=['NA'])

Using all default values:
```py
# Returns a DataFrame
pd.read_excel('path_to_file.xls')
```
Using None to get all sheets:

# Returns a dictionary of DataFrames
pd.read_excel('path_to_file.xls', sheet_name=None)

Using a list to get multiple sheets:
```py
# Returns the 1st and 4th sheet, as a dictionary of DataFrames.
pd.read_excel('path_to_file.xls', sheet_name=['Sheet1', 3])
```
`read_excel`  can read more than one sheet, by setting  `sheet_name`  to either a list of sheet names, a list of sheet positions, or  `None`  to read all sheets. Sheets can be specified by sheet index or sheet name, using an integer or string, respectively.

#### Reading a  `MultiIndex`[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-a-multiindex "Permalink to this headline")

`read_excel`  can read a  `MultiIndex`  index, by passing a list of columns to  `index_col`  and a  `MultiIndex`  column by passing a list of rows to  `header`. If either the  `index`  or  `columns`  have serialized level names those will be read in as well by specifying the rows/columns that make up the levels.

For example, to read in a  `MultiIndex`  index without names:
```py
In [316]: df = pd.DataFrame({'a': [1, 2, 3, 4], 'b': [5, 6, 7, 8]},
 .....:                  index=pd.MultiIndex.from_product([['a', 'b'], ['c', 'd']]))
 .....: 

In [317]: df.to_excel('path_to_file.xlsx')

In [318]: df = pd.read_excel('path_to_file.xlsx', index_col=[0, 1])

In [319]: df
```
```py
Out[319]: 

     a  b
a c  1  5
  d  2  6
b c  3  7
  d  4  8
```
If the index has level names, they will parsed as well, using the same parameters.
```py
In [320]: df.index = df.index.set_names(['lvl1', 'lvl2'])

In [321]: df.to_excel('path_to_file.xlsx')

In [322]: df = pd.read_excel('path_to_file.xlsx', index_col=[0, 1])

In [323]: df
```
```py
Out[323]: 
           a  b
lvl1 lvl2      
a    c     1  5
     d     2  6
b    c     3  7
     d     4  8
```
If the source file has both  `MultiIndex`  index and columns, lists specifying each should be passed to  `index_col`  and  `header`:
```py
In [324]: df.columns = pd.MultiIndex.from_product([['a'], ['b', 'd']],
 .....:                                        names=['c1', 'c2'])
 .....: 

In [325]: df.to_excel('path_to_file.xlsx')

In [326]: df = pd.read_excel('path_to_file.xlsx', index_col=[0, 1], header=[0, 1])

In [327]: df
```
```py
Out[327]: 
c1         a   
c2         b  d
lvl1 lvl2      
a    c     1  5
     d     2  6
b    c     3  7
     d     4  8

```
#### Parsing specific columns[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#parsing-specific-columns "Permalink to this headline")

It is often the case that users will insert columns to do temporary computations in Excel and you may not want to read in those columns.  `read_excel`  takes a  `usecols`  keyword to allow you to specify a subset of columns to parse.

Deprecated since version 0.24.0.

Passing in an integer for  `usecols`  has been deprecated. Please pass in a list of ints from 0 to  `usecols`  inclusive instead.

If  `usecols`  is an integer, then it is assumed to indicate the last column to be parsed.

pd.read_excel('path_to_file.xls', 'Sheet1', usecols=2)

You can also specify a comma-delimited set of Excel columns and ranges as a string:

pd.read_excel('path_to_file.xls', 'Sheet1', usecols='A,C:E')

If  `usecols`  is a list of integers, then it is assumed to be the file column indices to be parsed.

pd.read_excel('path_to_file.xls', 'Sheet1', usecols=[0, 2, 3])

Element order is ignored, so  `usecols=[0,  1]`  is the same as  `[1,  0]`.

New in version 0.24.

If  `usecols`  is a list of strings, it is assumed that each string corresponds to a column name provided either by the user in  `names`  or inferred from the document header row(s). Those strings define which columns will be parsed:

pd.read_excel('path_to_file.xls', 'Sheet1', usecols=['foo', 'bar'])

Element order is ignored, so  `usecols=['baz',  'joe']`  is the same as  `['joe',  'baz']`.

New in version 0.24.

If  `usecols`  is callable, the callable function will be evaluated against the column names, returning names where the callable function evaluates to  `True`.

pd.read_excel('path_to_file.xls', 'Sheet1', usecols=lambda x: x.isalpha())

#### Parsing dates[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#parsing-dates "Permalink to this headline")

Datetime-like values are normally automatically converted to the appropriate dtype when reading the excel file. But if you have a column of strings that  _look_  like dates (but are not actually formatted as dates in excel), you can use the  `parse_dates`  keyword to parse those strings to datetimes:

pd.read_excel('path_to_file.xls', 'Sheet1', parse_dates=['date_strings'])

#### Cell converters[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#cell-converters "Permalink to this headline")

It is possible to transform the contents of Excel cells via the  `converters`  option. For instance, to convert a column to boolean:

pd.read_excel('path_to_file.xls', 'Sheet1', converters={'MyBools': bool})

This options handles missing values and treats exceptions in the converters as missing data. Transformations are applied cell by cell rather than to the column as a whole, so the array dtype is not guaranteed. For instance, a column of integers with missing values cannot be transformed to an array with integer dtype, because NaN is strictly a float. You can manually mask missing data to recover integer dtype:

def cfun(x):
    return int(x) if x else -1

pd.read_excel('path_to_file.xls', 'Sheet1', converters={'MyInts': cfun})

#### Dtype specifications[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#dtype-specifications "Permalink to this headline")

As an alternative to converters, the type for an entire column can be specified using the  dtype  keyword, which takes a dictionary mapping column names to types. To interpret data with no type inference, use the type  `str`  or  `object`.

pd.read_excel('path_to_file.xls', dtype={'MyInts': 'int64', 'MyText': str})

### Writing Excel files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-excel-files "Permalink to this headline")

#### Writing Excel files to disk[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-excel-files-to-disk "Permalink to this headline")

To write a  `DataFrame`  object to a sheet of an Excel file, you can use the  `to_excel`  instance method. The arguments are largely the same as  `to_csv`  described above, the first argument being the name of the excel file, and the optional second argument the name of the sheet to which the  `DataFrame`  should be written. For example:

df.to_excel('path_to_file.xlsx', sheet_name='Sheet1')

Files with a  `.xls`  extension will be written using  `xlwt`  and those with a  `.xlsx`  extension will be written using  `xlsxwriter`  (if available) or  `openpyxl`.

The  `DataFrame`  will be written in a way that tries to mimic the REPL output. The  `index_label`  will be placed in the second row instead of the first. You can place it in the first row by setting the  `merge_cells`  option in  `to_excel()`  to  `False`:

df.to_excel('path_to_file.xlsx', index_label='label', merge_cells=False)

In order to write separate  `DataFrames`  to separate sheets in a single Excel file, one can pass an  `ExcelWriter`.

with pd.ExcelWriter('path_to_file.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Sheet1')
    df2.to_excel(writer, sheet_name='Sheet2')

Note

Wringing a little more performance out of  `read_excel`  Internally, Excel stores all numeric data as floats. Because this can produce unexpected behavior when reading in data, pandas defaults to trying to convert integers to floats if it doesn’t lose information (`1.0  -->  1`). You can pass  `convert_float=False`  to disable this behavior, which may give a slight performance improvement.

#### Writing Excel files to memory[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-excel-files-to-memory "Permalink to this headline")

Pandas supports writing Excel files to buffer-like objects such as  `StringIO`  or  `BytesIO`  using  `ExcelWriter`.

# Safe import for either Python 2.x or 3.x
try:
    from io import BytesIO
except ImportError:
    from cStringIO import StringIO as BytesIO

bio = BytesIO()

# By setting the 'engine' in the ExcelWriter constructor.
writer = pd.ExcelWriter(bio, engine='xlsxwriter')
df.to_excel(writer, sheet_name='Sheet1')

# Save the workbook
writer.save()

# Seek to the beginning and read to copy the workbook to a variable in memory
bio.seek(0)
workbook = bio.read()

Note

`engine`  is optional but recommended. Setting the engine determines the version of workbook produced. Setting  `engine='xlrd'`  will produce an Excel 2003-format workbook (xls). Using either  `'openpyxl'`  or  `'xlsxwriter'`  will produce an Excel 2007-format workbook (xlsx). If omitted, an Excel 2007-formatted workbook is produced.

### Excel writer engines[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#excel-writer-engines "Permalink to this headline")

Pandas chooses an Excel writer via two methods:

1.  the  `engine`  keyword argument
    
2.  the filename extension (via the default specified in config options)
    

By default, pandas uses the  [XlsxWriter](https://xlsxwriter.readthedocs.io/)  for  `.xlsx`,  [openpyxl](https://openpyxl.readthedocs.io/)  for  `.xlsm`, and  [xlwt](http://www.python-excel.org/)  for  `.xls`  files. If you have multiple engines installed, you can set the default engine through  [setting the config options](https://pandas.pydata.org/pandas-docs/stable/user_guide/options.html#options)  `io.excel.xlsx.writer`  and  `io.excel.xls.writer`. pandas will fall back on  [openpyxl](https://openpyxl.readthedocs.io/)  for  `.xlsx`  files if  [Xlsxwriter](https://xlsxwriter.readthedocs.io/)  is not available.

To specify which writer you want to use, you can pass an engine keyword argument to  `to_excel`  and to  `ExcelWriter`. The built-in engines are:

-   `openpyxl`: version 2.4 or higher is required
    
-   `xlsxwriter`
    
-   `xlwt`
    

# By setting the 'engine' in the DataFrame 'to_excel()' methods.
df.to_excel('path_to_file.xlsx', sheet_name='Sheet1', engine='xlsxwriter')

# By setting the 'engine' in the ExcelWriter constructor.
writer = pd.ExcelWriter('path_to_file.xlsx', engine='xlsxwriter')

# Or via pandas configuration.
from pandas import options  # noqa: E402
options.io.excel.xlsx.writer = 'xlsxwriter'

df.to_excel('path_to_file.xlsx', sheet_name='Sheet1')

### Style and formatting[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#style-and-formatting "Permalink to this headline")

The look and feel of Excel worksheets created from pandas can be modified using the following parameters on the  `DataFrame`’s  `to_excel`  method.

-   `float_format`  : Format string for floating point numbers (default  `None`).
    
-   `freeze_panes`  : A tuple of two integers representing the bottommost row and rightmost column to freeze. Each of these parameters is one-based, so (1, 1) will freeze the first row and first column (default  `None`).
    

Using the  [Xlsxwriter](https://xlsxwriter.readthedocs.io/)  engine provides many options for controlling the format of an Excel worksheet created with the  `to_excel`  method. Excellent examples can be found in the  [Xlsxwriter](https://xlsxwriter.readthedocs.io/)  documentation here:  [https://xlsxwriter.readthedocs.io/working_with_pandas.html](https://xlsxwriter.readthedocs.io/working_with_pandas.html)



> [Source : ](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#excel-files).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzg2MDQ0OTI2XX0=
-->