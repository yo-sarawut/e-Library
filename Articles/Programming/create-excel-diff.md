
Using Pandas to Create and Excel Diff (หาความแตกต่างของ Excel file)
 ===

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
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>935480</td>
      <td>Bruen Group</td>
      <td>5131 Nienow Viaduct Apt. 290</td>
      <td>Port Arlie</td>
      <td>Alabama</td>
      <td>14118</td>
      <td>old</td>
    </tr>
    <tr>
      <td>1</td>
      <td>371770</td>
      <td>Cruickshank-Boyer</td>
      <td>839 Lana Expressway Suite 234</td>
      <td>South Viviana</td>
      <td>Alabama</td>
      <td>57838</td>
      <td>old</td>
    </tr>
    <tr>
      <td>2</td>
      <td>548367</td>
      <td>Spencer, Grady and Herman</td>
      <td>65387 Lang Circle Apt. 516</td>
      <td>Greenholtbury</td>
      <td>Alaska</td>
      <td>58394</td>
      <td>old</td>
    </tr>
    <tr>
      <td>3</td>
      <td>296620</td>
      <td>Schamberger, Hagenes and Brown</td>
      <td>26340 Ferry Neck Apt. 612</td>
      <td>McCulloughstad</td>
      <td>Alaska</td>
      <td>74052</td>
      <td>old</td>
    </tr>
    <tr>
      <td>4</td>
      <td>132971</td>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
      <td>Jeremieburgh</td>
      <td>Arkansas</td>
      <td>62785</td>
      <td>old</td>
    </tr>
  </tbody>
</table>
</div>

