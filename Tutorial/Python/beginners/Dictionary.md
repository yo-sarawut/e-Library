# Dictionary

ในบทนี้ คุณจะได้เรียนรู้เกี่ยวกับโครงสร้างข้อมูล Dictionary ในภาษา Python เราจะแนะนำให้คุณรู้จักกับ Dictionary คืออะไร และการประกาศและใช้งานสำหรับเก็บข้อมูลในการเขียนโปรแกรม นอกจากนี้ เรายังจะพูดถึงการใช้งานเมธอดและ built-in functions ของ Dictionary และตัวอย่างการใช้งานกับการเขียนโปรแกรมใบรูปแบบต่างๆ ในภาษา Python

Dictionary คือประเภทข้อมูลที่เก็บข้อมูลในรูปแบบคู่ของ Key และ Value โดยที่ Key ใช้สำหรับเป็น Index ในการเข้าถึงข้อมูลและ Value เป็นค่าข้อมูลที่สอดคล้องกับ Key ของมัน การเข้าถึงข้อมูลใน Dictionary นั้นรวดเร็วเพราะว่าข้อมูลได้ถูกทำ Index ไว้อัตโนมัติโดยใช้ Key นอกจากนี้ Dictionary ยังมีเมธอดและฟังก์ชันอำนวยความสะดวกสำหรับการทำงานทั่วไป

## การประกาศ Dictionary ในภาษา Python

ในการใช้งาน Dictionary เรามักจะใช้เก็บข้อมูลที่สามารถใช้บางอย่างที่สามารถจำแนกข้อมูลออกจากกันได้ โดยกำหนดให้สิ่งนั้นเป็น Key ในการประกาศ Dictionary สมาชิกของมันจะอยู่ภายในวงเล็บปีกกา  `{}`  มาดูตัวอย่างในการประกาศ Dictionary ในภาษา Python

```
scores = {'james': 1828, 'thomas': 3628, 'danny': 9310}
scores['bobby'] = 4401

numbers = {1: 'One', 2: 'Two', 3: 'Three'}

print(scores)
print(numbers)

```

ในตัวอย่าง เราได้ประกาศตัวแปร Dictionary ที่มีชื่อว่า  `scores`  สำหรับเก็บคะแนนของแต่ละคนโดยใช้ชื่อเป็น Key และค่าของมันก็คือคะแนน สมาชิกของ Dictionary แต่ละตัวจะถูกกำหนดในรูปแบบ  `key: value`  และคั่นสมาชิกแต่ละตัวด้วยเครื่องหมายคอมมา เราได้กำหนดค่าเริ่มต้นสามค่าให้กับ Dictionary และสามารถกำหนดค่าให้กับ Dictionary ในรูปแบบ  `scores['bobby']`  ได้หลังจากที่ตัวแปรถูกสร้างแล้ว สังเกตว่าเราสามารถใช้ Key เป็น String หรือประเภทข้อมูลอื่นๆ ได้ ต่อมาตัวแปร  `numbers`  เป็น Dictionary ที่มี Key เป็นตัวเลข

```
{'james': 1828, 'thomas': 3628, 'danny': 9310, 'bobby': 4401}
{1: 'One', 2: 'Two', 3: 'Three'}

```

นี่เป็นผลลัพธ์ของโปรแกรมในการแสดงผลข้อมูลภายในตัวแปร Dictionary ทั้งสองที่เราได้สร้างขึ้น

## การเข้าถึงข้อมูลภายใน Dictionary

หลังจากที่เราได้ประกาศ Dictionary ไปแล้ว ต่อไปจะการเข้าถึงข้อมูลเพื่ออ่านและอัพเดทข้อมูลโดยผ่านทาง Key ของมัน มาดูตัวอย่างการเข้าถึงข้อมูลใน Dictionary

```py
scores = {'james': 1828, 'thomas': 3628, 'danny': 9310, 'bobby': 4401}

# display data
print('james =>', scores['james'])
print('thomas =>', scores['thomas'])
print('danny =>', scores['danny'])
print('bobby =>', scores['bobby'])

# update data
scores['james'] = scores['james'] + 1000
scores['thomas'] = 100

print('james =>', scores['james'])
print('thomas =>', scores['thomas'])

```

ในตัวอย่าง เรามีตัวแปร  `scores`  สำหรับเก็บคะแนนของผู้เล่นโดยชื่อเป็น Key ของ Dictionary ในการเข้าถึงข้อมูลนั้นจะใช้ Key ของมัน ในส่วนแรกเป็นการเข้าถึงข้อมูลภายใน Dictionary เพื่อแสดงผลคะแนนของแต่ละ Key ออกมาทางหน้าจอ ต่อมาเป็นการอัพเดทข้อมูลใน Dictionary โดยเราได้เพิ่มค่าให้กับ Key  `'james'`  ขึ้นไปอีก 1000 และกำหนดค่าให้กับ Key  `'thomas'`  เป็น 100 และแสดงผลอีกครั้ง

