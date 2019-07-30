Basic-Function

## ฟังก์ชันพื้นฐาน[¶](#ฟังก์ชันพื้นฐาน)

**Source**

-   [https://phyblas.hinaboshi.com/tsuchinoko04](https://phyblas.hinaboshi.com/tsuchinoko04)
-   [https://data-flair.training/blogs/python-built-in-functions/](https://data-flair.training/blogs/python-built-in-functions/)
-   [https://www.techbeamers.com/python-function/](https://www.techbeamers.com/python-function/)

**ฟังก์ชัน (function)** ในทางคณิตศาสตร์หมายถึงสิ่งที่แสดงความสัมพันธ์ระหว่างจำนวน โดยใส่ค่าตัวเลขลงไปจำนวนหนึ่ง แล้วจะได้ค่าตัวเลขอีกจำนวนหนึ่งคืนกลับมา ฟังก์ชันในทางภาษาคอมพิวเตอร์ก็มีลักษณะคล้ายกันนี้ คือใส่ค่าอะไรบางอย่าง (อาร์กิวเมนต์) ลงไปแล้วก็จะมีค่าคืนกลับออกมา

In \[1\]:

a = 1.111
b = int(a)
print(b)

1

In \[2\]:

len('sawatdi')

Out\[2\]:

7

In \[3\]:

c = 2.222
d = str(c)
print(d) \# ได้ '2.222'
print(c) \# ได้ 2.222

2.222
2.222

### อาร์กิวเมนต์หลายตัว[¶](#อาร์กิวเมนต์หลายตัว)

อาร์กิวเมนต์ไม่จำเป็นที่จะต้องมีแค่ตัวเดียว อาจมีหลายตัวก็ได้ หากมีหลายตัวก็ต้องคั่นด้วยเครื่องหมายจุลภาค ,

In \[4\]:

print('a =', 1, ', b =', 2)

a = 1 , b = 2

### คีย์เวิร์ดของฟังก์ชัน[¶](#คีย์เวิร์ดของฟังก์ชัน)

นอกจาก อาร์กิวเมนต์แล้ว ฟังก์ชันยังอาจประกอบด้วยสิ่งที่เรียกว่าคีย์เวิร์ด (keyword) ซึ่งเป็นอีกสิ่งหนึ่งที่สามารถป้อนให้กับฟังก์ชันได้ แต่ต่างจากอาร์กิวเมนต์ตรงที่ว่าการป้อนคีย์เวิร์ดจะต้องใส่ชื่อของ คีย์เวิร์ดนั้น

In \[5\]:

print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')

ฉันมีความสุข(^_^)555(^_^)๕๕๕(^_^)อยากหัวเราะดังๆ

In \[ \]:

ตัวอย่าง นี้จะเห็นว่าประกอบไปด้วยอาร์กิวเมนต์ ๔ ตัว และด้านหลังอาร์กิวเมนต์ หลังจุลภาคตัวสุดท้ายจะเห็น sep='(^_^)' ซึ่ง sep นี้ก็คือคีย์เวิร์ดที่ใส่เพิ่มลงไปนั่นเอง

ความหมายของ sep ในฟังก์ชัน print ก็คือคำที่ใช้แยกระหว่างอาร์กิวเมนต์แต่ละตัวที่ใส่ลงไป ดังนั้นจึงจะเห็นได้ว่ามี (^_^) ปรากฏขึ้นมาแทรก

โดยปกติแล้วถ้าหาก ไม่พิมพ์ sep ลงไปฟังก์ชันก็ยังทำงานได้ปกติ เพียงแต่ตัวคั่นระหว่างแต่ละอาร์กิวเมนต์จะกลายเป็นการเว้นวรรค ดังที่เห็นในตัวอย่างที่แล้ว การเพิ่มคีย์เวิร์ดเข้ามาจึงเป็นแค่การแต่งเสริมเพิ่มเติม

นอกจาก sep แล้วก็ยังมีคีย์เวิร์ดสำคัญอีกตัวคือ end ซึ่งเป็นตัวกำหนดการสิ้นสุดประโยค

In \[6\]:

print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')
print('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')
print('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')
print('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')

การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ!

### เมธอด[¶](#เมธอด)

ในภาษาไพธอนและอีกหลายภาษาที่เน้นการเขียนโปรแกรมเชิงวัตถุนั้นนอกจากฟังก์ชันแล้วยังมีคำสั่งอีกอีกชนิดหนึ่งซึ่งซึ่งมีลักษณะพิเศษเฉพาะ เรียกว่าเมธอด (method) ซึ่งก็อาจถือเป็นฟังก์ชันชนิดหนึ่ง เพียงแต่จะมีความจำเพาะต่อออบเจ็กต์

เมธอดจะถูกนิยามควบคู่ไปกับออบเจ็กต์แต่ละชนิด โดยออบเจ็กต์แต่ละชนิดจะมีเมธอดไม่เหมือนกัน เมธอดจะไม่ปรากฏขึ้นเดี่ยวๆเหมือนอย่างฟังก์ชันทั่วไป

เวลาเขียนเมธอดจะเขียนตามหลังวัตถุที่ต้องการใช้เมธอดนั้น โดยใช้จุด . คั่น

ขอยกตัวอย่างเช่น ออบเจ็กต์ชนิดจำนวนจริงมีเมธอดที่ชื่อว่า is_integer() คือเมธอดสำหรับตรวจว่าค่าของจำนวนจริงนั้นเป็นจำนวนเต็มในทางคณิตศาสตร์หรือ ไม่ (คือมีค่าเลขทศนิยมเป็น 0 หรือไม่) ถ้าเป็นก็คืนค่า True ถ้าไม่ใช่ก็คืนค่า False

In \[7\]:

x = 3.0
x.is_integer()

Out\[7\]:

True

In \[8\]:

(3.1).is_integer()

Out\[8\]:

False

In \[9\]:

(3).is_integer()

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-
AttributeError                            Traceback (most recent call last)
<ipython-input-9-6819ca9637d4> in <module>
----\> 1  (3).is_integer()

AttributeError: 'int' object has no attribute 'is_integer'

เพราะข้อมูลชนิดจำนวนเต็มไม่มีเมธอด is_integer ต้องเป็นข้อมูลชนิดจำนวนจริงเท่านั้นถึงจะมี

วงเล็บที่อยู่ด้านหลังนั้นสามารถใส่อาร์กิวเมนต์หรือคีย์เวิร์ดลงไปได้เช่นกันหากเมธอดนั้นเป็นเมธอดที่ต้องการหรือสามารถใส่เพิ่มอาร์กิวเมนต์หรือคีย์เวิร์ดได้

### ascii()[¶](#ascii())

In \[ \]:

ascii('ș')

In \[ \]:

ascii('ușor')

In \[ \]:

ascii(\['s','ș'\])

### bin()[¶](#bin())

In \[ \]:

bin(7)

### ord()[¶](#ord())

In \[ \]:

ord('A')

In \[ \]:

ord('9')

### chr()[¶](#chr())

In \[ \]:

chr(65)

In \[ \]:

chr(97)

In \[ \]:

chr(9)

In \[ \]:

str('Hello')

In \[ \]:

str(7)

In \[ \]:

sum(\[3,4,5\],3)

### classmethod()[¶](#classmethod())

In \[ \]:

>>> class fruit:
                def sayhi(self):
                                print("Hi, I'm a fruit") 
       
>>> fruit.sayhi=classmethod(fruit.sayhi)
>>> fruit.sayhi()

### compile()[¶](#compile())

In \[ \]:

exec(compile('a=5\\nb=7\\nprint(a+b)','','exec'))

### dict()[¶](#dict())

In \[10\]:

dict()

Out\[10\]:

{}

In \[11\]:

dict(\[(1,2),(3,4)\])

Out\[11\]:

{1: 2, 3: 4}

### dir()[¶](#dir())

In \[12\]:

>>> class fruit:
                size=7
                shape='round'
>>> orange=fruit()
>>> dir(orange)

Out\[12\]:

\['\_\_class\_\_',
 '\_\_delattr\_\_',
 '\_\_dict\_\_',
 '\_\_dir\_\_',
 '\_\_doc\_\_',
 '\_\_eq\_\_',
 '\_\_format\_\_',
 '\_\_ge\_\_',
 '\_\_getattribute\_\_',
 '\_\_gt\_\_',
 '\_\_hash\_\_',
 '\_\_init\_\_',
 '\_\_init\_subclass__',
 '\_\_le\_\_',
 '\_\_lt\_\_',
 '\_\_module\_\_',
 '\_\_ne\_\_',
 '\_\_new\_\_',
 '\_\_reduce\_\_',
 '\_\_reduce\_ex__',
 '\_\_repr\_\_',
 '\_\_setattr\_\_',
 '\_\_sizeof\_\_',
 '\_\_str\_\_',
 '\_\_subclasshook\_\_',
 '\_\_weakref\_\_',
 'shape',
 'size'\]

### enumerate()[¶](#enumerate())

In \[13\]:

for i in enumerate(\['a','b','c'\]):
                print(i)

(0, 'a')
(1, 'b')
(2, 'c')

### eval()[¶](#eval())

In \[14\]:

x=7
eval('x+7')

Out\[14\]:

14

In \[15\]:

eval('x+(x%2)')

Out\[15\]:

8

### exec()[¶](#exec())

In \[16\]:

exec('a=2;b=3;print(a+b)')

5

In \[17\]:

exec(input("Enter your program"))

Enter your program5

### iter()[¶](#iter())

In \[18\]:

for i in iter(\[1,2,3\]):
            print(i)

1
2
3

In \[19\]:

len({1,2,2,3})

Out\[19\]:

3

In \[20\]:

list({1,3,2,2})

Out\[20\]:

\[1, 2, 3\]

In \[21\]:

locals()

Out\[21\]:

{'\_\_name\_\_': '\_\_main\_\_',
 '\_\_doc\_\_': 'Automatically created module for IPython interactive environment',
 '\_\_package\_\_': None,
 '\_\_loader\_\_': None,
 '\_\_spec\_\_': None,
 '\_\_builtin\_\_': <module 'builtins' (built-in)>,
 '\_\_builtins\_\_': <module 'builtins' (built-in)>,
 '_ih': \['',
  'a = 1.111\\nb = int(a)\\nprint(b)',
  "len('sawatdi')",
  "c = 2.222\\nd = str(c)\\nprint(d) # ได้ '2.222'\\nprint(c) # ได้ 2.222",
  "print('a =', 1, ', b =', 2)",
  "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')",
  "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
  'x = 3.0\\nx.is_integer()',
  '(3.1).is_integer()',
  '(3).is_integer()',
  'dict()',
  'dict(\[(1,2),(3,4)\])',
  "class fruit:\\n                size=7\\n                shape='round'\\norange=fruit()\\ndir(orange)",
  "for i in enumerate(\['a','b','c'\]):\\n                print(i)",
  "x=7\\neval('x+7')",
  "eval('x+(x%2)')",
  "exec('a=2;b=3;print(a+b)')",
  'exec(input("Enter your program"))',
  'for i in iter(\[1,2,3\]):\\n            print(i)',
  'len({1,2,2,3})',
  'list({1,3,2,2})',
  'locals()'\],
 '_oh': {2: 7,
  7: True,
  8: False,
  10: {},
  11: {1: 2, 3: 4},
  12: \['\_\_class\_\_',
   '\_\_delattr\_\_',
   '\_\_dict\_\_',
   '\_\_dir\_\_',
   '\_\_doc\_\_',
   '\_\_eq\_\_',
   '\_\_format\_\_',
   '\_\_ge\_\_',
   '\_\_getattribute\_\_',
   '\_\_gt\_\_',
   '\_\_hash\_\_',
   '\_\_init\_\_',
   '\_\_init\_subclass__',
   '\_\_le\_\_',
   '\_\_lt\_\_',
   '\_\_module\_\_',
   '\_\_ne\_\_',
   '\_\_new\_\_',
   '\_\_reduce\_\_',
   '\_\_reduce\_ex__',
   '\_\_repr\_\_',
   '\_\_setattr\_\_',
   '\_\_sizeof\_\_',
   '\_\_str\_\_',
   '\_\_subclasshook\_\_',
   '\_\_weakref\_\_',
   'shape',
   'size'\],
  14: 14,
  15: 8,
  19: 3,
  20: \[1, 2, 3\]},
 '_dh': \['D:\\\Developer\\\Python\\\Tutorials\\\PythonBasic'\],
 'In': \['',
  'a = 1.111\\nb = int(a)\\nprint(b)',
  "len('sawatdi')",
  "c = 2.222\\nd = str(c)\\nprint(d) # ได้ '2.222'\\nprint(c) # ได้ 2.222",
  "print('a =', 1, ', b =', 2)",
  "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^_^)')",
  "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
  'x = 3.0\\nx.is_integer()',
  '(3.1).is_integer()',
  '(3).is_integer()',
  'dict()',
  'dict(\[(1,2),(3,4)\])',
  "class fruit:\\n                size=7\\n                shape='round'\\norange=fruit()\\ndir(orange)",
  "for i in enumerate(\['a','b','c'\]):\\n                print(i)",
  "x=7\\neval('x+7')",
  "eval('x+(x%2)')",
  "exec('a=2;b=3;print(a+b)')",
  'exec(input("Enter your program"))',
  'for i in iter(\[1,2,3\]):\\n            print(i)',
  'len({1,2,2,3})',
  'list({1,3,2,2})',
  'locals()'\],
 'Out': {2: 7,
  7: True,
  8: False,
  10: {},
  11: {1: 2, 3: 4},
  12: \['\_\_class\_\_',
   '\_\_delattr\_\_',
   '\_\_dict\_\_',
   '\_\_dir\_\_',
   '\_\_doc\_\_',
   '\_\_eq\_\_',
   '\_\_format\_\_',
   '\_\_ge\_\_',
   '\_\_getattribute\_\_',
   '\_\_gt\_\_',
   '\_\_hash\_\_',
   '\_\_init\_\_',
   '\_\_init\_subclass__',
   '\_\_le\_\_',
   '\_\_lt\_\_',
   '\_\_module\_\_',
   '\_\_ne\_\_',
   '\_\_new\_\_',
   '\_\_reduce\_\_',
   '\_\_reduce\_ex__',
   '\_\_repr\_\_',
   '\_\_setattr\_\_',
   '\_\_sizeof\_\_',
   '\_\_str\_\_',
   '\_\_subclasshook\_\_',
   '\_\_weakref\_\_',
   'shape',
   'size'\],
  14: 14,
  15: 8,
  19: 3,
  20: \[1, 2, 3\]},
 'get\_ipython': <bound method InteractiveShell.get\_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x000002B4A8881F98>>,
 'exit': <IPython.core.autocall.ZMQExitAutocall at 0x2b4a88de400>,
 'quit': <IPython.core.autocall.ZMQExitAutocall at 0x2b4a88de400>,
 '_': \[1, 2, 3\],
 '__': 3,
 '___': 8,
 'json': <module 'json' from 'D:\\\Anaconda\\\lib\\\json\\\\_\_init\_\_.py'>,
 'autopep8': <module 'autopep8' from 'D:\\\Anaconda\\\lib\\\site-packages\\\autopep8.py'>,
 '_i': 'list({1,3,2,2})',
 '_ii': 'len({1,2,2,3})',
 '_iii': 'for i in iter(\[1,2,3\]):\\n            print(i)',
 '_i1': 'a = 1.111\\nb = int(a)\\nprint(b)',
 'a': 2,
 'b': 3,
 '_i2': "len('sawatdi')",
 '_2': 7,
 '_i3': "c = 2.222\\nd = str(c)\\nprint(d) # ได้ '2.222'\\nprint(c) # ได้ 2.222",
 'c': 2.222,
 'd': '2.222',
 '_i4': "print('a =', 1, ', b =', 2)",
 '\_i5': "print('ฉันมีความสุข','555','๕๕๕','อยากหัวเราะดังๆ',sep='(^\_^)')",
 '_i6': "print('การฝึกฝนที่ไม่มีความเจ็บปวดมันไม่มีความหมาย',end=' ')\\nprint('เพราะคนเราไม่สามารถได้อะไรมาโดยที่ไม่ต้องเสียสละอะไร',end=' ')\\nprint('แต่ว่าเมื่อทนความเจ็บปวดนั้นและก้าวผ่านมันไปได้',end='')\\nprint('ถึงตอนนั้นคนเราก็จะมีจิตใจที่แกร่งกล้าไม่แพ้ใครๆ',end='!')",
 '\_i7': 'x = 3.0\\nx.is\_integer()',
 'x': 7,
 '_7': True,
 '\_i8': '(3.1).is\_integer()',
 '_8': False,
 '\_i9': '(3).is\_integer()',
 '_i10': 'dict()',
 '_10': {},
 '_i11': 'dict(\[(1,2),(3,4)\])',
 '_11': {1: 2, 3: 4},
 '_i12': ">>> class fruit:\\n                size=7\\n                shape='round'\\n>>> orange=fruit()\\n>>> dir(orange)",
 'fruit': \_\_main\_\_.fruit,
 'orange': <\_\_main\_\_.fruit at 0x2b4a8b16be0>,
 '\_12': \['\_\_class__',
  '\_\_delattr\_\_',
  '\_\_dict\_\_',
  '\_\_dir\_\_',
  '\_\_doc\_\_',
  '\_\_eq\_\_',
  '\_\_format\_\_',
  '\_\_ge\_\_',
  '\_\_getattribute\_\_',
  '\_\_gt\_\_',
  '\_\_hash\_\_',
  '\_\_init\_\_',
  '\_\_init\_subclass__',
  '\_\_le\_\_',
  '\_\_lt\_\_',
  '\_\_module\_\_',
  '\_\_ne\_\_',
  '\_\_new\_\_',
  '\_\_reduce\_\_',
  '\_\_reduce\_ex__',
  '\_\_repr\_\_',
  '\_\_setattr\_\_',
  '\_\_sizeof\_\_',
  '\_\_str\_\_',
  '\_\_subclasshook\_\_',
  '\_\_weakref\_\_',
  'shape',
  'size'\],
 '_i13': "for i in enumerate(\['a','b','c'\]):\\n                print(i)",
 'i': 3,
 '_i14': "x=7\\neval('x+7')",
 '_14': 14,
 '_i15': "eval('x+(x%2)')",
 '_15': 8,
 '_i16': "exec('a=2;b=3;print(a+b)')",
 '_i17': 'exec(input("Enter your program"))',
 '_i18': 'for i in iter(\[1,2,3\]):\\n            print(i)',
 '_i19': 'len({1,2,2,3})',
 '_19': 3,
 '_i20': 'list({1,3,2,2})',
 '_20': \[1, 2, 3\],
 '_i21': 'locals()'}

In \[22\]:

list(map(lambda x:x%2==0,\[1,2,3,4,5\]))

Out\[22\]:

\[False, True, False, True, False\]

In \[23\]:

max(2,3,4)

Out\[23\]:

4

In \[24\]:

>>> a=bytes(4)
>>> memoryview(a)

Out\[24\]:

<memory at 0x000002B4A8A46408>

In \[25\]:

min(3,5,1)

Out\[25\]:

1

In \[26\]:

>>> myIterator=iter(\[1,2,3,4,5\])
>>> next(myIterator)

Out\[26\]:

1

In \[27\]:

next(myIterator)

Out\[27\]:

2

In \[28\]:

next(myIterator)

Out\[28\]:

3

In \[29\]:

for i in range(7,2,-2):
         print(i)

7
5
3

In \[30\]:

a=reversed(\[3,2,1\])
>>> a

Out\[30\]:

<list_reverseiterator at 0x2b4a8b1a470>

In \[31\]:

for i in a:
    print(i)

1
2
3

In \[32\]:

type(a)

Out\[32\]:

list_reverseiterator

In \[33\]:

set(\[2,2,3,1\])

Out\[33\]:

{1, 2, 3}

In \[34\]:

sorted('Python')

Out\[34\]:

\['P', 'h', 'n', 'o', 't', 'y'\]

In \[35\]:

sorted(\[1,3,2\])

Out\[35\]:

\[1, 2, 3\]

In \[36\]:

tuple(\[1,3,2\])

Out\[36\]:

(1, 3, 2)

In \[37\]:

tuple({1:'a',2:'b'})

Out\[37\]:

(1, 2)

In \[38\]:

type({})

Out\[38\]:

dict

In \[39\]:

type((1))

Out\[39\]:

int

In \[40\]:

type(('A'))

Out\[40\]:

str

In \[41\]:

vars(fruit)

Out\[41\]:

mappingproxy({'\_\_module\_\_': '\_\_main\_\_',
              'size': 7,
              'shape': 'round',
              '\_\_dict\_\_': <attribute '\_\_dict\_\_' of 'fruit' objects>,
              '\_\_weakref\_\_': <attribute '\_\_weakref\_\_' of 'fruit' objects>,
              '\_\_doc\_\_': None})

### zip()[¶](#zip())

In \[42\]:

set(zip(\[1,2,3\],\['a','b','c'\]))

Out\[42\]:

{(1, 'a'), (2, 'b'), (3, 'c')}

In \[43\]:

set(zip(\[1,2\],\[3,4,5\]))

Out\[43\]:

{(1, 3), (2, 4)}

In \[44\]:

a=zip(\[1,2,3\],\['a','b','c'\])

**unzip**

In \[45\]:

>>> x,y,z=a
>>> x

Out\[45\]:

(1, 'a')

In \[46\]:

y

Out\[46\]:

(2, 'b')

In \[47\]:

z

Out\[47\]:

(3, 'c')

### super()[¶](#super())

In \[48\]:

>>> class person:
           def \_\_init\_\_(self):
               print("A person")
>>> class student(person):
            def \_\_init\_\_(self):
                super().\_\_init\_\_()
                print("A student")
>>> Avery=student()

A person
A student

In \[49\]:

>>> o=object()
>>> type(o)

Out\[49\]:

object

In \[50\]:

dir(o)

Out\[50\]:

\['\_\_class\_\_',
 '\_\_delattr\_\_',
 '\_\_dir\_\_',
 '\_\_doc\_\_',
 '\_\_eq\_\_',
 '\_\_format\_\_',
 '\_\_ge\_\_',
 '\_\_getattribute\_\_',
 '\_\_gt\_\_',
 '\_\_hash\_\_',
 '\_\_init\_\_',
 '\_\_init\_subclass__',
 '\_\_le\_\_',
 '\_\_lt\_\_',
 '\_\_ne\_\_',
 '\_\_new\_\_',
 '\_\_reduce\_\_',
 '\_\_reduce\_ex__',
 '\_\_repr\_\_',
 '\_\_setattr\_\_',
 '\_\_sizeof\_\_',
 '\_\_str\_\_',
 '\_\_subclasshook\_\_'\]

In \[51\]:

oct(8)

Out\[51\]:

'0o10'

In \[52\]:

>>> import os
>>> os.chdir('C:\\\Users\\\User\\\Desktop')

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-
FileNotFoundError                         Traceback (most recent call last)
<ipython-input-52-4e8668a7abff> in <module>
 1 import os
----\> 2  os.chdir('C:\\\Users\\\User\\\Desktop')

FileNotFoundError: \[WinError 3\] The system cannot find the path specified: 'C:\\\Users\\\User\\\Desktop'

In \[ \]:

>>> f=open('symbol-yahoo-finance.csv')
>>> f

In \[ \]:

type(f)

In \[ \]:

print(f.read())

### Example Of A Function Call[¶](#Example-Of-A-Function-Call)

In \[ \]:

def typeOfNum(num): \# Function header
    \# Function body
    if num % 2 == 0:
        def message():
            print("You entered an even number.")
    else:
        def message():
            print("You entered an odd number.")
    message()
\# End of function

typeOfNum(2)  \# call the function
typeOfNum(3)  \# call the function again

**Source** : [https://www.techbeamers.com/python-function/](https://www.techbeamers.com/python-function/)

### Example: Immutable Vs. Mutable[¶](#Example:-Immutable-Vs.-Mutable)

In \[ \]:

def test1(a, b) :
    a = 'Garbage' \# 'a' receives an immutable object
    b\[0\] = 'Python' \# 'b' receives a list object
                    \# list is mutable
                    \# it can undergo an in place change
def test2(a, b) :
    a = 'Garbage 2'
    b = 'Python 3' \# 'b' now is made to refer to new
                   \# object and therefore argument 'y'
                   \# is not changed

arg1 = 10
arg2 = \[1, 2, 3, 4\]
test1(arg1, arg2)
print("After executing test 1 =>", arg1, arg2)
test2(arg1, arg2)
print("After executing test 2 =>", arg1, arg2)

In \[ \]:

In \[ \]:
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTY4MjUxOV19
-->