```python
new.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>935480</td>
      <td>Bruen Group</td>
      <td>5131 Nienow Viaduct Apt. 290</td>
      <td>Port Arlie</td>
      <td>Alabama</td>
      <td>14118</td>
      <td>new</td>
    </tr>
    <tr>
      <td>1</td>
      <td>371770</td>
      <td>Cruickshank-Boyer</td>
      <td>839 Lana Expressway Suite 234</td>
      <td>South Viviana</td>
      <td>Alabama</td>
      <td>57838</td>
      <td>new</td>
    </tr>
    <tr>
      <td>2</td>
      <td>548367</td>
      <td>Spencer, Grady and Herman</td>
      <td>65387 Lang Circle Apt. 516</td>
      <td>Greenholtbury</td>
      <td>Alaska</td>
      <td>58394</td>
      <td>new</td>
    </tr>
    <tr>
      <td>3</td>
      <td>132971</td>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
      <td>Jeremieburgh</td>
      <td>Arkansas</td>
      <td>62785</td>
      <td>new</td>
    </tr>
    <tr>
      <td>4</td>
      <td>985603</td>
      <td>Bosco-Upton</td>
      <td>03369 Moe Way</td>
      <td>Port Casandra</td>
      <td>Arkansas</td>
      <td>86014</td>
      <td>new</td>
    </tr>
  </tbody>
</table>
</div>

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
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>935480</td>
      <td>Bruen Group</td>
      <td>5131 Nienow Viaduct Apt. 290</td>
      <td>Port Arlie</td>
      <td>Alabama</td>
      <td>14118</td>
      <td>old</td>
    </tr>
    <tr>
      <td>1</td>
      <td>371770</td>
      <td>Cruickshank-Boyer</td>
      <td>839 Lana Expressway Suite 234</td>
      <td>South Viviana</td>
      <td>Alabama</td>
      <td>57838</td>
      <td>old</td>
    </tr>
    <tr>
      <td>2</td>
      <td>548367</td>
      <td>Spencer, Grady and Herman</td>
      <td>65387 Lang Circle Apt. 516</td>
      <td>Greenholtbury</td>
      <td>Alaska</td>
      <td>58394</td>
      <td>old</td>
    </tr>
    <tr>
      <td>3</td>
      <td>296620</td>
      <td>Schamberger, Hagenes and Brown</td>
      <td>26340 Ferry Neck Apt. 612</td>
      <td>McCulloughstad</td>
      <td>Alaska</td>
      <td>74052</td>
      <td>old</td>
    </tr>
    <tr>
      <td>4</td>
      <td>132971</td>
      <td>Williamson, Schumm and Hettinger</td>
      <td>89403 Casimer Spring</td>
      <td>Jeremieburgh</td>
      <td>Arkansas</td>
      <td>62785</td>
      <td>old</td>
    </tr>
  </tbody>
</table>
</div>




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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>3</td>
      <td>296620</td>
      <td>Schamberger, Hagenes and Brown</td>
      <td>26340 Ferry Neck Apt. 612</td>
      <td>McCulloughstad</td>
      <td>Alaska</td>
      <td>74052</td>
      <td>old</td>
    </tr>
    <tr>
      <td>24</td>
      <td>595932</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias Inlet</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>89271</td>
      <td>old</td>
    </tr>
    <tr>
      <td>30</td>
      <td>558879</td>
      <td>Watsica Group</td>
      <td>95616 Enos Grove Suite 139</td>
      <td>West Atlas</td>
      <td>Iowa</td>
      <td>47419</td>
      <td>old</td>
    </tr>
    <tr>
      <td>96</td>
      <td>880043</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>64318</td>
      <td>old</td>
    </tr>
    <tr>
      <td>100</td>
      <td>935480</td>
      <td>Bruen Group</td>
      <td>5131 Nienow Viaduct Apt. 290</td>
      <td>Port Arlie</td>
      <td>Alabama</td>
      <td>14118</td>
      <td>new</td>
    </tr>
  </tbody>
</table>
</div>



## Get all the duplicate rows
```python
dupe_accts = changes[changes['account number'].duplicated() == True]['account number'].tolist()
dupes = changes[changes["account number"].isin(dupe_accts)]
```


```python
dupes
```
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>24</td>
      <td>595932</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias Inlet</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>89271</td>
      <td>old</td>
    </tr>
    <tr>
      <td>30</td>
      <td>558879</td>
      <td>Watsica Group</td>
      <td>95616 Enos Grove Suite 139</td>
      <td>West Atlas</td>
      <td>Iowa</td>
      <td>47419</td>
      <td>old</td>
    </tr>
    <tr>
      <td>96</td>
      <td>880043</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>64318</td>
      <td>old</td>
    </tr>
    <tr>
      <td>123</td>
      <td>595932</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias St</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>89271</td>
      <td>new</td>
    </tr>
    <tr>
      <td>129</td>
      <td>558879</td>
      <td>Watsica Group</td>
      <td>829 Big street</td>
      <td>Smithtown</td>
      <td>Ohio</td>
      <td>47919</td>
      <td>new</td>
    </tr>
    <tr>
      <td>195</td>
      <td>880043</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>64918</td>
      <td>new</td>
    </tr>
  </tbody>
</table>
</div>



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
<div>
<style scoped>
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
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="5" halign="left">old</th>
      <th colspan="5" halign="left">new</th>
    </tr>
    <tr>
      <th></th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
    </tr>
    <tr>
      <th>account number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>595932</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias Inlet</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>89271</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias St</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>89271</td>
    </tr>
    <tr>
      <td>558879</td>
      <td>Watsica Group</td>
      <td>95616 Enos Grove Suite 139</td>
      <td>West Atlas</td>
      <td>Iowa</td>
      <td>47419</td>
      <td>Watsica Group</td>
      <td>829 Big street</td>
      <td>Smithtown</td>
      <td>Ohio</td>
      <td>47919</td>
    </tr>
    <tr>
      <td>880043</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>64318</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>64918</td>
    </tr>
  </tbody>
</table>
</div>

```python
df_all_changes = df_all_changes.swaplevel(axis='columns')[change_new.columns[0:]]
```


```python
df_all_changes
```




<div>
<style scoped>
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
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">name</th>
      <th colspan="2" halign="left">street</th>
      <th colspan="2" halign="left">city</th>
      <th colspan="2" halign="left">state</th>
      <th colspan="2" halign="left">postal code</th>
    </tr>
    <tr>
      <th></th>
      <th>old</th>
      <th>new</th>
      <th>old</th>
      <th>new</th>
      <th>old</th>
      <th>new</th>
      <th>old</th>
      <th>new</th>
      <th>old</th>
      <th>new</th>
    </tr>
    <tr>
      <th>account number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>595932</td>
      <td>Kuhic, Eichmann and West</td>
      <td>Kuhic, Eichmann and West</td>
      <td>4059 Tobias Inlet</td>
      <td>4059 Tobias St</td>
      <td>New Rylanfurt</td>
      <td>New Rylanfurt</td>
      <td>Illinois</td>
      <td>Illinois</td>
      <td>89271</td>
      <td>89271</td>
    </tr>
    <tr>
      <td>558879</td>
      <td>Watsica Group</td>
      <td>Watsica Group</td>
      <td>95616 Enos Grove Suite 139</td>
      <td>829 Big street</td>
      <td>West Atlas</td>
      <td>Smithtown</td>
      <td>Iowa</td>
      <td>Ohio</td>
      <td>47419</td>
      <td>47919</td>
    </tr>
    <tr>
      <td>880043</td>
      <td>Beatty Inc</td>
      <td>Beatty Inc</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>3641 Schaefer Isle Suite 171</td>
      <td>North Gardnertown</td>
      <td>North Gardnertown</td>
      <td>Wyoming</td>
      <td>Wyoming</td>
      <td>64318</td>
      <td>64918</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_changed = df_all_changes.groupby(level=0, axis=1).apply(lambda frame: frame.apply(report_diff, axis=1))
df_changed = df_changed.reset_index()
```


