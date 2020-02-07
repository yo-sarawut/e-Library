
การจัดการวันเวลาใน python ด้วย datetime
===
>เขียนเมื่อ 2016/06/21 19:35

มอดูล datetime เป็นหนึ่งในมอดูลภายในตัวของไพธอน มีหน้าที่จัดการเกี่ยวกับเรื่องวันเดือนปีและเวลาต่างๆ  หน้าที่มีความคล้ายคลึงกับมอดูล time (อ่านรายละเอียดใน  [https://phyblas.hinaboshi.com/20160610](https://phyblas.hinaboshi.com/20160610)) แต่ก็มีความต่างกันอยู่ บางครั้งก็อาจใช้ร่วมกัน  datetime มักถูกใช้เมื่อต้องการจัดการกับข้อมูลที่อยู่ในรูปของวันเดือนปีหรือเวลาชั่วโมงนาทีวินาที  เวลาและวันเดือนปีนั้นเป็นปริมาณที่ใช้หน่วยหลากหลายในการอธิบาย และการแปลงหน่วยก็มีความยุ่งยากเพราะมีความไม่สม่ำเสมอ เช่นจำนวนวันในหนึ่งปีหรือหนึ่งเดือนเป็นต้น  
  
การใช้ออบเจ็กต์พิเศษของ datetime จะทำให้การคำนวณทำได้โดยง่ายขึ้น อีกทั้งยังสามารถปรับเปลี่ยนรูปแบบการแสดงผลให้เป็นไปตามที่ต้องการได้ง่ายด้วย  การใช้มอดูลนี้ก่อนอื่นต้องเริ่มจากทำการ import เรียกใช้ก่อน  
```py
import  datetime
```
  
  
  
**ออบเจ็กต์พิเศษใน datetime**  
มอดูล datetime นั้นมีการนิยามคลาสของออบเจ็กต์สำหรับเก็บค่าวันเดือนปีและเวลาโดยเฉพาะ มีอยู่ ๔ ชนิดคือ

- `datetime.date`	ออบเจ็กต์เก็บค่าวันเดือนปี
- `datetime.time`	ออบเจ็กต์เก็บค่าเวลา
- `datetime.datetime`	เป็นออบเจ็กต์ที่เอา datetime.date กับ datetime.time มารวมกัน เก็บค่าทั้งวันเดือนปีและเวลา
- `datetime.timedelta`	ออบเจ็กต์เก็บค่าระยะห่างระหว่างเวลาซึ่งมีหน่วยเป็นวันและวินาที

  
`datetime.date` จะเก็บค่าตัวเลขปี เดือน วัน ทั้งหมดเป็นจำนวนเต็มเอาไว้ ในการสร้าง `datetime.date` จะต้องใส่ค่าปี, เดือน, วัน ตามลำดับ เช่น
```py
datetime.date(1905, 6, 1)
```
  
เมื่อใช้คำสั่ง print จะแสดงผลเป็น  _ปี-เดือน-วัน_
```py
print(datetime.date(1905, 6, 1))  # ได้ 1905-06-01
```
  
ค่าเดือนจะใส่ได้แค่ 1 ถึง 12 และค่าวันจะใส่ได้แค่ไหนขึ้นอยู่กับจำนวนวันในเดือนนั้น และทั้งหมดต้องเป็นจำนวนเต็มเท่านั้น จะมีทศนิยมไม่ได้ ถ้าใส่ค่าที่ไม่อยู่ในขอบเขตที่กำหนดจะเกิดข้อผิดพลาดทันที เช่น
```py
datetime.date(1911,2,29)  # ได้ ValueError: day is out of range for month  
datetime.date(1911,0,28)  # ได้ ValueError: month must be in 1..12  
datetime.date(1911,2,27.1)  # ได้ TypeError: integer argument expected, got float
```
  
ส่วน `datetime.time`จะเก็บค่าเวลาในหน่วยชั่วโมง, นาที, วินาที และไมโครวินาที การสร้าง `datetime.time` จะต้องใส่ค่า ชั่วโมง, นาที, วินาที และไมโครวินาที เรียงตามลำดับ โดยจะใส่แต่ค่าชั่วโมงอย่างเดียวก็ได้ ค่าที่เหลือจะเป็น 0 เช่น

`datetime.time(1)`  # คือ 1 ชั่วโมง 0 นาที 0 วินาที 0 ไมโครวินาที  
`datetime.time(23, 59, 59, 999999)`  # คือ 23 ชั่วโมง 59 นาที 59 วินาที 999999 ไมโครวินาที

  
เมื่อสั่ง print จะแสดงผลเป็น  _ชั่วโมง:นาที:วินาที.ไมโครวินาที_
```py
print(datetime.time(23, 59, 59, 999999))  
# ได้ 23:59:59.999999
```
  
ค่าชั่วโมงจะต้องอยู่ในช่วง 0 ถึง 23 นาทีและวินาทีเป็น 0 ถึง 60 ส่วนไมโครวินาทีตั้งแต่ 0 ถึง 999999 ค่าทั้งหมดต้องเป็นจำนวนเต็มเท่านั้น  
  
ส่วนออบเจ็กต์ชนิด datetime.datetime นั้นเป็นตัวที่รวม datetime.date กับ datetime.time เข้าด้วยกัน คือจะเก็บค่า ปี, เดือน, วัน, ชั่วโมง, นาที, วินาที, ไมโครวินาที  
  
เวลาที่สร้าง `datetime.datetime` ขึ้นมาก็ใส่ค่าเรียงไล่ตั้งแต่ปีไปจนถึงไมโครวินาที โดยอาจใส่แค่ปีเดือนวัน ๓ ตัวเท่านั้นส่วนที่เหลือละไว้ก็ได้ เช่น
```py
datetime.datetime(2016,6,21)  
# 21 มิ.ย. 2016 เวลา 0:00:00:000000 น.
```
  
เมื่อสั่ง print จะแสดงผลเป็น  _ปี-เดือน-วัน ชั่วโมง:นาที:วินาที.ไมโครวินาที_
```py
print(datetime.datetime(2016,6,21,17,35,30,115421))  
# ได้ 2016-06-21 17:35:30.115421
```
  
ส่วน datetime.timedelta นั้นจะเก็บค่าช่วงระยะเวลา โดยเก็บในรูปของวัน, วินาที และ ไมโครวินาทีเท่านั้น โดย 1 วันมีค่าเท่ากับ 60*60*24 = 86400 วินาที  
  
การสร้าง datetime.timedelta นั้นต้องใส่ค่าเป็น วัน, วินาที และไมโครวินาที ตามลำดับ โดยสามารถละตัวหลังแล้วใส่แต่ตัวแรกๆก็ได้ เช่น
```py
datetime.timedelta(1, 60)  
# คือ 1 วัน 60 วินาที (1 นาที)
```
  
ค่าวันและวินาทีจะเป็นทศนิยมก็ได้ ถ้าใส่เป็นทศนิยมค่าจะถูกแปลงไปเป็นตัวหลังแทน เช่น
```py
datetime.timedelta(1.1)  
# กลายเป็น datetime.timedelta(1, 8640)  
datetime.timedelta(1.1111111111)  
# กลายเป็น datetime.timedelta(1, 9599, 999999)
```
  
ในทางกลับกันหากใส่ค่าวินาทีเกิน 86400 ก็จะถูกแปลงเป็นวัน และหากใส่ไมโครวินาทีเกิน 1 ล้านก็จะถูกแปลงเป็นวินาที  
  
ค่าที่ใส่จะติดลบก็ได้ ถ้าหากวินาทีหรือไมโครวินาทีติดลบจะถูกนำไปหักจากวันและวินาทีตามลำดับ เช่น
```py
datetime.timedelta(1,-1,-1)  
# กลายเป็น datetime.timedelta(0, 86398, 999999)
```
  
เรายังอาจสร้าง `datetime.timedelta` โดยกำหนดระยะเวลาเป็นมิลลิวินาที, นาที, ชั่วโมง, หรือสัปดาห์ได้ด้วย โดยใส่ในรูปคีย์เวิร์ด เวลาจะถูกแปลงเป็นหน่วยวัน, วินาที และไมโครวินาทีโดยอัตโนมัติ
```py
datetime.timedelta(weeks=1,hours=17,minutes=2,milliseconds=999)  
# ได้ datetime.timedelta(7, 61320, 999000)
```
  
เมื่อสั่ง print จะอยู่ในรูปของ  _วัน days, ชั่วโมง:นาที:วินาที.ไมโครวินาที_
```py
print(datetime.timedelta(111.9999999))  
# ได้ 111 days, 23:59:59.991360
```
  
  
  
**การคำนวณของ datetime.datetime และ datetime.timedelta**  
เมื่อนำ datetime.datetime มาลบกันจะได้ผลออกมาเป็น datetime.timedelta ซึ่งเก็บค่าระยะเวลาระหว่างสองเวลาที่เอามาลบกันนั้น เช่น
```py
datetime.datetime(2016,6,21)-datetime.datetime(2016,6,20)  
# ได้ datetime.timedelta(1)
```
  
เนื่องจากหน่วยที่เก็บใน datetime.timedelta นั้นใหญ่สุดเป็นวัน และรองลงมาเป็นวินาที ดังนั้นหน่วยอื่นก็จะถูกแปลงเป็นวันและวินาทีหมด
```py
datetime.datetime(2016,6,21,7)-datetime.datetime(2016,6,21,3)  
# ได้ datetime.timedelta(0, 14400)  
datetime.datetime(2016,6,21)-datetime.datetime(1905,6,21)  
# ได้ datetime.timedelta(40543)
```
  
นอกจากการลบกันแล้ว datetime.datetime และ datetime.datetime ด้วยกันไม่สามารถนำมาคำนวณอย่างอื่นได้เลย ทั้งบวก, คูณ, และยกกำลัง  
  
แต่ datetime.datetime สามารถนำมาบวกหรือลบกับ datetime.timedelta ได้ ซึ่งก็จะได้ผลเป็น datetime.datetime ตัวใหม่ เช่น
```py
datetime.datetime(2016,6,21)+datetime.timedelta(0.71)  # ได้ datetime.datetime(2016, 6, 21, 17, 2, 24)  
datetime.datetime(2016,6,21)-datetime.timedelta(1,1,1)  # ได้ datetime.datetime(2016, 6, 19, 23, 59, 58, 999999)
```
  
ส่วน datetime.timedelta นั้นสามารถเอามาคูณหรือหารกับตัวเลขได้ แต่ไม่สามารถบวกหรือลบหรือยกกำลังได้
```py
datetime.timedelta(1,1,1)*2 
# ได้ datetime.timedelta(2, 2, 2)  
datetime.timedelta(1,1,1)/2  
# ได้ datetime.timedelta(0, 43200, 500000)
```
  
datetime.timedelta กับ datetime.timedelta สามารถนำมาบวกหรือลบกันได้ แต่ไม่สามารถคูณหรือยกกำลังกันได้
```py
datetime.timedelta(1,1)+datetime.timedelta(0,0,111)  
# ได้ datetime.timedelta(1, 1, 111)  
datetime.timedelta(1,1,1)-datetime.timedelta(1,1,1)  
# ได้ datetime.timedelta(0)
```
  
และสามารถหารกันได้ ผลที่ได้คือค่าจำนวนเท่าของระยะเวลา
```py
datetime.timedelta(1,1,1)/datetime.timedelta(1)  
# ได้ 1.0000115740856481
```
  
และสามารถหารเอาเศษได้
```py
datetime.timedelta(7,1,1)%datetime.timedelta(1)  
# ได้ datetime.timedelta(0, 1, 1)  
datetime.timedelta(7,2,1)%datetime.timedelta(0,0,999999)  
# ได้ datetime.timedelta(0, 0, 604803)
```
  
สำหรับการเปรียบเทียบระหว่างเวลานั้น datetime.datetime นึงจะมากกว่าอีก datetime.datetime หนึ่งเมื่อเป็นเวลาช้ากว่า ส่วน datetime.timedelta ก็เทียบตามความยาวของเวลา
```py
datetime.datetime(2016,6,21)>datetime.datetime(2016,6,20)  
# ได้ True
```
  
  
**แอตทริบิวต์และเมธอดของ datetime.timedelta**  
ค่าของวัน, วินาที และไมโครวินาที ถูกเก็บอยู่ในแอตทริบิวต์ days, seconds และ microseconds ตามลำดับ  
  
สามารถแสดงค่าทั้งหมดเป็นวินาทีได้ด้วยเมธอด total_seconds()  
  
ตัวอย่าง
```py
tdt = datetime.timedelta(3,70000,400000)  
print(tdt.days)  # ได้ 3  
print(tdt.seconds)  # ได้ 70000  
print(tdt.microseconds)  # ได้ 400000  
print(tdt.total_seconds())  # ได้ 329200.4
```
  
  
  
**แอตทริบิวต์และเมธอดของ datetime.datetime**  
ภายในออบเจ็กต์ datetime.datetime นั้นเก็บข้อมูลของปี, เดือน, วัน, ชั่วโมง, นาที, วินาที, ไมโครวินาที เอาไว้โดยสามารถดูค่าแต่ละค่าได้ที่แอตทริบิวต์ year, month, day, hour, minute, second, microsecond
```py
dtdt = datetime.datetime(2016,6,21,17,35,30,115421)  
print(dtdt.year)  # ได้ 2016  
print(dtdt.month)  # ได้ 6  
print(dtdt.day)  # ได้ 21  
print(dtdt.hour)  # ได้ 17  
print(dtdt.minute)  # ได้ 35  
print(dtdt.second)  # ได้ 30  
print(dtdt.microsecond)  # ได้ 115421
```
  
datetime.datetime ยังประกอบด้วยเมธอดต่างๆที่ใช้แสดงผลข้อมูลส่วนต่างๆในรูปแบบต่างๆ ได้แก่
```py
date()	แสดงส่วนวันเดือนปีในรูป datetime.date
time()	แสดงส่วนเวลาในรูป datetime.time
weekday()	แสดงเลขวันในสัปดาห์ โดยวันจันทร์เป็น 0 วันอาทิตย์เป็น 6
isoweekday()	แสดงเลขวันในสัปดาห์ โดยวันจันทร์เป็น 1 วันอาทิตย์เป็น 7
isocalendar()	แสดงผลวันเดือนปีในรูปแบบทูเพิล
ctime()	แสดงวันเวลาในรูป  _วันในสัปดาห์ เดือน วัน ชั่วโมง:นาที:วินาที ปี_
timetuple()	แสดงวันเวลาในรูปออบเจ็กต์ time.struct_time
timestamp()	แสดงเวลาในรูปของจำนวนวินาทีนับจากเที่ยงคืนเวลา UTC ของวันที่ 1 ม.ค. 1970
isoformat()	แสดงวันเวลาในรูป  _ปี-เดือน-วันTชั่วโมง:นาที:วินาที.ไมโครวินาที_
```
  
สำหรับ isoformat ถ้าใส่อาร์กิวเมนต์ลงไปจะเป็นตัวคั่นระหว่างวันกับชั่วโมงแทนตัว T  
  
ตัวอย่างเมธอดต่างๆ
```py
dtdt = datetime.datetime(2016,6,21,17,35,30,115421)  
print(dtdt.date())  # ได้ 2016-06-21  
print(dtdt.time())  # ได้ 17:35:30.115421  
print(dtdt.weekday())  # ได้ 1  
print(dtdt.isoweekday())  # ได้ 2  
print(dtdt.isocalendar())  # ได้ (2016, 25, 2)  
print(dtdt.ctime())  # ได้ Tue Jun 21 17:35:30 2016  
print(dtdt.timetuple())  # ได้ time.struct_time(tm_year=2016, tm_mon=6, tm_mday=21, tm_hour=17, tm_min=35, tm_sec=30, tm_wday=1, tm_yday=173, tm_isdst=-1)  
print(dtdt.isoformat())  # ได้ 2016-06-21T17:35:30.115421  
print(dtdt.isoformat(' '))  # ได้ 2016-06-21 17:35:30.115421
```
  
สำหรับ timestamp() ค่าจะเป็น 0 ที่เวลา 7 โมงเช้าของวันที่ 1 ม.ค. 1970 เนื่องจากไทยอยู่เขตเวลา +7
```py
print(dtdt.timestamp())  
# ได้ 1466505330.115421  
print(datetime.datetime(1970,1,1,0,0,0).timestamp())  
# ได้ -25200.0  
print(datetime.datetime(1970,1,1,7,0,0).timestamp())  
# ได้ 0.0

```
  
  
**การแก้ค่าวันเวลาใน datetime.datetime**  
ใน datetime.datetime มีเมธอด replace ซึ่งใช้แก้ไขค่าต่างๆภายใน datetime.datetime โดยอาร์กิวเมนต์ที่ต้องใส่นั้นเหมือนกับตอนสร้าง datetime.datetime เพียงแต่ว่าจะใส่แค่บางค่าในรูปคีย์เวิร์ดเฉพาะค่าที่ต้องการแก้เท่านั้น  
  
เพียงแต่ว่าเมธอดนี้ไม่ได้ทำการเปลี่ยนแปลงตัว datetime.datetime แค่คืนค่าของ datetime.datetime ที่ถูกแก้แล้วกลับมาเท่านั้น  
  
ตัวอย่าง
```py
dtdt = datetime.datetime(2016,6,21,17,35,30,115421)  
dtdt.replace(2015)  
# ได้ datetime.datetime(2015, 6, 21, 17, 35, 30, 115421)  
dtdt.replace(month=7)  
# ได้ datetime.datetime(2016, 7, 21, 17, 35, 30, 115421)  
dtdt.replace(second=0,microsecond=0)  
# ได้ datetime.datetime(2016, 6, 21, 17, 35)
```
  
  
  
**การแสดงผลวันเวลาตามที่ต้องการ**  
นอกจาก การแสดงผล datetime.datetime ด้วยเมธอดตามที่กล่าวมาข้างต้น เราสามารถให้แสดงผลวันเวลาในรูปแบบตามที่ต้องการซึ่งกำหนดเองได้โดยใช้เมธอด strftime  
  
อาร์กิวเมนต์ที่ต้องใส่คือสายอักขระที่ประกอบไปด้วย % ตามด้วยอักษร ซึ่งแทนค่าในส่วนต่างๆในรูปแบบต่างๆของวันเวลา ซึ่งสรุปได้ตามนี้
```py
%a	วันในสัปดาห์ในรูปย่อ
%A	วันในสัปดาห์เป็นชื่อเต็ม
%w	วันในสัปดาห์เป็นตัวเลข อาทิตย์เป็น 0 เสาร์เป็น 6	
%d	วันที่ในรูปเลขสองหลัก (เติม 0 เมื่อมีหลักเดียว)
%b	ชื่อเดือนในรูปย่อ
%B	ชื่อเดือนเป็นชื่อเต็ม
%m	เลขเดือนเป็นเลขสองหลัก (เติม 0 เมื่อมีหลักเดียว)
%y	เลขปีในรูปเลขสองหลักสุดท้าย
%Y	เลขปีในรูปเลขสี่หลัก (เติม 0 เมื่อมีไม่ถึงสี่หลัก)
%H	เวลาชั่วโมงเป็นเลขสองหลักถึง 24 (เติม 0 เมื่อมีหลักเดียว)
%I	เวลาชั่วโมงเป็นเลขสองหลักไม่เกิน 12 (เติม 0 เมื่อมีหลักเดียว)
%p	เวลา AM หรือ PM
%M	เวลานาทีเป็นเลขสองหลัก (เติม 0 เมื่อมีหลักเดียว)
%S	เวลาวินาทีเป็นเลขสองหลัก (เติม 0 เมื่อมีหลักเดียว)
%f	เวลาไมโครวินาทีเป็นเลขหกหลัก (เติม 0 เมื่อมีไม่ถึงหกหลัก)
%j	เลขลำดับวันในปี (1 ถึง 366)
%U	หรือ %W ลำดับของสัปดาห์ภายในปี
%c	แสดงวันเวลาในรูปแบบเดียวกับ ctime()
%x	เดือน/ปี/วัน
%X	ชั่วโมง:นาที:วินาที
```
  
ตัวอย่าง
```py
dtdt = datetime.datetime(2016,6,21,17,35,30,115421)  
print(dtdt.strftime('%a'))  # ได้ Tue  
print(dtdt.strftime('%A'))  # ได้ Tuesday  
print(dtdt.strftime('%w'))  # ได้ 2  
print(dtdt.strftime('%d'))  # ได้ 21  
print(dtdt.strftime('%b'))  # ได้ Jun  
print(dtdt.strftime('%B'))  # ได้ June  
print(dtdt.strftime('%m'))  # ได้ 06  
print(dtdt.strftime('%y'))  # ได้ 16  
print(dtdt.strftime('%Y'))  # ได้ 2016  
print(dtdt.strftime('%H'))  # ได้ 17  
print(dtdt.strftime('%I'))  # ได้ 05  
print(dtdt.strftime('%p'))  # ได้ PM  
print(dtdt.strftime('%M'))  # ได้ 35  
print(dtdt.strftime('%S'))  # ได้ 30  
print(dtdt.strftime('%f'))  # ได้ 115421  
print(dtdt.strftime('%j'))  # ได้ 173  
print(dtdt.strftime('%U'))  # ได้ 25  
print(dtdt.strftime('%W'))  # ได้ 25  
print(dtdt.strftime('%c'))  # ได้ Tue Jun 21 17:35:30 2016  
print(dtdt.strftime('%x'))  # ได้ 06/21/16  
print(dtdt.strftime('%X'))  # ได้ 17:35:30
```
  
  
  
**การสร้าง datetime.datetime จากเมธอดของคลาส**  
เราสามารถสร้าง datetime.datetime ขึ้นมาจากเมธอดของคลาส datetime.datetime เองได้ด้วย  
  
เมธอดเหล่านั้นได้แก่
```py
now()	สร้าง datetime.datetime ขึ้นจากเวลาขณะนี้
utcnow()	สร้าง datetime.datetime ขึ้นจากเวลาขณะนี้ในเขตเวลาสากล
fromtimestamp()	สร้าง datetime.datetime ขึ้นจาก timestamp โดยอิงเวลาท้องถิ่น
utcfromtimestamp()	สร้าง datetime.datetime ขึ้นจาก timestamp โดยอิงเวลาสากล
combine()	สร้าง datetime.datetime โดยใช้ datetime.date และ datetime.time มารวมกัน
strptime()	สร้าง datetime.datetime ขึ้นจากกระบวนการตรงข้ามกับ strftime
```
  
ตัวอย่าง
```py
print(datetime.datetime.now())  # ได้เวลาปัจจุบัน  
print(datetime.datetime.utcnow())  # ได้เวลาปัจจุบันลบ 7 ชั่วโมง  
print(datetime.datetime.fromtimestamp(0))  # ได้ 1970-01-01 07:00:00  
print(datetime.datetime.utcfromtimestamp(0))  # ได้ 1970-01-01 00:00:00  
dtd = datetime.date(2016,6,21)  
dtt = datetime.time(17,35,30,115421)  
print(datetime.datetime.combine(dtd,dtt))  # ได้ 2016-06-21 17:35:30.115421
```
  
เมธอด strptime นั้นเป็นกระบวนการที่ตรงกันข้ามกันกับ strftime ใช้แปลงสายอักขระที่มีรูปแบบตามที่กำหนดให้กลายเป็น datetime.datetime   ในการใช้ให้ใส่สายอักขระที่จะแปลง ตามด้วยสายอักขระที่เขียนรูปแบบที่กำหนดการแปลง  
  
ตัวอย่าง
```py
print(datetime.datetime.strptime('11:11:11.1111','%X.%f'))  
# ได้ 1900-01-01 11:11:11.111100  
print(datetime.datetime.strptime('02','%H'))  
# ได้ 1900-01-01 02:00:00  
print(datetime.datetime.strptime('7/6/1991','%d/%m/%Y'))  
# ได้ 1991-06-07 00:00:00  
r =  u'1842-11-5 เวลา 8 โมง 41 นาที 32 วินาที'  
fmt =  u'%Y-%m-%d เวลา %I โมง %M นาที %S วินาที'  
print(datetime.datetime.strptime(r,fmt))  
# ได้ 1842-11-05 08:41:32
```
  
  
**อ้างอิง**

[http://docs.python.jp/3/library/datetime.html](http://docs.python.jp/3/library/datetime.html)  
[http://nkmk.github.io/blog/python-datetime](http://nkmk.github.io/blog/python-datetime)

> [Source : ](https://phyblas.hinaboshi.com/20160621)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyNzMyNTY1NCwtNjM4MzUxNTA3XX0=
-->