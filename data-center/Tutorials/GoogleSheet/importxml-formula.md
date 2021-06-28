
 IMPORTXML formula in Google Sheets
 ==
 ![enter image description here](https://blog.sheetgo.com/wp-content/uploads/2017/03/google-sheets-blog-images-05.png)

The  [IMPORTXML formula](https://support.google.com/docs/answer/3093342)  function in Google Sheets lets you import data from structured data types like HTML and XML. It also supports data import from CSV, TSV, RSS and ATOM XML feeds. This makes it a great tool for importing data from websites for web scraping or data mining purposes.

### Syntax

=IMPORTXML(url, xpath_query)

-   **url**  – this is the address (uniform resource locator) to the structured page on the web, from which you’re importing data. This can take two forms:

> A valid and fully qualified location in the form of text (enclosed in double quotes). For example: “https://en.wikipedia.org/wiki/Tiger_Woods”

> Or it can be a reference to a cell (like B1) within Google Sheets, where the url is stored.

-   **xpath_query**  – this is the XPath query to run on the structured data. Simply put, this specifies what kind of information we are trying to fetch. For instance, using “//h1/@id” as xpath_query gives all the id attributes within the anchor < h1 > tags available on the page. For XPath syntax guidelines, check out  [this link](https://www.w3schools.com/xml/xpath_syntax.asp).

If this is new to you, you may be a bit confused when looking at the  **xpath_query**  parameter. Essentially, this parameter tells the function what data to pull from the website.

There’s a wide range of options to enter for this parameter, so if you want to learn more about it I encourage you to click the link above and find out how you can import exactly the data you want!

### Usage: IMPORTXML formula

=IMPORTXML(url,”all the hyperlink titles in the page”)

Take a look at the snapshot below. I am trying to import the data into cell B3, which is therefore the destination to key in the IMPORTXML formula.

![importxml google sheets 1](https://blog.sheetgo.com/wp-content/uploads/2021/04/1.-IMPORTXML-function-info.png "1. IMPORTXML function info")

Ensure the url is valid by enclosing the url within  **double quotes**  and hitting the  **Enter key**. The formula I use here is  **=IMPORTXML(“https://en.wikipedia.org/wiki/Tiger_Woods”,”//a/@title”)**.

The Xpath query //a/@title is used to summon all the hyperlink titles within the article.

Below is what you’ll see as Google Sheets tries to fetch the data. The higher the number of nodes in the structured data file, the longer it might take to finish the data import.

![importxml google sheets 2](https://blog.sheetgo.com/wp-content/uploads/2021/04/2.-IMPORTXML-loading-data-500x300-1.png "2. IMPORTXML loading data 500x300")

While the data import is in progress, the cell in which you typed the formula looks like it generated an error.

However, it isn’t an error, just a transient state. This means that the data is loading. Hover your mouse over the cell to see the following description.

![importxml google sheets 3](https://blog.sheetgo.com/wp-content/uploads/2021/04/3.-IMPORTXML-loading-data-error-500x300-1.png "3. IMPORTXML loading data error 500x300")

As soon as Google Sheets loads the data, the error disappears. You’ll notice the data extends from the formula cell (B3) to the right and further down.

![importxml google sheets 4](https://blog.sheetgo.com/wp-content/uploads/2021/04/4.-IMPORTXML-hyperlink-example.png "4. IMPORTXML hyperlink example")

It’s important that you keep the expected area of the result clear of any values. Otherwise, IMPORTXML formula might cough up a #REF! error.

For example, the following image demonstrates what happens if you have any values, for instance, in cell B9.

![importxml google sheets 5](https://blog.sheetgo.com/wp-content/uploads/2021/04/5.-IMPORTXML-Ref-error-example.png "5. IMPORTXML Ref error example")

=IMPORTXML(url cell reference, “all the h2 headers in the page”)

In this example, in the cell B1, I have stored the  **url**  to the page from which I am trying to import the header information.

I’ll use that cell as a reference in the IMPORTXML formula:  **=IMPORTXML(B1,”//h2″)**.

![importxml google sheets 6](https://blog.sheetgo.com/wp-content/uploads/2021/04/6.-IMPORTXML-headers-example.png "6. IMPORTXML headers example")

As you can see, the data being pulled here is different from the previous example, even though the URL is the same.

This time, I have a list of the headers in the article. This could be useful for a variety of reasons. If there’s other information that you want to import from the URL, I encourage you to read more about  [XPath queries](https://www.w3schools.com/xml/xpath_syntax.asp).

You can also check out the following blog post to learn how to pull data into Google Sheets from a table or a list on an HTML page with the  [IMPORTHTML Google Sheets function](https://blog.sheetgo.com/google-sheets-formulas/importhtml-formula-google-sheets/).


> Reference : https://blog.sheetgo.com/google-sheets-formulas/importxml-formula-google-sheets/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5MjYyOTk2Ml19
-->