```python
df_changed
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>city</th>
      <th>name</th>
      <th>postal code</th>
      <th>state</th>
      <th>street</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>595932</td>
      <td>New Rylanfurt</td>
      <td>Kuhic, Eichmann and West</td>
      <td>89271</td>
      <td>Illinois</td>
      <td>4059 Tobias Inlet ---&gt; 4059 Tobias St</td>
    </tr>
    <tr>
      <td>1</td>
      <td>558879</td>
      <td>West Atlas ---&gt; Smithtown</td>
      <td>Watsica Group</td>
      <td>47419 ---&gt; 47919</td>
      <td>Iowa ---&gt; Ohio</td>
      <td>95616 Enos Grove Suite 139 ---&gt; 829 Big street</td>
    </tr>
    <tr>
      <td>2</td>
      <td>880043</td>
      <td>North Gardnertown</td>
      <td>Beatty Inc</td>
      <td>64318 ---&gt; 64918</td>
      <td>Wyoming</td>
      <td>3641 Schaefer Isle Suite 171</td>
    </tr>
  </tbody>
</table>
</div>





## Diff'ing is done, we need to get a list of removed and added items



```python
df_removed = changes[changes["account number"].isin(dropped_accts)]
df_removed
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>3</td>
      <td>296620</td>
      <td>Schamberger, Hagenes and Brown</td>
      <td>26340 Ferry Neck Apt. 612</td>
      <td>McCulloughstad</td>
      <td>Alaska</td>
      <td>74052</td>
      <td>old</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_added = changes[changes["account number"].isin(added_accts)]
df_added
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>account number</th>
      <th>name</th>
      <th>street</th>
      <th>city</th>
      <th>state</th>
      <th>postal code</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>199</td>
      <td>34777</td>
      <td>MyCo</td>
      <td>7833 Old Pine Drive</td>
      <td>Orlando</td>
      <td>Florida</td>
      <td>32789</td>
      <td>new</td>
    </tr>
  </tbody>
</table>
</div>



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



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NDQ1MDczNzJdfQ==
-->