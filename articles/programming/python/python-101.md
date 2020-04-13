# Python 101 ฉบับรวบลัด

## การแสดงผล และรับข้อมูล

เริ่มแรกลอง print “hello world” กันก่อน

```python
print("hello_world")
```

## Data type \(ประเภทข้อมูล\)

### 1. String

String ก็เป็นตัวแปรที่เก็ยตัวอักษร หรือข้อความ คราวนี้เรามาลองรับ input เป็นชื่อเก็บใส่ตัวแปรที่ชื่อว่า name แล้ว print ออกมากันครับ

ในที่นี้ตัวแปร name ก็จะมี data type คือ string นั้นเอง

```python
name = input("What is your name? ")
print("Hello ",name)
```

### 2. Numeric

| Type | Description |
| :---: | :--- |
| Integer | จำนวนเต็ม เช่น 10, 20 |
| Float | ทศนิยม เช่น 10.0, 20.5 |

ต่อมาลองรับ input เป็น integer 1 ตัว และ float 1 ตัว แล้วเอามาบวกกันแสดงผลรับเป็น integer

```python
num1 = input()

# Cast string to integer
num1 = int(num1)

num2 = input()

# Cast string to float
num2 = float(num2)

total  = num1 + num2

# Cast to integer
total = int(total)

print("total:",total)
```

### 3. List

List ก็คือตัวแปรที่คล้ายๆกับ array ใน C/C++ หรือภาษาอื่นๆนั้นเอง สำหรับใครที่เขียน python เป็นภาษาแรก ให้นึกถึง ตารางที่เก็บข้อมูล

สมมติ เรามีข้อมูลคะแนนนักเรียนอยู่ 5 คน ดังนี้ 20, 40, 30, 50, 35 เราก็จะสร้างตัวแปรชื่อ score ขึ้นมา

โดยที่ List จะเก็บค่าไว้ใน \[\] แต่ละข้อมูลคั่นด้วย comma \(,\)

```python
score = [20, 40, 30, 50, 35]
```

แล้วถ้าเรา อยากเก็บว่าเพื่อนในห้องเรียนนั่งตรงไหนกันบ้าง ให้เรามีเพื่อน 12 คน

มีเก้าอี้อยู่ 4 แถว แถวละ 3 ตัว เราก็วาดตารางขึ้นมาก่อน

|  | คอลัมน์ 1 | คอลัมน์ 2 | คอลัมน์ 3 |  |  |
| :---: | :---: | :---: | :---: | :--- | :--- |
| 0 | แถว1 | A | J | L | nan |
| 1 | แถว2 | F | B | I | nan |
| 2 | แถว3 | D | C | H | nan |
| 3 | แถว4 | G | E | K | nan |

เราก็จะสร้าง List แบบนี้

```python
table = [
    ['A','J','L'],  # row 1 
    ['F','B','I'],  # row 2 
    ['D','C','H'],  # row 3 
    ['G','E','K'],  # row 4         
]

print(table)
```

แต่ในการเขียน Program เราจะเริ่มนับแถว กับคอลัมน์ ตั้งแต่ 0 ใช้คำว่า Index ในการบอกตำแน่ง

่เช่น อยากรู้ว่า K นั่งอยู่ตรงไหน ก็คือ แถว 4 คอลัมน์ 3 พอเป็นในทาง programming เราก็จะบอกว่า K อยู่ที่ Index 3,2

และถ้าทุกคนสังเกต 2 ตัวอย่างผ่านมาจะรู้ว่า List สามารถเก็บตัวแปรประเภทใดก็ได้ สามารถเก็บตัวแปรคนละชนิด ไว้ใน List เดียวกันก็ได้ เช่น

```python
person = ["sk", "conan", "20"]

print("Name:", person[0], " Lastname:", person[1], " Age:", person[2])
```

### 4. Numpy array

อันนี้ผมอยากให้ทุกคนได้รู้จักเพราะว่า blog ของผมก็เป็น blog เกี่ยวกับ image processing กับ Computer vision เนอะ แล้วมันเกี่ยวกันยังไงใช่มั้ยครับ

เพราะว่า Library OpenCV ที่เราใช้ในการทำ Image processing กันเนี่ยมันจะเก็บข้อมูลรูปภาพไว้ใน Numpy array

Numpy array คือ ตารางหรือ array ที่เก็บค่าข้อมูลที่มี Data type เหมือนกัน ถ้าเป็นรูป ก็จะต้องมี Data type เป็น uint8 มาลองใช้งานกันเลยดีกว่าครับ

```python
import numpy as np

# Covert list to numpy array that have a datatype is uint8
a = np.array([1,2,3,4], np.uint8)
print(a)

# Show type of variable a
print(type(a))

# Show Data type in variable a
print(a.dtype)
```

## Operators \(ตัวดำเนินการ\)

มันก็จะถูกแบ่งแยกย่อยไปอีก เราจะดูเฉพาะตัวที่สำคัญๆนะครับ

### 1. Arithmetic Operators

จะเป็นตัวดำเนินเกี่ยวกับ Math โดยจะสรุปไว้ตามตารางข้างล่างนะครับ กำหนดให้ a = 10, b = 7

