
Python Pandas : House Market Analysis – Munich (2016-2017) (1/2)
===

[Source](https://www.datanalyst.info/python/python-others-ideas/python-pandas-house-market-analysis-munich-2016-2017-1-2/?camp=rf~medium~pandas-intro-2)

I started to use python for other things than Data Analysis at the beginning. I was a technical SEO consultant and wanted to use a crawler (or built one) and not knowing any programming language, python looked as the perfect language to start with…  
Flash forward to nowadays, I am even more fan of python now because of its versatility to do what I just mentioned and also to realize data analysis easily.

What if we could bring both of these worlds together ? I created my first crawler when I was injured from breaking my wrist, it is not beautiful, it was written with one hand but it worked.  
Now that I am looking at the data and I thought it would be a very nice and easy example on how to use the data that you have gathered, or have at your disposal, with python and mostly with Pandas.

## House Market in Munich

I am living in Munich now and I really like the city, I traveled a lot during the beginning of my career (New York / San Francisco / Taiwan / Paris) and I thought quickly that I would need some data to help searching for my home. If I want to buy somewhere, it is not a small amount that you need to pay, it is probably a lot of money, so you need to back up your wish with some solid data.

I gather data on the house market around Munich on my own with my little crawler. It is still a manual program because when I created it, I didn’t know and didn’t have time to make it a cloud native application that run 24/7.

I will probably try to improve it and make it cloud native so I can monitor it. This will be a blog post if I succeed in doing so.  
In the meantime, I ran this crawler time to time, in a stochastic way some may 

The House Market in Munich is expensive, not a bit, but really expensive.  
So I was doing my crawler in order to find a home that would match my budget. It is mostly apartment (because Houses are not in my budget) and in the area of Munich.

So to start with the bias of this analysis, here comes some :

-   I looked for “up to 4 room apartments”
-   I looked for “up to 600 000 €” apartment (around 690 000$)
-   I looked for “up to 20km away from Munich center”.
-   I looked if the flat was on the ground floor or up in the building, but I didn’t look at the specific floor.

I saved my data as csv and you can find it on my github account : https://github.com/pitchmuc/munich_housemarket.git

## Understanding the data with Pandas

When I have a data set to look at, I first do 2 things :

1.  I look at the size of the data set.
2.  I look at the type of data set.

For me, the data set is not so large (150 kb) so there is no problem for my computer to handle that.  
If it would be bigger, I would have split it to chunk of 100MB maximum so I can play and test my script easily. I would then produce a robust script to take all of your data through.  
When you execute your analysis on your full data set (ie: 5GB), you want to make sure that this is working before spending hours on running your analysis and finding it didn’t do what you wanted.

The type of the data that you have to handle can be :

-   clean : you just have to import it
-   half clean : you have to import it and take care of few missing data.
-   not clean at all : you have to clean it a bit, import it and take care of the missing data.

In our case, I have managed to have a pretty clean to half clean data but still some cleaning is required.  
On the following steps, you will see how to realize basic cleaning with python pandas :

1.  Import the libraries you want to use. In our case, you want to have pandas and numpy.  
    ```py    
    import pandas as  pd  #naming convention    
    import numpy as  np  #naming convention
    ``` 
2.  import your data set in your environment.  
    In my example, I am using ipython (or called jupyter notebook). I really like this environment for exploration. When things get serious, I usually go to Spyder.  
``` py
df  =  pd.read_csv('data_immoscout.csv',delimiter='\t')  
# df is going to be our dataframe. (place where we store all the data). I used tab as delimiter.
``` 
3.  Look at the data you have. Using the .head() function will give a preview of your data.  
  ```py
  df.head()  ## use df.head(20) to see the first 20 lines
  ``` 
4.  On top of df.head(), you can also try to see the exact type the data have been processed.  
    In order to do that, you can use the  
    
   ``` py
    df.dtypes  ##it will give you something like this :
 ``` 
 ```bush
index0 		int64    
terrace 	object    
bedrooms 	object    
construction_year object    
date_month 	int64    
date_year 	int64    
date_year_month object    
floor 		object    
rooms 		object    
price_room object    
price_surface object    
price 		object    
surface 	object    
zip 		int64
    
dtype:  object
 ```    
5.  Look at the type of column you have is quite important because this usually give you an idea of the type of data store. Or type of data that should be store.     
   ``` py
df.columns  #it will give you something like this :
 ```    
   ``` py
Index(['index0',  'terrace',  'bedrooms',  'construction_year',  'date_month',    
    'date_year',  'date_year_month',  'floor',  'rooms',  'price_room',    
    'price_surface',  'price',  'scout_id',  'surface'],    
    dtype='object')
  ```   

From that I can give you some explanation about these data, but looking at the data through dtypes and head() should actually already gave you the idea :

-   index0 : This is the index of the table
-   terrace : does there is a terrace or not
-   bedrooms : how many bedrooms there is
-   construction_year : when has it been built
-   date_month : Month of the year when the crawl has been realized
-   date_year : Year when the crawl has been realized
-   date_year_month : month and year when the crawl has been realized
-   floor : is it ground floor or not ?
-   rooms : number of rooms
-   price_rooms : price of the apartment divided by number of room
-   price_surface : price of the apartment divided by surface
-   price : price of the flat
-   surface : surface of the flat
-   zip : zip code of the flat

The first thing you want to do when you start with these data is that you make sure that they are recognized the correct way in the system.  
What does it mean “the correct way”?  
The correct way is : numbers are seen as numbers, strings as strings, dates as dates and NaN as NaN.

**What is a NaN ?**  
NaN stands for “Not a Number”. This is very important to know because this is the type of data we want to clean before we are finally processing them.

As you may have seen already, there are some rows where NAN is actually written. Is it recognized as NaN ?  
In order to see how many NaN you have, you can actually use this very useful function :
``` py
df.isna().sum()  ## The result will look like this :
``` 
``` py
index0  0
terrace  0
bedrooms  0
construction_year  0
date_month  0
date_year  0
date_year_month  0
floor  0
rooms  0
price_room  0
price_surface  0
price  0
surface  0
zip  0

dtype:  int64
``` 
This means that there is no NaN recognized in your current data set (or dataframe).  
The ‘NAN’ is just a string that I set when I actually ran my crawler.

You will then replaced the “NAN” string with the correct definition of a NaN. In order to do that, we will use the numpy library, you will just need to use it that way :
``` py
df.replace('NAN',np.NaN,inplace=True)
``` 

When we have done that,  we will then  see different result on the previous method  :
``` py
df.isna().sum()  ## The result will look like this :
``` 
```py 
index0  0
terrace  0
bedrooms  319
construction_year  49
date_month  0
date_year  0
date_year_month  0
floor  113
rooms  34
price_room  35
price_surface  212
price  1
surface  211
zip  0
dtype:  int64
``` 
Here we start to see what is actually going on on these data.  
You see that we are missing a lot of data for bedrooms information.  
Our role in the next steps is to make sure to have as less as NaN as possible.  
We will try to assume some different strategies to fill the NaN here.

If you want to see the global quality of your data set, you can actually use some calculation.  
Like this :

``` py
(df.isnull().sum()  /  len(df))*100  ## result will look like this 
``` 

``` result
index0  0.000000
terrace  0.000000
bedrooms  36.708861
construction_year  5.638665
date_month  0.000000
date_year  0.000000
date_year_month  0.000000
floor  13.003452
rooms  3.912543
price_room  4.027618
price_surface  24.395857
price  0.115075
surface  24.280783
zip  0.000000

dtype:  float64
``` 
So the data I provided is not perfect but you will probably see lots of data set uglier than that.  
To understand the data : 36,7% of the rows don’t have bedrooms information.

What was really troubling is that we are missing the price information for one specific data point.  
Price is really hard to forecast but let see what data it is and we may figure out something :
``` py
df[df['price'].isna()].T  ##the result will look like this :
``` 
You will see that we are missing the price and the number of bedrooms.  
There are 2 options we can do :

-   Estimate the price with the information we have (5 room, 209 square meter, construction year : 2016)
-   Remove this line from your dataset

On our case, 200 square meter built in 2016 will probably be out of my data set restriction (<600 K€). I will then remove the line from the data set.

From my extract, I saw that the index of that line is 367.  
I can remove the line by doing this simple manipulation :

``` py
df.drop(df.index[367],inplace=True)
``` 
but if you have more than one index, how do you manage ?

You just need to call out the index of your condition :

``` py
df.drop(df[df['price'].isna()].index,inplace  =  True)
``` 
As we are deleting useless information, we can take the opportunity to delete the index0 column as you could have seen that pandas automatically generate an index to your dataframe.  
In order to delete a column completely, you will need to realize this action :
```py 
df.drop(['index0'],axis=1,inplace=True)  #axis = 1 make sure that you are deleting column
``` 
Now we want to have the correct data type recognize by pandas.  
Having the correct data type will allow us to realize numeric operation on numeric type (int or float).  
We will be able to deal with NaN in a better way if we have the correct data type set.

What I would recommend is always to try to set the numeric value to int.  
Why  **int**  ?  
Because it easier to handle and interpret but you could try to have everything into float.  
Floating numbers can represent integer (2.0 == 2) but integers cannot represent some floating numbers (2.1 != 2)

A easy loop could look like :


``` py
for  col in  list(df.columns):  # for each column
try:
	df[col]  =  df[col].astype(int)  #try to set it as int
except:
	df[col]  =  df[col].astype(str)  # if not sucessful try to set it as string
``` 
When you have realized this operation, you can see that not all columns have been changed to numeric.  
This is mostly due to some column not being an integer but being a float. (so a decimal)

You can realize another loop on that :

``` py
for  col in  list(df.columns):
	if  df[col].dtypes  ==  object:
try:
	df[col]  =  df[col].astype(float)
except:
	df[col]  =  df[col].astype(str)
``` 

Then  by doing  a  simple overview,  your data start to  look like something you can work  :
``` py
df.dtypes  # it will show something like this :
``` 


## Filling the NaN

Now that we are ready to manipulate the difference type of data, we will be using our brain a bit to deal with the different data type and fill the NaN values.  
As explained previously, before doing any analysis, you would want to feel the maximum of the missing value in order to do calculation to the maximum of values.

1.  **Filling the Floor Column**  
    As you should remember, this column tells us if this is Ground floor or not.  
    By doing this simple method, you can see the different values and the number of time they are appearing.  
```   
 df['floor'].value_counts()  ### Should show something like this :
   ```  
      
``` py    
   up floor  687    
   nan  112    
   ground floor  69    
   Name:  floor,  dtype:  int64
```     
      
    what you would need to do is to calculate the distribution between an the up floor and the ground floor and apply this distribution to the remaining data.  
    You can easily calculate that the number of ground floor apartment represent around 10% of this column.  
    Therefore we would need to replace 1/10 of the na with a “ground floor” value.
    
    We can do that by simply creating a function :
    
   ```py 
def fill10pct():
	if  np.random.random_integers(0,9)  ==  0:
		  return  'ground floor'    
    else:    
	    return  'up floor'
  ```   
    Then you need to apply this to the your rows :
 ``` py
for  index,  value in  df.iterrows():
	if  df.loc[index,'floor']=='nan':    
	    df.loc[index,'floor']  =  fill10pct()
```     
You can run a df[‘floor’].value_counts() to check if the distribution was kept.
    
2.  **Filling the room**  

Now we will try to fill the room.  

We will try a different technique here. We have some information that can help us identify how many rooms there is in total.  

There are the bedroom information, so in Germany in the post of apartment, the bedrooms are the only room counted separated from the number of room.  
Which is : 3 rooms mean 2 bedroom, one big room and a kitchen and a bathroom.  
    
So we could say that the number of room is number of bedroom + 1But what if we don’t have the number of bedrooms ?  

Then, to make it simple we can say that the number of room is 2. which is the minimum I would get.For this we will create our 2 conditions (there is a number of bedroom, or there isn’t)
    
```py   
 conditions  =  [  
(df['rooms'].isnull())  &amp;  (df['bedrooms'].isnull()),    
(df['rooms'].isnull())  &amp;  (df['bedrooms'].notnull())]    
choices  =  [2,df['bedrooms']+1]
```  
And we are going to use the numpy select function to decide which option to apply
 ```py 
df['rooms']  =  np.select(conditions,  choices,  default=2)
```     
 
    
Pretty easy when you know how to  do  it.  :)
It is  so easy that we will make it  a  bit more robust and  integrate the surface in  it.
We will say that if  the surface is  bigger than  75  square meter,  we will set the number of room to  3.
   ``` py
conditions  =[
(df['rooms'].isnull())  &amp;  (df['bedrooms'].isnull())  &amp;  (df['surface'].isnull()),    
(df['rooms'].isnull())  &amp;  (df['bedrooms'].isnull())  &amp;  (df['surface']&gt;75),    
(df['rooms'].isnull())  &amp;  (df['bedrooms'].notnull()),    
  ]    
choices  =  [2,3,df['bedrooms']+1]    
df['rooms']  =  np.select(conditions,choices,default=2)
```   
3.  **Filling the bedrooms**  
Filling the bedroom is actually the opposite logic. If you have the number of room, you can actually guess the number of bedroom.  
    
