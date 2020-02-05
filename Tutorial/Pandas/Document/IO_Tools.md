
# IO tools (text, CSV, HDF5, …)[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-tools-text-csv-hdf5 "Permalink to this headline")

The pandas I/O API is a set of top level  `reader`  functions accessed like  [`pandas.read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv")  that generally return a pandas object. The corresponding  `writer`  functions are object methods that are accessed like  [`DataFrame.to_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html#pandas.DataFrame.to_csv "pandas.DataFrame.to_csv"). Below is a table containing available  `readers`  and  `writers`.


| Type |Data Description |Reader |Writer |
|-----|----------|----------|----------|
| text |CSV |read_csv |to_csv |
| text |Fixed-Width Text File |read_fwf |- |
| text |JSON |read_json |to_json |
| text |HTML |read_html |to_html |
| text |Local clipboard |read_clipboard |to_clipboard |
| - |MS Excel |read_excel |to_excel |
| binary |OpenDocument |read_excel |- |
| binary |HDF5 Format |read_hdf |to_hdf |
| binary |Feather Format |read_feather |to_feather |
| binary |Parquet Format |read_parquet |to_parquet |
| binary |ORC Format |read_orc |- |
| binary |Msgpack |read_msgpack |to_msgpack |
| binary |Stata |read_stata |to_stata |
| binary |SAS |read_sas |- |
| binary |SPSS |read_spss |- |
| binary |Python Pickle Format |read_pickle |to_pickle |
| SQL |SQL |read_sql |to_sql |
| SQL |Google BigQuery |read_gbq |to_gbq |

[Here](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-perf)  is an informal performance comparison for some of these IO methods.

>Note

>For examples that use the  `StringIO`  class, make sure you import it according to your Python version, i.e.  `from  StringIO  import  StringIO`  for Python 2 and  `from  io  import  StringIO`  for Python 3.

## CSV & text files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#csv-text-files "Permalink to this headline")

The workhorse function for reading text files (a.k.a. flat files) is  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv"). See the  [cookbook](https://pandas.pydata.org/pandas-docs/stable/user_guide/cookbook.html#cookbook-csv)  for some advanced strategies.

### Parsing options[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#parsing-options "Permalink to this headline")

[`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv")  accepts the following common arguments:

#### Basic[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#basic "Permalink to this headline")

filepath_or_buffervarious

Either a path to a file (a  [`str`](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.8)"),  [`pathlib.Path`](https://docs.python.org/3/library/pathlib.html#pathlib.Path "(in Python v3.8)"), or  `py._path.local.LocalPath`), URL (including http, ftp, and S3 locations), or any object with a  `read()`  method (such as an open file or  [`StringIO`](https://docs.python.org/3/library/io.html#io.StringIO "(in Python v3.8)")).

sepstr, defaults to  `','`  for  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv"),  `\t`  for  [`read_table()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_table.html#pandas.read_table "pandas.read_table")

Delimiter to use. If sep is  `None`, the C engine cannot automatically detect the separator, but the Python parsing engine can, meaning the latter will be used and automatically detect the separator by Python’s builtin sniffer tool,  [`csv.Sniffer`](https://docs.python.org/3/library/csv.html#csv.Sniffer "(in Python v3.8)"). In addition, separators longer than 1 character and different from  `'\s+'`  will be interpreted as regular expressions and will also force the use of the Python parsing engine. Note that regex delimiters are prone to ignoring quoted data. Regex example:  `'\\r\\t'`.

**delimiterstr, default**  `None`
Alternative argument name for sep.

**delim_whitespaceboolean, default False**
Specifies whether or not whitespace (e.g.  `'  '`  or  `'\t'`) will be used as the delimiter. Equivalent to setting  `sep='\s+'`. If this option is set to  `True`, nothing should be passed in for the  `delimiter`  parameter.

#### Column and index locations and names[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#column-and-index-locations-and-names "Permalink to this headline")

headerint or list of ints, default  `'infer'`

Row number(s) to use as the column names, and the start of the data. Default behavior is to infer the column names: if no names are passed the behavior is identical to  `header=0`  and column names are inferred from the first line of the file, if column names are passed explicitly then the behavior is identical to  `header=None`. Explicitly pass  `header=0`  to be able to replace existing names.

The header can be a list of ints that specify row locations for a MultiIndex on the columns e.g.  `[0,1,3]`. Intervening rows that are not specified will be skipped (e.g. 2 in this example is skipped). Note that this parameter ignores commented lines and empty lines if  `skip_blank_lines=True`, so header=0 denotes the first line of data rather than the first line of the file.

namesarray-like, default  `None`

List of column names to use. If file contains no header row, then you should explicitly pass  `header=None`. Duplicates in this list are not allowed.

index_colint, str, sequence of int / str, or False, default  `None`

Column(s) to use as the row labels of the  `DataFrame`, either given as string name or column index. If a sequence of int / str is given, a MultiIndex is used.

Note:  `index_col=False`  can be used to force pandas to  _not_  use the first column as the index, e.g. when you have a malformed file with delimiters at the end of each line.

usecolslist-like or callable, default  `None`

Return a subset of the columns. If list-like, all elements must either be positional (i.e. integer indices into the document columns) or strings that correspond to column names provided either by the user in  names  or inferred from the document header row(s). For example, a valid list-like  usecols  parameter would be  `[0,  1,  2]`  or  `['foo',  'bar',  'baz']`.

Element order is ignored, so  `usecols=[0,  1]`  is the same as  `[1,  0]`. To instantiate a DataFrame from  `data`  with element order preserved use  `pd.read_csv(data,  usecols=['foo',  'bar'])[['foo',  'bar']]`  for columns in  `['foo',  'bar']`  order or  `pd.read_csv(data,  usecols=['foo',  'bar'])[['bar',  'foo']]`  for  `['bar',  'foo']`  order.

If callable, the callable function will be evaluated against the column names, returning names where the callable function evaluates to True:
```py
In [1]: import pandas as pd

In [2]: from io import StringIO

In [3]: data = ('col1,col2,col3\n'
 ...:        'a,b,1\n'
 ...:        'a,b,2\n'
 ...:        'c,d,3')
 ...: 

In [4]: pd.read_csv(StringIO(data))
Out[4]: 
 col1 col2  col3
0    a    b     1
1    a    b     2
2    c    d     3

In [5]: pd.read_csv(StringIO(data), usecols=lambda x: x.upper() in ['COL1', 'COL3'])
Out[5]: 
 col1  col3
0    a     1
1    a     2
2    c     3
```
Using this parameter results in much faster parsing time and lower memory usage.

**squeezeboolean, default**  `False`
If the parsed data only contains one column then return a  `Series`.

**prefixstr, default**  `None`
Prefix to add to column numbers when no header, e.g. ‘X’ for X0, X1, …

**mangle_dupe_colsboolean, default**  `True`
Duplicate columns will be specified as ‘X’, ‘X.1’…’X.N’, rather than ‘X’…’X’. Passing in  `False`  will cause data to be overwritten if there are duplicate names in the columns.

#### General parsing configuration[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#general-parsing-configuration "Permalink to this headline")

dtypeType name or dict of column -> type, default  `None`

Data type for data or columns. E.g.  `{'a':  np.float64,  'b':  np.int32}`  (unsupported with  `engine='python'`). Use  str  or  object  together with suitable  `na_values`  settings to preserve and not interpret dtype.

engine{`'c'`,  `'python'`}

Parser engine to use. The C engine is faster while the Python engine is currently more feature-complete.

convertersdict, default  `None`

Dict of functions for converting values in certain columns. Keys can either be integers or column labels.

true_valueslist, default  `None`

Values to consider as  `True`.

false_valueslist, default  `None`

Values to consider as  `False`.

skipinitialspaceboolean, default  `False`

Skip spaces after delimiter.

skiprowslist-like or integer, default  `None`

Line numbers to skip (0-indexed) or number of lines to skip (int) at the start of the file.

If callable, the callable function will be evaluated against the row indices, returning True if the row should be skipped and False otherwise:
```py
In [6]: data = ('col1,col2,col3\n'
 ...:        'a,b,1\n'
 ...:        'a,b,2\n'
 ...:        'c,d,3')
 ...: 

In [7]: pd.read_csv(StringIO(data))
Out[7]: 
 col1 col2  col3
0    a    b     1
1    a    b     2
2    c    d     3

In [8]: pd.read_csv(StringIO(data), skiprows=lambda x: x % 2 != 0)
Out[8]: 
 col1 col2  col3
0    a    b     2
```
**skipfooterint, default**  `0`
Number of lines at bottom of file to skip (unsupported with engine=’c’).

**nrowsint, default**  `None`
Number of rows of file to read. Useful for reading pieces of large files.

**low_memoryboolean, default**  `True`
Internally process the file in chunks, resulting in lower memory use while parsing, but possibly mixed type inference. To ensure no mixed types either set  `False`, or specify the type with the  `dtype`  parameter. Note that the entire file is read into a single  `DataFrame`  regardless, use the  `chunksize`  or  `iterator`  parameter to return the data in chunks. (Only valid with C parser)

**memory_mapboolean, default False**
If a filepath is provided for  `filepath_or_buffer`, map the file object directly onto memory and access the data directly from there. Using this option can improve performance because there is no longer any I/O overhead.

#### NA and missing data handling[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#na-and-missing-data-handling "Permalink to this headline")

**na_valuesscalar, str, list-like, or dict, default**  `None`
Additional strings to recognize as NA/NaN. If dict passed, specific per-column NA values. See  [na values const](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-navaluesconst)  below for a list of the values interpreted as NaN by default.

**keep_default_naboolean, default**  `True`
Whether or not to include the default NaN values when parsing the data. Depending on whether  na_values  is passed in, the behavior is as follows:

-   If  keep_default_na  is  `True`, and  na_values  are specified,  na_values  is appended to the default NaN values used for parsing.
    
-   If  keep_default_na  is  `True`, and  na_values  are not specified, only the default NaN values are used for parsing.
    
-   If  keep_default_na  is  `False`, and  na_values  are specified, only the NaN values specified  na_values  are used for parsing.
    
-   If  keep_default_na  is  `False`, and  na_values  are not specified, no strings will be parsed as NaN.
    

Note that if  na_filter  is passed in as  `False`, the  keep_default_na  and  na_values  parameters will be ignored.

na_filterboolean, default  `True`

Detect missing value markers (empty strings and the value of na_values). In data without any NAs, passing  `na_filter=False`  can improve the performance of reading a large file.

verboseboolean, default  `False`

Indicate number of NA values placed in non-numeric columns.

skip_blank_linesboolean, default  `True`

If  `True`, skip over blank lines rather than interpreting as NaN values.

#### Datetime handling[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#datetime-handling "Permalink to this headline")

parse_datesboolean or list of ints or names or list of lists or dict, default  `False`.

-   If  `True`  -> try parsing the index.
    
-   If  `[1,  2,  3]`  -> try parsing columns 1, 2, 3 each as a separate date column.
    
-   If  `[[1,  3]]`  -> combine columns 1 and 3 and parse as a single date column.
    
-   If  `{'foo':  [1,  3]}`  -> parse columns 1, 3 as date and call result ‘foo’. A fast-path exists for iso8601-formatted dates.
    

infer_datetime_formatboolean, default  `False`

If  `True`  and parse_dates is enabled for a column, attempt to infer the datetime format to speed up the processing.

keep_date_colboolean, default  `False`

If  `True`  and parse_dates specifies combining multiple columns then keep the original columns.

date_parserfunction, default  `None`

Function to use for converting a sequence of string columns to an array of datetime instances. The default uses  `dateutil.parser.parser`  to do the conversion. pandas will try to call date_parser in three different ways, advancing to the next if an exception occurs: 1) Pass one or more arrays (as defined by parse_dates) as arguments; 2) concatenate (row-wise) the string values from the columns defined by parse_dates into a single array and pass that; and 3) call date_parser once for each row using one or more strings (corresponding to the columns defined by parse_dates) as arguments.

