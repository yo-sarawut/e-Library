
How to scrape Yahoo Finance and extract fundamental stock market data using Python, LXML, and Pandas
===
In this blog post I’ll show you how to scrape  [Income Statement](https://finance.yahoo.com/quote/MFT.NZ/financials?p=MFT.NZ),  [Balance Sheet](https://finance.yahoo.com/quote/MFT.NZ/balance-sheet?p=MFT.NZ), and  [Cash Flow](https://finance.yahoo.com/quote/MFT.NZ/cash-flow?p=MFT.NZ)  data for companies from Yahoo Finance using  [Python](https://www.python.org/),  [LXML](https://lxml.de/), and  [Pandas](https://pandas.pydata.org/).

I’ll use data from  [Mainfreight NZ (MFT.NZ)](https://finance.yahoo.com/quote/MFT.NZ/financials?p=MFT.NZ)  as an example, but the code will work for any stock symbol on Yahoo Finance.

The screenshot below shows a Pandas DataFrame with MFT.NZ balance sheet data, which you can expect to get by following the steps in this blog post:

![](https://www.mattbutton.com/images/2019/mft-dataframe-balance-sheet-final-oct-2019.png)

After taking you step by step on how to fetch data from the balance sheet, I’ll show you how to generalise the code to also generate a DataFrame containing data from the Income Statement, and Cash Flow statement.

After creating the Pandas DataFrames, I’ll then show you how to export everything to an Excel file, so you’ll have output that looks something like this:

![](https://www.mattbutton.com/images/2019/mft-nz-scraped-oct-2019.png)

This post was last updated in October, 2019. Prior to this, Yahoo Finance conveniently had all this data in a regular HTML table, which made extracting the data super easy. Since then, they’ve updated the page with a new structure, which was a wee bit tricker to get the data from. Fortunately, it’s still possible. Read on to find out how.

### Disclaimers

Before we start, a few disclaimers:

-   This code doesn’t come with any guarantee or warranty.
-   I’m not a financial advisor. This blog post doesn’t represent financial advice.
-   I don’t recommend the use of this code for any investment decisions.
-   This code is designed for personal use, and isn’t designed for high-volume extractions.
-   Use the code at your own risk.

### Prerequisites

Make sure you have installed the  [Anaconda distribution of Python](https://www.anaconda.com/download/)  .. this includes  [Jupyter Notebook](https://jupyter.org/), which we’ll use throughout this blog post.

Now we begin!

### Find the ticker symbol

In this case, we’ll be scraping data for Mainfreight NZ.

In Yahoo Finance, the symbol for Mainfreight is  [MFT.NZ](https://finance.yahoo.com/quote/MFT.NZ/balance-sheet?p=MFT.NZ):

![](https://www.mattbutton.com/images/2019/mft-symbol-oct-2019.png)

### Take a look at the Balance Sheet data that we’re going to scrape.

Here’s an example of some of the financial data we’ll be wanting to extract. Take note of the data displayed. Once we’ve scraped the data, we’ll cross-check it to ensure the scraping was accurate.

![](https://www.mattbutton.com/images/2019/mft-balance-sheet-top-oct-2019.png)

### Inspect the page source

Open up the Chrome developer tools, and inspect the page source. If you inspect the “Cash And Cash Equivalents” row, you’ll see something like this:

![](https://www.mattbutton.com/images/2019/mft-balance-sheet-table-oct-2019.png)

Note that:

-   Table rows in the table have the class  `D(tbr)`
-   Values such as  `Cash And Cash Equivalents`  and  `115,184`  are within a  `span`  within each row
-   This is true for all rows in the table, including the first row titled  `Breakdown`  with dates such as  `3/31/2019`

Because of this, we can use XPath queries to extract the data that we want.

### Scrape some balance sheet data

Open up  [Jupyter Notebook](https://jupyter.org/), and execute the following code block:

```python
from datetime import datetime
import lxml
from lxml import html
import requests
import numpy as np
import pandas as pd

symbol = 'MFT.NZ'

url = 'https://finance.yahoo.com/quote/' + symbol + '/balance-sheet?p=' + symbol

# Set up the request headers that we're going to use, to simulate
# a request by the Chrome browser. Simulating a request from a browser
# is generally good practice when building a scraper
headers = {
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3',
    'Accept-Encoding': 'gzip, deflate, br',
    'Accept-Language': 'en-US,en;q=0.9',
    'Cache-Control': 'max-age=0',
    'Pragma': 'no-cache',
    'Referrer': 'https://google.com',
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36'
}

# Fetch the page that we're going to parse, using the request headers
# defined above
page = requests.get(url, headers)

# Parse the page with LXML, so that we can start doing some XPATH queries
# to extract the data that we want
tree = html.fromstring(page.content)

# Smoke test that we fetched the page by fetching and displaying the H1 element
tree.xpath("//h1/text()")
```

You should see some output which looks like the following:

![](https://www.mattbutton.com/images/2019/mft-balance-sheet-h1-oct-2019.png)

### Reading the financial data

Add a new cell to your Jupyter notebook, and add the following:

```python
table_rows = tree.xpath("//div[contains(@class, 'D(tbr)')]")

# Ensure that some table rows are found; if none are found, then it's possible
# that Yahoo Finance has changed their page layout, or have detected
# that you're scraping the page.
assert len(table_rows) > 0

parsed_rows = []

for table_row in table_rows:
    parsed_row = []
    el = table_row.xpath("./div")
    
    none_count = 0
    
    for rs in el:
        try:
            (text,) = rs.xpath('.//span/text()[1]')
            parsed_row.append(text)
        except ValueError:
            parsed_row.append(np.NaN)
            none_count += 1

    if (none_count < 4):
        parsed_rows.append(parsed_row)

df = pd.DataFrame(parsed_rows)
df
```

After executing the code, you should see output which looks like:

![](https://www.mattbutton.com/images/2019/mft-balance-sheet-initial-scrape-oct-2019.png)

There are a few observations to be taken from the screenshot of the Pandas DataFrame above:

-   The header row contains index values (0, 1, 2, 3, etc), rather than useful column names.
-   The first row of the table contains dates.
-   The first column contains account names.
-   Rows such as  **Short Term Investments**  contain “None” where there are dashes (which represent no value) in Yahoo Finance, and 0’s when there are 0’s.

Cross-check this output with the Balance Sheet in Yahoo Finance. The data should match. For example:

![](https://www.mattbutton.com/images/2019/mft-balance-sheet-table-oct-2019.png)

Next, we’ll do some data cleanups and transformations to make the data more useful.

### Clean up the data

Because we’re using Pandas, it’ll be more convenient if the columns are the account names, and the rows are indexed by Date, so let’s do that now:

```python
df = pd.DataFrame(parsed_rows)
df = df.set_index(0) # Set the index to the first column: 'Period Ending'.
df = df.transpose() # Transpose the DataFrame, so that our header contains the account names

# Rename the "Breakdown" column to "Date"
cols = list(df.columns)
cols[0] = 'Date'
df = df.set_axis(cols, axis='columns', inplace=False)

df
```

You should now see output which looks like:

![](https://www.mattbutton.com/images/2019/mft-transposed-oct-2019.png)

Much better!

Now, let’s look at the data types of these columns:

```python
df.dtypes
```

![](https://www.mattbutton.com/images/2019/mft-raw-dtypes-oct-2019.png)

A few observations:

-   **Period Ending**  is of type ‘object’ when it should be a date type. We’re not going to be able to convert this to a date column since Income Statement and Statement of Cash Flows have “ttm” as the date value of the first column.
-   All other columns such as  **Cash and Cash Equivalents**  are also of type ‘object’ when they should be numeric.

Let’s do the conversion to numeric:

```python
numeric_columns = list(df.columns)[1::] # Take all columns, except the first (which is the 'Date' column)

for column_name in numeric_columns:
    df[column_name] = df[column_name].str.replace(',', '') # Remove the thousands separator
    df[column_name] = df[column_name].astype(np.float64) # Convert the column to float64

df.dtypes
```

The numeric columns should be now of type  **float64**:

![](https://www.mattbutton.com/images/2019/mft-float-columns-oct-2019.png)

Let’s have another look at the DataFrame,:

```python
df
```

Which should output something something like:

![](https://www.mattbutton.com/images/2019/mft-dataframe-balance-sheet-final-oct-2019.png)

Looking good! Now the Balance Sheet data has been fully scraped, with correct data types, in a form that’s ready to use.

## Scraping Income Statement data from Yahoo Finance

Now we’ll create a more generalised form of the code above, by combining the code into a method.

```python
from datetime import datetime
import lxml
from lxml import html
import requests
import numpy as np
import pandas as pd

def get_page(url):
    # Set up the request headers that we're going to use, to simulate
    # a request by the Chrome browser. Simulating a request from a browser
    # is generally good practice when building a scraper
    headers = {
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3',
        'Accept-Encoding': 'gzip, deflate, br',
        'Accept-Language': 'en-US,en;q=0.9',
        'Cache-Control': 'max-age=0',
        'Pragma': 'no-cache',
        'Referrer': 'https://google.com',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36'
    }

    return requests.get(url, headers)

def parse_rows(table_rows):
    parsed_rows = []

    for table_row in table_rows:
        parsed_row = []
        el = table_row.xpath("./div")

        none_count = 0

        for rs in el:
            try:
                (text,) = rs.xpath('.//span/text()[1]')
                parsed_row.append(text)
            except ValueError:
                parsed_row.append(np.NaN)
                none_count += 1

        if (none_count < 4):
            parsed_rows.append(parsed_row)
            
    return pd.DataFrame(parsed_rows)

def clean_data(df):
    df = df.set_index(0) # Set the index to the first column: 'Period Ending'.
    df = df.transpose() # Transpose the DataFrame, so that our header contains the account names
    
    # Rename the "Breakdown" column to "Date"
    cols = list(df.columns)
    cols[0] = 'Date'
    df = df.set_axis(cols, axis='columns', inplace=False)
    
    numeric_columns = list(df.columns)[1::] # Take all columns, except the first (which is the 'Date' column)

    for column_name in numeric_columns:
        df[column_name] = df[column_name].str.replace(',', '') # Remove the thousands separator

        df[column_name] = df[column_name].astype(np.float64) # Convert the column to
        
    return df

def scrape_table(url):
    # Fetch the page that we're going to parse
    page = get_page(url);

    # Parse the page with LXML, so that we can start doing some XPATH queries
    # to extract the data that we want
    tree = html.fromstring(page.content)

    # Fetch all div elements which have class 'D(tbr)'
    table_rows = tree.xpath("//div[contains(@class, 'D(tbr)')]")
    
    # Ensure that some table rows are found; if none are found, then it's possible
    # that Yahoo Finance has changed their page layout, or have detected
    # that you're scraping the page.
    assert len(table_rows) > 0
    
    df = parse_rows(table_rows)
    df = clean_data(df)
        
    return df

symbol = 'MFT.NZ'
balance_sheet_url = 'https://finance.yahoo.com/quote/' + symbol + '/balance-sheet?p=' + symbol

df_balance_sheet = scrape_table(balance_sheet_url)
df_balance_sheet
```

You should get the same output as the final balance sheet above. The only change will be that the ‘Period Ending’ column is now called ‘Date’.

Now, let’s try the same method with the URL for income statement:

```python
df_income_statement = scrape_table('https://finance.yahoo.com/quote/' + symbol + '/financials?p=' + symbol)
df_income_statement
```

![](https://www.mattbutton.com/images/2019/mft-income-statement.png)

Cross check these values with the income statement on yahoo finance:

![](https://www.mattbutton.com/images/2019/mft-yahoo-income-statement.png)

and they match!

## Scraping Statement of Cash Flows data from Yahoo Finance

Now that we’ve got a generic method that can be used on the Balance Sheet, and Income Statement, let’s try it on the Cash Flow statement.

```python
df_cash_flow = scrape_table('https://finance.yahoo.com/quote/' + symbol + '/cash-flow?p=' + symbol)
df_cash_flow
```

![](https://www.mattbutton.com/images/2019/mft-cash-flow.png)

Cross check these values with the cash flow statement on Yahoo Finance:

![](https://www.mattbutton.com/images/2019/mft-yahoo-cash-flow.png)

and they match!

Now you’ve got the following Pandas  [DataFrames](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.html):

-   **df_cash_flow**, containing data scraped from the Statement of Cash Flows
-   **df_income_statement**, containing data scraped from the Income Statement
-   **df_balance_sheet**, containing data scraped from the Balance Sheet

## Exporting to Excel

It’s possible to export the Pandas DataFrame to Excel via ExcelWriter.

Below is the code to export to an Excel file with three worksheets; Income Statement, Balance Sheet, and Statement of Cash Flows

```python
date = datetime.today().strftime('%Y-%m-%d')
writer = pd.ExcelWriter(symbol + '-' + date + '-scraped.xlsx')
df_income_statement.to_excel(writer,'Income Statement')
df_balance_sheet.to_excel(writer,'Balance Sheet')
df_cash_flow.to_excel(writer,'Statement of Cash Flows')
writer.save()
```

I imported the file into Google Sheets, and got the following:

![](https://www.mattbutton.com/images/2019/mft-nz-scraped.png)








> Source: [MattButton.com](https://www.mattbutton.com/2019/01/24/how-to-scrape-yahoo-finance-and-extract-fundamental-stock-market-data-using-python-lxml-and-pandas/?fbclid=IwAR1BxGgqEpZHsgm5s_XbH_WsfKt1tAhdWBrvx1xMwiXS3_zXhJVSsfhLnHs).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1Mzk0NzQzNF19
-->