This time, we will use the method select from numpy :
``` py
df['bedrooms']  =  np.where(df['bedrooms'].isnull(),  df['rooms']-1,  df['bedrooms'])
 ```   
4.  **Filling the Surface**  
For the surface, we are missing 211 data points. We can have the same strategy than the number of rooms. Extrapolate the surface of the existing apartment to fill the missing value of the surface.  
If we can the average surface for the 2, 3 and 4 room apartment, we could assign the mean value to these room.
    
For realizing this, we are going to use one of the most important function of pandas. The  **groupby**.
    
  ``` py    
  df.groupby(['rooms'])['surface'].mean()  
##it should give you something like :
```     
 ```py     
2.0  89.988924    
 3.0  91.100000
 4.0  100.400000
```    
    It is interesting to see that the average surface for your 2 and 3 rooms apartment are not that different.  
    Most probably our data are not that clean and some 3 rooms apartment were fetched as 2 rooms apartment.
 

 ```py  
conditions  =  [    
(df['rooms']==2  &amp;  df['surface'].isnull()),    
(df['rooms']==3  &amp;  df['surface'].isnull()),    
(df['rooms']==4  &amp;  df['surface'].isnull())    
]    
choices  =  [90,91.1,100]    
 df['surface']  =  np.select(conditions,choices,default=90.5)#default in between 2 and 3 rooms
  ```   