```py
james => 1828
thomas => 3628
danny => 9310
bobby => 4401
james => 2828
thomas => 100

```

นี่เป็นผลลัพธ์การทำงานของโปรแกรม ในการเข้าถึงข้อมูลภายใน Dictionary เพื่ออ่านค่าและอัพเดทข้อมูล

ในการเข้าถึงข้อมูลภายใน Dictionary นั้น คุณต้องตรวจสอบให้แน่ใจว่า Key นั้นมีอยู่จริง ไม่เช่นนั้นโปรแกรมจะเกิดข้อผิดพลาดขึ้น ยกตัวอย่างเช่น

```py
scores = {'james': 1828, 'thomas': 3628, 'danny': 9310, 'bobby': 4401}
print(scores['smith']) # Error

# check if key smith exist
if 'smith' in scores.keys():
    print(scores['smith'])

```

ในตัวอย่างข้างบน โปรแกรมจะเกิดความผิดพลาดขึ้นเพราะเราได้เข้าถึง Key  `'smith'`  ซึ่งไม่มีอยู่ใน  `scores`  อย่าไรก็ตาม เราสามารถตรวจว่า Key มีอยู่หรือไม่ได้โดยการใช้คำสั่ง  `in`  เพื่อตรวจสอบจาก Key ในเมธอด  `keys()`  ของ Dictionary

## การอ่านค่าใน Dictionary ด้วยคำสั่ง For loop

คำสั่ง For loop นั้นเป็นคำสั่งที่ยืดหยุ่นและสามารถใช้งานได้อย่างหลากหลาย ในการอ่านค่าใน Dictionary นั้นเราสามารถใช้ For loop เพื่อวนอ่านค่าทั้ง Key และ Values ใน Dictionary ได้ มาดูตัวอย่างของโปรแกรม

```
countries = {'de': 'Germany', 'ua': 'Ukraine',
             'th': 'Thailand', 'nl': 'Netherlands'}

for k, v in countries.items():
    print(k, v)

# iterate through keys
print('Key:', end = ' ')
for k in countries.keys():
    print(k, end = ' ')

# iterate through values
print('\nValue:', end = ' ')
for v in countries.values():
    print(v, end = ' ')

```

ในตัวอย่าง เป็นการใช้งานคำสั่ง For loop วนอ่านค่าใน Dictionary ซึ่งมี 3 loop ด้วยกัน ในลูปแรกเป็นการอ่านค่าแบบ Key และ Value ในแต่ละรอบของการทำงานเราเอาข้อมูลใน Dictionary ด้วยเมธอด  `items()`  ซึ่งจะส่งค่ากลับเป็น Key และ Value กับมาและโหลดใส่ในตัวแปร  `k`  และ  `v`  ตามลำดับ

ในลูปที่สอง เป็นการวนอ่าน Key ทั้งหมดภายใน Dictionary โดยเมธอด  `keys()`  จะส่งค่ากลับเป็น List ของ Key ทั้งหมดและโหลดใส่ในตัวแปร  `k`  แต่ละรอบของลูป และในลูปสุดท้ายนั้นเป็นการอ่าน Value ทั้งหมด และเมธอด  `values()`  เพื่อรับค่าของ Value ทั้งหมดมาและใส่ในตัวแปร  `v`  ในแต่ละรอบของลูป

```
de Germany
ua Ukraine
th Thailand
nl Netherlands
Key: de ua th nl 
Value: Germany Ukraine Thailand Netherlands

```

นี่เป็นผลลัพธ์การทำงานของโปรแกรม ในการใช้คำสั่ง For loop เพื่ออ่านข้อมูลใน Dictionary ในภาษา Python

## Python Dictionary methods

เช่นเดียวกับข้อมูลประเภทอื่นๆ Dictionary มีเมธอดที่ให้คุณสามารถทำงานกับมันได้ง่ายขึ้น โดยส่วนมากแล้วมักจะเป็นเมธอดในการอัพเดทและรับค่าข้อมูลภายใน Dictionary ต่อไปมาดูตัวอย่างการใช้งานเมธอดของ Dictionary ในภาษา Python

```
countries = {'de': 'Germany', 'ua': 'Ukraine',
             'th': 'Thailand', 'nl': 'Netherlands'}

print(countries.keys())
print(countries.values())

print(countries.get('de')) # equal to countries['de']
countries.setdefault('tr', 'Turkey')

print(countries.popitem())
print(countries.popitem())

print(countries.items())

```

ในตัวอย่าง เป็นโปรแกรมในการใช้งานเมธอดของ Dictionary ตัวแปรของเรา  `countries`  มาจากตัวอย่างก่อนหน้าที่มี Key เป็นชื่อย่อของประเทศและ Value เป็นชื่อเต็มของประเทศ เมธอด  `keys()`  ส่งค่ากลับเป็น List ของ Key ทั้งหมดภายใน Dictionary และเมธอด  `values()`  นั้นจะส่งเป็น List ของ Value