dayfirstboolean, default  `False`

DD/MM format dates, international and European format.

cache_datesboolean, default True

If True, use a cache of unique, converted dates to apply the datetime conversion. May produce significant speed-up when parsing duplicate date strings, especially ones with timezone offsets.

New in version 0.25.0.

#### Iteration[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#iteration "Permalink to this headline")

iteratorboolean, default  `False`

Return  TextFileReader  object for iteration or getting chunks with  `get_chunk()`.

chunksizeint, default  `None`

Return  TextFileReader  object for iteration. See  [iterating and chunking](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-chunking)  below.

#### Quoting, compression, and file format[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#quoting-compression-and-file-format "Permalink to this headline")

compression{`'infer'`,  `'gzip'`,  `'bz2'`,  `'zip'`,  `'xz'`,  `None`}, default  `'infer'`

For on-the-fly decompression of on-disk data. If ‘infer’, then use gzip, bz2, zip, or xz if filepath_or_buffer is a string ending in ‘.gz’, ‘.bz2’, ‘.zip’, or ‘.xz’, respectively, and no decompression otherwise. If using ‘zip’, the ZIP file must contain only one data file to be read in. Set to  `None`  for no decompression.

Changed in version 0.24.0: ‘infer’ option added and set to default.

thousandsstr, default  `None`

Thousands separator.

decimalstr, default  `'.'`

Character to recognize as decimal point. E.g. use  `','`  for European data.

float_precisionstring, default None

Specifies which converter the C engine should use for floating-point values. The options are  `None`  for the ordinary converter,  `high`  for the high-precision converter, and  `round_trip`  for the round-trip converter.

lineterminatorstr (length 1), default  `None`

Character to break file into lines. Only valid with C parser.

quotecharstr (length 1)

The character used to denote the start and end of a quoted item. Quoted items can include the delimiter and it will be ignored.

quotingint or  `csv.QUOTE_*`  instance, default  `0`

Control field quoting behavior per  `csv.QUOTE_*`  constants. Use one of  `QUOTE_MINIMAL`  (0),  `QUOTE_ALL`  (1),  `QUOTE_NONNUMERIC`  (2) or  `QUOTE_NONE`  (3).

doublequoteboolean, default  `True`

When  `quotechar`  is specified and  `quoting`  is not  `QUOTE_NONE`, indicate whether or not to interpret two consecutive  `quotechar`  elements  **inside**  a field as a single  `quotechar`  element.

escapecharstr (length 1), default  `None`

One-character string used to escape delimiter when quoting is  `QUOTE_NONE`.

commentstr, default  `None`

Indicates remainder of line should not be parsed. If found at the beginning of a line, the line will be ignored altogether. This parameter must be a single character. Like empty lines (as long as  `skip_blank_lines=True`), fully commented lines are ignored by the parameter  header  but not by  skiprows. For example, if  `comment='#'`, parsing ‘#empty\na,b,c\n1,2,3’ with  header=0  will result in ‘a,b,c’ being treated as the header.

encodingstr, default  `None`