5.  **Filling the construction year**  
    On this one, this is pretty hard as the construction year can be really random. You cannot really guess a construction year based on the previous data.  
    On that case, in order to not false the data to much, I would chose to fill the blank with the mean of this dimension.  
    This is another method you can use quick often with pandas :
    
 ``` py
df['construction_year'].fillna(df['construction_year'].mean(),inplace=True)
  ```   
6.  **Filling the rest…**  
    As you may notice while doing a df.isnull().sum() some other columns have NaN but they are actually calculation of other columns.  
    So you just have to redo the calculation with your primary columns filled and all the NaN will disappear.

I hope this tutorial on how to clean your data will help you if you are discovering Data Analysis with Python and Pandas.  
This is a very important part of working with Data and if you plan to machine learning, cleaning the data and creating value out of NaN data points is one of the most important aspect of Machine Learning.

As the title suggest, we will have a 2nd article where we actually analyze the data and we will probably try to do some visualization.

Don’t hesitate to comment and give your tip to analyze this data set.  
As explained above, both data set (the clean one and the uncleane one) and the Jupyter notebook are available on my Github account : https://github.com/pitchmuc/munich_housemarket
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgwMjE5MTI4Miw4Mzk3NTk2MDEsLTE0Mz
c3NTI2MzldfQ==
-->