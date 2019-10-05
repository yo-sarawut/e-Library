How to Generate FiveThirtyEight Graphs in Python
===

- [https://www.dataquest.io/blog/making-538-plots/](https://www.dataquest.io/blog/making-538-plots/)


![](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/538-graphs.png "538-graphs")

If you read data science articles, you may have already stumbled upon  [FiveThirtyEight’s](http://fivethirtyeight.com/)  content. Naturally, you were impressed by their  [awesome visualizations](https://fivethirtyeight.com/features/the-52-best-and-weirdest-charts-we-made-in-2016/). You wanted to make your own awesome visualizations and so asked  [Quora](https://www.quora.com/How-does-FiveThirtyEight-create-their-data-visualizations)  and  [Reddit](https://www.reddit.com/r/statistics/comments/2jon2b/anyone_knows_how_are_made_the_graphs_on/)  how to do it. You received some answers, but they were rather vague. You still can’t get the graphs done yourself.

In this post, we’ll help you. Using Python’s  [matplotlib](https://matplotlib.org/index.html#)  and  [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html), we’ll see that it’s rather easy to replicate the core parts of any FiveThirtyEight (FTE) visualization.

We’ll start here:

![default_graph](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/default_graph.png)

And, at the end of the tutorial, arrive here:

![final3](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/final3.png)

To follow along, you’ll need at least some basic knowledge of Python. If you know what’s the difference between methods and attributes, then you’re good to go.

## Introducing the dataset

We’ll work with data describing the percentages of Bachelors conferred to women in the US from 1970 to 2011. We’ll use a dataset compiled by data scientist  [Randal Olson](http://www.randalolson.com/2014/06/14/percentage-of-bachelors-degrees-conferred-to-women-by-major-1970-2012/), who collected the data from the  [National Center for Education Statistics](https://nces.ed.gov/about/).

If you want to follow along by writing code yourself, you can download the data from  [Randal’s blog](http://www.randalolson.com/wp-content/uploads/percent-bachelors-degrees-women-usa.csv). To save yourself some time, you can skip downloading the file, and just pass in the direct link to pandas’  `read_csv()`  [function](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html?highlight=read_csv#pandas.read_csv). In the following code cell, we:

-   Import the pandas module.
-   Assign the direct link toward the dataset as a  `string`  to a variable named  `direct_link`.
-   Read in the data by using  `read_csv()`, and assign the content to  `women_majors`.
-   Print information about the dataset by using the  `info()`  [method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.info.html?highlight=dataframe%20info#pandas.DataFrame.info). We’re looking for the number of rows and columns, and checking for null values at the same time.
-   Show the first five rows to understand better the structure of the dataset by using the  `head()`  [method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.head.html?highlight=dataframe%20head#pandas.DataFrame.head).

```python
import pandas as pd
direct_link = 'http://www.randalolson.com/wp-content/uploads/percent-bachelors-degrees-women-usa.csv'
women_majors = pd.read_csv(direct_link)
print(women_majors.info())
women_majors.head()
```

```python
RangeIndex: 42 entries, 0 to 41
Data columns (total 18 columns):
Year                             42 non-null int64
Agriculture                      42 non-null float64
Architecture                     42 non-null float64
Art and Performance              42 non-null float64
Biology                          42 non-null float64
Business                         42 non-null float64
Communications and Journalism    42 non-null float64
Computer Science                 42 non-null float64
Education                        42 non-null float64
Engineering                      42 non-null float64
English                          42 non-null float64
Foreign Languages                42 non-null float64
Health Professions               42 non-null float64
Math and Statistics              42 non-null float64
Physical Sciences                42 non-null float64
Psychology                       42 non-null float64
Public Administration            42 non-null float64
Social Sciences and History      42 non-null float64
dtypes: float64(17), int64(1)
memory usage: 6.0 KB
None
```
<div class="output_html rendered_html output_subarea output_execute_result">
<style>    .dataframe thead tr:only-child th {        text-align: right;    }</p>
<pre class="language-python"><code>.dataframe thead th {    text-align: left;}.dataframe tbody tr th {    vertical-align: top;}</code></pre>
</style>
<div style="overflow-x:auto;">
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Year</th>
<th>Agriculture</th>
<th>Architecture</th>
<th>Art and Performance</th>
<th>Biology</th>
<th>Business</th>
<th>Communications and Journalism</th>
<th>Computer Science</th>
<th>Education</th>
<th>Engineering</th>
<th>English</th>
<th>Foreign Languages</th>
<th>Health Professions</th>
<th>Math and Statistics</th>
<th>Physical Sciences</th>
<th>Psychology</th>
<th>Public Administration</th>
<th>Social Sciences and History</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>1970</td>
<td>4.229798</td>
<td>11.921005</td>
<td>59.7</td>
<td>29.088363</td>
<td>9.064439</td>
<td>35.3</td>
<td>13.6</td>
<td>74.535328</td>
<td>0.8</td>
<td>65.570923</td>
<td>73.8</td>
<td>77.1</td>
<td>38.0</td>
<td>13.8</td>
<td>44.4</td>
<td>68.4</td>
<td>36.8</td>
</tr>
<tr>
<th>1</th>
<td>1971</td>
<td>5.452797</td>
<td>12.003106</td>
<td>59.9</td>
<td>29.394403</td>
<td>9.503187</td>
<td>35.5</td>
<td>13.6</td>
<td>74.149204</td>
<td>1.0</td>
<td>64.556485</td>
<td>73.9</td>
<td>75.5</td>
<td>39.0</td>
<td>14.9</td>
<td>46.2</td>
<td>65.5</td>
<td>36.2</td>
</tr>
<tr>
<th>2</th>
<td>1972</td>
<td>7.420710</td>
<td>13.214594</td>
<td>60.4</td>
<td>29.810221</td>
<td>10.558962</td>
<td>36.6</td>
<td>14.9</td>
<td>73.554520</td>
<td>1.2</td>
<td>63.664263</td>
<td>74.6</td>
<td>76.9</td>
<td>40.2</td>
<td>14.8</td>
<td>47.6</td>
<td>62.6</td>
<td>36.1</td>
</tr>
<tr>
<th>3</th>
<td>1973</td>
<td>9.653602</td>
<td>14.791613</td>
<td>60.2</td>
<td>31.147915</td>
<td>12.804602</td>
<td>38.4</td>
<td>16.4</td>
<td>73.501814</td>
<td>1.6</td>
<td>62.941502</td>
<td>74.9</td>
<td>77.4</td>
<td>40.9</td>
<td>16.5</td>
<td>50.4</td>
<td>64.3</td>
<td>36.4</td>
</tr>
<tr>
<th>4</th>
<td>1974</td>
<td>14.074623</td>
<td>17.444688</td>
<td>61.9</td>
<td>32.996183</td>
<td>16.204850</td>
<td>40.5</td>
<td>18.9</td>
<td>73.336811</td>
<td>2.2</td>
<td>62.413412</td>
<td>75.3</td>
<td>77.9</td>
<td>41.8</td>
<td>18.2</td>
<td>52.6</td>
<td>66.1</td>
<td>37.3</td>
</tr>
</tbody>
</table>
</div>
</div>

Besides the  `Year`  column, every other column name indicates the subject of a Bachelor degree. Every datapoint in the Bachelor columns represents the percentage of Bachelor degrees conferred to women. Thus, every row describes the percentage for various Bachelors conferred to women in a given year.

As mentioned before, we have data from 1970 to 2011. To confirm the latter limit, let’s print the last five rows of the dataset by using the  `tail()`  [method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.tail.html?highlight=tail#pandas.DataFrame.tail):

```python
women_majors.tail()
```

<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Year</th>
<th>Agriculture</th>
<th>Architecture</th>
<th>Art and Performance</th>
<th>Biology</th>
<th>Business</th>
<th>Communications and Journalism</th>
<th>Computer Science</th>
<th>Education</th>
<th>Engineering</th>
<th>English</th>
<th>Foreign Languages</th>
<th>Health Professions</th>
<th>Math and Statistics</th>
<th>Physical Sciences</th>
<th>Psychology</th>
<th>Public Administration</th>
<th>Social Sciences and History</th>
</tr>
</thead>
<tbody>
<tr>
<th>37</th>
<td>2007</td>
<td>47.605026</td>
<td>43.100459</td>
<td>61.4</td>
<td>59.411993</td>
<td>49.000459</td>
<td>62.5</td>
<td>17.6</td>
<td>78.721413</td>
<td>16.8</td>
<td>67.874923</td>
<td>70.2</td>
<td>85.4</td>
<td>44.1</td>
<td>40.7</td>
<td>77.1</td>
<td>82.1</td>
<td>49.3</td>
</tr>
<tr>
<th>38</th>
<td>2008</td>
<td>47.570834</td>
<td>42.711730</td>
<td>60.7</td>
<td>59.305765</td>
<td>48.888027</td>
<td>62.4</td>
<td>17.8</td>
<td>79.196327</td>
<td>16.5</td>
<td>67.594028</td>
<td>70.2</td>
<td>85.2</td>
<td>43.3</td>
<td>40.7</td>
<td>77.2</td>
<td>81.7</td>
<td>49.4</td>
</tr>
<tr>
<th>39</th>
<td>2009</td>
<td>48.667224</td>
<td>43.348921</td>
<td>61.0</td>
<td>58.489583</td>
<td>48.840474</td>
<td>62.8</td>
<td>18.1</td>
<td>79.532909</td>
<td>16.8</td>
<td>67.969792</td>
<td>69.3</td>
<td>85.1</td>
<td>43.3</td>
<td>40.7</td>
<td>77.1</td>
<td>82.0</td>
<td>49.4</td>
</tr>
<tr>
<th>40</th>
<td>2010</td>
<td>48.730042</td>
<td>42.066721</td>
<td>61.3</td>
<td>59.010255</td>
<td>48.757988</td>
<td>62.5</td>
<td>17.6</td>
<td>79.618625</td>
<td>17.2</td>
<td>67.928106</td>
<td>69.0</td>
<td>85.0</td>
<td>43.1</td>
<td>40.2</td>
<td>77.0</td>
<td>81.7</td>
<td>49.3</td>
</tr>
<tr>
<th>41</th>
<td>2011</td>
<td>50.037182</td>
<td>42.773438</td>
<td>61.2</td>
<td>58.742397</td>
<td>48.180418</td>
<td>62.2</td>
<td>18.2</td>
<td>79.432812</td>
<td>17.5</td>
<td>68.426730</td>
<td>69.5</td>
<td>84.8</td>
<td>43.1</td>
<td>40.1</td>
<td>76.7</td>
<td>81.9</td>
<td>49.2</td>
</tr>
</tbody>
</table>

## The context of our FiveThirtyEight graph

Almost every FTE graph is part of an article. The graphs complement the text by illustrating a little story, or an interesting idea. We’ll need to be mindful of this while replicating our FTE graph.

To avoid digressing from our main task in this tutorial, let’s just pretend we’ve already written most of an article about the evolution of gender disparity in US education. We now need to create a graph to help readers visualize the evolution of gender disparity for Bachelors where the situation was really bad for women in 1970. We’ve already set a threshold of 20%, and now we want to graph the evolution for every Bachelor where the percentage of women graduates was less than 20% in 1970.

Let’s first identify those specific Bachelors. In the following code cell, we will:

-   Use  `.loc`, a  [label-based indexer](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.loc.html?highlight=loc#pandas.DataFrame.loc), to:
    -   select the first row (the one that corresponds to 1970);
    -   select the items in the first row only where the values are less than 20; the  `Year`  field will be checked as well, but will obviously not be included because 1970 is much greater than 20.
-   Assign the resulting content to  `under_20`.

```python
under_20 = women_majors.loc[0, women_majors.loc[0] < 20]
under_20
```

```python
Agriculture           4.229798
Architecture         11.921005
Business              9.064439
Computer Science     13.600000
Engineering           0.800000
Physical Sciences    13.800000
Name: 0, dtype: float64
```

## Using matplotlib’s default style

Let’s begin working on our graph. We’ll first take a peek at what we can build by default. In the following code block, we will:

-   Run the Jupyter magic  `%matplotlib`  to  [enable Jupyter and matplotlib work together effectively](http://ipython.readthedocs.io/en/stable/interactive/plotting.html#id1), and add  `inline`  to have our graphs displayed inside the notebook.
-   Plot the graph by using the  `plot()`  [method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html?highlight=plot#pandas.DataFrame.plot)  on  `women_majors`. We pass in to  `plot()`  the following parameters:
    -   `x`  – specifies the column from  `women_majors`  to use for the x-axis;
    -   `y`  – specifies the columns from  `women_majors`  to use for the y-axis; we’ll use the index labels of  `under_20`  which are stored in the  `.index`  attribute of this object;
    -   `figsize`  – sets the size of the figure as a  `tuple`  with the format  `(width, height)`  in inches.
-   Assign the plot object to a variable named  `under_20_graph`, and print its type to show that pandas uses  `matplotlib`  objects under the hood.

```python
under_20_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
print('Type:', type(under_20_graph))
```

```python
Type: <class 'matplotlib.axes._subplots.AxesSubplot'>
```

![](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_7_1.png)

## Using matplotlib’s fivethirtyeight style

The graph above has certain characteristics, like the width and color of the spines, the font size of the y-axis label, the absence of a grid, etc. All of these characteristics make up matplotlib’s default style.

As a short parenthesis, it’s worth mentioning that we’ll use a few technical terms about the parts of a graph throughout this post. If you feel lost at any point, you can refer to the legend below.

![anatomy1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/anatomy1.png)

Source:  [Matplotlib.org](http://matplotlib.org/faq/usage_faq.html#parts-of-a-figure)

Besides the default style, matplotlib comes with several built-in styles that we can use readily. To see a list of the available styles, we will:

-   Import the  `matplotlib.style`  [module](https://matplotlib.org/api/style_api.html?highlight=style%20available#module-matplotlib.style)  under the name  `style`.
-   Explore the content of  `matplotlib.style.available`  (a predefined variable of this module), which contains a list of all the available in-built styles.

```python
import matplotlib.style as style
style.available
```

```python
['seaborn-deep',
'seaborn-muted',
'bmh',
'seaborn-white',
'dark_background',
'seaborn-notebook',
'seaborn-darkgrid',
'grayscale',
'seaborn-paper',
'seaborn-talk',
'seaborn-bright',
'classic',
'seaborn-colorblind',
'seaborn-ticks',
'ggplot',
'seaborn',
'_classic_test',
'fivethirtyeight',
'seaborn-dark-palette',
'seaborn-dark',
'seaborn-whitegrid',
'seaborn-pastel',
'seaborn-poster']
```

You might have already observed that there’s a built-in style called  `fivethirtyeight`. Let’s use this style, and see where that leads. For that, we’ll use the aptly named  `use()`  [function](https://matplotlib.org/api/style_api.html?highlight=style%20available#matplotlib.style.use)  from the same  `matplotlib.style`  module (which we imported under the name  `style`). Then we’ll generate our graph using the same code as earlier.

```python
style.use('fivethirtyeight')
women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
```

![538_graphs_AO_11_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_11_1.png)

Wow, that’s a major change! With respect to our first graph, we can see that this one has a different background color, it has grid lines, there are no spines whatsoever, the weight and the font size of the major tick labels are different, etc.

You can read a technical description of the  `fivethirtyeight`  style  [here](https://github.com/matplotlib/matplotlib/blob/38be7aeaaac3691560aeadafe46722dda427ef47/lib/matplotlib/mpl-data/stylelib/fivethirtyeight.mplstyle)  – it should also give you a good idea about what code runs under the hood when we use this style. The author of the style sheet,  [Cameron David-Pilon](https://github.com/CamDavidsonPilon), discusses some of the characteristics  [here](https://dataorigami.net/blogs/napkin-folding/17543615-replicating-538s-plot-styles-in-matplotlib).

## The limitations of matplotlib’s fivethirtyeight style

All in all, using the  `fivethirtyeight`  style clearly brings us much closer to our goal. Nonetheless, there’s still a lot left to do. Let’s examine a simple FTE graph, and see what else we need to add to our graph.

![fandango](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/fandango.png)

Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/fandango-movies-ratings/)

By comparing the above graph with what we’ve made so far, we can see that we still need to:

-   Add a title and a subtitle.
-   Remove the block-style legend, and add labels near the relevant plot lines. We’ll also have to make the grid lines transparent around these labels.
-   Add a signature bottom bar which mentions the author of the graph and the source of the data.
-   Add a couple of other small adjustments:
    -   increase the font size of the tick labels;
    -   add a “%” symbol to one of the major tick labels of the y-axis;
    -   remove the x-axis label;
    -   bold the horizontal grid line at y = 0;
    -   add an extra grid line next to the tick labels of the y-axis;
    -   increase the lateral margins of the figure.

![adjustments](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/adjustments.png)

Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/fandango-movies-ratings/)

To minimize the time spent with generating the graph, it’s important to avoid beginning adding the title, the subtitle, or any other text snippet. In matplotlib, a text snippet is positioned by specifying the x and y coordinates, as we’ll see in some of the sections below. To replicate in detail the FTE graph above, notice that we’ll have to align vertically the tick labels of the y-axis with the title and the subtitle. We want to avoid a situation where we have the vertical alignment we want, lost it by increasing the font size of the tick labels, and then have to change the position of the title and subtitle again.

![align_vert](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/align_vert.png)

Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/fandango-movies-ratings/)

For teaching purposes, we’re now going to proceed incrementally with adjusting our FTE graph. Consequently, our code will span over multiple code cells. In practice, however, no more than one code cell will be required.

## Customizing the tick labels

We’ll start by increasing the font size of the tick labels. In the following code cell, we:

-   Plot the graph using the same code as earlier, and assign the resulting object to  `fte_graph`. Assigning to a variable allows us to repeatedly and easily apply methods on the object, or access its attributes.
-   Increase the font size of all the major tick labels using the  `tick_params()`  [method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html?highlight=tick_params#matplotlib.axes.Axes.tick_params)  with the following parameters:
    -   `axis`  – specifies the axis that the tick labels we want to modify belong to; here we want to modify the tick labels of  _both_  axes;
    -   `which`  – indicates what tick labels to be affected (the major or the minor ones; see the legend shown earlier if you don’t know the difference);
    -   `labelsize`  – sets the font size of the tick labels.

```python
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
```

![538_graphs_AO_13_0](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_13_0.png)

You may have noticed that we didn’t use  `style.use('fivethirtyeight')`  this time. That’s because the preference for any matplotlib style becomes global once it’s first declared in our code. We’ve set the style earlier as  `fivethirtyeight`, and from there on all subsequent graphs inherit this style. If for some reason you want to return to the default state, just run  `style.use('default')`.

We’ll now build upon our previous changes by making a few adjustments to the tick labels of the y-axis:

-   We add a “%” symbol to 50, the highest visible tick label of the y-axis.
-   We also add a few whitespace characters after the other visible labels to align them elegantly with the new “50%” label.

To make these changes to the tick labels of the y-axis, we’ll use the  `set_yticklabels()`  [method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.set_yticklabels.html?highlight=set_yticklabels#matplotlib.axes.Axes.set_yticklabels)  along with the  `label`  parameter. As you can deduce from the code below, this parameter can take in a list of mixed data types, and doesn’t require any fixed number of labels to be passed in.

```python
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)

# Customizing the tick labels of the y-axis fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
print('The tick labels of the y-axis:', fte_graph.get_yticks()) # -10 and 60 are not visible on the graph
```

```python
The tick labels of the y-axis: [-10.   0.  10.  20.  30.  40.  50.  60.]
```

![538_graphs_AO_15_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_15_1.png)

## Bolding the horizontal line at y = 0

We will now bold the horizontal line where the y-coordinate is 0. For that, we’ll use the  `axhline()`  [method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.axhline.html?highlight=axhline#matplotlib.axes.Axes.axhline)  to add a new horizontal grid line, and cover the existing one. The parameters we use for  `axhline()`  are:

-   `y`  – specifies the y-coordinate of the horizontal line;
-   `color`  – indicates the color of the line;
-   `linewidth`  – sets the width of the line;
-   `alpha`  – regulates the transparency of the line, but we use it here to regulate the intensity of the black color; the values for  `alpha`  range from 0 (completely transparent) to 1 (completely opaque).

```python
#
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])

# Generate a bolded horizontal line at y = 0
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
```

![538_graphs_AO_17_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_17_1.png)

## Add an extra vertical line

As we mentioned earlier, we have to add another vertical grid line in the immediate vicinity of the tick labels of the y-axis. For that, we simply tweak the range of the values of the x-axis. Increasing the range’s left limit will result in the extra vertical grid line we want.

Below, we use the  `set_xlim()`  [method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.set_xlim.html?highlight=set_xlim#matplotlib.axes.Axes.set_xlim)  with the self-explanatory parameters  `left`  and  `right`.

```python
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)

# Add an extra vertical line by tweaking the range of the x-axis
fte_graph.set_xlim(left = 1969, right = 2011)
```

![538_graphs_AO_19_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_19_1.png)

## Generating a signature bar

The signature bar of the example FTE graph presented above has a few obvious characteristics:

-   It’s positioned at the bottom of the graph.
-   The author’s name is located on the left side of the signature bar.
-   The source of the data is mentioned on the right side of the signature bar.
-   The text has a light grey color (the same as the background color of the graph), and a dark grey background.
-   The area in-between the author’s name and the source name has a dark grey background as well.

![fandango-1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/fandango-1.png)

The image is posted again so you don’t have to scroll back. Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/fandango-movies-ratings/)

It may seem difficult to add such a signature bar, but with a little ingenuity we can get it done quite easily.

We’ll add a single snippet of text, give it a light grey color, and a background color of dark grey. We’ll write both the author’s name and the source in a single text snippet, but we’ll space out these two such that one ends up on the far left side, and the other on the far right. The nice thing is that the whitespace characters will get a dark grey background as well, which will create the effect of a signature bar.

We’ll also use some white space characters to align the author’s name and the name of the source, as you’ll be able to see in the next code block.

This is also a good moment to remove the label of the x-axis. This way, we can get a better visual sense of how the signature bar fits in the overall scheme of the graph. In the next code cell, we’ll build up on what we’ve done so far, and we will:

-   Remove the label of the x-axis by passing in a  `False`  value to the  `set_visible()`  method we apply to the object  `fte_graph.xaxis.label`. Think of it this way: we access the  `xaxis`  attribute of  `fte_graph`, and then we access the  `label`  attribute of  `fte_graph.xaxis`. Then we finally apply  `set_visible()`  to  `fte_graph.xaxis.label`.
-   Add a snippet of text on the graph in the way discussed above. We’ll use the  `text()`  [method](https://matplotlib.org/api/figure_api.html?highlight=figure%20text#matplotlib.figure.Figure.text)  with the following parameters:
    -   `x`  – specifies the x-coordinate of the text;
    -   `y`  – specifies the y-coordinate of the text;
    -   `s`  – indicates the text to be added;
    -   `fontsize`  – sets the size of the text;
    -   `color`  – specifies the color of the text; the format of the value we use below is  [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal); we use this format to match exactly the background color of the entire graph (as specified in  [the code of the  `fivethirtyeight`  style](https://github.com/matplotlib/matplotlib/blob/38be7aeaaac3691560aeadafe46722dda427ef47/lib/matplotlib/mpl-data/stylelib/fivethirtyeight.mplstyle));
    -   `backgroundcolor`  – sets the background color of the text snippet.

```python
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
fte_graph.set_xlim(left = 1969, right = 2011)

# Remove the label of the x-axis
fte_graph.xaxis.label.set_visible(False)

# The signature bar
fte_graph.text(x = 1965.8, y = -7,
    s = ' ©DATAQUEST Source: National Center for Education Statistics',fontsize = 14, color = '#f0f0f0', backgroundcolor = 'grey')
```

![538_graphs_AO_21_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/538_graphs_AO_21_1.png)

The x and y coordinates of the text snippet added were found through a process of trial and error. You can pass in  `floats`  to the  `x`  and  `y`  parameters, so you’ll be able to control the position of the text with a high level of precision.

It’s also worth mentioning that we tweaked the positioning of the signature bar in such a way that we added some visually refreshing lateral margins (we discussed this adjustment earlier). To increase the left margin, we simply lowered the value of the x-coordinate. To increase the right one, we added more whitespace characters between the author’s name and the source’s name – this pushes the source’s name to the right, which results in adding the desired margin.

## A different kind of signature bar

You’ll also meet a slightly different kind of signature bar:

![olympics1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/olympics1.png)

Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/old-olympians-ride-horses-young-ones-do-flips/)

This kind of signature bar can be replicated quite easily as well. We’ll just add some grey colored text, and a line right above it.

We’ll create the visual effect of a line by adding a snippet of text of multiple underscore characters (“_”). You might wonder why we’re not using  `axhline()`  to simply draw a horizontal line at the y-coordinate we want. We don’t do that because the new line will drag down the entire grid of the graph, and this won’t create the desired effect.

We could also try adding an arrow, and then remove the pointer so we end up with a line. However, the “underscore” solution is much simpler.

In the next code block, we implement what we’ve just discussed. The methods and parameters we use here should already be familiar from earlier sections.

```python
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
fte_graph.xaxis.label.set_visible(False)
fte_graph.set_xlim(left = 1969, right = 2011)

# The other signature bar
fte_graph.text(x = 1967.1, y = -6.5,
    s = '________________________________________________________________________________________________________________',
    color = 'grey', alpha = .7)

fte_graph.text(x = 1966.1, y = -9,
    s = '   ©DATAQUEST                                                                               Source: National Center for Education Statistics   ',
    fontsize = 14, color = 'grey', alpha = .7)
```

![538_graphs_AO_23_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/538_graphs_AO_23_1.png)

## Adding a title and subtitle

If you examine  [a couple of FTE graphs](https://fivethirtyeight.com/features/the-52-best-and-weirdest-charts-we-made-in-2016/), you may notice these patterns with regard to the title and the subtitle:

-   The title is almost invariably complemented by a subtitle.
-   The title gives a contextual angle to look from at a particular graph. The title is almost never technical, and it usually expresses a single, simple idea. It’s also almost never emotionally-neutral. In the Fandango graph above, we can see a simple, “emotionally-active” title (“Fandango LOVES Movies”), and not a bland “The distribution of various movie rating types”.
-   The subtitle offers technical information about the graph. This information is what makes axis labels redundant oftentimes. We should be careful to customize our subtitle accordingly since we’ve already dropped the x-axis label.
-   Visually, the title and the subtitle have different font weights, and they are left-aligned (unlike most titles, which are centered). Also, they are aligned vertically with the major tick labels of the y-axis, as we showed earlier.

Let’s now add a title and a subtitle to our graph while being mindful of the above observations. In the code block below, we’ll build upon what we’ve coded so far, and we will:

-   Add a title and a subtitle by using the same  `text()`  method we used to add text in the signature bar. If you already have some experience with matplotlib, you might wonder why we don’t use the  `title()`  and  `suptitle()`  methods. This is because these two methods have an awful functionality with regard to moving text with precision. The only new parameter for  `text()`  is  `weight`. We use it to bold the title.

```python
# The previous code
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8))
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
fte_graph.xaxis.label.set_visible(False)
fte_graph.set_xlim(left = 1969, right = 2011)
fte_graph.text(x = 1965.8, y = -7,
    s = '   ©DATAQUEST                                                                                 Source: National Center for Education Statistics   ',
    fontsize = 14, color = '#f0f0f0', backgroundcolor = 'grey')


# Adding a title and a subtitle
fte_graph.text(x = 1966.65, y = 62.7, s = "The gender gap is transitory - even for extreme cases",
               fontsize = 26, weight = 'bold', alpha = .75)
fte_graph.text(x = 1966.65, y = 57,
               s = 'Percentage of Bachelors conferred to women from 1970 to 2011 in the US for\nextreme cases where the percentage was less than 20% in 1970',
              fontsize = 19, alpha = .85)
```

![538_graphs_AO_25_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_25_1.png)

In case you were wondering, the font used in the original FTE graphs is Decima Mono, a paywalled font. For this reason, we’ll stick with Matplotlib’s default font, which looks pretty similar anyway.

## Adding colorblind-friendly colors

Right now, we have that clunky, rectangular legend. We’ll get rid of it, and add colored labels near each plot line. Each line will have a certain color, and a word of an identical color will name the Bachelor which that line corresponds to.

First, however, we’ll modify the default colors of the plot lines, and add  [colorblind-friendly](https://en.wikipedia.org/wiki/Color_blindness)  colors:

![cb_friendly](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/cb_friendly.jpg)

Source:  [Points of View: Color blindness by Bang Wong](http://www.nature.com/nmeth/journal/v8/n6/full/nmeth.1618.html#ref1)

We’ll compile a list of  [RGB](https://en.wikipedia.org/wiki/RGB_color_model)  parameters for colorblind-friendly colors by using values from the above image. As a side note, we avoid using yellow because text snippets with that color are not easily readable on the graph’s dark grey background color.

After compiling this list of RGB parameters, we’ll then pass it to the  `color`  parameter of the  `plot()`  method we used in our previous code. Note that matplotlib will require the RGB parameters to be within a 0-1 range, so we’ll divide every value by 255, the maximum RGB value. We won’t bother dividing the zeros because 0/255 = 0.

```python
# Colorblind-friendly colors
colors = [[0,0,0], [230/255,159/255,0], [86/255,180/255,233/255], [0,158/255,115/255],
          [213/255,94/255,0], [0,114/255,178/255]]

# The previous code we modify
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8), color = colors)

# The previous code that remains the same
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
fte_graph.xaxis.label.set_visible(False)
fte_graph.set_xlim(left = 1969, right = 2011)
fte_graph.text(x = 1965.8, y = -7,
    s = '   ©DATAQUEST                                                                                 Source: National Center for Education Statistics   ',
    fontsize = 14, color = '#f0f0f0', backgroundcolor = 'grey')
fte_graph.text(x = 1966.65, y = 62.7, s = "The gender gap is transitory - even for extreme cases",
               fontsize = 26, weight = 'bold', alpha = .75)
fte_graph.text(x = 1966.65, y = 57,
               s = 'Percentage of Bachelors conferred to women from 1970 to 2011 in the US for\nextreme cases where the percentage was less than 20% in 1970',
              fontsize = 19, alpha = .85)
```

![538_graphs_AO_27_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_27_1.png)

## Changing the legend style by adding colored labels

Finally, we add colored labels to each plot line by using the  `text()`  method used earlier. The only new parameter is  `rotation`, which we use to rotate each label so that it fits elegantly on the graph.

We’ll also do a little trick here, and make the grid lines transparent around labels by simply modifying their background color to match that of the graph.

In our previous code we only modify the  `plot()`  method by setting the  `legend`  parameter to  `False`. This will get us rid of the default legend. We also skip redeclaring the  `colors`  list since it’s already stored in memory from the previous cell.

```python
# The previous code we modify
fte_graph = women_majors.plot(x = 'Year', y = under_20.index, figsize = (12,8), color = colors, legend = False)

# The previous code that remains unchanged
fte_graph.tick_params(axis = 'both', which = 'major', labelsize = 18)
fte_graph.set_yticklabels(labels = [-10, '0   ', '10   ', '20   ', '30   ', '40   ', '50%'])
fte_graph.axhline(y = 0, color = 'black', linewidth = 1.3, alpha = .7)
fte_graph.xaxis.label.set_visible(False)
fte_graph.set_xlim(left = 1969, right = 2011)
fte_graph.text(x = 1965.8, y = -7,
    s = '   ©DATAQUEST                                                                                 Source: National Center for Education Statistics   ',
    fontsize = 14, color = '#f0f0f0', backgroundcolor = 'grey')
fte_graph.text(x = 1966.65, y = 62.7, s = "The gender gap is transitory - even for extreme cases",
               fontsize = 26, weight = 'bold', alpha = .75)
fte_graph.text(x = 1966.65, y = 57,
               s = 'Percentage of Bachelors conferred to women from 1970 to 2011 in the US for\nextreme cases where the percentage was less than 20% in 1970',
              fontsize = 19, alpha = .85)

# Add colored labels
fte_graph.text(x = 1994, y = 44, s = 'Agriculture', color = colors[0], weight = 'bold', rotation = 33,
              backgroundcolor = '#f0f0f0')
fte_graph.text(x = 1985, y = 42.2, s = 'Architecture', color = colors[1], weight = 'bold', rotation = 18,
              backgroundcolor = '#f0f0f0')
fte_graph.text(x = 2004, y = 51, s = 'Business', color = colors[2], weight = 'bold', rotation = -5,
               backgroundcolor = '#f0f0f0')
fte_graph.text(x = 2001, y = 30, s = 'Computer Science', color = colors[3], weight = 'bold', rotation = -42.5,
              backgroundcolor = '#f0f0f0')
fte_graph.text(x = 1987, y = 11.5, s = 'Engineering', color = colors[4], weight = 'bold',
              backgroundcolor = '#f0f0f0')
fte_graph.text(x = 1976, y = 25, s = 'Physical Sciences', color = colors[5], weight = 'bold', rotation = 27,
              backgroundcolor = '#f0f0f0')
```

![538_graphs_AO_29_1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/2019/01/538_graphs_AO_29_1.png)

## Next steps

That’s it, our graph is now ready for publication!

To do a short recap, we’ve started with generating a graph with matplotlib’s default style. We then brought that graph to “FTE-level” through a series of steps:

-   We used matplotlib’s in-built  `fivethirtyeight`  style.
-   We added a title and a subtitle, and customized each.
-   We added a signature bar.
-   We removed the default legend, and added colored labels.
-   We made a series of other small adjustments: customizing the tick labels, bolding the horizontal line at y = 0, adding a vertical grid line near the tick labels, removing the label of the x-axis, and increasing the lateral margins of the y-axis.

To build upon what you’ve learned, here are a few next steps to consider:

-   Generate a similar graph for other Bachelors.
-   Generate different kinds of FTE graphs: a histogram, a scatter plot etc.
-   Explore  [matplotlib’s gallery](https://matplotlib.org/gallery.html)  to search for potential elements to enrich your FTE graphs (like inserting images, or adding arrows etc.). Adding images can take your FTE graphs to a whole new level:

![dinos1](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img/https://www.dataquest.io/wp-content/uploads/dinos1.png)

Source:  [FiveThirtyEight](https://fivethirtyeight.com/features/the-biggest-dinosaur-in-history-may-never-have-existed/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjM0NDk4MzFdfQ==
-->