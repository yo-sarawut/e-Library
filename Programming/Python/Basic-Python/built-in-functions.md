
# ฟังก์ชันพื้นฐาน

**Source**
- https://phyblas.hinaboshi.com/tsuchinoko04
- https://data-flair.training/blogs/python-built-in-functions/
- https://www.techbeamers.com/python-function/

**ฟังก์ชัน (function)** ในทางคณิตศาสตร์หมายถึงสิ่งที่แสดงความสัมพันธ์ระหว่างจำนวน โดยใส่ค่าตัวเลขลงไปจำนวนหนึ่ง แล้วจะได้ค่าตัวเลขอีกจำนวนหนึ่งคืนกลับมา ฟังก์ชันในทางภาษาคอมพิวเตอร์ก็มีลักษณะคล้ายกันนี้ คือใส่ค่าอะไรบางอย่าง (อาร์กิวเมนต์) ลงไปแล้วก็จะมีค่าคืนกลับออกมา


```python
a = 1.111
b = int(a)
print(b)
```

    1
    


```python
len('sawatdi')
```




    7




```python
c = 2.222
d = str(c)
print(d) # ได้ '2.222'
print(c) # ได้ 2.222
```

    2.222
    2.222
    

## อาร์กิวเมนต์หลายตัว
อาร์กิวเมนต์ไม่จำเป็นที่จะต้องมีแค่ตัวเดียว อาจมีหลายตัวก็ได้ หากมีหลายตัวก็ต้องคั่นด้วยเครื่องหมายจุลภาค , 


```python
print('a =', 1, ', b =', 2)
```

    a = 1 , b = 2
    

## คีย์เวิร์ดของฟังก์ชัน
นอกจาก อาร์กิวเมนต์แล้ว ฟังก์ชันยังอาจประกอบด้วยสิ่งที่เรียกว่าคีย์เวิร์ด (keyword) ซึ่งเป็นอีกสิ่งหนึ่งที่สามารถป้อนให้กับฟังก์ชันได้ แต่ต่างจากอาร์กิวเมนต์ตรงที่ว่าการป้อนคีย์เวิร์ดจะต้องใส่ชื่อของ คีย์เวิร์ดนั้น


```python
print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')
```

    ฉันมีความสุข(^_^)555(^_^)๕๕๕(^_^)อยากหัวเราะดังๆ
    


```python

```

ตัวอย่าง นี้จะเห็นว่าประกอบไปด้วยอาร์กิวเมนต์ ๔ ตัว และด้านหลังอาร์กิวเมนต์ หลังจุลภาคตัวสุดท้ายจะเห็น sep='(^_^)' ซึ่ง sep นี้ก็คือคีย์เวิร์ดที่ใส่เพิ่มลงไปนั่นเอง

ความหมายของ sep ในฟังก์ชัน print ก็คือคำที่ใช้แยกระหว่างอาร์กิวเมนต์แต่ละตัวที่ใส่ลงไป ดังนั้นจึงจะเห็นได้ว่ามี (^_^) ปรากฏขึ้นมาแทรก

โดยปกติแล้วถ้าหาก ไม่พิมพ์ sep ลงไปฟังก์ชันก็ยังทำงานได้ปกติ เพียงแต่ตัวคั่นระหว่างแต่ละอาร์กิวเมนต์จะกลายเป็นการเว้นวรรค ดังที่เห็นในตัวอย่างที่แล้ว การเพิ่มคีย์เวิร์ดเข้ามาจึงเป็นแค่การแต่งเสริมเพิ่มเติม

นอกจาก sep แล้วก็ยังมีคีย์เวิร์ดสำคัญอีกตัวคือ end ซึ่งเป็นตัวกำหนดการสิ้นสุดประโยค


```python
print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')
print('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')
print('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')
print('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')
```

    การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ!

## เมธอด
ในภาษาไพธอนและอีกหลายภาษาที่เน้นการเขียนโปรแกรมเชิงวัตถุนั้นนอกจากฟังก์ชันแล้วยังมีคำสั่งอีกอีกชนิดหนึ่งซึ่งซึ่งมีลักษณะพิเศษเฉพาะ เรียกว่าเมธอด (method) ซึ่งก็อาจถือเป็นฟังก์ชันชนิดหนึ่ง เพียงแต่จะมีความจำเพาะต่อออบเจ็กต์

เมธอดจะถูกนิยามควบคู่ไปกับออบเจ็กต์แต่ละชนิด โดยออบเจ็กต์แต่ละชนิดจะมีเมธอดไม่เหมือนกัน เมธอดจะไม่ปรากฏขึ้นเดี่ยวๆเหมือนอย่างฟังก์ชันทั่วไป

เวลาเขียนเมธอดจะเขียนตามหลังวัตถุที่ต้องการใช้เมธอดนั้น โดยใช้จุด . คั่น

