
Python 101 สําหรับมือใหม่
===

Interpreted Language (ความหมายง่ายๆของภาษาแบบนี้คือ มันสามารถทํางานได้บนทุกแพลตฟอร์มขอให้มีแค่ interpreter ให้มันก็พอ และ อีกอย่างคือมันจะทําการแปลงจากโค้ดที่เรามีไปเป็นภาษาที่เครื่องเข้าใจแบบ on the fly)

ถ้าเทียบกับการพัฒนาโปรแกรมด้วย Java การเขียน Python นี้จะแตกต่างแล้วก็เห็นได้ชัดเลยว่ามันเร็วกว่ามากๆ เช่นตัวอย่างนี้เลย
```py
public class
{
 public static void main(String[]args)
 {
   System.out.println("Hello, world!");
 }
}
```
ตัวอย่างภาษา Java

`print``(``"Hello, world!"``)`

ตัวอย่างภาษา Python

แค่เทียบก็เห็นละว่า Line of code น้อยกว่ามาก เขียนสั้นง่ายๆดี

## Basic Python

#### Syntax

_Indent_

ปกติภาษาเขียนโปรแกรมทั่วไปจะต้องมี วงเล็บ (Bracket – {}) เพื่อระบุว่าอะไรคือขอบเขตของมัน แต่ Python ไม่ได้ใช้วงเล็บ แต่ใช้ Indent หรือ Space แทน
```py
public class
{
 public static void main(String[]args)
 {
   System.out.println("Hello, world!");
 }
}
```
แบบ Java ใช้ Bracket
```js
def functionname( parameters ):
   """function_doc"""
   function_detail
   return [expression]
```
แบบ python ใช้ Indent ซึ่งตาม [สไตลด์ไกด์](https://www.python.org/dev/peps/pep-0008/#indentation) ที่ดีควรเว้น 4 Indents น่ะ

_Quotation_

Python รับได้หมดทั้ง 3 แบบนี้ในการใส่ quote

1.  ‘…..’ ( single quote )
2.  “…..” ( double quote )
3.  “””……””” ( tripple double quote – สไตล์นี้ควรจะใช้กับ Document เท่านั้นน่ะ)

_Comment_

มี 2 รูปแบบ

1.  Inline Comment # …… ( 1 sharp )
2.  Multiple Line Comment ”’ ……. ”’ ( 3 single quote )

#### Data Types

Python มี data types ง่ายๆเลยแค่ 5 อย่าง

1.  Numbers (int,float,long,complex)
2.  String
3.  List
4.  Tuple
5.  Dictionary

ใน python เราเองไม่ต้องประกาศตัวแปรว่าเป็น type ไหนก่อนใช้ ( explicit declaration ) มันจะถูกกําหนด type เมื่อมีการ assign ค่าให้มัน
#### Number
```py
no_need_to_declare_int = 2 
no_need_to_declare_float = 3.14
```

ซึ่งใน Number เนี่ย มันจะ support type อยู่ 4 แบบคือ

-   int
-   long
-   float
-   complex

แต่จริงๆแล้วเราไม่จําเป็นต้องรู้ก็ได้ เพราะถึงเวลาใช้ เราไม่จําเป็นต้องประกาศอะไร

#### String

String ใน python มีลูกเล่นมากกว่าภาษาอื่นตรงที่มีว่ามี function ในการ slice ที่แตกต่างไป โดยใช้คําสั่งต่อไปนี้

-   [] สามารถใส่ Index ลงไปตรงๆได้เลย
-   [:] เลือกจะเอาหัวหรือท้ายได้
-   * ใช้วิธี Multiple ให้ string มีหลายตัวก็ได้
-   concat ก็ตรงๆคือ เครื่องหมาย +
```py
str = 'Hello World!'
 
print str # Prints complete string
print str[0] # Prints first character of the string
print str[2:5] # Prints characters starting from 3rd to 5th
print str[2:] # Prints string starting from 3rd character
print str * 2 # Prints string two times
print str + "TEST" # Prints concatenated string
```
#### Lists

list ใน Python ถูกเอาไปใช้หลากหลายได้มากสุดละ มี function คล้ายๆ string แหละ

-   [] สามารถใส่ Index ลงไปตรงๆได้เลย
-   [:] เลือกจะเอาหัวหรือท้ายได้
-   * ใช้วิธี Multiple ให้ string มีหลายตัวก็ได้
-   concat ก็ตรงๆคือ เครื่องหมาย +
```py
list = [ 'abcd', 786 , 2.23, 'john', 70.2 ]
tinylist = [123, 'john']
 
print list # Prints complete list
print list[0] # Prints first element of the list
print list[1:3] # Prints elements starting from 2nd till 3rd
print list[2:] # Prints elements starting from 3rd element
print tinylist * 2 # Prints list two times
print list + tinylist # Prints concatenated lists
```

#### Tuple

ตัวนี้จะแปลกหน่อยถ้าคนไม่รู้จัก type นี้ มันคือ tuple ตัวแปลที่ลักษณะคล้าย List แต่จะแตกต่างกันตรงที่มันจะปิดด้วย Parentheses () ไม่ใช่ square bracket และมันจะ read-only เท่านั้น!
```py
tuple = ( 'abcd', 786 , 2.23, 'john', 70.2 )
tinytuple = (123, 'john')
 
print tuple # Prints complete list
print tuple[0] # Prints first element of the list
print tuple[1:3] # Prints elements starting from 2nd till 3rd 
print tuple[2:] # Prints elements starting from 3rd element
print tinytuple * 2 # Prints list two times
print tuple + tinytuple # Prints concatenated lists
```

#### Dictionary

อันนี้มีทุกภาษาแหละ การใช้ key,value หรือ dictionary ในการเก็บข้อมูลแบบต่างๆ
```py
dict = {}
dict['one'] = "This is one"
dict[2] = "This is two"
 
tinydict = {'name': 'john','code':6734, 'dept': 'sales'}
print dict['one'] # Prints value for 'one' key
print dict[2] # Prints value for 2 key
print tinydict # Prints complete dictionary
print tinydict.keys() # Prints all the keys
print tinydict.values() # Prints all the values
```
#### Operators

Operator อื่นๆ ที่ใช้กันประจํา พวก +,-,*,/ หรือ % คงไม่ต้องพูดถึงเพราะเป็นพื้นฐานที่มีในทุกภาษา แต่ตัวที่น่าสนใจคือ operator 2 ตัวนี้มากกว่า

1.  Membership
2.  Identity

_Membership_
Operator	Description	Example
in	จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นอยู่ในกรอบที่ต้องการเช็คหรือไม่	x in y จะ return true เมื่อ x อยู่ใน y หรือจะ return false เมื่อ x ไม่ได้อยู่
not in	จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นไม่ได้อยู่ในกรอบที่ต้องการเช็ค	x not in y จะ return true เมื่อ x ไม่ได้อยู่ใน y และ return false เมื่อ x อยู่ใน y

| Operator |Description |Example |
|----------|----------|----------|
| in |จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นอยู่ในกรอบที่ต้องการเช็คหรือไม่ |x in y จะ return true เมื่อ x อยู่ใน y หรือจะ return false เมื่อ x ไม่ได้อยู่ |
| not in |จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นไม่ได้อยู่ในกรอบที่ต้องการเช็ค |x not in y จะ return true เมื่อ x ไม่ได้อยู่ใน y และ return false เมื่อ x อยู่ใน y |
```py
name = "John"
if name in ["John", "Rick"]:
print("Your name is either John or Rick.")
```
| Operator |Description |Example |
|----------|----------|----------|
| is |จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นชี้ไปที่ object เดียวกัน |x is y จะ return true เมื่อ x ชี้ไปที่ object เดียวกับ y หรือจะ return false เมื่อ x ไม่ได้ชี้ไปที่ object เดียวกับ y ชี้ |
| not is |จะให้ค่า true หรือ false เมื่อเช็คว่าค่าของสิ่งนั้นไม่ได้ชี้ไปที่ object เดียวกัน |x is y จะ return true เมื่อ x ไม่ได้ชี้ไปที่ object เดียวกับ y หรือจะ return false เมื่อ x ไม่ได้ชี้ไปที่ object เดียวกับ y ชี้ |
```py
x = [1,2,3]
y = [1,2,3]
print(x == y) # Prints out True
print(x is y) # Prints out False
```
#### Condition

อย่างนึงที่น่าสนใจเกี่ยวกับ Python ก็คือมันสะดวก กระทัดรัด และใช้งานได้ดีเลย เช่น ในกรณีของ If-else ใน Java แบบบรรทัดเดียวจะหน้าตาแบบนี้
```py
name = ((city.getName() == null) ? "N/A" : city.getName());
```
ไม่รู้คนอื่นเข้าง่ายรึเปล่าแต่สําหรับผมแล้วมันเข้าใจอยากที่เดียวเลย แต่ถ้าเป็นใน Python จะเป็น
```py
'Yes' if fruit == 'Apple' else 'No'
 
# value_when_true if condition else value_when_false
```
มันมีความแตกต่างกันอย่างเห็นได้ชัดในการเขียน Python กับ Java มันมีความสะดวกสบายกว่ามากๆเลย (ternary operator)

#### String Formatting

การ Format string ใน Python เราจะใช้ % operator เป็นตัวระบุไปที่ string และตัวแปรนั้นๆเช่น
```py
name = "John"
print("Hello, %s!" % name)
 
#Hello, John
 
name = "John"
age = 23
print("%s is %d years old." % (name, age))

#John is 23 years old.
```
ซึ่งการ Format string มีความหมายแตกต่างกันดั่งด้านล่างนี้

-   %s = string
-   %d = integer

#### Loops

ไม่เหมือนนกับภาษา Java ที่ต้อง for แล้ววนตามตัวเลข index ( index.length() แบบนั้น ) แต่ Python สามารถใช้ list วนเข้าไปได้เลย ทําให้สะดวกสบายกว่ามาก

_for loop_
```py
for(int i=1; i<11; i++){
     System.out.println("Count is: " + i);
}
```
แบบภาษา Java เห็นว่าต้อง set เยอะมากในการลูป
```py
# Prints out the numbers 0,1,2,3,4
for x in range(5):
   print(x)
 
# Prints out 3,4,5
for x in ["3","5"]:
   print(x)
```
python ก็แค่โยน list เข้าไปให้มันลูปง่ายๆแค่นั้นเอง

_while loop_

อันนี้เหมือนทั่วไป ไม่มีไรแปลกใหม่
```py
count = 0
while (count < 5):
   print(count)
   count += 1 # This is the same as count = count + 1
```
แต่ที่เด็ดน่ะคือ ซึ่งภาษา Java ไม่มีก็คือ มันสามารถใส่ else กับ loop ได้ เช่น
```py
count=0
while(count < 5):
   print(count)
   count +=1
else:
   print("count value reached %d" %(count))
 
# Prints out 1,2,3,4
for i in range(1, 10):
   if(i%5==0):
      break
   print(i)
else:
   print("this is not printed because for loop is terminated because of break but not due to fail in condition")
```

#### Functions

วิธีการสร้าง Function ใน Python จะใช้ “:” เป็นตัว บอกว่ากําลังจะสร้าง function แบบนี้ ไม่ซับซ้อนอะไรเรื่องนี้

  ```py
def my_function():
   print("Hello From My Function!")
 
def sum_two_numbers(a, b):
   return a + b
```
#### Modules and Packages

_importing_

Modules ใน Python นี้คือเข้าใจง่ายมาก แค่ไฟล์ .py ไฟล์เดียว ซึ่งจะรวบรวม functions ต่างๆไว้ เพราะฉะนั้นแค่ใช้คําสั่ง import เข้ามาเลยก็จะสามารถทํางานได้เลย

ซึ่งไม่จบแค่นั้นใน modules ของ python เรามี function ช่วยอีกหลายอย่าง เช่น

-   สามารถ Explore Modules ได้ด้วยการใช้คําสั่ง dir(x) กับ modules
-   ใช้คําสั่ง help(x) เพื่อดูว่ามันมี document อะไรบ้าง

แต่จริงๆเปิดเว็ปเอาก็ได้น่ะ ฮรี่ๆ ง่ายกว่า
```py
import urllib 
dir(urllib) 
help(urllib)
```
วิธีการใช้ Package ต่างๆ
มีหลักๆ 2 แบบคือ

Import เฉพาะ function ของ package เพื่อใช้งานแค่นั้น
Import package แล้วเปลี่ยน​ alias name ก็ได้
```py
import numpy as np 
np.pi #3.14XXXXX เป็นต้น 
from mupy import array 
a = array([1,2,3])
```

#### Exception Handling

การจัดการกับ exception ใน python ก็คล้ายๆทั่วไป แต่ที่แปลกคือเราสามารใช้ else-block เข้ามจัดการโค้ดได้ด้วย เหมือน Loop ต่างๆ
```py
try:
   fh = open("testfile", "w")
   fh.write("This is my test file for exception handling!!")
except IOError:
   print "Error: can\'t find file or read data"
else:
   print "Written content in the file successfully"
   fh.close()
```
โดยถ้าต้องการที่จัดการกับ exception ทั้งหมด ก็ทําได้โดยการไม่ใส่ specific exception ลงไปง่ายๆเลย

หรือจะใส่เป็น multiple exception ก็ได้แบบตัวอยางด้านล่าง
```py
try:
   You do your operations here;
   ......................
except:
   If there is any exception, then execute this block.
   ......................
else:
   If there is no exception then execute this block. 
 
 
try:
   You do your operations here;
   ......................
except(Exception1[, Exception2[,...ExceptionN]]]):
   If there is any exception from the given exception list, 
   then execute this block.
   ......................
else:
   If there is no exception then execute this block. 
```

## Summary

เนื้อหาเยอะอย่างแรง… แต่ภาพรวมของภาษา Python มีแค่นี้แหละที่เป็น Basic เพราะถ้าเรารู้เรื่องของ syntax – indent, loop, data type แค่นั้นเราก็สามารถต่อยอดได้อีกเยอะละ  

จะเริ่มเขียน Python ให้ดีควรเขียนให้ถูกต้องตามสไตล์ guide ด้วยน่ะ ดูได้จากทที่นี้เลย  [Pep 8 Style guides](https://www.python.org/dev/peps/pep-0008/)

เดี๋ยวครั้งหน้าจะมาลงรายละเอียดตัวอื่นๆเช่นพวก Regular Expression, Files I/O อีกหน่อย จะได้ใช้งานได้ง่าย

Credit Knowledge:

-   https://www.tutorialspoint.com/python
-   https://www.learnpython.org/
-   http://stackoverflow.com/questions/8898590/short-form-for-java-if-statement
-   http://stackoverflow.com/questions/2802726/putting-a-simple-if-then-statement-on-one-line

Credit Image:

-   http://www.pygamepro.com/


> [Source : ](https://www.howtoautomate.in.th/python-101-for-beginner/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxNjMwMzg1LDUzMzgwODg0MV19
-->