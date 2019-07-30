
# Python Basic Tutorials

## Link:
- https://www.techbeamers.com/python-tutorial-step-by-step/
- https://data-flair.training/blogs/python-syntax-semantics/
- https://phyblas.hinaboshi.com/saraban/python
- https://www.geeksforgeeks.org/python-programming-language/

## Variables and Python Data Types (ตัวแปรและชนิดของข้อมูล)

**Source :**

- https://data-flair.training/blogs/python-variables-and-data-types/
- https://phyblas.hinaboshi.com/tsuchinoko03


```python
from IPython.display import IFrame, YouTubeVideo, SVG, HTML
```


```python

```

### ตารางสรุปชนิดของข้อมูล

|   ชื่อย่อ      | ความหมาย |ตัวอย่าง |
|  :----: |  :----: | :----: |
int	 |จำนวนเต็ม	 |12345|
float |	จำนวนจริง |	123.45|
complex |	จำนวนเชิงซ้อน |	123+45j|
bool |	บูล	 |True|
str	 |สายอักขระ |	'12345'|
list |	ลิสต์ |	[1,2,3,4,5]|
tuple	 |ทูเพิล |	(1,2,3,4,5)|
set	 |เซ็ต |	{1,2,3,4,5}|
dict |	ดิกชันนารี |	{'ก':1,'ข':2,'ค':3,'ง':4,'จ':5}|
range |	เรนจ์ |	range(1,6)|

## String Formatters


```python
x=10;
printer="Dell"
print("I just printed %s pages to the printer %s" % (x, printer))
```

    I just printed 10 pages to the printer Dell
    


```python
print("I just printed {0} pages to the printer {1}".format(x, printer))
print("I  just printed {x} pages to the printer {printer}".format(x=7, printer=Dell))
```

    I just printed 10 pages to the printer Dell
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-3-bb7f5cfe0295> in <module>
          1 print("I just printed {0} pages to the printer {1}".format(x, printer))
    ----> 2 print("I  just printed {x} pages to the printer {printer}".format(x=7, printer=Dell))
    

    NameError: name 'Dell' is not defined



```python
print(f"I just printed {x} pages to the printer {printer}")
```


```python
>>> a='10'
>>> print(a+a)
```


```python
print('10'+10)
```

## Lists


---




```python
>>> days=['Monday','Tuesday',3,4,5,6,7]
>>> days
```




    ['Monday', 'Tuesday', 3, 4, 5, 6, 7]



### Slicing a list


```python
days[1:3]
```




    ['Tuesday', 3]



### Length of a list


```python
>>> len(days)
```




    7



### Reassigning elements


```python
>>> days[2]='Wednesday'
>>> days
```




    ['Monday', 'Tuesday', 'Wednesday', 4, 5, 6, 7]



### Multidimensional


```python
>>> a=[[1,2,3],[4,5,6]]
>>> a
```




    [[1, 2, 3], [4, 5, 6]]



## Tuples


---




```python
subjects=('Physics','Chemistry','Maths')
subjects
```




    ('Physics', 'Chemistry', 'Maths')




```python
>>> subjects[1]
```




    'Chemistry'



### A tuple is immutable


```python
subjects[2]='Biology'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-35-2da265783d49> in <module>
    ----> 1 subjects[2]='Biology'
    

    TypeError: 'tuple' object does not support item assignment



```python
subjects[3]='Computer Science'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-58-06e10c6d99b8> in <module>
    ----> 1 subjects[3]='Computer Science'
    

    TypeError: 'tuple' object does not support item assignment


**Read:** [Python Namespace and Variable Scope – Local and Global Variables](https://data-flair.training/blogs/python-namespace-and-variable-scope/)

## Dictionaries


---




```python
>>> person={'city':'Ahmedabad','age':7}
>>> person
```




    {'city': 'Ahmedabad', 'age': 7}




```python
>>> type(person)
```




    dict




```python
>>> person['city']
```




    'Ahmedabad'




```python
>>> person['age']=21
>>> person['age']
```




    21




```python
>>> person.keys()
```




    dict_keys(['city', 'age'])




```python
>>> a=2>1
>>> type(a)
```




    bool



## Sets


```python
>>> a={1,2,3}
>>> a
```




    {1, 2, 3}




```python
>>> a={1,2,2,3}
>>> a
```




    {1, 2, 3}




```python
>>> a[2]
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-67-fc907be37984> in <module>
    ----> 1 a[2]
    

    TypeError: 'set' object does not support indexing



```python
>>> a={1,2,3,4}
>>> a
```




    {1, 2, 3, 4}




```python
>>> a.remove(4)
>>> a
```




    {1, 2, 3}




```python
>>> a.add(4)
>>> a
```




    {1, 2, 3, 4}



# Type Conversion


---



## int()


```python
>>> int(3.7)
```




    3




```python
>>> int(True)
```




    1




```python
>>> int(False)
```




    0




```python
>>> int("77")
```




    77



## float()


```python
>>> float(7)
```




    7.0




```python
>>> float(7.7)
```




    7.7




```python
>>> float(True)
```




    1.0




```python
>>> float("11")
```




    11.0




```python
>>> float("2.1e-2")
```




    0.021



##str()


```python
>>> str(2.1)
```




    '2.1'




```python
>>> str(7)
```




    '7'




```python
>>> str(True)
```




    'True'




```python
>>> str([1,2,3])
```




    '[1, 2, 3]'



## bool()


```python
>>> bool(3)
```




    True




```python
>>> bool(0)
```




    False




```python
>>> bool(True)
```




    True




```python
>>> bool(0.1)
```




    True




```python
>>> bool([1,2])
```




    True




```python
>>> bool()
```




    False



## set()


```python
>>> set([1,2,2,3])
```




    {1, 2, 3}




```python
>>> set({1,2,2,3})
```




    {1, 2, 3}



## list()


```python
del list
list("123")
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-57-0df7b9eaea97> in <module>
    ----> 1 del list
          2 list("123")
    

    NameError: name 'list' is not defined



```python
>>> list({1,2,2,3})
```




    [1, 2, 3]




```python
>>> list({"a":1,"b":2})
```




    ['a', 'b']




```python
>>> list({a:1,b:2})
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-91-7e0924f42afa> in <module>
    ----> 1 list({a:1,b:2})
    

    NameError: name 'b' is not defined


## tuple()


```python
>>> tuple({1,2,2,3})
```




    (1, 2, 3)




```python
>>> tuple(list(set([1,2])))
```




    (1, 2)



#Python Local and Python Global Variables


---



## Local variables


```python
>>> def func1():
  uvw=2
  print(uvw)
>>> func1()
```

    2
    


```python
>>> uvw
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-95-7d9dbcb0ea37> in <module>
    ----> 1 uvw
    

    NameError: name 'uvw' is not defined


## Global variables


```python
xyz=3
def func2():
  xyz+=1
print(xyz)
xyz
```

    3
    




    3




```python
foo=1
def func2():
  global foo
  foo=3
  print(foo)
func2()
```

    3
    


```python
>>> foo
```




    3



**Read:**[ Data Structures in Python – Lists, Tuples, Sets, Dictionaries](https://data-flair.training/blogs/python-data-structures-tutorial/)


```python

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDg5NDE5NDVdfQ==
-->