ขอยกตัวอย่างเช่น ออบเจ็กต์ชนิดจำนวนจริงมีเมธอดที่ชื่อว่า is_integer() คือเมธอดสำหรับตรวจว่าค่าของจำนวนจริงนั้นเป็นจำนวนเต็มในทางคณิตศาสตร์หรือ ไม่ (คือมีค่าเลขทศนิยมเป็น 0 หรือไม่) ถ้าเป็นก็คืนค่า True ถ้าไม่ใช่ก็คืนค่า False


```python
x = 3.0
x.is_integer()
```




    True




```python
(3.1).is_integer()
```




    False




```python
(3).is_integer()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-9-6819ca9637d4> in <module>
    ----> 1 (3).is_integer()
    

    AttributeError: 'int' object has no attribute 'is_integer'


เพราะข้อมูลชนิดจำนวนเต็มไม่มีเมธอด is_integer ต้องเป็นข้อมูลชนิดจำนวนจริงเท่านั้นถึงจะมี

วงเล็บที่อยู่ด้านหลังนั้นสามารถใส่อาร์กิวเมนต์หรือคีย์เวิร์ดลงไปได้เช่นกันหากเมธอดนั้นเป็นเมธอดที่ต้องการหรือสามารถใส่เพิ่มอาร์กิวเมนต์หรือคีย์เวิร์ดได้

### ascii()


```python
ascii('ș')
```


```python
ascii('ușor')
```


```python
ascii(['s','ș'])
```

### bin()


```python
bin(7)
```

### ord()


```python
ord('A')
```


```python
ord('9')
```

### chr()


```python
chr(65)
```


```python
chr(97)
```


```python
chr(9)
```


```python
str('Hello')
```


```python
str(7)
```


```python
sum([3,4,5],3)
```

### classmethod()


```python
>>> class fruit:
                def sayhi(self):
                                print("Hi, I'm a fruit") 
       
>>> fruit.sayhi=classmethod(fruit.sayhi)
>>> fruit.sayhi()
```

### compile()


```python
exec(compile('a=5\nb=7\nprint(a+b)','','exec'))
```

### dict()


```python
dict()
```




    {}




```python
dict([(1,2),(3,4)])
```




    {1: 2, 3: 4}



### dir()


```python
>>> class fruit:
                size=7
                shape='round'
>>> orange=fruit()
>>> dir(orange)
```




    ['__class__',
     '__delattr__',
     '__dict__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__le__',
     '__lt__',
     '__module__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     '__weakref__',
     'shape',
     'size']



### enumerate()


```python
for i in enumerate(['a','b','c']):
                print(i)
```

    (0, 'a')
    (1, 'b')
    (2, 'c')
    

### eval()


```python
x=7
eval('x+7')
```




    14




```python
eval('x+(x%2)')
```




    8



### exec()


```python
exec('a=2;b=3;print(a+b)')
```

    5
    


```python
exec(input("Enter your program"))
```

    Enter your program5
    

### iter()


```python
for i in iter([1,2,3]):
            print(i)