หลังจากนั้นเป็นการเข้าถึงข้อมูลด้วยเมธอด  `get()`  โดยมี Key เป็นอาร์กิวเมนต์ซึ่งผลลัพธ์การทำงานของมันจะเหมือนกับการเข้าถึงข้อมูลโดยตรง เช่น  `countries['de']`  และเมธอด  `setdefault()`  ใช้รับค่าจากคีย์ที่กำหนด ถ้าไม่มีจะเป็นการเพิ่มค่าดังกล่าวเข้าไปใน Dictionary และต่อมาเมธอด  `popitem()`  จะนำสมาชิกตัวสุดท้ายออกจาก Dictionary และส่งค่าดังกล่าวกลับมาเป็น Tuple ออบเจ็ค ส่วนเมธอด  `items()`  นั้นจะค่ากลับมาเป็น List ของ Tuple ของออบเจ็คของ Key และ Value ทั้งหมด

```
dict_keys(['de', 'ua', 'th', 'nl'])
dict_values(['Germany', 'Ukraine', 'Thailand', 'Netherlands'])
Germany
('tr', 'Turkey')
('nl', 'Netherlands')
dict_items([('de', 'Germany'), ('ua', 'Ukraine'), ('th', 'Thailand')])

```

นี่เป็นผลลัพธ์การทำงานของโปรแกรม ในการใช้เมธอดใน Dictionary ในภาษา Python และจากในตัวอย่างนั้นเป็นเพียงส่วนหนึ่งของเมธอดที่มีเท่านั้น สำหรับเมธอดทั้งหมดใน Dictionary นั้นแสดงดังตารางข้างล่างนี้


| Methods |Description |
|----------|----------|
| clear() |ลบข้อมูลทั้งหมดภายใน Dictionary |
| copy() |คัดลอก Dictionary ทั้งหมดไปยังอันใหม่ |
| get(key[, default]) |ส่งค่าข้อมูลใน Dictionary จาก Key ที่กำหนด ถ้าหากไม่มี Key อยู่และไม่ได้กำหนด default จะทำให้เกิดข้อผิดพลาด KeyError |
| items() |ส่งค่ากลับเป็นออบเจ็คของ Key และ Value |
| keys() |ส่งค่ากลับเป็น List ของ Key ทั้งหมดใน Dictionary |
| pop(key[, default]) |ส่งค่ากลับเป็นค่าสุดท้ายใน Dictionary |
| popitem() |ส่งค่ากลับเป็น Tuple ออบเจ็คของ Key และ Value |
| setdefault(key[, default]) |ส่งค่ากลับเป็นค่าของ Key ที่กำหนด ถ้าหากไม่มี Key อยู่ใส่ข้อมูลเข้าไปใน Dictionary |
| update([other]) |อัพเดท Dictionary กับคู่ของ Key และ Value จากออบเจ็คอื่น และเขียนทับ Key ที่มีอยู่ |
| values() |ส่งค่ากลับเป็น List ของ Value ทั้งหมดใน Dictionary |
## Python Dictionary functions

ฟังก์ชันที่เป็นพื้นฐานและสามารถใช้ได้กับโครงสร้างข้อมูลทุกประเภทคือฟังก์ชัน  `len()`  เป็นฟังก์ชันที่ใช้สำหรับนับจำนวนสมาชิกของเจ็ค และ Dictionary ยังมีฟังก์ชัน  `iter()`  ที่ทำงานเหมือนกับเมธอด  `items()`  นี่เป็นตารางของฟังก์ชันที่สามารถใช้ได้กับ Dictionary

|Function|Description|
|--------|----------|
|len(dict)|ส่งค่ากลับเป็นจำนวนของออบเจ็คใน Dictionary|
iter(dict)|ส่งค่ากลับเป็นออบเจ็คของ Key และ Value|

คุณสามารถใช้คำสั่ง  `del`  เพื่อลบข้อมูลภายใน Dictionary ได้ เช่น คำสั่ง  `del countries['de']`  เพื่อลบสมาชิกที่มี Key ที่กำหนดออกไป และคำสั่ง  `del countries`  นั้นเป็นการลบทั้งตัวแปร

ในบทนี้ คุณได้เรียนรู้เกี่ยวกับ Dictionary ในภาษา Python คุณได้ทราบวิธีการสร้างและใช้งาน Dictionary และสถานการณ์ที่เหมาะสมที่จะใช้ข้อมูลประเภทนี้ เราได้แสดงให้เห็นถึงการเข้าถึงข้อมูลภายใน Dictionary แบบพื้นฐานและด้วยการใช้คำสั่งวนซ้ำ For loop รวมถึงการใช้งานเมธอดและฟังก์ชันสำหรับจัดการ Dictionary

Reference :  [http://marcuscode.com/lang/python/dictionary](http://marcuscode.com/lang/python/dictionary)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxOTIwNDM1NywtMTM2MDI5NzU0NiwtND
M3ODQzMTEyXX0=
-->