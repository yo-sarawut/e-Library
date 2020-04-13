# IO tools \(text, CSV, HDF5, …\)

The pandas I/O API is a set of top level `reader` functions accessed like [`pandas.read_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv) that generally return a pandas object. The corresponding `writer` functions are object methods that are accessed like [`DataFrame.to_csv()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html#pandas.DataFrame.to_csv). Below is a table containing available `readers` and `writers`.

| Type | Data Description | Reader | Writer |
| :--- | :--- | :--- | :--- |
| text | CSV | read\_csv | to\_csv |
| text | Fixed-Width Text File | read\_fwf | - |
| text | JSON | read\_json | to\_json |
| text | HTML | read\_html | to\_html |
| text | Local clipboard | read\_clipboard | to\_clipboard |
| - | MS Excel | read\_excel | to\_excel |
| binary | OpenDocument | read\_excel | - |
| binary | HDF5 Format | read\_hdf | to\_hdf |
| binary | Feather Format | read\_feather | to\_feather |
| binary | Parquet Format | read\_parquet | to\_parquet |
| binary | ORC Format | read\_orc | - |
| binary | Msgpack | read\_msgpack | to\_msgpack |
| binary | Stata | read\_stata | to\_stata |
| binary | SAS | read\_sas | - |
| binary | SPSS | read\_spss | - |
| binary | Python Pickle Format | read\_pickle | to\_pickle |
| SQL | SQL | read\_sql | to\_sql |
| SQL | Google BigQuery | read\_gbq | to\_gbq |

[Here](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-perf) is an informal performance comparison for some of these IO methods.

> Note
>
> For examples that use the `StringIO` class, make sure you import it according to your Python version, i.e. `from StringIO import StringIO` for Python 2 and `from io import StringIO` for Python 3.
>
> [Source : ](https://).

