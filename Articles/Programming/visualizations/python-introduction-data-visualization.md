Introduction to Data Visualization in Python
===
[Source](https://towardsdatascience.com/introduction-to-data-visualization-in-python-89a54c97fbed)

![enter image description here](https://miro.medium.com/max/6144/0*hzU1K3AH2u6n4wPw)

Data visualization is the discipline of trying to understand data by placing it in a visual context so that patterns, trends and correlations that might not otherwise be detected can be exposed.

Python offers multiple great graphing libraries that come packed with lots of different features. No matter if you want to create interactive, live or highly customized plots python has an excellent library for you.

To get a little overview here are a few popular plotting libraries:

-   [**Matplotlib:**](https://matplotlib.org/)  low level, provides lots of freedom
-   [**Pandas Visualization:**](https://pandas.pydata.org/pandas-docs/stable/visualization.html)  easy to use interface, built on Matplotlib
-   [**Seaborn:**](https://seaborn.pydata.org/)  high-level interface, great default styles
-   [**ggplot:**](http://ggplot.yhathq.com/)  based on R’s ggplot2, uses  [Grammar of Graphics](https://www.amazon.com/Grammar-Graphics-Statistics-Computing/dp/0387245448)
-   [**Plotly:**](https://plot.ly/python/)  can create interactive plots

In this article, we will learn how to create basic plots using Matplotlib, Pandas visualization and Seaborn as well as how to use some specific features of each library. This article will focus on the syntax and not on interpreting the graphs, which I will cover in another blog post.

In further articles, I will go over interactive plotting tools like Plotly, which is built on D3 and can also be used with JavaScript.

----------

# Importing Datasets

In this article, we will use two datasets which are freely available. The  [Iris](https://archive.ics.uci.edu/ml/datasets/iris)  and  [Wine Reviews](https://www.kaggle.com/zynicide/wine-reviews)  dataset, which we can both load in using pandas  `read_csv`  method.

![](https://miro.medium.com/max/30/1*sl_B5DS5rHD1kDvrg3qllg.png?q=20)

![](https://miro.medium.com/max/411/1*sl_B5DS5rHD1kDvrg3qllg.png)

Figure 2: Iris dataset head

![](https://miro.medium.com/max/30/1*DHn89aKqAruVzVsGqEdZYg.png?q=20)

![](https://miro.medium.com/max/996/1*DHn89aKqAruVzVsGqEdZYg.png)

Figure 3: Wine Review dataset head

----------

# Matplotlib

Matplotlib is the most popular python plotting library. It is a low-level library with a Matlab like interface which offers lots of freedom at the cost of having to write more code.

To install Matplotlib pip and conda can be used.

pip install matplotlib  
or  
conda install matplotlib

Matplotlib is specifically good for creating basic graphs like line charts, bar charts, histograms and many more. It can be imported by typing:

import matplotlib.pyplot as plt

## Scatter Plot

To create a scatter plot in Matplotlib we can use the  `scatter`  method. We will also create a figure and an axis using  `plt.subplots`  so we can give our plot a title and labels.

![](https://miro.medium.com/max/30/1*wHJsVsCZsIN2mvYOGhIcCA.png?q=20)

![](https://miro.medium.com/max/390/1*wHJsVsCZsIN2mvYOGhIcCA.png)

Figure 4: Matplotlib Scatter plot

We can give the graph more meaning by coloring in each data-point by its class. This can be done by creating a dictionary which maps from class to color and then scattering each point on its own using a for-loop and passing the respective color.

![](https://miro.medium.com/max/30/1*g7ZE1by6rcM27ulB45h3eA.png?q=20)

![](https://miro.medium.com/max/390/1*g7ZE1by6rcM27ulB45h3eA.png)

Figure 5: Scatter Plot colored by class

## Line Chart

In Matplotlib we can create a line chart by calling the  `plot`  method. We can also plot multiple columns in one graph, by looping through the columns we want and plotting each column on the same axis.

![](https://miro.medium.com/max/30/1*7_h8orPIGV42e5AIWF-7bA.png?q=20)

![](https://miro.medium.com/max/366/1*7_h8orPIGV42e5AIWF-7bA.png)

Figure 6: Line Chart

## Histogram

In Matplotlib we can create a Histogram using the  `hist`  method. If we pass it categorical data like the points column from the wine-review dataset it will automatically calculate how often each class occurs.

![](https://miro.medium.com/max/30/1*uNfH13lMewuE-n2XNbWGiw.png?q=20)

![](https://miro.medium.com/max/405/1*uNfH13lMewuE-n2XNbWGiw.png)

Figure 7: Histogram

## Bar Chart

A bar chart can be created using the  `bar`  method. The bar-chart isn’t automatically calculating the frequency of a category so we are going to use pandas  `value_counts`  function to do this. The bar-chart is useful for categorical data that doesn’t have a lot of different categories (less than 30) because else it can get quite messy.

![](https://miro.medium.com/max/30/1*XZNu7gvDaXYb7-xJ6PXNIQ.png?q=20)

![](https://miro.medium.com/max/405/1*XZNu7gvDaXYb7-xJ6PXNIQ.png)

Figure 8: Bar-Chart

----------

# Pandas Visualization

Pandas is an open source high-performance, easy-to-use library providing data structures, such as dataframes, and data analysis tools like the visualization tools we will use in this article.

Pandas Visualization makes it really easy to create plots out of a pandas dataframe and series. It also has a higher level API than Matplotlib and therefore we need less code for the same results.

Pandas can be installed using either pip or conda.

pip install pandas  
or  
conda install pandas

## Scatter Plot

To create a scatter plot in Pandas we can call  `<dataset>.plot.scatter()`  and pass it two arguments, the name of the x-column as well as the name of the y-column. Optionally we can also pass it a title.

![](https://miro.medium.com/max/30/1*rKWbvmZnJi4PDwkMt2tQ5g.png?q=20)

![](https://miro.medium.com/max/390/1*rKWbvmZnJi4PDwkMt2tQ5g.png)

Figure 9: Scatter Plot

As you can see in the image it is automatically setting the x and y label to the column names.

## Line Chart

To create a line-chart in Pandas we can call  `<dataframe>.plot.line()`. Whilst in Matplotlib we needed to loop-through each column we wanted to plot, in Pandas we don’t need to do this because it automatically plots all available numeric columns (at least if we don’t specify a specific column/s).

![](https://miro.medium.com/max/30/1*7_h8orPIGV42e5AIWF-7bA.png?q=20)

![](https://miro.medium.com/max/366/1*7_h8orPIGV42e5AIWF-7bA.png)

Figure 10: Line Chart

If we have more than one feature Pandas automatically creates a legend for us, as can be seen in the image above.

## Histogram

In Pandas, we can create a Histogram with the  `plot.hist`  method. There aren’t any required arguments but we can optionally pass some like the bin size.

![](https://miro.medium.com/max/30/1*beVHz116spOm-r5OYunZoA.png?q=20)

![](https://miro.medium.com/max/405/1*beVHz116spOm-r5OYunZoA.png)

Figure 11: Histogram

It’s also really easy to create multiple histograms.

![](https://miro.medium.com/max/30/1*xwANpRZID0XPhr4ESfS6qg.png?q=20)

![](https://miro.medium.com/max/609/1*xwANpRZID0XPhr4ESfS6qg.png)

Figure 12: Multiple Histograms

The  `subplots`  argument specifies that we want a separate plot for each feature and the  `layout`  specifies the number of plots per row and column.

## Bar Chart

To plot a bar-chart we can use the  `plot.bar()`  method, but before we can call this we need to get our data. For this we will first count the occurrences using the  `value_count()`  method and then sort the occurrences from smallest to largest using the  `sort_index()`  method.

![](https://miro.medium.com/max/30/1*OcOW7mKcLv4c71jNY40qiA.png?q=20)

![](https://miro.medium.com/max/391/1*OcOW7mKcLv4c71jNY40qiA.png)

Figure 13: Vertical Bar-Chart

It’s also really simple to make a horizontal bar-chart using the  `plot.barh()`  method.

![](https://miro.medium.com/max/30/1*z9vf-rjL7Ty0T68DIWzlng.png?q=20)

![](https://miro.medium.com/max/380/1*z9vf-rjL7Ty0T68DIWzlng.png)

Figure 14: Horizontal Bar-Chart

We can also plot other data then the number of occurrences.

![](https://miro.medium.com/max/30/1*AoST_ulRv6JvmmLFPqgK4w.png?q=20)

![](https://miro.medium.com/max/372/1*AoST_ulRv6JvmmLFPqgK4w.png)

Figure 15: Countries with the most expensive wine(on average)

In the example above we grouped the data by country and then took the mean of the wine prices, ordered it, and plotted the 5 countries with the highest average wine price.

----------

# Seaborn

Seaborn is a Python data visualization library based on Matplotlib. It provides a high-level interface for creating attractive graphs.

Seaborn has a lot to offer. You can create graphs in one line that would take you multiple tens of lines in Matplotlib. Its standard designs are awesome and it also has a nice interface for working with pandas dataframes.

It can be imported by typing:

import seaborn as sns

## Scatter plot

We can use the  `.scatterplot`  method for creating a scatterplot, and just as in Pandas we need to pass it the column names of the x and y data, but now we also need to pass the data as an additional argument because we aren’t calling the function on the data directly as we did in Pandas.

![](https://miro.medium.com/max/30/1*paa5lGLVyCPzuzxM0g1hCg.png?q=20)

![](https://miro.medium.com/max/390/1*paa5lGLVyCPzuzxM0g1hCg.png)

Figure 16: Scatterplot

We can also highlight the points by class using the  `hue`  argument, which is a lot easier than in Matplotlib.

![](https://miro.medium.com/max/30/1*WpOCsT4LhXv2PE6_Kntw9A.png?q=20)

![](https://miro.medium.com/max/390/1*WpOCsT4LhXv2PE6_Kntw9A.png)

Figure 17: Scatterplot colored by class

## Line chart

To create a line-chart the  `sns.lineplot`  method can be used. The only required argument is the data, which in our case are the four numeric columns from the Iris dataset. We could also use the  `sns.kdeplot`  method which rounds of the edges of the curves and therefore is cleaner if you have a lot of outliers in your dataset.

![](https://miro.medium.com/max/30/0*dDnPHTxd_0hiZloL?q=20)

![](https://miro.medium.com/max/337/0*dDnPHTxd_0hiZloL)

Figure 18: Line Chart

## Histogram

To create a histogram in Seaborn we use the  `sns.distplot`  method. We need to pass it the column we want to plot and it will calculate the occurrences itself. We can also pass it the number of bins, and if we want to plot a gaussian kernel density estimate inside the graph.

![](https://miro.medium.com/max/30/1*3bXHuQVWK8W9EgdxgCrzLg.png?q=20)

![](https://miro.medium.com/max/391/1*3bXHuQVWK8W9EgdxgCrzLg.png)

Figure 19: Histogram

![](https://miro.medium.com/max/30/1*icIVAWYElWDkzCdB1BuE6g.png?q=20)

![](https://miro.medium.com/max/388/1*icIVAWYElWDkzCdB1BuE6g.png)

Figure 20: Histogram with gaussian kernel density estimate

## Bar chart

In Seaborn a bar-chart can be created using the  `sns.countplot`  method and passing it the data.

![](https://miro.medium.com/max/30/1*JK28mO0Ph0WI4BpGAolBkg.png?q=20)

![](https://miro.medium.com/max/405/1*JK28mO0Ph0WI4BpGAolBkg.png)

Figure 21: Bar-Chart

# Other graphs

Now that you have a basic understanding of the Matplotlib, Pandas Visualization and Seaborn syntax I want to show you a few other graph types that are useful for extracting insides.

For most of them, Seaborn is the go-to library because of its high-level interface that allows for the creation of beautiful graphs in just a few lines of code.

## Box plots

A Box Plot is a graphical method of displaying the  [five-number summary](https://en.wikipedia.org/wiki/Five-number_summary). We can create box plots using seaborns  `sns.boxplot`  method and passing it the data as well as the x and y column name.

![](https://miro.medium.com/max/30/0*Zsl-nF0hT9BrMFp4?q=20)

![](https://miro.medium.com/max/364/0*Zsl-nF0hT9BrMFp4)

Figure 22: Boxplot

Box Plots, just like bar-charts are great for data with only a few categories but can get messy really quickly.

## Heatmap

A Heatmap is a graphical representation of data where the individual values contained in a  [matrix](https://en.wikipedia.org/wiki/Matrix_(mathematics))  are represented as colors. Heatmaps are perfect for exploring the correlation of features in a dataset.

To get the correlation of the features inside a dataset we can call  `<dataset>.corr()`, which is a Pandas dataframe method. This will give us the  [correlation matrix](https://www.displayr.com/what-is-a-correlation-matrix/).

We can now use either Matplotlib or Seaborn to create the heatmap.

Matplotlib:

![](https://miro.medium.com/max/30/1*Y73510z5S8jbBtAdhuU0-A.png?q=20)

![](https://miro.medium.com/max/305/1*Y73510z5S8jbBtAdhuU0-A.png)

Figure 23: Heatmap without annotations

To add annotations to the heatmap we need to add two for loops:

![](https://miro.medium.com/max/30/1*djE6fjLgvNR8id_9-TQQvQ.png?q=20)

![](https://miro.medium.com/max/305/1*djE6fjLgvNR8id_9-TQQvQ.png)

Figure 24: Heatmap with annotations

Seaborn makes it way easier to create a heatmap and add annotations:

![](https://miro.medium.com/max/30/1*nFikwCXWGr8vD95CGPBB4Q.png?q=20)

![](https://miro.medium.com/max/418/1*nFikwCXWGr8vD95CGPBB4Q.png)

Figure 25: Heatmap with annotations

## Faceting

Faceting is the act of breaking data variables up across multiple subplots and combining those subplots into a single figure.

Faceting is really helpful if you want to quickly explore your dataset.

To use one kind of faceting in Seaborn we can use the  `FacetGrid`. First of all, we need to define the  `FacetGrid`  and pass it our data as well as a row or column, which will be used to split the data. Then we need to call the  `map` function on our  `FacetGrid`  object and define the plot type we want to use, as well as the column we want to graph.

![](https://miro.medium.com/max/30/0*5hVqRSiIBn7VxvdC?q=20)

![](https://miro.medium.com/max/584/0*5hVqRSiIBn7VxvdC)

Figure 26: Facet-plot

You can make plots a lot bigger and more complicated than the example above. You can find a few examples  [here](https://seaborn.pydata.org/generated/seaborn.FacetGrid.html).

## Pairplot

Lastly, I will show you Seaborns  `pairplot`  and Pandas  `scatter_matrix`  , which enable you to plot a grid of pairwise relationships in a dataset.

![](https://miro.medium.com/max/30/0*KcPZIjL_6IA3WjVs?q=20)

![](https://miro.medium.com/max/637/0*KcPZIjL_6IA3WjVs)

Figure 27: Pairplot

![](https://miro.medium.com/max/30/1*HxQS2-d8kG4m1i2Q3m88dA.png?q=20)

![](https://miro.medium.com/max/722/1*HxQS2-d8kG4m1i2Q3m88dA.png)

Figure 28: Scatter matrix

As you can see in the images above these techniques are always plotting two features with each other. The diagonal of the graph is filled with histograms and the other plots are scatter plots.

----------

# Recommended Reading

[](https://towardsdatascience.com/scraping-reddit-data-1c0af3040768?source=post_page-----89a54c97fbed----------------------)

## 

Scraping Reddit data

### 

How to scrape data from Reddit using the Python Reddit API Wrapper(PRAW)

#### 

towardsdatascience.com

----------

# Conclusion

Data visualization is the discipline of trying to understand data by placing it in a visual context so that patterns, trends and correlations that might not otherwise be detected can be exposed.

Python offers multiple great graphing libraries that come packed with lots of different features. In this article, we looked at Matplotlib, Pandas visualization and Seaborn.

If you liked this article consider subscribing on my  [Youtube Channel](https://www.youtube.com/channel/UCBOKpYBjPe2kD8FSvGRhJwA)  and following me on social media.

The code covered in this article is available as a  [Github Repository](https://github.com/TannerGilbert/Tutorials/blob/master/Introduction%20to%20Data%20Visualization%20in%C2%A0Python/Introduction%20to%20Data%20Visualization%20in%C2%A0Python.ipynb).

If you have any questions, recommendations or critiques, I can be reached via  [Twitter](https://twitter.com/Tanner__Gilbert)  or the comment section.

[](https://towardsdatascience.com/?source=post_sidebar--------------------------post_sidebar-)

## Towards Data Science

#### Sharing concepts, ideas, and codes.

Follow

#### 757

#### Thanks to  TDS Team  and  David Errington.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA5OTExNDA0MV19
-->