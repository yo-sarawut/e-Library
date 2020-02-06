---
bookFlatSection: true

title: HTML

bookToc: true

---


## HTML[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#html "Permalink to this headline")

### Reading HTML content[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#reading-html-content "Permalink to this headline")

*Warning*

We  **highly encourage**  you to read the  [HTML Table Parsing gotchas](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-html-gotchas)  below regarding the issues surrounding the BeautifulSoup4/html5lib/lxml parsers.

The top-level  `read_html()`  function can accept an HTML string/file/URL and will parse HTML tables into list of pandas  `DataFrames`. Let’s look at a few examples.

Note

`read_html`  returns a  `list`  of  `DataFrame`  objects, even if there is only a single table contained in the HTML content.

Read a URL with no options:
```py
In [296]: url = 'https://www.fdic.gov/bank/individual/failed/banklist.html'

In [297]: dfs = pd.read_html(url)

In [298]: dfs
Out[298]: 
[                               Bank Name        City  ST   CERT                Acquiring Institution       Closing Date
 0       City National Bank of New Jersey      Newark  NJ  21111                      Industrial Bank   November 1, 2019
 1                          Resolute Bank      Maumee  OH  58317                   Buckeye State Bank   October 25, 2019
 2                  Louisa Community Bank      Louisa  KY  58112    Kentucky Farmers Bank Corporation   October 25, 2019
 3                   The Enloe State Bank      Cooper  TX  10716                   Legend Bank, N. A.       May 31, 2019
 4    Washington Federal Bank for Savings     Chicago  IL  30570                   Royal Savings Bank  December 15, 2017
 ..                                   ...         ...  ..    ...                                  ...                ...
 554                   Superior Bank, FSB    Hinsdale  IL  32646                Superior Federal, FSB      July 27, 2001
 555                  Malta National Bank       Malta  OH   6629                    North Valley Bank        May 3, 2001
 556      First Alliance Bank & Trust Co.  Manchester  NH  34264  Southern New Hampshire Bank & Trust   February 2, 2001
 557    National State Bank of Metropolis  Metropolis  IL   3815              Banterra Bank of Marion  December 14, 2000
 558                     Bank of Honolulu    Honolulu  HI  21029                   Bank of the Orient   October 13, 2000
  
 [559 rows x 6 columns]]
```
Note

The data from the above URL changes every Monday so the resulting data above and the data below may be slightly different.

Read in the content of the file from the above URL and pass it to  `read_html`  as a string:
```py
In [299]: with open(file_path, 'r') as f:
 .....:    dfs = pd.read_html(f.read())
 .....: 

In [300]: dfs
Out[300]: 
[                                    Bank Name          City  ST   CERT                Acquiring Institution       Closing Date       Updated Date
 0    Banks of Wisconsin d/b/a Bank of Kenosha       Kenosha  WI  35386                North Shore Bank, FSB       May 31, 2013       May 31, 2013
 1                        Central Arizona Bank    Scottsdale  AZ  34527                   Western State Bank       May 14, 2013       May 20, 2013
 2                                Sunrise Bank      Valdosta  GA  58185                         Synovus Bank       May 10, 2013       May 21, 2013
 3                       Pisgah Community Bank     Asheville  NC  58701                   Capital Bank, N.A.       May 10, 2013       May 14, 2013
 4                         Douglas County Bank  Douglasville  GA  21649                  Hamilton State Bank     April 26, 2013       May 16, 2013
 ..                                        ...           ...  ..    ...                                  ...                ...                ...
 500                        Superior Bank, FSB      Hinsdale  IL  32646                Superior Federal, FSB      July 27, 2001       June 5, 2012
 501                       Malta National Bank         Malta  OH   6629                    North Valley Bank        May 3, 2001  November 18, 2002
 502           First Alliance Bank & Trust Co.    Manchester  NH  34264  Southern New Hampshire Bank & Trust   February 2, 2001  February 18, 2003
 503         National State Bank of Metropolis    Metropolis  IL   3815              Banterra Bank of Marion  December 14, 2000     March 17, 2005
 504                          Bank of Honolulu      Honolulu  HI  21029                   Bank of the Orient   October 13, 2000     March 17, 2005
  
 [505 rows x 7 columns]]
```
You can even pass in an instance of  `StringIO`  if you so desire:
```py
In [301]: with open(file_path, 'r') as f:
 .....:    sio = StringIO(f.read())
 .....: 

In [302]: dfs = pd.read_html(sio)

In [303]: dfs
Out[303]: 
[                                    Bank Name          City  ST   CERT                Acquiring Institution       Closing Date       Updated Date
 0    Banks of Wisconsin d/b/a Bank of Kenosha       Kenosha  WI  35386                North Shore Bank, FSB       May 31, 2013       May 31, 2013
 1                        Central Arizona Bank    Scottsdale  AZ  34527                   Western State Bank       May 14, 2013       May 20, 2013
 2                                Sunrise Bank      Valdosta  GA  58185                         Synovus Bank       May 10, 2013       May 21, 2013
 3                       Pisgah Community Bank     Asheville  NC  58701                   Capital Bank, N.A.       May 10, 2013       May 14, 2013
 4                         Douglas County Bank  Douglasville  GA  21649                  Hamilton State Bank     April 26, 2013       May 16, 2013
 ..                                        ...           ...  ..    ...                                  ...                ...                ...
 500                        Superior Bank, FSB      Hinsdale  IL  32646                Superior Federal, FSB      July 27, 2001       June 5, 2012
 501                       Malta National Bank         Malta  OH   6629                    North Valley Bank        May 3, 2001  November 18, 2002
 502           First Alliance Bank & Trust Co.    Manchester  NH  34264  Southern New Hampshire Bank & Trust   February 2, 2001  February 18, 2003
 503         National State Bank of Metropolis    Metropolis  IL   3815              Banterra Bank of Marion  December 14, 2000     March 17, 2005
 504                          Bank of Honolulu      Honolulu  HI  21029                   Bank of the Orient   October 13, 2000     March 17, 2005
  
 [505 rows x 7 columns]]
```
Note