Encoding to use for UTF when reading/writing (e.g.  `'utf-8'`).  [List of Python standard encodings](https://docs.python.org/3/library/codecs.html#standard-encodings).

dialectstr or  [`csv.Dialect`](https://docs.python.org/3/library/csv.html#csv.Dialect "(in Python v3.8)")  instance, default  `None`

If provided, this parameter will override values (default or not) for the following parameters:  delimiter,  doublequote,  escapechar,  skipinitialspace,  quotechar, and  quoting. If it is necessary to override values, a ParserWarning will be issued. See  [`csv.Dialect`](https://docs.python.org/3/library/csv.html#csv.Dialect "(in Python v3.8)")  documentation for more details.

#### Error handling[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#error-handling "Permalink to this headline")

error_bad_linesboolean, default  `True`

Lines with too many fields (e.g. a csv line with too many commas) will by default cause an exception to be raised, and no  `DataFrame`  will be returned. If  `False`, then these “bad lines” will dropped from the  `DataFrame`  that is returned. See  [bad lines](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-bad-lines)  below.

warn_bad_linesboolean, default  `True`

If error_bad_lines is  `False`, and warn_bad_lines is  `True`, a warning for each “bad line” will be output.

### Specifying column data types[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-column-data-types "Permalink to this headline")

You can indicate the data type for the whole  `DataFrame`  or individual columns:
```py
In [9]: import numpy as np

In [10]: data = ('a,b,c,d\n'
 ....:        '1,2,3,4\n'
 ....:        '5,6,7,8\n'
 ....:        '9,10,11')
 ....: 

In [11]: print(data)
a,b,c,d
1,2,3,4
5,6,7,8
9,10,11

In [12]: df = pd.read_csv(StringIO(data), dtype=object)

In [13]: df
Out[13]: 
 a   b   c    d
0  1   2   3    4
1  5   6   7    8
2  9  10  11  NaN

In [14]: df['a'][0]
Out[14]: '1'

In [15]: df = pd.read_csv(StringIO(data),
 ....:                 dtype={'b': object, 'c': np.float64, 'd': 'Int64'})
 ....: 

In [16]: df.dtypes
Out[16]: 
a      int64
b     object
c    float64
d      Int64
dtype: object

Fortunately, pandas offers more than one way to ensure that your column(s) contain only one  `dtype`. If you’re unfamiliar with these concepts, you can see  [here](https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#basics-dtypes)  to learn more about dtypes, and  [here](https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#basics-object-conversion)  to learn more about  `object`  conversion in pandas.

For instance, you can use the  `converters`  argument of  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv"):

In [17]: data = ("col_1\n"
 ....:        "1\n"
 ....:        "2\n"
 ....:        "'A'\n"
 ....:        "4.22")
 ....: 

In [18]: df = pd.read_csv(StringIO(data), converters={'col_1': str})

In [19]: df
Out[19]: 
 col_1
0     1
1     2
2   'A'
3  4.22

In [20]: df['col_1'].apply(type).value_counts()
Out[20]: 
<class 'str'>    4
Name: col_1, dtype: int64
```
Or you can use the  [`to_numeric()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html#pandas.to_numeric "pandas.to_numeric")  function to coerce the dtypes after reading in the data,
```py
In [21]: df2 = pd.read_csv(StringIO(data))

In [22]: df2['col_1'] = pd.to_numeric(df2['col_1'], errors='coerce')

In [23]: df2
Out[23]: 
 col_1
0   1.00
1   2.00
2    NaN
3   4.22

In [24]: df2['col_1'].apply(type).value_counts()
Out[24]: 
<class 'float'>    4
Name: col_1, dtype: int64
```
which will convert all valid parsing to floats, leaving the invalid parsing as  `NaN`.

Ultimately, how you deal with reading in columns containing mixed dtypes depends on your specific needs. In the case above, if you wanted to  `NaN`  out the data anomalies, then  [`to_numeric()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html#pandas.to_numeric "pandas.to_numeric")  is probably your best option. However, if you wanted for all the data to be coerced, no matter the type, then using the  `converters`  argument of  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv")  would certainly be worth trying.

Note

In some cases, reading in abnormal data with columns containing mixed dtypes will result in an inconsistent dataset. If you rely on pandas to infer the dtypes of your columns, the parsing engine will go and infer the dtypes for different chunks of the data, rather than the whole dataset at once. Consequently, you can end up with column(s) with mixed dtypes. For example,
```py
In [25]: col_1 = list(range(500000)) + ['a', 'b'] + list(range(500000))

In [26]: df = pd.DataFrame({'col_1': col_1})

In [27]: df.to_csv('foo.csv')

In [28]: mixed_df = pd.read_csv('foo.csv')

In [29]: mixed_df['col_1'].apply(type).value_counts()
Out[29]: 
<class 'int'>    737858
<class 'str'>    262144
Name: col_1, dtype: int64

In [30]: mixed_df['col_1'].dtype
Out[30]: dtype('O')
```
will result with  mixed_df  containing an  `int`  dtype for certain chunks of the column, and  `str`  for others due to the mixed dtypes from the data that was read in. It is important to note that the overall column will be marked with a  `dtype`  of  `object`, which is used for columns with mixed dtypes.

### Specifying categorical dtype[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-categorical-dtype "Permalink to this headline")

`Categorical`  columns can be parsed directly by specifying  `dtype='category'`  or  `dtype=CategoricalDtype(categories,  ordered)`.
```py
In [31]: data = ('col1,col2,col3\n'
 ....:        'a,b,1\n'
 ....:        'a,b,2\n'
 ....:        'c,d,3')
 ....: 

In [32]: pd.read_csv(StringIO(data))
Out[32]: 
 col1 col2  col3
0    a    b     1
1    a    b     2
2    c    d     3

In [33]: pd.read_csv(StringIO(data)).dtypes
Out[33]: 
col1    object
col2    object
col3     int64
dtype: object

In [34]: pd.read_csv(StringIO(data), dtype='category').dtypes
Out[34]: 
col1    category
col2    category
col3    category
dtype: object

Individual columns can be parsed as a  `Categorical`  using a dict specification:

In [35]: pd.read_csv(StringIO(data), dtype={'col1': 'category'}).dtypes
Out[35]: 
col1    category
col2      object
col3       int64
dtype: object

New in version 0.21.0.

Specifying  `dtype='category'`  will result in an unordered  `Categorical`  whose  `categories`  are the unique values observed in the data. For more control on the categories and order, create a  `CategoricalDtype`  ahead of time, and pass that for that column’s  `dtype`.

In [36]: from pandas.api.types import CategoricalDtype

In [37]: dtype = CategoricalDtype(['d', 'c', 'b', 'a'], ordered=True)

In [38]: pd.read_csv(StringIO(data), dtype={'col1': dtype}).dtypes
Out[38]: 
col1    category
col2      object
col3       int64
dtype: object
```
When using  `dtype=CategoricalDtype`, “unexpected” values outside of  `dtype.categories`  are treated as missing values.
```py
In [39]: dtype = CategoricalDtype(['a', 'b', 'd'])  # No 'c'

In [40]: pd.read_csv(StringIO(data), dtype={'col1': dtype}).col1
Out[40]: 
0      a
1      a
2    NaN
Name: col1, dtype: category
Categories (3, object): [a, b, d]
```
This matches the behavior of  `Categorical.set_categories()`.

Note

With  `dtype='category'`, the resulting categories will always be parsed as strings (object dtype). If the categories are numeric they can be converted using the  [`to_numeric()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html#pandas.to_numeric "pandas.to_numeric")  function, or as appropriate, another converter such as  [`to_datetime()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html#pandas.to_datetime "pandas.to_datetime").

When  `dtype`  is a  `CategoricalDtype`  with homogeneous  `categories`  ( all numeric, all datetimes, etc.), the conversion is done automatically.
```py
In [41]: df = pd.read_csv(StringIO(data), dtype='category')

In [42]: df.dtypes
Out[42]: 
col1    category
col2    category
col3    category
dtype: object

In [43]: df['col3']
Out[43]: 
0    1
1    2
2    3
Name: col3, dtype: category
Categories (3, object): [1, 2, 3]

In [44]: df['col3'].cat.categories = pd.to_numeric(df['col3'].cat.categories)

In [45]: df['col3']
Out[45]: 
0    1
1    2
2    3
Name: col3, dtype: category
Categories (3, int64): [1, 2, 3]
```
### Naming and using columns[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#naming-and-using-columns "Permalink to this headline")

#### Handling column names[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#handling-column-names "Permalink to this headline")

A file may or may not have a header row. pandas assumes the first row should be used as the column names:
```py
In [46]: data = ('a,b,c\n'
 ....:        '1,2,3\n'
 ....:        '4,5,6\n'
 ....:        '7,8,9')
 ....: 

In [47]: print(data)
a,b,c
1,2,3
4,5,6
7,8,9

In [48]: pd.read_csv(StringIO(data))
Out[48]: 
 a  b  c
0  1  2  3
1  4  5  6
2  7  8  9

By specifying the  `names`  argument in conjunction with  `header`  you can indicate other names to use and whether or not to throw away the header row (if any):

In [49]: print(data)
a,b,c
1,2,3
4,5,6
7,8,9

In [50]: pd.read_csv(StringIO(data), names=['foo', 'bar', 'baz'], header=0)
Out[50]: 
 foo  bar  baz
0    1    2    3
1    4    5    6
2    7    8    9

In [51]: pd.read_csv(StringIO(data), names=['foo', 'bar', 'baz'], header=None)
Out[51]: 
 foo bar baz
0   a   b   c
1   1   2   3
2   4   5   6
3   7   8   9
```
If the header is in a row other than the first, pass the row number to  `header`. This will skip the preceding rows:
```py
In [52]: data = ('skip this skip it\n'
 ....:        'a,b,c\n'
 ....:        '1,2,3\n'
 ....:        '4,5,6\n'
 ....:        '7,8,9')
 ....: 

In [53]: pd.read_csv(StringIO(data), header=1)
Out[53]: 
 a  b  c
0  1  2  3
1  4  5  6
2  7  8  9
```
>Note

>Default behavior is to infer the column names: if no names are passed the behavior is identical to  `header=0`  and column names are inferred from the first non-blank line of the file, if column names are passed explicitly then the behavior is identical to  `header=None`.

### Duplicate names parsing[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#duplicate-names-parsing "Permalink to this headline")

If the file or header contains duplicate names, pandas will by default distinguish between them so as to prevent overwriting data:
```py
In [54]: data = ('a,b,a\n'
 ....:        '0,1,2\n'
 ....:        '3,4,5')
 ....: 

In [55]: pd.read_csv(StringIO(data))
Out[55]: 
 a  b  a.1
0  0  1    2
1  3  4    5
```
There is no more duplicate data because  `mangle_dupe_cols=True`  by default, which modifies a series of duplicate columns ‘X’, …, ‘X’ to become ‘X’, ‘X.1’, …, ‘X.N’. If  `mangle_dupe_cols=False`, duplicate data can arise:
```py
In [2]: data = 'a,b,a\n0,1,2\n3,4,5'
In [3]: pd.read_csv(StringIO(data), mangle_dupe_cols=False)
Out[3]:
 a  b  a
0  2  1  2
1  5  4  5
```
To prevent users from encountering this problem with duplicate data, a  `ValueError`  exception is raised if  `mangle_dupe_cols  !=  True`:
```py
In [2]: data = 'a,b,a\n0,1,2\n3,4,5'
In [3]: pd.read_csv(StringIO(data), mangle_dupe_cols=False)
...
ValueError: Setting mangle_dupe_cols=False is not supported yet
```
#### Filtering columns (`usecols`)[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#filtering-columns-usecols "Permalink to this headline")

The  `usecols`  argument allows you to select any subset of the columns in a file, either using the column names, position numbers or a callable:
```py
In [56]: data = 'a,b,c,d\n1,2,3,foo\n4,5,6,bar\n7,8,9,baz'

In [57]: pd.read_csv(StringIO(data))
Out[57]: 
 a  b  c    d
0  1  2  3  foo
1  4  5  6  bar
2  7  8  9  baz

In [58]: pd.read_csv(StringIO(data), usecols=['b', 'd'])
Out[58]: 
 b    d
0  2  foo
1  5  bar
2  8  baz

In [59]: pd.read_csv(StringIO(data), usecols=[0, 2, 3])
Out[59]: 
 a  c    d
0  1  3  foo
1  4  6  bar
2  7  9  baz

In [60]: pd.read_csv(StringIO(data), usecols=lambda x: x.upper() in ['A', 'C'])
Out[60]: 
 a  c
0  1  3
1  4  6
2  7  9
```
The  `usecols`  argument can also be used to specify which columns not to use in the final result:
```py
In [61]: pd.read_csv(StringIO(data), usecols=lambda x: x not in ['a', 'c'])
Out[61]: 
 b    d
0  2  foo
1  5  bar
2  8  baz
```
In this case, the callable is specifying that we exclude the “a” and “c” columns from the output.

### Comments and empty lines[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#comments-and-empty-lines "Permalink to this headline")

#### Ignoring line comments and empty lines[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#ignoring-line-comments-and-empty-lines "Permalink to this headline")

If the  `comment`  parameter is specified, then completely commented lines will be ignored. By default, completely blank lines will be ignored as well.
```py
In [62]: data = ('\n'
 ....:        'a,b,c\n'
 ....:        ' \n'
 ....:        '# commented line\n'
 ....:        '1,2,3\n'
 ....:        '\n'
 ....:        '4,5,6')
 ....: 

In [63]: print(data)

a,b,c
  
# commented line
1,2,3

4,5,6

In [64]: pd.read_csv(StringIO(data), comment='#')
Out[64]: 
 a  b  c
0  1  2  3
1  4  5  6
```
If  `skip_blank_lines=False`, then  `read_csv`  will not ignore blank lines:
```py
In [65]: data = ('a,b,c\n'
 ....:        '\n'
 ....:        '1,2,3\n'
 ....:        '\n'
 ....:        '\n'
 ....:        '4,5,6')
 ....: 

In [66]: pd.read_csv(StringIO(data), skip_blank_lines=False)
Out[66]: 
 a    b    c
0  NaN  NaN  NaN
1  1.0  2.0  3.0
2  NaN  NaN  NaN
3  NaN  NaN  NaN
4  4.0  5.0  6.0
```
>Warning

>The presence of ignored lines might create ambiguities involving line numbers; the parameter  `header`  uses row numbers (ignoring commented/empty lines), while  `skiprows`  uses line numbers (including commented/empty lines):
```py
In [67]: data = ('#comment\n'
 ....:        'a,b,c\n'
 ....:        'A,B,C\n'
 ....:        '1,2,3')
 ....: 

In [68]: pd.read_csv(StringIO(data), comment='#', header=1)
Out[68]: 
 A  B  C
0  1  2  3

In [69]: data = ('A,B,C\n'
 ....:        '#comment\n'
 ....:        'a,b,c\n'
 ....:        '1,2,3')
 ....: 

In [70]: pd.read_csv(StringIO(data), comment='#', skiprows=2)
Out[70]: 
 a  b  c
0  1  2  3
```
If both  `header`  and  `skiprows`  are specified,  `header`  will be relative to the end of  `skiprows`. For example:
```py
In [71]: data = ('# empty\n'
 ....:        '# second empty line\n'
 ....:        '# third emptyline\n'
 ....:        'X,Y,Z\n'
 ....:        '1,2,3\n'
 ....:        'A,B,C\n'
 ....:        '1,2.,4.\n'
 ....:        '5.,NaN,10.0\n')
 ....: 

In [72]: print(data)
# empty
# second empty line
# third emptyline
X,Y,Z
1,2,3
A,B,C
1,2.,4.
5.,NaN,10.0

In [73]: pd.read_csv(StringIO(data), comment='#', skiprows=4, header=1)
Out[73]: 
 A    B     C
0  1.0  2.0   4.0
1  5.0  NaN  10.0
```
#### Comments[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#comments "Permalink to this headline")

Sometimes comments or meta data may be included in a file:
```py
In [74]: print(open('tmp.csv').read())
ID,level,category
Patient1,123000,x # really unpleasant
Patient2,23000,y # wouldn't take his medicine
Patient3,1234018,z # awesome
```
By default, the parser includes the comments in the output:
```py
In [75]: df = pd.read_csv('tmp.csv')

In [76]: df
Out[76]: 
 ID    level                        category
0  Patient1   123000           x # really unpleasant
1  Patient2    23000  y # wouldn't take his medicine
2  Patient3  1234018                     z # awesome
```
We can suppress the comments using the  `comment`  keyword:
```py
In [77]: df = pd.read_csv('tmp.csv', comment='#')

In [78]: df
Out[78]: 
 ID    level category
0  Patient1   123000       x 
1  Patient2    23000       y 
2  Patient3  1234018       z 
```
### Dealing with Unicode data[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#dealing-with-unicode-data "Permalink to this headline")

The  `encoding`  argument should be used for encoded unicode data, which will result in byte strings being decoded to unicode in the result:
```py
In [79]: from io import BytesIO

In [80]: data = (b'word,length\n'
 ....:        b'Tr\xc3\xa4umen,7\n'
 ....:        b'Gr\xc3\xbc\xc3\x9fe,5')
 ....: 

In [81]: data = data.decode('utf8').encode('latin-1')

In [82]: df = pd.read_csv(BytesIO(data), encoding='latin-1')

In [83]: df
Out[83]: 
 word  length
0  Träumen       7
1    Grüße       5

In [84]: df['word'][1]
Out[84]: 'Grüße'
```
Some formats which encode all characters as multiple bytes, like UTF-16, won’t parse correctly at all without specifying the encoding.  [Full list of Python standard encodings](https://docs.python.org/3/library/codecs.html#standard-encodings).

### Index columns and trailing delimiters[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#index-columns-and-trailing-delimiters "Permalink to this headline")

If a file has one more column of data than the number of column names, the first column will be used as the  `DataFrame`’s row names:
```py
In [85]: data = ('a,b,c\n'
 ....:        '4,apple,bat,5.7\n'
 ....:        '8,orange,cow,10')
 ....: 

In [86]: pd.read_csv(StringIO(data))
Out[86]: 
 a    b     c
4   apple  bat   5.7
8  orange  cow  10.0

In [87]: data = ('index,a,b,c\n'
 ....:        '4,apple,bat,5.7\n'
 ....:        '8,orange,cow,10')
 ....: 

In [88]: pd.read_csv(StringIO(data), index_col=0)
Out[88]: 
 a    b     c
index 
4       apple  bat   5.7
8      orange  cow  10.0
```
Ordinarily, you can achieve this behavior using the  `index_col`  option.

There are some exception cases when a file has been prepared with delimiters at the end of each data line, confusing the parser. To explicitly disable the index column inference and discard the last column, pass  `index_col=False`:
```py
In [89]: data = ('a,b,c\n'
 ....:        '4,apple,bat,\n'
 ....:        '8,orange,cow,')
 ....: 

In [90]: print(data)
a,b,c
4,apple,bat,
8,orange,cow,

In [91]: pd.read_csv(StringIO(data))
Out[91]: 
 a    b   c
4   apple  bat NaN
8  orange  cow NaN

In [92]: pd.read_csv(StringIO(data), index_col=False)
Out[92]: 
 a       b    c
0  4   apple  bat
1  8  orange  cow
```
If a subset of data is being parsed using the  `usecols`  option, the  `index_col`  specification is based on that subset, not the original data.
```py
In [93]: data = ('a,b,c\n'
 ....:        '4,apple,bat,\n'
 ....:        '8,orange,cow,')
 ....: 

In [94]: print(data)
a,b,c
4,apple,bat,
8,orange,cow,

In [95]: pd.read_csv(StringIO(data), usecols=['b', 'c'])
Out[95]: 
 b   c
4  bat NaN
8  cow NaN

In [96]: pd.read_csv(StringIO(data), usecols=['b', 'c'], index_col=0)
Out[96]: 
 b   c
4  bat NaN
8  cow NaN
```
### Date Handling[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#date-handling "Permalink to this headline")

#### Specifying date columns[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-date-columns "Permalink to this headline")

To better facilitate working with datetime data,  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv")  uses the keyword arguments  `parse_dates`  and  `date_parser`  to allow users to specify a variety of columns and date/time formats to turn the input text data into  `datetime`  objects.

The simplest case is to just pass in  `parse_dates=True`:
```py
# Use a column as an index, and parse it as dates.
In [97]: df = pd.read_csv('foo.csv', index_col=0, parse_dates=True)

In [98]: df
Out[98]: 
 A  B  C
date 
2009-01-01  a  1  2
2009-01-02  b  3  4
2009-01-03  c  4  5

# These are Python datetime objects
In [99]: df.index
Out[99]: DatetimeIndex(['2009-01-01', '2009-01-02', '2009-01-03'], dtype='datetime64[ns]', name='date', freq=None)
```
It is often the case that we may want to store date and time data separately, or store various date fields separately. the  `parse_dates`  keyword can be used to specify a combination of columns to parse the dates and/or times from.

You can specify a list of column lists to  `parse_dates`, the resulting date columns will be prepended to the output (so as to not affect the existing column order) and the new column names will be the concatenation of the component column names:
```py
In [100]: print(open('tmp.csv').read())
KORD,19990127, 19:00:00, 18:56:00, 0.8100
KORD,19990127, 20:00:00, 19:56:00, 0.0100
KORD,19990127, 21:00:00, 20:56:00, -0.5900
KORD,19990127, 21:00:00, 21:18:00, -0.9900
KORD,19990127, 22:00:00, 21:56:00, -0.5900
KORD,19990127, 23:00:00, 22:56:00, -0.5900

In [101]: df = pd.read_csv('tmp.csv', header=None, parse_dates=[[1, 2], [1, 3]])

In [102]: df
Out[102]: 
 1_2                 1_3     0     4
0 1999-01-27 19:00:00 1999-01-27 18:56:00  KORD  0.81
1 1999-01-27 20:00:00 1999-01-27 19:56:00  KORD  0.01
2 1999-01-27 21:00:00 1999-01-27 20:56:00  KORD -0.59
3 1999-01-27 21:00:00 1999-01-27 21:18:00  KORD -0.99
4 1999-01-27 22:00:00 1999-01-27 21:56:00  KORD -0.59
5 1999-01-27 23:00:00 1999-01-27 22:56:00  KORD -0.59
```
By default the parser removes the component date columns, but you can choose to retain them via the  `keep_date_col`  keyword:

In [103]: df = pd.read_csv('tmp.csv', header=None, parse_dates=[[1, 2], [1, 3]],
 .....:                 keep_date_col=True)
 .....: 

In [104]: df
Out[104]: 
 1_2                 1_3     0         1          2          3     4
0 1999-01-27 19:00:00 1999-01-27 18:56:00  KORD  19990127   19:00:00   18:56:00  0.81
1 1999-01-27 20:00:00 1999-01-27 19:56:00  KORD  19990127   20:00:00   19:56:00  0.01
2 1999-01-27 21:00:00 1999-01-27 20:56:00  KORD  19990127   21:00:00   20:56:00 -0.59
3 1999-01-27 21:00:00 1999-01-27 21:18:00  KORD  19990127   21:00:00   21:18:00 -0.99
4 1999-01-27 22:00:00 1999-01-27 21:56:00  KORD  19990127   22:00:00   21:56:00 -0.59
5 1999-01-27 23:00:00 1999-01-27 22:56:00  KORD  19990127   23:00:00   22:56:00 -0.59

Note that if you wish to combine multiple columns into a single date column, a nested list must be used. In other words,  `parse_dates=[1,  2]`  indicates that the second and third columns should each be parsed as separate date columns while  `parse_dates=[[1,  2]]`  means the two columns should be parsed into a single column.

You can also use a dict to specify custom name columns:

In [105]: date_spec = {'nominal': [1, 2], 'actual': [1, 3]}

In [106]: df = pd.read_csv('tmp.csv', header=None, parse_dates=date_spec)

In [107]: df
Out[107]: 
 nominal              actual     0     4
0 1999-01-27 19:00:00 1999-01-27 18:56:00  KORD  0.81
1 1999-01-27 20:00:00 1999-01-27 19:56:00  KORD  0.01
2 1999-01-27 21:00:00 1999-01-27 20:56:00  KORD -0.59
3 1999-01-27 21:00:00 1999-01-27 21:18:00  KORD -0.99
4 1999-01-27 22:00:00 1999-01-27 21:56:00  KORD -0.59
5 1999-01-27 23:00:00 1999-01-27 22:56:00  KORD -0.59

It is important to remember that if multiple text columns are to be parsed into a single date column, then a new column is prepended to the data. The  index_col  specification is based off of this new set of columns rather than the original data columns:

In [108]: date_spec = {'nominal': [1, 2], 'actual': [1, 3]}

In [109]: df = pd.read_csv('tmp.csv', header=None, parse_dates=date_spec,
 .....:                 index_col=0)  # index is the nominal column
 .....: 

In [110]: df
Out[110]: 
 actual     0     4
nominal 
1999-01-27 19:00:00 1999-01-27 18:56:00  KORD  0.81
1999-01-27 20:00:00 1999-01-27 19:56:00  KORD  0.01
1999-01-27 21:00:00 1999-01-27 20:56:00  KORD -0.59
1999-01-27 21:00:00 1999-01-27 21:18:00  KORD -0.99
1999-01-27 22:00:00 1999-01-27 21:56:00  KORD -0.59
1999-01-27 23:00:00 1999-01-27 22:56:00  KORD -0.59

Note

If a column or index contains an unparsable date, the entire column or index will be returned unaltered as an object data type. For non-standard datetime parsing, use  [`to_datetime()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html#pandas.to_datetime "pandas.to_datetime")  after  `pd.read_csv`.

Note

read_csv has a fast_path for parsing datetime strings in iso8601 format, e.g “2000-01-01T00:01:02+00:00” and similar variations. If you can arrange for your data to store datetimes in this format, load times will be significantly faster, ~20x has been observed.

Note

When passing a dict as the  parse_dates  argument, the order of the columns prepended is not guaranteed, because  dict  objects do not impose an ordering on their keys. On Python 2.7+ you may use  collections.OrderedDict  instead of a regular  dict  if this matters to you. Because of this, when using a dict for ‘parse_dates’ in conjunction with the  index_col  argument, it’s best to specify  index_col  as a column label rather then as an index on the resulting frame.

#### Date parsing functions[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#date-parsing-functions "Permalink to this headline")

Finally, the parser allows you to specify a custom  `date_parser`  function to take full advantage of the flexibility of the date parsing API:

In [111]: df = pd.read_csv('tmp.csv', header=None, parse_dates=date_spec,
 .....:                 date_parser=pd.io.date_converters.parse_date_time)
 .....: 

In [112]: df
Out[112]: 
 nominal              actual     0     4
0 1999-01-27 19:00:00 1999-01-27 18:56:00  KORD  0.81
1 1999-01-27 20:00:00 1999-01-27 19:56:00  KORD  0.01
2 1999-01-27 21:00:00 1999-01-27 20:56:00  KORD -0.59
3 1999-01-27 21:00:00 1999-01-27 21:18:00  KORD -0.99
4 1999-01-27 22:00:00 1999-01-27 21:56:00  KORD -0.59
5 1999-01-27 23:00:00 1999-01-27 22:56:00  KORD -0.59

Pandas will try to call the  `date_parser`  function in three different ways. If an exception is raised, the next one is tried:

1.  `date_parser`  is first called with one or more arrays as arguments, as defined using  parse_dates  (e.g.,  `date_parser(['2013',  '2013'],  ['1',  '2'])`).
    
2.  If #1 fails,  `date_parser`  is called with all the columns concatenated row-wise into a single array (e.g.,  `date_parser(['2013  1',  '2013  2'])`).
    
3.  If #2 fails,  `date_parser`  is called once for every row with one or more string arguments from the columns indicated with  parse_dates  (e.g.,  `date_parser('2013',  '1')`  for the first row,  `date_parser('2013',  '2')`  for the second, etc.).
    

Note that performance-wise, you should try these methods of parsing dates in order:

1.  Try to infer the format using  `infer_datetime_format=True`  (see section below).
    
2.  If you know the format, use  `pd.to_datetime()`:  `date_parser=lambda  x:  pd.to_datetime(x,  format=...)`.
    
3.  If you have a really non-standard format, use a custom  `date_parser`  function. For optimal performance, this should be vectorized, i.e., it should accept arrays as arguments.
    

You can explore the date parsing functionality in  [date_converters.py](https://github.com/pandas-dev/pandas/blob/master/pandas/io/date_converters.py)  and add your own. We would love to turn this module into a community supported set of date/time parsers. To get you started,  `date_converters.py`  contains functions to parse dual date and time columns, year/month/day columns, and year/month/day/hour/minute/second columns. It also contains a  `generic_parser`  function so you can curry it with a function that deals with a single date rather than the entire array.

#### Parsing a CSV with mixed timezones[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#parsing-a-csv-with-mixed-timezones "Permalink to this headline")

Pandas cannot natively represent a column or index with mixed timezones. If your CSV file contains columns with a mixture of timezones, the default result will be an object-dtype column with strings, even with  `parse_dates`.

In [113]: content = """\
 .....: a
 .....: 2000-01-01T00:00:00+05:00
 .....: 2000-01-01T00:00:00+06:00"""
 .....: 

In [114]: df = pd.read_csv(StringIO(content), parse_dates=['a'])

In [115]: df['a']
Out[115]: 
0    2000-01-01 00:00:00+05:00
1    2000-01-01 00:00:00+06:00
Name: a, dtype: object

To parse the mixed-timezone values as a datetime column, pass a partially-applied  [`to_datetime()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html#pandas.to_datetime "pandas.to_datetime")  with  `utc=True`  as the  `date_parser`.

In [116]: df = pd.read_csv(StringIO(content), parse_dates=['a'],
 .....:                 date_parser=lambda col: pd.to_datetime(col, utc=True))
 .....: 

In [117]: df['a']
Out[117]: 
0   1999-12-31 19:00:00+00:00
1   1999-12-31 18:00:00+00:00
Name: a, dtype: datetime64[ns, UTC]

#### Inferring datetime format[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#inferring-datetime-format "Permalink to this headline")

If you have  `parse_dates`  enabled for some or all of your columns, and your datetime strings are all formatted the same way, you may get a large speed up by setting  `infer_datetime_format=True`. If set, pandas will attempt to guess the format of your datetime strings, and then use a faster means of parsing the strings. 5-10x parsing speeds have been observed. pandas will fallback to the usual parsing if either the format cannot be guessed or the format that was guessed cannot properly parse the entire column of strings. So in general,  `infer_datetime_format`  should not have any negative consequences if enabled.

Here are some examples of datetime strings that can be guessed (All representing December 30th, 2011 at 00:00:00):

-   “20111230”
    
-   “2011/12/30”
    
-   “20111230 00:00:00”
    
-   “12/30/2011 00:00:00”
    
-   “30/Dec/2011 00:00:00”
    
-   “30/December/2011 00:00:00”
    

Note that  `infer_datetime_format`  is sensitive to  `dayfirst`. With  `dayfirst=True`, it will guess “01/12/2011” to be December 1st. With  `dayfirst=False`  (default) it will guess “01/12/2011” to be January 12th.

# Try to infer the format for the index column
In [118]: df = pd.read_csv('foo.csv', index_col=0, parse_dates=True,
 .....:                 infer_datetime_format=True)
 .....: 

In [119]: df
Out[119]: 
 A  B  C
date 
2009-01-01  a  1  2
2009-01-02  b  3  4
2009-01-03  c  4  5

#### International date formats[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#international-date-formats "Permalink to this headline")

While US date formats tend to be MM/DD/YYYY, many international formats use DD/MM/YYYY instead. For convenience, a  `dayfirst`  keyword is provided:

In [120]: print(open('tmp.csv').read())
date,value,cat
1/6/2000,5,a
2/6/2000,10,b
3/6/2000,15,c

In [121]: pd.read_csv('tmp.csv', parse_dates=[0])
Out[121]: 
 date  value cat
0 2000-01-06      5   a
1 2000-02-06     10   b
2 2000-03-06     15   c

In [122]: pd.read_csv('tmp.csv', dayfirst=True, parse_dates=[0])
Out[122]: 
 date  value cat
0 2000-06-01      5   a
1 2000-06-02     10   b
2 2000-06-03     15   c

### Specifying method for floating-point conversion[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-method-for-floating-point-conversion "Permalink to this headline")

The parameter  `float_precision`  can be specified in order to use a specific floating-point converter during parsing with the C engine. The options are the ordinary converter, the high-precision converter, and the round-trip converter (which is guaranteed to round-trip values after writing to a file). For example:

In [123]: val = '0.3066101993807095471566981359501369297504425048828125'

In [124]: data = 'a,b,c\n1,2,{0}'.format(val)

In [125]: abs(pd.read_csv(StringIO(data), engine='c',
 .....:                float_precision=None)['c'][0] - float(val))
 .....: 
Out[125]: 1.1102230246251565e-16

In [126]: abs(pd.read_csv(StringIO(data), engine='c',
 .....:                float_precision='high')['c'][0] - float(val))
 .....: 
Out[126]: 5.551115123125783e-17

In [127]: abs(pd.read_csv(StringIO(data), engine='c',
 .....:                float_precision='round_trip')['c'][0] - float(val))
 .....: 
Out[127]: 0.0

### Thousand separators[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#thousand-separators "Permalink to this headline")

For large numbers that have been written with a thousands separator, you can set the  `thousands`  keyword to a string of length 1 so that integers will be parsed correctly:

By default, numbers with a thousands separator will be parsed as strings:

In [128]: print(open('tmp.csv').read())
ID|level|category
Patient1|123,000|x
Patient2|23,000|y
Patient3|1,234,018|z

In [129]: df = pd.read_csv('tmp.csv', sep='|')

In [130]: df
Out[130]: 
 ID      level category
0  Patient1    123,000        x
1  Patient2     23,000        y
2  Patient3  1,234,018        z

In [131]: df.level.dtype
Out[131]: dtype('O')

The  `thousands`  keyword allows integers to be parsed correctly:

In [132]: print(open('tmp.csv').read())
ID|level|category
Patient1|123,000|x
Patient2|23,000|y
Patient3|1,234,018|z

In [133]: df = pd.read_csv('tmp.csv', sep='|', thousands=',')

In [134]: df
Out[134]: 
 ID    level category
0  Patient1   123000        x
1  Patient2    23000        y
2  Patient3  1234018        z

In [135]: df.level.dtype
Out[135]: dtype('int64')

### NA values[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#na-values "Permalink to this headline")

To control which values are parsed as missing values (which are signified by  `NaN`), specify a string in  `na_values`. If you specify a list of strings, then all values in it are considered to be missing values. If you specify a number (a  `float`, like  `5.0`  or an  `integer`  like  `5`), the corresponding equivalent values will also imply a missing value (in this case effectively  `[5.0,  5]`  are recognized as  `NaN`).

To completely override the default values that are recognized as missing, specify  `keep_default_na=False`.

The default  `NaN`  recognized values are  `['-1.#IND',  '1.#QNAN',  '1.#IND',  '-1.#QNAN',  '#N/A  N/A',  '#N/A',  'N/A',  'n/a',  'NA',  '<NA>',  '#NA',  'NULL',  'null',  'NaN',  '-NaN',  'nan',  '-nan',  '']`.

Let us consider some examples:

pd.read_csv('path_to_file.csv', na_values=[5])

In the example above  `5`  and  `5.0`  will be recognized as  `NaN`, in addition to the defaults. A string will first be interpreted as a numerical  `5`, then as a  `NaN`.

pd.read_csv('path_to_file.csv', keep_default_na=False, na_values=[""])

Above, only an empty field will be recognized as  `NaN`.

pd.read_csv('path_to_file.csv', keep_default_na=False, na_values=["NA", "0"])

Above, both  `NA`  and  `0`  as strings are  `NaN`.

pd.read_csv('path_to_file.csv', na_values=["Nope"])

The default values, in addition to the string  `"Nope"`  are recognized as  `NaN`.

### Infinity[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#infinity "Permalink to this headline")

`inf`  like values will be parsed as  `np.inf`  (positive infinity), and  `-inf`  as  `-np.inf`  (negative infinity). These will ignore the case of the value, meaning  `Inf`, will also be parsed as  `np.inf`.

### Returning Series[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#returning-series "Permalink to this headline")

Using the  `squeeze`  keyword, the parser will return output with a single column as a  `Series`:

In [136]: print(open('tmp.csv').read())
level
Patient1,123000
Patient2,23000
Patient3,1234018

In [137]: output = pd.read_csv('tmp.csv', squeeze=True)

In [138]: output
Out[138]: 
Patient1     123000
Patient2      23000
Patient3    1234018
Name: level, dtype: int64

In [139]: type(output)
Out[139]: pandas.core.series.Series

### Boolean values[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#boolean-values "Permalink to this headline")

The common values  `True`,  `False`,  `TRUE`, and  `FALSE`  are all recognized as boolean. Occasionally you might want to recognize other values as being boolean. To do this, use the  `true_values`  and  `false_values`  options as follows:

In [140]: data = ('a,b,c\n'
 .....:        '1,Yes,2\n'
 .....:        '3,No,4')
 .....: 

In [141]: print(data)
a,b,c
1,Yes,2
3,No,4

In [142]: pd.read_csv(StringIO(data))
Out[142]: 
 a    b  c
0  1  Yes  2
1  3   No  4

In [143]: pd.read_csv(StringIO(data), true_values=['Yes'], false_values=['No'])
Out[143]: 
 a      b  c
0  1   True  2
1  3  False  4

### Handling “bad” lines[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#handling-bad-lines "Permalink to this headline")

Some files may have malformed lines with too few fields or too many. Lines with too few fields will have NA values filled in the trailing fields. Lines with too many fields will raise an error by default:

In [144]: data = ('a,b,c\n'
 .....:        '1,2,3\n'
 .....:        '4,5,6,7\n'
 .....:        '8,9,10')
 .....: 

In [145]: pd.read_csv(StringIO(data))
---------------------------------------------------------------------------
ParserError  Traceback (most recent call last)
<ipython-input-145-6388c394e6b8> in <module>
----> 1 pd.read_csv(StringIO(data))

/pandas/pandas/io/parsers.py in parser_f(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, dialect, error_bad_lines, warn_bad_lines, delim_whitespace, low_memory, memory_map, float_precision)
  674         )
  675 
--> 676         return _read(filepath_or_buffer, kwds)
  677 
  678     parser_f.__name__ = name

/pandas/pandas/io/parsers.py in _read(filepath_or_buffer, kwds)
  452 
  453     try:
--> 454         data = parser.read(nrows)
  455     finally:
  456         parser.close()

/pandas/pandas/io/parsers.py in read(self, nrows)
  1131     def read(self, nrows=None):
  1132         nrows = _validate_integer("nrows", nrows)
-> 1133         ret = self._engine.read(nrows)
  1134 
  1135         # May alter columns / col_dict

/pandas/pandas/io/parsers.py in read(self, nrows)
  2035     def read(self, nrows=None):
  2036         try:
-> 2037             data = self._reader.read(nrows)
  2038         except StopIteration:
  2039             if self._first_chunk:

/pandas/pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader.read()

/pandas/pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._read_low_memory()

/pandas/pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._read_rows()

/pandas/pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._tokenize_rows()

/pandas/pandas/_libs/parsers.pyx in pandas._libs.parsers.raise_parser_error()

ParserError: Error tokenizing data. C error: Expected 3 fields in line 3, saw 4

You can elect to skip bad lines:

In [29]: pd.read_csv(StringIO(data), error_bad_lines=False)
Skipping line 3: expected 3 fields, saw 4

Out[29]:
 a  b   c
0  1  2   3
1  8  9  10

You can also use the  `usecols`  parameter to eliminate extraneous column data that appear in some lines but not others:

In [30]: pd.read_csv(StringIO(data), usecols=[0, 1, 2])

 Out[30]:
 a  b   c
 0  1  2   3
 1  4  5   6
 2  8  9  10

### Dialect[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#dialect "Permalink to this headline")

The  `dialect`  keyword gives greater flexibility in specifying the file format. By default it uses the Excel dialect but you can specify either the dialect name or a  [`csv.Dialect`](https://docs.python.org/3/library/csv.html#csv.Dialect "(in Python v3.8)")  instance.

Suppose you had data with unenclosed quotes:

In [146]: print(data)
label1,label2,label3
index1,"a,c,e
index2,b,d,f

By default,  `read_csv`  uses the Excel dialect and treats the double quote as the quote character, which causes it to fail when it finds a newline before it finds the closing double quote.

We can get around this using  `dialect`:

In [147]: import csv

In [148]: dia = csv.excel()

In [149]: dia.quoting = csv.QUOTE_NONE

In [150]: pd.read_csv(StringIO(data), dialect=dia)
Out[150]: 
 label1 label2 label3
index1     "a      c      e
index2      b      d      f

All of the dialect options can be specified separately by keyword arguments:

In [151]: data = 'a,b,c~1,2,3~4,5,6'

In [152]: pd.read_csv(StringIO(data), lineterminator='~')
Out[152]: 
 a  b  c
0  1  2  3
1  4  5  6

Another common dialect option is  `skipinitialspace`, to skip any whitespace after a delimiter:

In [153]: data = 'a, b, c\n1, 2, 3\n4, 5, 6'

In [154]: print(data)
a, b, c
1, 2, 3
4, 5, 6

In [155]: pd.read_csv(StringIO(data), skipinitialspace=True)
Out[155]: 
 a  b  c
0  1  2  3
1  4  5  6

The parsers make every attempt to “do the right thing” and not be fragile. Type inference is a pretty big deal. If a column can be coerced to integer dtype without altering the contents, the parser will do so. Any non-numeric columns will come through as object dtype as with the rest of pandas objects.

### Quoting and Escape Characters[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#quoting-and-escape-characters "Permalink to this headline")

Quotes (and other escape characters) in embedded fields can be handled in any number of ways. One way is to use backslashes; to properly parse this data, you should pass the  `escapechar`  option:

In [156]: data = 'a,b\n"hello, \\"Bob\\", nice to see you",5'

In [157]: print(data)
a,b
"hello, \"Bob\", nice to see you",5

In [158]: pd.read_csv(StringIO(data), escapechar='\\')
Out[158]: 
 a  b
0  hello, "Bob", nice to see you  5

### Files with fixed width columns[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#files-with-fixed-width-columns "Permalink to this headline")

While  [`read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv "pandas.read_csv")  reads delimited data, the  [`read_fwf()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_fwf.html#pandas.read_fwf "pandas.read_fwf")  function works with data files that have known and fixed column widths. The function parameters to  `read_fwf`  are largely the same as  read_csv  with two extra parameters, and a different usage of the  `delimiter`  parameter:

-   `colspecs`: A list of pairs (tuples) giving the extents of the fixed-width fields of each line as half-open intervals (i.e., [from, to[ ). String value ‘infer’ can be used to instruct the parser to try detecting the column specifications from the first 100 rows of the data. Default behavior, if not specified, is to infer.
    
-   `widths`: A list of field widths which can be used instead of ‘colspecs’ if the intervals are contiguous.
    
-   `delimiter`: Characters to consider as filler characters in the fixed-width file. Can be used to specify the filler character of the fields if it is not spaces (e.g., ‘~’).
    

Consider a typical fixed-width data file:

In [159]: print(open('bar.csv').read())
id8141    360.242940   149.910199   11950.7
id1594    444.953632   166.985655   11788.4
id1849    364.136849   183.628767   11806.2
id1230    413.836124   184.375703   11916.8
id1948    502.953953   173.237159   12468.3

In order to parse this file into a  `DataFrame`, we simply need to supply the column specifications to the  read_fwf  function along with the file name:

# Column specifications are a list of half-intervals
In [160]: colspecs = [(0, 6), (8, 20), (21, 33), (34, 43)]

In [161]: df = pd.read_fwf('bar.csv', colspecs=colspecs, header=None, index_col=0)

In [162]: df
Out[162]: 
 1           2        3
0 
id8141  360.242940  149.910199  11950.7
id1594  444.953632  166.985655  11788.4
id1849  364.136849  183.628767  11806.2
id1230  413.836124  184.375703  11916.8
id1948  502.953953  173.237159  12468.3

Note how the parser automatically picks column names X.<column number> when  `header=None`  argument is specified. Alternatively, you can supply just the column widths for contiguous columns:

# Widths are a list of integers
In [163]: widths = [6, 14, 13, 10]

In [164]: df = pd.read_fwf('bar.csv', widths=widths, header=None)

In [165]: df
Out[165]: 
 0           1           2        3
0  id8141  360.242940  149.910199  11950.7
1  id1594  444.953632  166.985655  11788.4
2  id1849  364.136849  183.628767  11806.2
3  id1230  413.836124  184.375703  11916.8
4  id1948  502.953953  173.237159  12468.3

The parser will take care of extra white spaces around the columns so it’s ok to have extra separation between the columns in the file.

By default,  `read_fwf`  will try to infer the file’s  `colspecs`  by using the first 100 rows of the file. It can do it only in cases when the columns are aligned and correctly separated by the provided  `delimiter`  (default delimiter is whitespace).

In [166]: df = pd.read_fwf('bar.csv', header=None, index_col=0)

In [167]: df
Out[167]: 
 1           2        3
0 
id8141  360.242940  149.910199  11950.7
id1594  444.953632  166.985655  11788.4
id1849  364.136849  183.628767  11806.2
id1230  413.836124  184.375703  11916.8
id1948  502.953953  173.237159  12468.3

`read_fwf`  supports the  `dtype`  parameter for specifying the types of parsed columns to be different from the inferred type.

In [168]: pd.read_fwf('bar.csv', header=None, index_col=0).dtypes
Out[168]: 
1    float64
2    float64
3    float64
dtype: object

In [169]: pd.read_fwf('bar.csv', header=None, dtype={2: 'object'}).dtypes
Out[169]: 
0     object
1    float64
2     object
3    float64
dtype: object

### Indexes[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#indexes "Permalink to this headline")

#### Files with an “implicit” index column[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#files-with-an-implicit-index-column "Permalink to this headline")

Consider a file with one less entry in the header than the number of data column:

In [170]: print(open('foo.csv').read())
A,B,C
20090101,a,1,2
20090102,b,3,4
20090103,c,4,5

In this special case,  `read_csv`  assumes that the first column is to be used as the index of the  `DataFrame`:

In [171]: pd.read_csv('foo.csv')
Out[171]: 
 A  B  C
20090101  a  1  2
20090102  b  3  4
20090103  c  4  5

Note that the dates weren’t automatically parsed. In that case you would need to do as before:

In [172]: df = pd.read_csv('foo.csv', parse_dates=True)

In [173]: df.index
Out[173]: DatetimeIndex(['2009-01-01', '2009-01-02', '2009-01-03'], dtype='datetime64[ns]', freq=None)

#### Reading an index with a  `MultiIndex`[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-an-index-with-a-multiindex "Permalink to this headline")

Suppose you have data indexed by two columns:

In [174]: print(open('data/mindex_ex.csv').read())
year,indiv,zit,xit
1977,"A",1.2,.6
1977,"B",1.5,.5
1977,"C",1.7,.8
1978,"A",.2,.06
1978,"B",.7,.2
1978,"C",.8,.3
1978,"D",.9,.5
1978,"E",1.4,.9
1979,"C",.2,.15
1979,"D",.14,.05
1979,"E",.5,.15
1979,"F",1.2,.5
1979,"G",3.4,1.9
1979,"H",5.4,2.7
1979,"I",6.4,1.2

The  `index_col`  argument to  `read_csv`  can take a list of column numbers to turn multiple columns into a  `MultiIndex`  for the index of the returned object:

In [175]: df = pd.read_csv("data/mindex_ex.csv", index_col=[0, 1])

In [176]: df
Out[176]: 
 zit   xit
year indiv 
1977 A      1.20  0.60
 B      1.50  0.50
 C      1.70  0.80
1978 A      0.20  0.06
 B      0.70  0.20
 C      0.80  0.30
 D      0.90  0.50
 E      1.40  0.90
1979 C      0.20  0.15
 D      0.14  0.05
 E      0.50  0.15
 F      1.20  0.50
 G      3.40  1.90
 H      5.40  2.70
 I      6.40  1.20

In [177]: df.loc[1978]
Out[177]: 
 zit   xit
indiv 
A      0.2  0.06
B      0.7  0.20
C      0.8  0.30
D      0.9  0.50
E      1.4  0.90

#### Reading columns with a  `MultiIndex`[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-columns-with-a-multiindex "Permalink to this headline")

By specifying list of row locations for the  `header`  argument, you can read in a  `MultiIndex`  for the columns. Specifying non-consecutive rows will skip the intervening rows.

In [178]: from pandas._testing import makeCustomDataframe as mkdf

In [179]: df = mkdf(5, 3, r_idx_nlevels=2, c_idx_nlevels=4)

In [180]: df.to_csv('mi.csv')

In [181]: print(open('mi.csv').read())
C0,,C_l0_g0,C_l0_g1,C_l0_g2
C1,,C_l1_g0,C_l1_g1,C_l1_g2
C2,,C_l2_g0,C_l2_g1,C_l2_g2
C3,,C_l3_g0,C_l3_g1,C_l3_g2
R0,R1,,,
R_l0_g0,R_l1_g0,R0C0,R0C1,R0C2
R_l0_g1,R_l1_g1,R1C0,R1C1,R1C2
R_l0_g2,R_l1_g2,R2C0,R2C1,R2C2
R_l0_g3,R_l1_g3,R3C0,R3C1,R3C2
R_l0_g4,R_l1_g4,R4C0,R4C1,R4C2

In [182]: pd.read_csv('mi.csv', header=[0, 1, 2, 3], index_col=[0, 1])
Out[182]: 
C0              C_l0_g0 C_l0_g1 C_l0_g2
C1              C_l1_g0 C_l1_g1 C_l1_g2
C2              C_l2_g0 C_l2_g1 C_l2_g2
C3              C_l3_g0 C_l3_g1 C_l3_g2
R0      R1 
R_l0_g0 R_l1_g0    R0C0    R0C1    R0C2
R_l0_g1 R_l1_g1    R1C0    R1C1    R1C2
R_l0_g2 R_l1_g2    R2C0    R2C1    R2C2
R_l0_g3 R_l1_g3    R3C0    R3C1    R3C2
R_l0_g4 R_l1_g4    R4C0    R4C1    R4C2

`read_csv`  is also able to interpret a more common format of multi-columns indices.

In [183]: print(open('mi2.csv').read())
,a,a,a,b,c,c
,q,r,s,t,u,v
one,1,2,3,4,5,6
two,7,8,9,10,11,12

In [184]: pd.read_csv('mi2.csv', header=[0, 1], index_col=0)
Out[184]: 
 a         b   c 
 q  r  s   t   u   v
one  1  2  3   4   5   6
two  7  8  9  10  11  12

Note: If an  `index_col`  is not specified (e.g. you don’t have an index, or wrote it with  `df.to_csv(...,  index=False)`, then any  `names`  on the columns index will be  _lost_.

### Automatically “sniffing” the delimiter[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#automatically-sniffing-the-delimiter "Permalink to this headline")

`read_csv`  is capable of inferring delimited (not necessarily comma-separated) files, as pandas uses the  [`csv.Sniffer`](https://docs.python.org/3/library/csv.html#csv.Sniffer "(in Python v3.8)")  class of the csv module. For this, you have to specify  `sep=None`.

In [185]: print(open('tmp2.sv').read())
:0:1:2:3
0:0.4691122999071863:-0.2828633443286633:-1.5090585031735124:-1.1356323710171934
1:1.2121120250208506:-0.17321464905330858:0.11920871129693428:-1.0442359662799567
2:-0.8618489633477999:-2.1045692188948086:-0.4949292740687813:1.071803807037338
3:0.7215551622443669:-0.7067711336300845:-1.0395749851146963:0.27185988554282986
4:-0.42497232978883753:0.567020349793672:0.27623201927771873:-1.0874006912859915
5:-0.6736897080883706:0.1136484096888855:-1.4784265524372235:0.5249876671147047
6:0.4047052186802365:0.5770459859204836:-1.7150020161146375:-1.0392684835147725
7:-0.3706468582364464:-1.1578922506419993:-1.344311812731667:0.8448851414248841
8:1.0757697837155533:-0.10904997528022223:1.6435630703622064:-1.4693879595399115
9:0.35702056413309086:-0.6746001037299882:-1.776903716971867:-0.9689138124473498

In [186]: pd.read_csv('tmp2.sv', sep=None, engine='python')
Out[186]: 
 Unnamed: 0         0         1         2         3
0           0  0.469112 -0.282863 -1.509059 -1.135632
1           1  1.212112 -0.173215  0.119209 -1.044236
2           2 -0.861849 -2.104569 -0.494929  1.071804
3           3  0.721555 -0.706771 -1.039575  0.271860
4           4 -0.424972  0.567020  0.276232 -1.087401
5           5 -0.673690  0.113648 -1.478427  0.524988
6           6  0.404705  0.577046 -1.715002 -1.039268
7           7 -0.370647 -1.157892 -1.344312  0.844885
8           8  1.075770 -0.109050  1.643563 -1.469388
9           9  0.357021 -0.674600 -1.776904 -0.968914

### Reading multiple files to create a single DataFrame[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-multiple-files-to-create-a-single-dataframe "Permalink to this headline")

It’s best to use  [`concat()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html#pandas.concat "pandas.concat")  to combine multiple files. See the  [cookbook](https://pandas.pydata.org/pandas-docs/stable/user_guide/cookbook.html#cookbook-csv-multiple-files)  for an example.

### Iterating through files chunk by chunk[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#iterating-through-files-chunk-by-chunk "Permalink to this headline")

Suppose you wish to iterate through a (potentially very large) file lazily rather than reading the entire file into memory, such as the following:

In [187]: print(open('tmp.sv').read())
|0|1|2|3
0|0.4691122999071863|-0.2828633443286633|-1.5090585031735124|-1.1356323710171934
1|1.2121120250208506|-0.17321464905330858|0.11920871129693428|-1.0442359662799567
2|-0.8618489633477999|-2.1045692188948086|-0.4949292740687813|1.071803807037338
3|0.7215551622443669|-0.7067711336300845|-1.0395749851146963|0.27185988554282986
4|-0.42497232978883753|0.567020349793672|0.27623201927771873|-1.0874006912859915
5|-0.6736897080883706|0.1136484096888855|-1.4784265524372235|0.5249876671147047
6|0.4047052186802365|0.5770459859204836|-1.7150020161146375|-1.0392684835147725
7|-0.3706468582364464|-1.1578922506419993|-1.344311812731667|0.8448851414248841
8|1.0757697837155533|-0.10904997528022223|1.6435630703622064|-1.4693879595399115
9|0.35702056413309086|-0.6746001037299882|-1.776903716971867|-0.9689138124473498

In [188]: table = pd.read_csv('tmp.sv', sep='|')

In [189]: table
Out[189]: 
 Unnamed: 0         0         1         2         3
0           0  0.469112 -0.282863 -1.509059 -1.135632
1           1  1.212112 -0.173215  0.119209 -1.044236
2           2 -0.861849 -2.104569 -0.494929  1.071804
3           3  0.721555 -0.706771 -1.039575  0.271860
4           4 -0.424972  0.567020  0.276232 -1.087401
5           5 -0.673690  0.113648 -1.478427  0.524988
6           6  0.404705  0.577046 -1.715002 -1.039268
7           7 -0.370647 -1.157892 -1.344312  0.844885
8           8  1.075770 -0.109050  1.643563 -1.469388
9           9  0.357021 -0.674600 -1.776904 -0.968914

By specifying a  `chunksize`  to  `read_csv`, the return value will be an iterable object of type  `TextFileReader`:

In [190]: reader = pd.read_csv('tmp.sv', sep='|', chunksize=4)

In [191]: reader
Out[191]: <pandas.io.parsers.TextFileReader at 0x7f9184154b50>

In [192]: for chunk in reader:
 .....:    print(chunk)
 .....: 
 Unnamed: 0         0         1         2         3
0           0  0.469112 -0.282863 -1.509059 -1.135632
1           1  1.212112 -0.173215  0.119209 -1.044236
2           2 -0.861849 -2.104569 -0.494929  1.071804
3           3  0.721555 -0.706771 -1.039575  0.271860
 Unnamed: 0         0         1         2         3
4           4 -0.424972  0.567020  0.276232 -1.087401
5           5 -0.673690  0.113648 -1.478427  0.524988
6           6  0.404705  0.577046 -1.715002 -1.039268
7           7 -0.370647 -1.157892 -1.344312  0.844885
 Unnamed: 0         0        1         2         3
8           8  1.075770 -0.10905  1.643563 -1.469388
9           9  0.357021 -0.67460 -1.776904 -0.968914

Specifying  `iterator=True`  will also return the  `TextFileReader`  object:

In [193]: reader = pd.read_csv('tmp.sv', sep='|', iterator=True)

In [194]: reader.get_chunk(5)
Out[194]: 
 Unnamed: 0         0         1         2         3
0           0  0.469112 -0.282863 -1.509059 -1.135632
1           1  1.212112 -0.173215  0.119209 -1.044236
2           2 -0.861849 -2.104569 -0.494929  1.071804
3           3  0.721555 -0.706771 -1.039575  0.271860
4           4 -0.424972  0.567020  0.276232 -1.087401

### Specifying the parser engine[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#specifying-the-parser-engine "Permalink to this headline")

Under the hood pandas uses a fast and efficient parser implemented in C as well as a Python implementation which is currently more feature-complete. Where possible pandas uses the C parser (specified as  `engine='c'`), but may fall back to Python if C-unsupported options are specified. Currently, C-unsupported options include:

-   `sep`  other than a single character (e.g. regex separators)
    
-   `skipfooter`
    
-   `sep=None`  with  `delim_whitespace=False`
    

Specifying any of the above options will produce a  `ParserWarning`  unless the python engine is selected explicitly using  `engine='python'`.

### Reading remote files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-remote-files "Permalink to this headline")

You can pass in a URL to a CSV file:

df = pd.read_csv('https://download.bls.gov/pub/time.series/cu/cu.item',
                 sep='\t')

S3 URLs are handled as well but require installing the  [S3Fs](https://pypi.org/project/s3fs/)  library:

df = pd.read_csv('s3://pandas-test/tips.csv')

If your S3 bucket requires credentials you will need to set them as environment variables or in the  `~/.aws/credentials`  config file, refer to the  [S3Fs documentation on credentials](https://s3fs.readthedocs.io/en/latest/#credentials).

### Writing out data[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-out-data "Permalink to this headline")

#### Writing to CSV format[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-to-csv-format "Permalink to this headline")

The  `Series`  and  `DataFrame`  objects have an instance method  `to_csv`  which allows storing the contents of the object as a comma-separated-values file. The function takes a number of arguments. Only the first is required.

-   `path_or_buf`: A string path to the file to write or a file object. If a file object it must be opened with  newline=’’
    
-   `sep`  : Field delimiter for the output file (default “,”)
    
-   `na_rep`: A string representation of a missing value (default ‘’)
    
-   `float_format`: Format string for floating point numbers
    
-   `columns`: Columns to write (default None)
    
-   `header`: Whether to write out the column names (default True)
    
-   `index`: whether to write row (index) names (default True)
    
-   `index_label`: Column label(s) for index column(s) if desired. If None (default), and  header  and  index  are True, then the index names are used. (A sequence should be given if the  `DataFrame`  uses MultiIndex).
    
-   `mode`  : Python write mode, default ‘w’
    
-   `encoding`: a string representing the encoding to use if the contents are non-ASCII, for Python versions prior to 3
    
-   `line_terminator`: Character sequence denoting line end (default  os.linesep)
    
-   `quoting`: Set quoting rules as in csv module (default csv.QUOTE_MINIMAL). Note that if you have set a  float_format  then floats are converted to strings and csv.QUOTE_NONNUMERIC will treat them as non-numeric
    
-   `quotechar`: Character used to quote fields (default ‘”’)
    
-   `doublequote`: Control quoting of  `quotechar`  in fields (default True)
    
-   `escapechar`: Character used to escape  `sep`  and  `quotechar`  when appropriate (default None)
    
-   `chunksize`: Number of rows to write at a time
    
-   `date_format`: Format string for datetime objects
    

#### Writing a formatted string[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-a-formatted-string "Permalink to this headline")

The  `DataFrame`  object has an instance method  `to_string`  which allows control over the string representation of the object. All arguments are optional:

-   `buf`  default None, for example a StringIO object
    
-   `columns`  default None, which columns to write
    
-   `col_space`  default None, minimum width of each column.
    
-   `na_rep`  default  `NaN`, representation of NA value
    
-   `formatters`  default None, a dictionary (by column) of functions each of which takes a single argument and returns a formatted string
    
-   `float_format`  default None, a function which takes a single (float) argument and returns a formatted string; to be applied to floats in the  `DataFrame`.
    
-   `sparsify`  default True, set to False for a  `DataFrame`  with a hierarchical index to print every MultiIndex key at each row.
    
-   `index_names`  default True, will print the names of the indices
    
-   `index`  default True, will print the index (ie, row labels)
    
-   `header`  default True, will print the column labels
    
-   `justify`  default  `left`, will print column headers left- or right-justified
    

The  `Series`  object also has a  `to_string`  method, but with only the  `buf`,  `na_rep`,  `float_format`  arguments. There is also a  `length`  argument which, if set to  `True`, will additionally output the length of the Series.

> [Source : ](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTEwMzA5MDksMTgxMjIwODk5NF19
-->