```

    1
    2
    3
    


```python
len({1,2,2,3})
```




    3




```python
list({1,3,2,2})
```




    [1, 2, 3]




```python
locals()
```




    {'__name__': '__main__',
     '__doc__': 'Automatically created module for IPython interactive environment',
     '__package__': None,
     '__loader__': None,
     '__spec__': None,
     '__builtin__': <module 'builtins' (built-in)>,
     '__builtins__': <module 'builtins' (built-in)>,
     '_ih': ['',
      'a = 1.111\nb = int(a)\nprint(b)',
      "len('sawatdi')",
      "c = 2.222\nd = str(c)\nprint(d) # ได้ '2.222'\nprint(c) # ได้ 2.222",
      "print('a =', 1, ', b =', 2)",
      "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')",
      "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
      'x = 3.0\nx.is_integer()',
      '(3.1).is_integer()',
      '(3).is_integer()',
      'dict()',
      'dict([(1,2),(3,4)])',
      "class fruit:\n                size=7\n                shape='round'\norange=fruit()\ndir(orange)",
      "for i in enumerate(['a','b','c']):\n                print(i)",
      "x=7\neval('x+7')",
      "eval('x+(x%2)')",
      "exec('a=2;b=3;print(a+b)')",
      'exec(input("Enter your program"))',
      'for i in iter([1,2,3]):\n            print(i)',
      'len({1,2,2,3})',
      'list({1,3,2,2})',
      'locals()'],
     '_oh': {2: 7,
      7: True,
      8: False,
      10: {},
      11: {1: 2, 3: 4},
      12: ['__class__',
       '__delattr__',
       '__dict__',
       '__dir__',
       '__doc__',
       '__eq__',
       '__format__',
       '__ge__',
       '__getattribute__',
       '__gt__',
       '__hash__',
       '__init__',
       '__init_subclass__',
       '__le__',
       '__lt__',
       '__module__',
       '__ne__',
       '__new__',
       '__reduce__',
       '__reduce_ex__',
       '__repr__',
       '__setattr__',
       '__sizeof__',
       '__str__',
       '__subclasshook__',
       '__weakref__',
       'shape',
       'size'],
      14: 14,
      15: 8,
      19: 3,
      20: [1, 2, 3]},
     '_dh': ['D:\\Developer\\Python\\Tutorials\\PythonBasic'],
     'In': ['',
      'a = 1.111\nb = int(a)\nprint(b)',
      "len('sawatdi')",
      "c = 2.222\nd = str(c)\nprint(d) # ได้ '2.222'\nprint(c) # ได้ 2.222",
      "print('a =', 1, ', b =', 2)",
      "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')",
      "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
      'x = 3.0\nx.is_integer()',
      '(3.1).is_integer()',
      '(3).is_integer()',
      'dict()',
      'dict([(1,2),(3,4)])',
      "class fruit:\n                size=7\n                shape='round'\norange=fruit()\ndir(orange)",
      "for i in enumerate(['a','b','c']):\n                print(i)",
      "x=7\neval('x+7')",
      "eval('x+(x%2)')",
      "exec('a=2;b=3;print(a+b)')",
      'exec(input("Enter your program"))',
      'for i in iter([1,2,3]):\n            print(i)',
      'len({1,2,2,3})',
      'list({1,3,2,2})',
      'locals()'],
     'Out': {2: 7,
      7: True,
      8: False,
      10: {},
      11: {1: 2, 3: 4},
      12: ['__class__',
       '__delattr__',
       '__dict__',
       '__dir__',
       '__doc__',
       '__eq__',
       '__format__',
       '__ge__',
       '__getattribute__',
       '__gt__',
       '__hash__',
       '__init__',
       '__init_subclass__',
       '__le__',
       '__lt__',
       '__module__',
       '__ne__',
       '__new__',
       '__reduce__',
       '__reduce_ex__',
       '__repr__',
       '__setattr__',
       '__sizeof__',
       '__str__',
       '__subclasshook__',
       '__weakref__',
       'shape',
       'size'],
      14: 14,
      15: 8,
      19: 3,
      20: [1, 2, 3]},
     'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x000002B4A8881F98>>,
     'exit': <IPython.core.autocall.ZMQExitAutocall at 0x2b4a88de400>,
     'quit': <IPython.core.autocall.ZMQExitAutocall at 0x2b4a88de400>,
     '_': [1, 2, 3],
     '__': 3,
     '___': 8,
     'json': <module 'json' from 'D:\\Anaconda\\lib\\json\\__init__.py'>,
     'autopep8': <module 'autopep8' from 'D:\\Anaconda\\lib\\site-packages\\autopep8.py'>,
     '_i': 'list({1,3,2,2})',
     '_ii': 'len({1,2,2,3})',
     '_iii': 'for i in iter([1,2,3]):\n            print(i)',
     '_i1': 'a = 1.111\nb = int(a)\nprint(b)',
     'a': 2,
     'b': 3,
     '_i2': "len('sawatdi')",
     '_2': 7,
     '_i3': "c = 2.222\nd = str(c)\nprint(d) # ได้ '2.222'\nprint(c) # ได้ 2.222",
     'c': 2.222,
     'd': '2.222',
     '_i4': "print('a =', 1, ', b =', 2)",
     '_i5': "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')",
     '_i6': "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
     '_i7': 'x = 3.0\nx.is_integer()',
     'x': 7,
     '_7': True,
     '_i8': '(3.1).is_integer()',
     '_8': False,
     '_i9': '(3).is_integer()',
     '_i10': 'dict()',
     '_10': {},
     '_i11': 'dict([(1,2),(3,4)])',
     '_11': {1: 2, 3: 4},
     '_i12': ">>> class fruit:\n                size=7\n                shape='round'\n>>> orange=fruit()\n>>> dir(orange)",
     'fruit': __main__.fruit,
     'orange': <__main__.fruit at 0x2b4a8b16be0>,
     '_12': ['__class__',
      '__delattr__',
      '__dict__',
      '__dir__',
      '__doc__',
      '__eq__',
      '__format__',
      '__ge__',
      '__getattribute__',
      '__gt__',
      '__hash__',
      '__init__',
      '__init_subclass__',
      '__le__',
      '__lt__',
      '__module__',
      '__ne__',
      '__new__',
      '__reduce__',
      '__reduce_ex__',
      '__repr__',
      '__setattr__',
      '__sizeof__',
      '__str__',
      '__subclasshook__',
      '__weakref__',
      'shape',
      'size'],
     '_i13': "for i in enumerate(['a','b','c']):\n                print(i)",
     'i': 3,
     '_i14': "x=7\neval('x+7')",
     '_14': 14,
     '_i15': "eval('x+(x%2)')",
     '_15': 8,
     '_i16': "exec('a=2;b=3;print(a+b)')",
     '_i17': 'exec(input("Enter your program"))',
     '_i18': 'for i in iter([1,2,3]):\n            print(i)',
     '_i19': 'len({1,2,2,3})',
     '_19': 3,
     '_i20': 'list({1,3,2,2})',
     '_20': [1, 2, 3],
     '_i21': 'locals()'}




```python
list(map(lambda x:x%2==0,[1,2,3,4,5]))
```




    [False, True, False, True, False]




```python
max(2,3,4)
```




    4




```python
>>> a=bytes(4)
>>> memoryview(a)
```




    <memory at 0x000002B4A8A46408>




```python
min(3,5,1)
```




    1




```python
>>> myIterator=iter([1,2,3,4,5])
>>> next(myIterator)
```




    1




```python
next(myIterator)
```




    2




```python
next(myIterator)
```




    3




```python
for i in range(7,2,-2):
         print(i)