|  | Operator | Description | Example | Result |
| :---: | :---: | :---: | :---: | ---: |
| 0 | + | การบวก | a + b | 17.0 |
| 1 | - | การลบ | a - b | 3.0 |
| 2 | \* | การคูณ | a \* b | 70.0 |
| 3 | / | การหาร | a / b | 1.4285714 |
| 4 | % | การหาเศษ จากการหาร | a % b | 3.0 |
| 5 | \*\* | การยกกำลัง | a\*\*b | 10000000.0 |
| 6 | // | การหารแบบไม่เอาเศษ | a//b | 1.0 |

### 2. Assignment Operators

จะเป็นการให้ค่าตัวแปร กำหนดให้ a = 10

| Operator | Example | Result of a |
| :---: | :---: | ---: |
| += | a += 3 | 13.0 |
| -= | a -= 3 | 7.0 |
| \*= | a \*= 3 | 30.0 |
| / | a / b | 1.4285714 |
| % | a %= 3 | 1.0 |
| \*\* = | a\*\* = 3 | 1000.0 |
| //= | a//=3 | 1.0 |

### 3. Comparison Operators

จะเป็นการเปรียบเทียบ กำหนดให้ a = 10, b = 10

|  | Operator | Description | Example | Result |
| :---: | :---: | :---: | :---: | :---: |
| 0 | == | ความเท่ากัน | a == b | True |
| 1 | != | ความไม่เท่ากัน | a != b | False |
| 2 | &gt; | มากกว่า | a &gt; b | False |
| 3 | &lt; | น้อยกว่า | a &lt; b | False |
| 4 | &gt;= | มากกว่าเท่ากับ | a &gt;= b | True |
| 5 | &lt;= | น้อยกว่าเท่ากับ | a &lt;= b | True |

### 4. Logical Operators

เป็นการเปรียบเทียบทางตรรกศาสตร์ กำหนดให้ a = True, b = False

| Operator | Description | Example | Result |
| :---: | :--- | :---: | :---: |
| and | ต้องจริงทั้ง 2 ค่า ถึงจะเป็นจริง นอกนั้นเป็นเท็จ | a and b | False |
| or | ต้องเท็จ 2 ค่า ถึงจะเป็นเท็จ นอกนั้นเป็นจริง | a or b | True |
| not | ให้ค่าตรงข้าม | not \(a and a\) | False |

## If-Else Condition

เป็นการเขียนเพื่อควบคุมการทำงานของโปรแกรมให้เป็นไปตาม ทางเลือก ที่เราตั้งไว้ เช่น ตัวอย่างที่ฮิตก็เป็นการตัดเกรด 80 มากกว่าเท่ากับได้ A, 70 -&gt; B, 60 -&gt; C, 40 -&gt; D และต่ำกว่า 40 ได้ F

โดยรูปแบบการเขียนก็มี 3 แบบ

### 1. if condition

ถ้า if เป็นจริงก็ทำ statement1

```python
if condition:
    statement 1
```

### 2. if-else condition

ในส่วนของ if else ก็แปลตรงตัวเลยครับ ถ้า if เป็นจริงก็ทำ statement1 ถ้าไม่จริงก็ทำ statement2 ใน else

```python
if condition:
    statement 1
else:
    statement 2
```

### 3. if-elif-else condition

ในส่วนนี้ก็ถ้า if เป็นจริงก็ทำ statement1 ถ้าไม่จริงก็ไล่ check ทีละ elif ถ้า codition ไหนเป็นจริงก็เข้าไปทำ statement นั้น โดย elif จะมีมากกว่า 2 อันก็ได้ สุดท้ายถ้าไม่มี condition ไหนที่เป็นจริงเลยก็ทำ else

```python
if condition 1:
    statement 1
elif condition 2:
    statement 2
elif condition 3:
    statement 3
else:
    statement 4
```

มาดูโค้ดตัดเกรดกันครับ

```python
    score = int(input())
    if score >= 80:
        print("You got A")
    elif  score >= 70:
        print("You got B")
    elif  score >= 60:    
        print("You got C")
    elif  score >= 40:
        print("You got D")
    else:
        print("You got F")
```

## While Loop

เป็นการทำอะไรที่ต้องวนหลายๆรอบจน กระทั่ง เงื่อนไขที่ตั้งไว้เป็น False เช่น ให้แสดงเลข 1 ถึง n

```python
n = int(input())

i = 1

while i <= n:
    print(i)
    i += 1
```

จากโค้ดข้างบนเราจะเห็นว่ามีการตั้ง Condition ไว้ว่า ถ้า i &lt;= n ก็ยังให้ loop ทำงานอยู่ ซึ่งในการทำงานแต่ละรอบ ค่า i ก็จะถูกเพิ่มค่าทีละ 1 เราจะเห็นว่าเมื่อค่า i เพิ่มค่าเป็น n+1 Loop ก็จะไม่ทำงาน

## For Loops

การทำงานคล้ายๆ กับ while loop ต่างกันที่ for มีการกำหนดตัวแปร และเพิ่มค่าตรงส่วนของ Condition เลย โดยการเขียน for มีลักษณะ ดังนี้

```python
# Loop 1 
for i in range(start, stop, step):
    statement

# Loop 2 
for i in range(start, stop)
    statement
```

อันนี้เป็นการสรุปคร่าวๆนะครับ เนื่องจากว่าช่วงนี้ต้องสอน Python ในรุ่นน้องด้วยเวลาที่จำกัดก็เลยลองเขียนบทความนี้ขึ้นมา เดี๋ยวจะมาอัพเดทเรื่อยๆครับ

> ที่มาบทความ : [skconan.com](https://www.skconan.com/python-cheat-101/).

