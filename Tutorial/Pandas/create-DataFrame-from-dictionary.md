
[Create DataFrame from Dictionary using default Constructor](https://thispointer.com/python-pandas-how-to-create-dataframe-from-dictionary/)
===
DataFrame constructor accepts a data object that can be ndarray, dictionary etc. i.e.
```py
pandas.DataFrame(data=None, index=None, columns=None, dtype=None, copy=False)
```

But if we are passing a dictionary in data, then it should  contain a list like objects in value field like Series, arrays or lists etc i.e.

# Dictionary with list object in values
studentData = {
'name' : ['jack', 'Riti', 'Aadi'],
'age' : [34, 30, 16],
'city' : ['Sydney', 'Delhi', 'New york']
}
1
2
3
4
5
6
# Dictionary with list object in values
studentData = {
    'name' : ['jack', 'Riti', 'Aadi'],
    'age' : [34, 30, 16],
    'city' : ['Sydney', 'Delhi', 'New york']
}
On Initialising a DataFrame object with this kind of dictionary, each item (Key / Value pair) in dictionary will be converted to one column i.e. key will become Column Name and list in the value field will be the column data i.e.

''' 
Pass dictionary in Dataframe constructor to create a new object
keys will be the column names and lists in values will be column data
'''
dfObj = pd.DataFrame(studentData) 
1
2
3
4
5
''' 
Pass dictionary in Dataframe constructor to create a new object
keys will be the column names and lists in values will be column data
'''
dfObj = pd.DataFrame(studentData) 
It will create a DataFrame object like this,

age      city  name
0   34    Sydney  jack
1   30     Delhi  Riti
2   16  New york  Aadi
1
2
3
4
   age      city  name
0   34    Sydney  jack
1   30     Delhi  Riti
2   16  New york  Aadi
All the keys in dictionary will be converted to column names and lists in each its value field will we converted to column Data.

Create DataFrame from Dictionary with custom indexes
We can also pass the index list to the DataFrame constructor to replace the default index list i.e.

# Pass custom names of index as list during initialization
dfObj = pd.DataFrame(studentData, index=['a', 'b', 'c'])
1
2
# Pass custom names of index as list during initialization
dfObj = pd.DataFrame(studentData, index=['a', 'b', 'c'])
It will create a DataFrame object like this,

age      city  name
a   34    Sydney  jack
b   30     Delhi  Riti
c   16  New york  Aadi
1
2
3
4
   age      city  name
a   34    Sydney  jack
b   30     Delhi  Riti
c   16  New york  Aadi

 
Create DataFrame from not compatible dictionary
As DataFrame constructor accepts a dictionary which should contain a list like objects in values. But what if we have a dictionary that doesn’t have lists in value i.e.

studentAgeData = {
'Jack' : 12,
'Roma' : 13,
'Ritika' : 10,
'Aadi' : 11
}
1
2
3
4
5
6
studentAgeData = {
    'Jack' : 12,
    'Roma' : 13,
    'Ritika' : 10,
    'Aadi' : 11
}
If we will directly pass this dictionary to DataFrame constructor then it will throw following error,
ValueError: If using all scalar values, you must pass an index

So, how to create a two column DataFrame object from this kind of dictionary and put all keys and values as these separate columns like this,

0   1
a    Roma  13
b    Jack  12
c    Aadi  11
d  Ritika  10
1
2
3
4
5
        0   1
a    Roma  13
b    Jack  12
c    Aadi  11
d  Ritika  10
For that we will create a list to tuples (key / value) from this dictionary and pass it to another dataframe constructor that accepts a list i.e.

'''
Creating dataframe by converting dict to list of items
'''
dfObj = pd.DataFrame(list(studentAgeData.items()), index=['a', 'b', 'c', 'd'])
1
2
3
4
'''
Creating dataframe by converting dict to list of items
'''
dfObj = pd.DataFrame(list(studentAgeData.items()), index=['a', 'b', 'c', 'd'])
It will create a DataFrame object like this,

0   1
a    Roma  13
b    Jack  12
c    Aadi  11
d  Ritika  10
1
2
3
4
5
        0   1
a    Roma  13
b    Jack  12
c    Aadi  11
d  Ritika  10
Create DataFrame from Dictionary and skip data
But we want to create a DataFrame object from dictionary by skipping some of the items. Let’s see how to do that,

Suppose we have dictionary like this,

# Dictionary with list object in values
studentData = {
'name' : ['jack', 'Riti', 'Aadi'],
'age' : [34, 30, 16],
'city' : ['Sydney', 'Delhi', 'New york']
}
1
2
3
4
5
6
# Dictionary with list object in values
studentData = {
    'name' : ['jack', 'Riti', 'Aadi'],
    'age' : [34, 30, 16],
    'city' : ['Sydney', 'Delhi', 'New york']
}
Create a DataFrame from this by skipping items with key ‘age’ ,

# Creating Dataframe from Dictionary by Skipping 2nd Item from dict
dfObj = pd.DataFrame(studentData, columns=['name', 'city'])
1
2
# Creating Dataframe from Dictionary by Skipping 2nd Item from dict
dfObj = pd.DataFrame(studentData, columns=['name', 'city'])
As in columns parameter we provided a list with only two column names. So, DataFrame should contain only 2 columns i.e.

name      city
0  jack    Sydney
1  Riti     Delhi
2  Aadi  New york
1
2
3
4
   name      city
0  jack    Sydney
1  Riti     Delhi
2  Aadi  New york
Create DataFrame from Dictionary with different Orientation
We can create a DataFrame from dictionary using DataFrame.from_dict() function too i.e.

DataFrame.from_dict(data, orient='columns', dtype=None)
1
DataFrame.from_dict(data, orient='columns', dtype=None)
It accepts a dictionary and orientation too. By default orientation is columns it means keys in dictionary will be used as columns while creating DataFrame.
We can also pass the orientation as ‘index’, which changes the default orientation and makes the keys in dictionary as index i.e.

Dictionary :

studentData = {
'name' : ['jack', 'Riti', 'Aadi'],
'age' : [34, 30, 16],
'city' : ['Sydney', 'Delhi', 'New york']
}
1
2
3
4
5
studentData = {
    'name' : ['jack', 'Riti', 'Aadi'],
    'age' : [34, 30, 16],
    'city' : ['Sydney', 'Delhi', 'New york']
}
Create DataFrame with index in orientation i.e.

# Create dataframe from dic and make keys, index in dataframe
dfObj = pd.DataFrame.from_dict(studentData, orient='index')
1
2
# Create dataframe from dic and make keys, index in dataframe
dfObj = pd.DataFrame.from_dict(studentData, orient='index')
It will create a DataFrame object like this,

0      1         2
name    jack   Riti      Aadi
city  Sydney  Delhi  New york
age       34     30        16
1
2
3
4
           0      1         2
name    jack   Riti      Aadi
city  Sydney  Delhi  New york
age       34     30        16
Create DataFrame from nested Dictionary
Suppose we have a nested dictionary i.e.

# Nested Dictionary
studentData = { 
0 : {
'name' : 'Aadi',
'age' : 16,
'city' : 'New york'
},
1 : {
'name' : 'Jack',
'age' : 34,
'city' : 'Sydney'
},
2 : {
'name' : 'Riti',
'age' : 30,
'city' : 'Delhi'
}
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
# Nested Dictionary
studentData = { 
0 : {
    'name' : 'Aadi',
    'age' : 16,
    'city' : 'New york'
    },
1 : {
    'name' : 'Jack',
    'age' : 34,
    'city' : 'Sydney'
    },
2 : {
    'name' : 'Riti',
    'age' : 30,
    'city' : 'Delhi'
    }
}
It has 3 items in it and each item contains a dictionary in value field which internally contains the same keys but with different value.

We can directly pass it in DataFrame constructor, but it will use the keys of dict as columns and  DataFrame object like this will be generated i.e.

'''
Create dataframe from nested dictionary 
'''
dfObj = pd.DataFrame(studentData)
1
2
3
4
'''
Create dataframe from nested dictionary 
'''
dfObj = pd.DataFrame(studentData)
It will create a DataFrame object like this,

0       1      2
age         16      34     30
city  New york  Sydney  Delhi
name      Aadi    Jack   Riti
1
2
3
4
             0       1      2
age         16      34     30
city  New york  Sydney  Delhi
name      Aadi    Jack   Riti
Now let’s transpose this matrix to swap the column with indexes i.e. data will be more readable with this i.e.

# Transpose dataframe object
dfObj = dfObj.transpose()
1
2
# Transpose dataframe object
dfObj = dfObj.transpose()
Now contents of DataFrame will be like this,

age      city  name
0  16  New york  Aadi
1  34    Sydney  Jack
2  30     Delhi  Riti
1
2
3
4
  age      city  name
0  16  New york  Aadi
1  34    Sydney  Jack
2  30     Delhi  Riti
 

Complete example is as follows,

import pandas as pd
def main():
# Dictionary with list object in values
studentData = {
'name' : ['jack', 'Riti', 'Aadi'],
'age' : [34, 30, 16],
'city' : ['Sydney', 'Delhi', 'New york']
}
print('Creating Dataframe from Dictionary')
''' 
Pass dictionary in Dataframe constructor to create a new object
keys will be the column names and lists in values will be column data
'''
dfObj = pd.DataFrame(studentData) 
# Print data frame object on console
print(dfObj)
print('Creating Dataframe from Dictionary and Custom Indexes')
# Pass custom names of index as list during initialization
dfObj = pd.DataFrame(studentData, index=['a', 'b', 'c'])
# Print dataframe object on console
print(dfObj)
print('Creating Dataframe from non compatible Dictionary')
studentAgeData = {
'Jack' : 12,
'Roma' : 13,
'Ritika' : 10,
'Aadi' : 11
}
'''
Creating dataframe by converting dict to list of items
'''
dfObj = pd.DataFrame(list(studentAgeData.items()), index=['a', 'b', 'c', 'd'])
# Print Dataframe object on console
print(dfObj)
print('Creating Dataframe from Dictionary by Skipping data')
studentData = {
'name' : ['jack', 'Riti', 'Aadi'],
'age' : [34, 30, 16],
'city' : ['Sydney', 'Delhi', 'New york']
}
# Creating Dataframe from Dictionary by Skipping 2nd Item from dict
dfObj = pd.DataFrame(studentData, columns=['name', 'city']) 
# Print Dataframe object on console
print(dfObj)
print('Creating Dataframe from Dictionary With different orientation')
# Create dataframe from dic and make keys, index in dataframe
dfObj = pd.DataFrame.from_dict(studentData, orient='index')
print(dfObj)
print('Creating Dataframe from nested Dictionary')
# Nested Dictionary
studentData = { 
0 : {
'name' : 'Aadi',
'age' : 16,
'city' : 'New york'
},
1 : {
'name' : 'Jack',
'age' : 34,
'city' : 'Sydney'
},
2 : {
'name' : 'Riti',
'age' : 30,
'city' : 'Delhi'
}
}
'''
Create dataframe from nested dictionary 
'''
dfObj = pd.DataFrame(studentData) 
# Print Dataframe object on console
print(dfObj)
print("Transpose the dictionary")
# Transpose dataframe object
dfObj = dfObj.transpose()
print(dfObj)
if __name__ == '__main__':
main()
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
import pandas as pd
 
def main():
    
    # Dictionary with list object in values
    studentData = {
        'name' : ['jack', 'Riti', 'Aadi'],
        'age' : [34, 30, 16],
        'city' : ['Sydney', 'Delhi', 'New york']
    }
    
    print('Creating Dataframe from Dictionary')
    
    ''' 
    Pass dictionary in Dataframe constructor to create a new object
    keys will be the column names and lists in values will be column data
    '''
    dfObj = pd.DataFrame(studentData) 
 
    # Print data frame object on console
    print(dfObj)
    
    print('Creating Dataframe from Dictionary and Custom Indexes')
    
    # Pass custom names of index as list during initialization
    dfObj = pd.DataFrame(studentData, index=['a', 'b', 'c'])
    
    # Print dataframe object on console
    print(dfObj)
    
    print('Creating Dataframe from non compatible Dictionary')
 
    studentAgeData = {
        'Jack' : 12,
        'Roma' : 13,
        'Ritika' : 10,
        'Aadi' : 11
    }
    
    '''
    Creating dataframe by converting dict to list of items
    '''
    dfObj = pd.DataFrame(list(studentAgeData.items()), index=['a', 'b', 'c', 'd'])
    
    # Print Dataframe object on console
    print(dfObj)
    
    print('Creating Dataframe from Dictionary by Skipping data')
    
    studentData = {
        'name' : ['jack', 'Riti', 'Aadi'],
        'age' : [34, 30, 16],
        'city' : ['Sydney', 'Delhi', 'New york']
    }
    
    # Creating Dataframe from Dictionary by Skipping 2nd Item from dict
    dfObj = pd.DataFrame(studentData, columns=['name', 'city']) 
    
    # Print Dataframe object on console
    print(dfObj)
    
    print('Creating Dataframe from Dictionary With different orientation')
    
    # Create dataframe from dic and make keys, index in dataframe
    dfObj = pd.DataFrame.from_dict(studentData, orient='index')
    
    print(dfObj)
    
    print('Creating Dataframe from nested Dictionary')
    
    # Nested Dictionary
    studentData = { 
    0 : {
        'name' : 'Aadi',
        'age' : 16,
        'city' : 'New york'
        },
    1 : {
        'name' : 'Jack',
        'age' : 34,
        'city' : 'Sydney'
        },
    2 : {
        'name' : 'Riti',
        'age' : 30,
        'city' : 'Delhi'
        }
    }
 
    '''
    Create dataframe from nested dictionary 
    '''
    dfObj = pd.DataFrame(studentData) 
 
    # Print Dataframe object on console
    print(dfObj)
    
    print("Transpose the dictionary")
    
    # Transpose dataframe object
    dfObj = dfObj.transpose()
   
    print(dfObj)
 
if __name__ == '__main__':
    main()
Output:

Creating Dataframe from Dictionary
age      city  name
0   34    Sydney  jack
1   30     Delhi  Riti
2   16  New york  Aadi
Creating Dataframe from Dictionary and Custom Indexes
age      city  name
a   34    Sydney  jack
b   30     Delhi  Riti
c   16  New york  Aadi
Creating Dataframe from non compatible Dictionary
0   1
a    Aadi  11
b    Roma  13
c    Jack  12
d  Ritika  10
Creating Dataframe from Dictionary by Skipping data
name      city
0  jack    Sydney
1  Riti     Delhi
2  Aadi  New york
Creating Dataframe from Dictionary With different orientation
0      1         2
age       34     30        16
name    jack   Riti      Aadi
city  Sydney  Delhi  New york
Creating Dataframe from nested Dictionary
0       1      2
age         16      34     30
city  New york  Sydney  Delhi
name      Aadi    Jack   Riti
Transpose the dictionary
age      city  name
0  16  New york  Aadi
1  34    Sydney  Jack
2  30     Delhi  Riti
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
Creating Dataframe from Dictionary
   age      city  name
0   34    Sydney  jack
1   30     Delhi  Riti
2   16  New york  Aadi
Creating Dataframe from Dictionary and Custom Indexes
   age      city  name
a   34    Sydney  jack
b   30     Delhi  Riti
c   16  New york  Aadi
Creating Dataframe from non compatible Dictionary
        0   1
a    Aadi  11
b    Roma  13
c    Jack  12
d  Ritika  10
Creating Dataframe from Dictionary by Skipping data
   name      city
0  jack    Sydney
1  Riti     Delhi
2  Aadi  New york
Creating Dataframe from Dictionary With different orientation
           0      1         2
age       34     30        16
name    jack   Riti      Aadi
city  Sydney  Delhi  New york
Creating Dataframe from nested Dictionary
             0       1      2
age         16      34     30
city  New york  Sydney  Delhi
name      Aadi    Jack   Riti
Transpose the dictionary
  age      city  name
0  16  New york  Aadi
1  34    Sydney  Jack
2  30     Delhi  Riti
 

Python Recommendations:
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNjg1NDIxLDM1ODU2NDQ4OV19
-->