The following examples are not run by the IPython evaluator due to the fact that having so many network-accessing functions slows down the documentation build. If you spot an error or an example that doesn’t run, please do not hesitate to report it over on  [pandas GitHub issues page](https://www.github.com/pandas-dev/pandas/issues).

Read a URL and match a table that contains specific text:
```py
match = 'Metcalf Bank'
df_list = pd.read_html(url, match=match)
```
Specify a header row (by default  `<th>`  or  `<td>`  elements located within a  `<thead>`  are used to form the column index, if multiple rows are contained within  `<thead>`  then a MultiIndex is created); if specified, the header row is taken from the data minus the parsed header elements (`<th>`  elements).
```py
dfs = pd.read_html(url, header=0)

Specify an index column:

dfs = pd.read_html(url, index_col=0)

Specify a number of rows to skip:

dfs = pd.read_html(url, skiprows=0)

Specify a number of rows to skip using a list (`xrange`  (Python 2 only) works as well):

dfs = pd.read_html(url, skiprows=range(2))

Specify an HTML attribute:

dfs1 = pd.read_html(url, attrs={'id': 'table'})
dfs2 = pd.read_html(url, attrs={'class': 'sortable'})
print(np.array_equal(dfs1[0], dfs2[0]))  # Should be True
```
Specify values that should be converted to NaN:
```py
dfs = pd.read_html(url, na_values=['No Acquirer'])

Specify whether to keep the default set of NaN values:

dfs = pd.read_html(url, keep_default_na=False)

Specify converters for columns. This is useful for numerical text data that has leading zeros. By default columns that are numerical are cast to numeric types and the leading zeros are lost. To avoid this, we can convert these columns to strings.

url_mcc = 'https://en.wikipedia.org/wiki/Mobile_country_code'
dfs = pd.read_html(url_mcc, match='Telekom Albania', header=0,
                   converters={'MNC': str})

Use some combination of the above:

dfs = pd.read_html(url, match='Metcalf Bank', index_col=0)
```
Read in pandas  `to_html`  output (with some loss of floating point precision):
```py
df = pd.DataFrame(np.random.randn(2, 2))
s = df.to_html(float_format='{0:.40g}'.format)
dfin = pd.read_html(s, index_col=0)
```
The  `lxml`  backend will raise an error on a failed parse if that is the only parser you provide. If you only have a single parser you can provide just a string, but it is considered good practice to pass a list with one string if, for example, the function expects a sequence of strings. You may use:
```py
dfs = pd.read_html(url, 'Metcalf Bank', index_col=0, flavor=['lxml'])
```
Or you could pass  `flavor='lxml'`  without a list:
```py
dfs = pd.read_html(url, 'Metcalf Bank', index_col=0, flavor='lxml')
```
However, if you have bs4 and html5lib installed and pass  `None`  or  `['lxml',  'bs4']`  then the parse will most likely succeed. Note that  _as soon as a parse succeeds, the function will return_.
```py
dfs = pd.read_html(url, 'Metcalf Bank', index_col=0, flavor=['lxml', 'bs4'])
```
### Writing to HTML files[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#writing-to-html-files "Permalink to this headline")

`DataFrame`  objects have an instance method  `to_html`  which renders the contents of the  `DataFrame`  as an HTML table. The function arguments are as in the method  `to_string`  described above.

Note

Not all of the possible options for  `DataFrame.to_html`  are shown here for brevity’s sake. See  `to_html()`  for the full set of options.
```py
In [304]: df = pd.DataFrame(np.random.randn(2, 2))

In [305]: df
Out[305]: 
 0         1
0 -0.184744  0.496971
1 -0.856240  1.857977
```

In [306]: print(df.to_html())  # raw html
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>0</th>
 <th>1</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>-0.184744</td>
 <td>0.496971</td>
 </tr>
 <tr>
 <th>1</th>
 <td>-0.856240</td>
 <td>1.857977</td>
 </tr>
 </tbody>
</table>



The  `columns`  argument will limit the columns shown:
```py
In [307]: print(df.to_html(columns=[0]))
```
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>0</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>-0.184744</td>
 </tr>
 <tr>
 <th>1</th>
 <td>-0.856240</td>
 </tr>
 </tbody>
</table>


`float_format`  takes a Python callable to control the precision of floating point values:
```py
In [308]: print(df.to_html(float_format='{0:.10f}'.format))
```
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>0</th>
 <th>1</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>-0.1847438576</td>
 <td>0.4969711327</td>
 </tr>
 <tr>
 <th>1</th>
 <td>-0.8562396763</td>
 <td>1.8579766508</td>
 </tr>
 </tbody>
</table>


`bold_rows`  will make the row labels bold by default, but you can turn that off:

In [309]: print(df.to_html(bold_rows=False))
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>0</th>
 <th>1</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <td>0</td>
 <td>-0.184744</td>
 <td>0.496971</td>
 </tr>
 <tr>
 <td>1</td>
 <td>-0.856240</td>
 <td>1.857977</td>
 </tr>
 </tbody>
</table>

0

1

0

-0.184744

0.496971

1

-0.856240

1.857977

The  `classes`  argument provides the ability to give the resulting HTML table CSS classes. Note that these classes are  _appended_  to the existing  `'dataframe'`  class.

In [310]: print(df.to_html(classes=['awesome_table_class', 'even_more_awesome_class']))
<table border="1" class="dataframe awesome_table_class even_more_awesome_class">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>0</th>
 <th>1</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>-0.184744</td>
 <td>0.496971</td>
 </tr>
 <tr>
 <th>1</th>
 <td>-0.856240</td>
 <td>1.857977</td>
 </tr>
 </tbody>
</table>

The  `render_links`  argument provides the ability to add hyperlinks to cells that contain URLs.

New in version 0.24.

In [311]: url_df = pd.DataFrame({
 .....:    'name': ['Python', 'Pandas'],
 .....:    'url': ['https://www.python.org/', 'https://pandas.pydata.org']})
 .....: 

In [312]: print(url_df.to_html(render_links=True))
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>name</th>
 <th>url</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>Python</td>
 <td><a href="https://www.python.org/" target="_blank">https://www.python.org/</a></td>
 </tr>
 <tr>
 <th>1</th>
 <td>Pandas</td>
 <td><a href="https://pandas.pydata.org" target="_blank">https://pandas.pydata.org</a></td>
 </tr>
 </tbody>
</table>

HTML:

name

url

0

Python

[https://www.python.org/](https://www.python.org/)

1

Pandas

[https://pandas.pydata.org](https://pandas.pydata.org/)

Finally, the  `escape`  argument allows you to control whether the “<”, “>” and “&” characters escaped in the resulting HTML (by default it is  `True`). So to get the HTML without escaped characters pass  `escape=False`

In [313]: df = pd.DataFrame({'a': list('&<>'), 'b': np.random.randn(3)})

Escaped:

In [314]: print(df.to_html())
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>a</th>
 <th>b</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>&amp;</td>
 <td>-0.474063</td>
 </tr>
 <tr>
 <th>1</th>
 <td>&lt;</td>
 <td>-0.230305</td>
 </tr>
 <tr>
 <th>2</th>
 <td>&gt;</td>
 <td>-0.400654</td>
 </tr>
 </tbody>
</table>

a

b

0

&

-0.474063

1

<

-0.230305

2

>

-0.400654

Not escaped:

In [315]: print(df.to_html(escape=False))
<table border="1" class="dataframe">
 <thead>
 <tr style="text-align: right;">
 <th></th>
 <th>a</th>
 <th>b</th>
 </tr>
 </thead>
 <tbody>
 <tr>
 <th>0</th>
 <td>&</td>
 <td>-0.474063</td>
 </tr>
 <tr>
 <th>1</th>
 <td><</td>
 <td>-0.230305</td>
 </tr>
 <tr>
 <th>2</th>
 <td>></td>
 <td>-0.400654</td>
 </tr>
 </tbody>
</table>

a

b

0

&

-0.474063

1

<

-0.230305

2

>

-0.400654

Note

Some browsers may not show a difference in the rendering of the previous two HTML tables.

### HTML Table Parsing Gotchas[](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#html-table-parsing-gotchas "Permalink to this headline")

There are some versioning issues surrounding the libraries that are used to parse HTML tables in the top-level pandas io function  `read_html`.

**Issues with**  [**lxml**](https://lxml.de/)

-   Benefits
    
    > -   [**lxml**](https://lxml.de/)  is very fast.
    >     
    > -   [**lxml**](https://lxml.de/)  requires Cython to install correctly.
    >     
    
-   Drawbacks
    
    > -   [**lxml**](https://lxml.de/)  does  _not_  make any guarantees about the results of its parse  _unless_  it is given  [**strictly valid markup**](https://validator.w3.org/docs/help.html#validation_basics).
    >     
    > -   In light of the above, we have chosen to allow you, the user, to use the  [**lxml**](https://lxml.de/)  backend, but  **this backend will use**  [**html5lib**](https://github.com/html5lib/html5lib-python)  if  [**lxml**](https://lxml.de/)  fails to parse
    >     
    > -   It is therefore  _highly recommended_  that you install both  [**BeautifulSoup4**](https://www.crummy.com/software/BeautifulSoup)  and  [**html5lib**](https://github.com/html5lib/html5lib-python), so that you will still get a valid result (provided everything else is valid) even if  [**lxml**](https://lxml.de/)  fails.
    >     
    

**Issues with**  [**BeautifulSoup4**](https://www.crummy.com/software/BeautifulSoup)  **using**  [**lxml**](https://lxml.de/)  **as a backend**

-   The above issues hold here as well since  [**BeautifulSoup4**](https://www.crummy.com/software/BeautifulSoup)  is essentially just a wrapper around a parser backend.
    

**Issues with**  [**BeautifulSoup4**](https://www.crummy.com/software/BeautifulSoup)  **using**  [**html5lib**](https://github.com/html5lib/html5lib-python)  **as a backend**

-   Benefits
    
    > -   [**html5lib**](https://github.com/html5lib/html5lib-python)  is far more lenient than  [**lxml**](https://lxml.de/)  and consequently deals with  _real-life markup_  in a much saner way rather than just, e.g., dropping an element without notifying you.
    >     
    > -   [**html5lib**](https://github.com/html5lib/html5lib-python)  _generates valid HTML5 markup from invalid markup automatically_. This is extremely important for parsing HTML tables, since it guarantees a valid document. However, that does NOT mean that it is “correct”, since the process of fixing markup does not have a single definition.
    >     
    > -   [**html5lib**](https://github.com/html5lib/html5lib-python)  is pure Python and requires no additional build steps beyond its own installation.
    >     
    
-   Drawbacks
    
    > -   The biggest drawback to using  [**html5lib**](https://github.com/html5lib/html5lib-python)  is that it is slow as molasses. However consider the fact that many tables on the web are not big enough for the parsing algorithm runtime to matter. It is more likely that the bottleneck will be in the process of reading the raw text from the URL over the web, i.e., IO (input-output). For very large tables, this might not be true.
    >

> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NTYwOTYxODVdfQ==
-->