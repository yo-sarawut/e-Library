
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
tuple = ( 'abcd', 786 , 2.23, 'john', 70.2 )
tinytuple = (123, 'john')
 
print tuple # Prints complete list
print tuple[0] # Prints first element of the list
print tuple[1:3] # Prints elements starting from 2nd till 3rd 
print tuple[2:] # Prints elements starting from 3rd element
print tinytuple * 2 # Prints list two times
print tuple + tinytuple # Prints concatenated lists


> [Source : ](https://www.howtoautomate.in.th/python-101-for-beginner/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzNDYwNjMzNF19
-->