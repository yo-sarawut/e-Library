Web Scraping Craigslist: A Complete Tutorial
===

![enter image description here](https://miro.medium.com/max/1025/1*329SDPRG7M8eJF3TwXiOOQ.png)

I’ve been looking to make a move recently. And what better way to know I’m getting a good price than to sample from the “population” of housing on Craigslist? Sounds like a job for…Python and web scraping!

In this article, I’m going to walk you through my code that scrapes East Bay Area Craigslist for apartments. The code here, and/or the URI parameters rather, can be modified to pull from any region, category, property type, etc. Pretty cool, huh?

I’m going to share GitHub gists of each cell in the original Jupyter Notebook. If you’d like to just see the whole code at once,  [clone the repo](https://github.com/rileypredum/East-Bay-Housing-Web-Scrape). Otherwise, enjoy the read and follow along!

## Getting the Data

First things first I needed to use the get module from the requests package. Then I defined a variable, response, and assigned it to the get method called on the base URL. What I mean by base URL is the URL at the first page you want to pull data from, minus any extra arguments. I went to the apartments section for the East Bay and checked the “Has Picture” filter to narrow down the search just a little though, so it’s not a true base URL.

I then imported BeautifulSoup from bs4, which is the module that can actually parse the HTML of the web page retrieved from the server. I then checked the type and length of that item to make sure it matches the number of posts on the page (there are 120). You can find my import statements and setup code below:

It prints out the length of posts which is 120, as expected.

Using the find_all method on the newly created html_soup variable in the code above, I found the posts. I needed to examine the website’s structure to find the parent tag of the posts. Looking at the screenshot below, you can see that it’s <li class=“result-row”>. That is the tag for one single post, which is literally the box that contains all the elements I grabbed!

![](https://miro.medium.com/max/30/1*ZBl8WpsjsfG98h5B4-5aMw.png?q=20)

![](https://miro.medium.com/max/1916/1*ZBl8WpsjsfG98h5B4-5aMw.png)

Element inspection with Chrome (Ctrl+Shift+C shortcut!)

In order to scale this, make sure to work in the following way: grab the first post and all the variables you want from it, make sure you know how to access each of them for one post before you loop the whole page, and lastly, make sure you successfully scraped one page before adding the loop that goes through all pages.

Class bs4.element.ResultSet is indexed, so I looked at the first apartment by indexing  `posts[0]`. Surprise, it’s all the code that belongs to that <li> tag!

![](https://miro.medium.com/max/30/1*FGX4E8X4Sb6Hghq5sbCZDg.png?q=20)

![](https://miro.medium.com/max/1691/1*FGX4E8X4Sb6Hghq5sbCZDg.png)

You should have this output for the first post in posts (posts[0]), assigned to post_one.

The price of the post is easy to grab:

.strip() removes whitespace before and after a string

I grabbed the date and time by specifying the attribute ‘datetime’ on class ‘result-date’. By specifying the ‘datetime’ attribute, I saved a step in data cleaning by making it unnecessary to convert this attribute from a string to a datetime object. This could also be made into a one-liner by placing  `['datetime']`  at the end of the  `.find()`  call, but I split it into two lines for clarity.

The URL and post title are easy because the ‘href’ attribute is the link and is pulled by specifying that argument. The title is just the text of that tag.

The number of bedrooms and square footage are in the same tag, so I split these two values and grabbed each one element-wise. The neighborhood is the <span> tag of class “result-hood”, so I grabbed the text of that.

The next block is the loop for all the pages for the East Bay. Since there isn’t always information on square footage and number of bedrooms, I built in a series of if statements embedded within the for loop to handle all cases.

The loop starts on the first page, and for each post in that page, it works through the following logic:

![](https://miro.medium.com/max/30/1*UjFFWF96FbLm2kRp9wILAA.png?q=20)

![](https://miro.medium.com/max/915/1*UjFFWF96FbLm2kRp9wILAA.png)

I included some data cleaning steps in the loop, like pulling the ‘datetime’ attribute and removing the ‘ft2’ from the square footage variable, and making that value an integer. I removed ‘br’ from the number of bedrooms as that was scraped as well. That way, I started data cleaning with some work already done. Elegant code is the best! I wanted to do more, but the code would become too specific to this region and might not work across areas.

The code below creates the dataframe from the lists of values!

![](https://miro.medium.com/max/30/1*yJPhDKP8l_NlTJYSmctpag.png?q=20)

![](https://miro.medium.com/max/777/1*yJPhDKP8l_NlTJYSmctpag.png)

Awesome! There it is. Admittedly, there is still a little bit of data cleaning to be done. I’ll go through that real quick, and then it’s time to explore the data!

## Exploratory Data Analysis

Sadly, after removing the duplicate URLs I saw that there are only 120 instances. These numbers will be different if you run the code, since there will be different posts at different times of scraping. There were about 20 posts that didn’t have bedrooms or square footage listed too. For statistical reasons, this isn’t an incredible data set, but I took note of that and pushed forward.

![](https://miro.medium.com/max/30/1*OvQ4muugfqWYjpULCkFW3g.png?q=20)

![](https://miro.medium.com/max/627/1*OvQ4muugfqWYjpULCkFW3g.png)

![](https://miro.medium.com/max/30/1*FBPovr7In-waFg899o87WA.png?q=20)

![](https://miro.medium.com/max/1287/1*FBPovr7In-waFg899o87WA.png)

Descriptive statistics for the quantitative variables

I wanted to see the distribution of the pricing for the East Bay so I made the above plot. Calling the  `.describe()`  method, I got a more detailed look. The cheapest place is $850, and the most expensive is $4,800.

The next code block generates a scatter plot, where the points are colored by the number of bedrooms. This shows a clear and understandable stratification: we see layers of points clustered around particular prices and square footages, and as price and square footage increase so do the number of bedrooms.

![](https://miro.medium.com/max/30/1*g_nDPpysPEHgZM9LvMXYyw.png?q=20)

![](https://miro.medium.com/max/880/1*g_nDPpysPEHgZM9LvMXYyw.png)

Let’s not forget the workhorse of Data Science: linear regression. We can call a  `regplot()`  on these two variables to get a regression line with a bootstrap confidence interval calculated about the line and shown as a shaded region with the code below. If you haven’t heard of bootstrap confidence intervals, they are a really cool statistical technique that are  [worth a read](https://www.inferentialthinking.com/chapters/13/2/Bootstrap.html).

![](https://miro.medium.com/max/30/1*oz8V7pwCp3uWrYYnTVEdtA.png?q=20)

![](https://miro.medium.com/max/756/1*oz8V7pwCp3uWrYYnTVEdtA.png)

It looks like we have an okay fit of the line on these two variables. Let’s check the correlations. I called  `eb_apts.corr()`  to get these:

![](https://miro.medium.com/max/30/1*chVwnttqtA18ls2t5yTSTw.png?q=20)

![](https://miro.medium.com/max/731/1*chVwnttqtA18ls2t5yTSTw.png)

Correlation matrix for our variables

As suspected, correlation is strong between number of bedrooms and square footage. That makes sense since square footage increases as the number of bedrooms increases.

## Pricing By Neighborhood Continued

I wanted to get a sense of how location affects price, so I grouped by neighborhood, and aggregated by calculating the mean for each variable.

The following is produced with this single line of code:  `eb_apts.groupby('neighborhood').mean()`  where ‘neighborhood’ is the ‘by=’ argument, and the aggregator function is the mean.

![](https://miro.medium.com/max/16/1*pACNq2uzhaJgDjhnJeLDGg.png?q=20)

![](https://miro.medium.com/max/421/1*pACNq2uzhaJgDjhnJeLDGg.png)

I noticed that there are two North Oaklands: North Oakland and Oakland North, so I recoded one of them into the other like so:

`eb_apts['neighborhood'].replace('North Oakland', ‘Oakland North', inplace=True)`.

Grabbing the price and sorting it in ascending order can show the cheapest and most expensive places to live. The full line of code is now:  `eb_apts.groupby('neighborhood').mean()['price'].sort_values()`  and results in the following output:

![](https://miro.medium.com/max/17/1*Qu3hJ1nBVpBV7SKCO--lTA.png?q=20)

![](https://miro.medium.com/max/289/1*Qu3hJ1nBVpBV7SKCO--lTA.png)

Average price by neighborhood sorted in ascending order

Lastly, I looked at the spread of each neighborhood in terms of price. By doing this, I saw how prices in neighborhoods can vary, and to what degree.

Here’s the code that produces the plot that follows.

![](https://miro.medium.com/max/30/1*jDccgcLeozWBcG-dV63QVw.png?q=20)

![](https://miro.medium.com/max/922/1*jDccgcLeozWBcG-dV63QVw.png)

Berkeley had a huge spread. This is probably because it includes South Berkeley, West Berkeley, and Downtown Berkeley. In a future version of this project it may be important to consider changing the scope of each of the variables so they are more reflective of the variability of price between neighborhoods in each city.

Well, there you have it! Take a look at this the next time you’re in the market for housing to see what a good price should be. Feel free to check out the  [repo](https://github.com/rileypredum/East-Bay-Housing-Web-Scrape)  and try it for yourself, or fork the project and do it for your city! Let me know what you come up with!

[Scrape responsibly](https://www.scrapehero.com/how-to-prevent-getting-blacklisted-while-scraping/).





>  [Source :](https://towardsdatascience.com/web-scraping-craigslist-a-complete-tutorial-c41cea4f4981).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwNzI3MDU4N119
-->