
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

> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTk2MzA5NDRdfQ==
-->