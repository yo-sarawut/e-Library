การใช้งาน Virtualenv
===

### Virtualenv คืออะไร

Virtualenv(ironment) คือ environment ของ python เช่น คุณทำโปรแกรมอยู่ 2 ตัว A กับ B แล้วเวลาคุณจะติดตั้ง library ถ้าคุณ pip install ลงไปเลย

-   library ที่คุณใช้กับงาน A กับปนมั่วกับงาน B

เช่น เวลาจะทำไฟล์ requirement เพื่อให้คนอื่น สามารถติดตั้ง library ที่ใช้กับงานเราได้สะดวกมากขึ้นก็กลับกลายเป็นว่า งาน A ใช้ 5 library งาน B ใช้ 10 Libray สรุป คนที่เอาโปรแกรมเราไม่ไปใช้ก็ไม่รู้ว่า โปรแกรมเราใช้ library อะไรบ้างก็ต้องติดตั้งทั้งหมด 15 library

-   หรือแบบไม่สามารถแยก version ของ library กันได้

เช่น งาน A ใช้ OpenCV 3 แต่ งาน B ใช้ OpenCV 4 ทำไงให้ลง 2 version พร้อมกันได้ละ ก็ต้องให้เจ้า Virtualenv ช่วยเราไง

โดยเจ้า Virtualenv จะสร้าง environment ใหม่ขึ้นมา ที่มีแต่ตัว Python เปล่าๆ แล้วเวลาเราติดตั้ง library อะไรไปมันก็จะเก็บไว้ใน Folder ของ environment แต่ละตัวไม่มาปนกัน

ตอนนี้อาจจะ งง เดี๋ยวไปลองติดตั้งแล้วใช้งานจริงกันเลยดีกว่าครับ

  

### การติดตั้ง Virtualenv

เราจะติดตั้ง Virtualenv ผ่าน pip กันนะครับ โดยการพิมพ์ command

```shell
pip install virtualenv
```

  

### การใช้งาน Virtualenv

สมมติ ผมทำโปรเจค image_enhancement อยู่ผมก็จะเข้าไปใน folder โปรเจคของผม

ในทีนี้ผมจะสร้าง python environment ชื่อ env โดยสั่ง

```shell
virtualenv.exe env
```

  

เวลาจะใช้งานก็สั่ง command

```shell
.\env\Scripts\activate
```

  
[![pip 00](https://www.skconan.com/static/4532781f8248da2f308149f100b825e7/fb8a0/pip-00.png)](https://www.skconan.com/static/4532781f8248da2f308149f100b825e7/e1a0c/pip-00.png)  

### Note:

สำหรับใครที่ใช้ Virtualenv แล้วติดปัญหาเกี่ยวกับ execution policies แบบในรูปด้านล่าง

[![virtualenv error](https://www.skconan.com/static/83dcaa6797ca6992755add5f6e4baf32/fb8a0/virtualenv-error.png)](https://www.skconan.com/static/83dcaa6797ca6992755add5f6e4baf32/e1a0c/virtualenv-error.png)  

ก็ให้เปิด Powershell หรือ Command Prompt แบบ Admin แล้วสั่ง

```shell
Set-ExecutionPolicy AllSigned
```

  
กับ

```shell
Set-ExecutionPolicy RemoteSigned
```

โดยจะเลือกแบบ Yes หรือ Yes to All ก็ได้ ดูรายละเอียดได้จาก  [User Guid](https://virtualenv.pypa.io/en/stable/userguide/)  ของ virtualenv ครับ

กลับมาเข้าเรื่องของเราต่อครับ เมื่อเราสั่ง activate แล้วจะมีชื่อ environment ของเราอยู่หน้าบรรทัดของ powershell หรือ command

  

### การใช้งาน Virtualenv (ต่อ)

คราวนี้ถ้าเราอยากรู้ว่า environment ของเรามี library อะไรอยู่บ้างก็ให้ลองสั่ง

```py
pip freeze
```

  

ซึ่งเราจะยังไม่เห็น library ใดๆ คราวนนี้เรามาลองติดตั้ง library OpenCV กัน

```py
pip install opencv-python
```

  

แล้วลอง pip freeze อีกรอบ เราก็จะเห็นว่ามี library OpenCV เพิ่มเข้ามา

```py
numpy==1.16.3
opencv-python==4.1.0.25
```

  

ทีนี้ก็มาลองทดสอบ library ที่เพิ่งลงกันครับ

[![use cv2](https://www.skconan.com/static/98028e7c1d764ae8e4cb5f48fac51861/fb8a0/use-cv2.png)](https://www.skconan.com/static/98028e7c1d764ae8e4cb5f48fac51861/e1a0c/use-cv2.png)  

ถ้าเราใช้งาน environment เสร็จแล้ว ก็ให้สั่ง

```shell
deactivate
```

  

เพื่อออกจาก environment นั้น

  

### ประโยชน์ของ Virtualenv

สมมติ ว่าเราทำโปรเจคเสร็จ แล้วคนอื่นอยากนำไปใช้งานต่อ ให้เราสั่ง

```shell
pip freeze > requirement.txt
```

  

เพื่อจะรวบรวม library ไว้ในไฟล์ requirement.txt เราอาจจะใช้ชื่อไฟล์อื่นก็ได้นะครับ

[![pip freeze](https://www.skconan.com/static/1793746c981b2c1dc6cce89125108a35/fb8a0/pip-freeze.png)](https://www.skconan.com/static/1793746c981b2c1dc6cce89125108a35/cab54/pip-freeze.png)  

เวลาคนอื่นเอาไปใช้ เค้าก็จะสั่ง

```shell
pip install -r <file requirement>
```

  

เจ้า pip ก็จะลง library ทุกตัวให้อัตโนมัติ ของเพียงแค่ version ของ python เหมือนกัน เพราะ บางทีถ้าเรา freeze library จาก python 3.7 แล้วไปลงใน python 3.6 version ของ library บางตัวอาจจะไม่มีก็ได้ครับ

### สรุป



|Command|	Descriptions|
|-------|-----------------|
|virtualenv <env_name>|	สร้าง environment|
|<env_name>/Scripts/activate|	ใช้งาน environment
|deactivate	ออกจาก environtment
|pip install <library_name>	ติดตั้ง library
|pip freeze	แสดงรายชื่อ library
สัญลักษณ์ > <output_file>	เป็นการบอกให้เขียนใส่ <output_file>


Command

Descriptions

virtualenv <env_name>

สร้าง environment

<env_name>/Scripts/activate

ใช้งาน environment

deactivate

ออกจาก environtment

pip install <library_name>

ติดตั้ง library

pip freeze

แสดงรายชื่อ library

สัญลักษณ์ > <output_file>

เป็นการบอกให้เขียนใส่ <output_file>

[หากใครชอบเนื้อหาที่ผมเขียน สามารถร่วมกัน Donate เพื่อเป็นค่ากาแฟได้นะครับ ^^](https://www.skconan.com/donate)

  
ใครที่สงสัยจุดไหน หรือพบว่าจุดไหนที่ผมอธิบายผิด สามารถเข้ามาพูดคุยกันได้นะครับ inbox มาที่ Facebook, Twitter เลยก็ได้ครับ หรือ mail มาที่ supakit.kr@gmail.com จะยินดีมากเลยครับ

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUyODU3OTg2Ml19
-->