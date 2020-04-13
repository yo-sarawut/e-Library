# Using Pandas to Create and Excel Diff \(หาความแตกต่างของ Excel file\)

The [original article](http://pbpython.com/excel-diff-pandas.html) contains some Updating the Excel diff article to work with more recent versions of pandas that no longer use panel.

The new article can be read [here](http://pbpython.com/excel-diff-pandas-update.html)

```python
import pandas as pd
```

## Define the diff function to show the changes in each field

```python
def report_diff(x):
    return x[0] if x[0] == x[1] else '{} ---> {}'.format(*x)
```

## Read in the two files but call the data old and new and create columns to track

```python
old = pd.read_excel('data/sample-address-1.xlsx', 'Sheet1', na_values=['NA'])
new = pd.read_excel('data/sample-address-2.xlsx', 'Sheet1', na_values=['NA'])
old['version'] = "old"
new['version'] = "new"
```

```python
old.head()
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 935480 | Bruen Group | 5131 Nienow Viaduct Apt. 290 | Port Arlie | Alabama | 14118 | old |
| 1 | 371770 | Cruickshank-Boyer | 839 Lana Expressway Suite 234 | South Viviana | Alabama | 57838 | old |
| 2 | 548367 | Spencer, Grady and Herman | 65387 Lang Circle Apt. 516 | Greenholtbury | Alaska | 58394 | old |
| 3 | 296620 | Schamberger, Hagenes and Brown | 26340 Ferry Neck Apt. 612 | McCulloughstad | Alaska | 74052 | old |
| 4 | 132971 | Williamson, Schumm and Hettinger | 89403 Casimer Spring | Jeremieburgh | Arkansas | 62785 | old |

```python
new.head()
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 935480 | Bruen Group | 5131 Nienow Viaduct Apt. 290 | Port Arlie | Alabama | 14118 | new |
| 1 | 371770 | Cruickshank-Boyer | 839 Lana Expressway Suite 234 | South Viviana | Alabama | 57838 | new |
| 2 | 548367 | Spencer, Grady and Herman | 65387 Lang Circle Apt. 516 | Greenholtbury | Alaska | 58394 | new |
| 3 | 132971 | Williamson, Schumm and Hettinger | 89403 Casimer Spring | Jeremieburgh | Arkansas | 62785 | new |
| 4 | 985603 | Bosco-Upton | 03369 Moe Way | Port Casandra | Arkansas | 86014 | new |

## check what is added, dropped and potentially changed

```python
# We use the account numbers as the keys to check what is added, dropped and potentially changed
# Using sets makes the deduping easy and we can use set operations to figure out groupings
old_accts_all = set(old['account number'])
new_accts_all = set(new['account number'])

dropped_accts = old_accts_all - new_accts_all
added_accts = new_accts_all - old_accts_all
```

```python
#Join all the data together and ignore indexes so it all gets concatenated
all_data = pd.concat([old,new],ignore_index=True)
```

```python
all_data.head()
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 935480 | Bruen Group | 5131 Nienow Viaduct Apt. 290 | Port Arlie | Alabama | 14118 | old |
| 1 | 371770 | Cruickshank-Boyer | 839 Lana Expressway Suite 234 | South Viviana | Alabama | 57838 | old |
| 2 | 548367 | Spencer, Grady and Herman | 65387 Lang Circle Apt. 516 | Greenholtbury | Alaska | 58394 | old |
| 3 | 296620 | Schamberger, Hagenes and Brown | 26340 Ferry Neck Apt. 612 | McCulloughstad | Alaska | 74052 | old |
| 4 | 132971 | Williamson, Schumm and Hettinger | 89403 Casimer Spring | Jeremieburgh | Arkansas | 62785 | old |

```python
# Let's see what changes in the main columns we care about
# Change drop_duplicates syntax: keep=last
changes = all_data.drop_duplicates(subset=["account number", 
                                           "name", "street", 
                                           "city","state", 
                                           "postal code"], keep='last')
```

```python
changes.head()
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | 296620 | Schamberger, Hagenes and Brown | 26340 Ferry Neck Apt. 612 | McCulloughstad | Alaska | 74052 | old |
| 24 | 595932 | Kuhic, Eichmann and West | 4059 Tobias Inlet | New Rylanfurt | Illinois | 89271 | old |
| 30 | 558879 | Watsica Group | 95616 Enos Grove Suite 139 | West Atlas | Iowa | 47419 | old |
| 96 | 880043 | Beatty Inc | 3641 Schaefer Isle Suite 171 | North Gardnertown | Wyoming | 64318 | old |
| 100 | 935480 | Bruen Group | 5131 Nienow Viaduct Apt. 290 | Port Arlie | Alabama | 14118 | new |

## Get all the duplicate rows

```python
dupe_accts = changes[changes['account number'].duplicated() == True]['account number'].tolist()
dupes = changes[changes["account number"].isin(dupe_accts)]
```

```python
dupes
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 24 | 595932 | Kuhic, Eichmann and West | 4059 Tobias Inlet | New Rylanfurt | Illinois | 89271 | old |
| 30 | 558879 | Watsica Group | 95616 Enos Grove Suite 139 | West Atlas | Iowa | 47419 | old |
| 96 | 880043 | Beatty Inc | 3641 Schaefer Isle Suite 171 | North Gardnertown | Wyoming | 64318 | old |
| 123 | 595932 | Kuhic, Eichmann and West | 4059 Tobias St | New Rylanfurt | Illinois | 89271 | new |
| 129 | 558879 | Watsica Group | 829 Big street | Smithtown | Ohio | 47919 | new |
| 195 | 880043 | Beatty Inc | 3641 Schaefer Isle Suite 171 | North Gardnertown | Wyoming | 64918 | new |

## Pull out the old and new data into separate dataframes

```python
change_new = dupes[(dupes["version"] == "new")]
change_old = dupes[(dupes["version"] == "old")]
```

## Drop the temp columns - we don't need them now

```python
change_new = change_new.drop(['version'], axis=1)
change_old = change_old.drop(['version'], axis=1)
```

## Index on the account numbers

```python
change_new.set_index('account number', inplace=True)
change_old.set_index('account number', inplace=True)
```

```python
df_all_changes = pd.concat([change_old, change_new],
                           axis='columns',
                           keys=['old', 'new'],
                           join='outer')
```

```python
df_all_changes
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead tr th {  
        text-align: left;  
    }  
  
    .dataframe thead tr:last-of-type th {  
        text-align: right;  
    }  


|  | old | new |  |  |  |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  | name | street | city | state | postal code | name | street | city | state | postal code |
| account number |  |  |  |  |  |  |  |  |  |  |
| 595932 | Kuhic, Eichmann and West | 4059 Tobias Inlet | New Rylanfurt | Illinois | 89271 | Kuhic, Eichmann and West | 4059 Tobias St | New Rylanfurt | Illinois | 89271 |
| 558879 | Watsica Group | 95616 Enos Grove Suite 139 | West Atlas | Iowa | 47419 | Watsica Group | 829 Big street | Smithtown | Ohio | 47919 |
| 880043 | Beatty Inc | 3641 Schaefer Isle Suite 171 | North Gardnertown | Wyoming | 64318 | Beatty Inc | 3641 Schaefer Isle Suite 171 | North Gardnertown | Wyoming | 64918 |

```python
df_all_changes = df_all_changes.swaplevel(axis='columns')[change_new.columns[0:]]
```

```python
df_all_changes
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead tr th {  
        text-align: left;  
    }  
  
    .dataframe thead tr:last-of-type th {  
        text-align: right;  
    }  


|  | name | street | city | state | postal code |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  | old | new | old | new | old | new | old | new | old | new |
| account number |  |  |  |  |  |  |  |  |  |  |
| 595932 | Kuhic, Eichmann and West | Kuhic, Eichmann and West | 4059 Tobias Inlet | 4059 Tobias St | New Rylanfurt | New Rylanfurt | Illinois | Illinois | 89271 | 89271 |
| 558879 | Watsica Group | Watsica Group | 95616 Enos Grove Suite 139 | 829 Big street | West Atlas | Smithtown | Iowa | Ohio | 47419 | 47919 |
| 880043 | Beatty Inc | Beatty Inc | 3641 Schaefer Isle Suite 171 | 3641 Schaefer Isle Suite 171 | North Gardnertown | North Gardnertown | Wyoming | Wyoming | 64318 | 64918 |

```python
df_changed = df_all_changes.groupby(level=0, axis=1).apply(lambda frame: frame.apply(report_diff, axis=1))
df_changed = df_changed.reset_index()
```

```python
df_changed
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | city | name | postal code | state | street |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 595932 | New Rylanfurt | Kuhic, Eichmann and West | 89271 | Illinois | 4059 Tobias Inlet ---&gt; 4059 Tobias St |
| 1 | 558879 | West Atlas ---&gt; Smithtown | Watsica Group | 47419 ---&gt; 47919 | Iowa ---&gt; Ohio | 95616 Enos Grove Suite 139 ---&gt; 829 Big street |
| 2 | 880043 | North Gardnertown | Beatty Inc | 64318 ---&gt; 64918 | Wyoming | 3641 Schaefer Isle Suite 171 |

## Diff'ing is done, we need to get a list of removed and added items

```python
df_removed = changes[changes["account number"].isin(dropped_accts)]
df_removed
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | 296620 | Schamberger, Hagenes and Brown | 26340 Ferry Neck Apt. 612 | McCulloughstad | Alaska | 74052 | old |

```python
df_added = changes[changes["account number"].isin(added_accts)]
df_added
```

  
    .dataframe tbody tr th:only-of-type {  
        vertical-align: middle;  
    }  
  
    .dataframe tbody tr th {  
        vertical-align: top;  
    }  
  
    .dataframe thead th {  
        text-align: right;  
    }  


|  | account number | name | street | city | state | postal code | version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 199 | 34777 | MyCo | 7833 Old Pine Drive | Orlando | Florida | 32789 | new |

## Save the changes to excel but only include the columns we care about

```python
output_columns = ["account number", "name", "street", "city", "state", "postal code"]
writer = pd.ExcelWriter("data/my-diff.xlsx")
df_changed.to_excel(writer,"changed", index=False, columns=output_columns)
df_removed.to_excel(writer,"removed",index=False, columns=output_columns)
df_added.to_excel(writer,"added",index=False, columns=output_columns)
writer.save()
print('success')
```