```

    7
    5
    3
    


```python
a=reversed([3,2,1])
>>> a
```




    <list_reverseiterator at 0x2b4a8b1a470>




```python
for i in a:
    print(i)
```

    1
    2
    3
    


```python
type(a)
```




    list_reverseiterator




```python
set([2,2,3,1])
```




    {1, 2, 3}




```python
sorted('Python')
```




    ['P', 'h', 'n', 'o', 't', 'y']




```python
sorted([1,3,2])
```




    [1, 2, 3]




```python
tuple([1,3,2])
```




    (1, 3, 2)




```python
tuple({1:'a',2:'b'})
```




    (1, 2)




```python
type({})
```




    dict




```python
type((1))
```




    int




```python
type(('A'))
```




    str




```python
vars(fruit)
```




    mappingproxy({'__module__': '__main__',
                  'size': 7,
                  'shape': 'round',
                  '__dict__': <attribute '__dict__' of 'fruit' objects>,
                  '__weakref__': <attribute '__weakref__' of 'fruit' objects>,
                  '__doc__': None})



### zip()


```python
set(zip([1,2,3],['a','b','c']))
```




    {(1, 'a'), (2, 'b'), (3, 'c')}




```python
set(zip([1,2],[3,4,5]))
```




    {(1, 3), (2, 4)}




```python
a=zip([1,2,3],['a','b','c'])
```

**unzip**


```python
>>> x,y,z=a
>>> x
```




    (1, 'a')




```python
y
```




    (2, 'b')




```python
z
```




    (3, 'c')



### super()


```python
>>> class person:
           def __init__(self):
               print("A person")
>>> class student(person):
            def __init__(self):
                super().__init__()
                print("A student")
>>> Avery=student()
```

    A person
    A student
    


```python
>>> o=object()
>>> type(o)
```




    object




```python
dir(o)
```




    ['__class__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__le__',
     '__lt__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__']




```python
oct(8)
```




    '0o10'




```python
>>> import os
>>> os.chdir('C:\\Users\\User\\Desktop')
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-52-4e8668a7abff> in <module>
          1 import os
    ----> 2 os.chdir('C:\\Users\\User\\Desktop')
    

    FileNotFoundError: [WinError 3] The system cannot find the path specified: 'C:\\Users\\User\\Desktop'



```python
>>> f=open('symbol-yahoo-finance.csv')
>>> f
```


```python
type(f)
```


```python
print(f.read())
```

## Example Of A Function Call


```python
def typeOfNum(num): # Function header
    # Function body
    if num % 2 == 0:
        def message():
            print("You entered an even number.")
    else:
        def message():
            print("You entered an odd number.")
    message()
# End of function

typeOfNum(2)  # call the function
typeOfNum(3)  # call the function again
```

**Source** : https://www.techbeamers.com/python-function/

## Example: Immutable Vs. Mutable


```python
def test1(a, b) :
    a = 'Garbage' # 'a' receives an immutable object
    b[0] = 'Python' # 'b' receives a list object
                    # list is mutable
                    # it can undergo an in place change
def test2(a, b) :
    a = 'Garbage 2'
    b = 'Python 3' # 'b' now is made to refer to new
                   # object and therefore argument 'y'
                   # is not changed

arg1 = 10
arg2 = [1, 2, 3, 4]
test1(arg1, arg2)
print("After executing test 1 =>", arg1, arg2)
test2(arg1, arg2)
print("After executing test 2 =>", arg1, arg2)
```





> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTk0MjY3NDk0XX0=
-->