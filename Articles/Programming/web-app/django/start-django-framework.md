เริ่มพัฒนา Web Application กับภาษา Python ด้วย Django Framework
===

![enter image description here](https://miro.medium.com/max/896/1*4QDbb-eO98wIB32CNNuWjw.png)

ภาษา Python เริ่มถูกใช้งานอย่างแพร่หลายมากขึ้นเรื่อยๆ ในช่วงนี้เนื่องจากความง่ายในการเรียนรู้ และความสะดวกในการทดสอบโปรแกรม เนื่องจาก Python เป็นภาษาประเภท Script ซึ่งจะแตกต่างกับภาษาประเภท Java หรือ C ที่ต้อง compile code ให้ออกมาเป็น binary ก่อนนำไปรันได้จริง เช่น หากต้องการทดสอบ function substring ว่าจะสามารถตัดคำให้เราถูกต้องหรือไม่ กรณีใช้ภาษา Java หรือ C ก็ต้องเขียน class, main function หรืออื่นๆ อีกมากมายกว่าจะเริ่มทดสอบ function เล็กๆ นี้ได้ แต่ใน Python นั้น เพียงแค่เข้า Python console ก็สามารถทดสอบ function เหล่านี้ได้ทันที

[Django](https://www.djangoproject.com/)  (อ่านว่าจังโก้ หรือแจงโก้ โดยไม่ออกเสียงตัว D) เป็น framework ที่ใช้ในการสร้าง Web Application ในฝั่งของ Back End ที่พัฒนาด้วยภาษา Python โดยในตัว framework จะมีส่วนประกอบทุกอย่างที่จำเป็นตั้งแต่การเชื่อมต่อฐานข้อมูล ไปจนถึงการ render ข้อมูลออกมาให้ฝั่ง Front End แสดงผลข้อมูลเหล่านั้นได้ ซึ่ง framework ในรูปแบบนี้ในภาษาอื่นๆ เช่น  [Ruby on rails](http://rubyonrails.org/)  สำหรับภาษา Ruby,  [Play Framework](https://www.playframework.com/)  สำหรับภาษา Java หรือ Scala,  [Groovy on Grails](https://grails.org/)  สำหรับภาษา Groovy,  [Laravel](https://laravel.com/)  สำหรับภาษา PHP, หรือ  [Express](https://expressjs.com/) สำหรับภาษา Javascript ของ Node.js เป็นต้น ซึ่งข้อมูลที่อ้างอิงมาจาก  [www.hotframeworks.com](http://hotframeworks.com/)  จะเห็นว่า Django มีการใช้งานอย่างแพร่หลายมาก

![](https://miro.medium.com/max/30/1*dbCBacpdN_GShJIcmBoqyw.png?q=20)

![](https://miro.medium.com/max/1717/1*dbCBacpdN_GShJIcmBoqyw.png)

Web Frameworks Popularity Ranking อ้างอิงจาก  [www.hotframeworks](http://www.hotframeworks/).com

----------

บทความนี้จะเป็นการสอนพัฒนา Web Application ด้วย Django Framework โดยโปรแกรมตัวอย่างในที่นี้คือ โปรแกรมห้องสมุด ซึ่งโปรแกรมเราจะทำหน้าที่บันทึกหนังสือเข้าในห้องสมุดที่สร้างขึ้น ซึ่งเราจะใช้ Python version 3 และ Django version 1.11.5 ซึ่งเป็น version ล่าสุดขณะเขียนบทความนี้

**สารบัญ  
**[การติดตั้ง Python และ Django](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#9cb8)  
[สร้าง Django Project](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#2803)  
[สร้าง Django Application](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#ed29)  
[Django Template](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#6120)  
[การเชื่อมต่อฐานข้อมูล](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#0090)  
[Django Shell](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#de30)  
[Django admin site](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706#3106)

----------

# การติดตั้ง Python และ Django

1.  ติดตั้ง Python  
    - สำหรับ Windows สามารถ Download ได้จาก  [ที่นี่](https://www.python.org/downloads/)  ** สำคัญมากต้องติ๊กช่อง “Add python 3.X to PATH” ด้วย  
    - สำหรับ Linux version ใหม่ๆ จะมี python3 ติดตั้งมาให้ โดย default อยู่แล้ว  
    - สำหรับ Mac สามารถทำตาม  [Tutorial นี้](http://docs.python-guide.org/en/latest/starting/install3/osx/)  เพื่อติดตั้งได้  
    หลังจากติดตั้งแล้วบน Windows พิมพ์คำสั่ง $ py  
    บน Linux, Mac พิมพ์คำสั่ง $ python3  
    จะต้องได้หน้า python console ออกมาเหมือนในรูปด้านล่างนี้

![](https://miro.medium.com/max/30/1*7Rj5BCriqN-R9yHL0GpLJw.png?q=20)

![](https://miro.medium.com/max/1040/1*7Rj5BCriqN-R9yHL0GpLJw.png)

ตัวอย่าง Python3 console

2. ติดตั้ง pip3  
pip3 คือ package manager ที่ใช้สำหรับติดตั้ง package เสริมให้กับ Python3 (คล้ายๆ คำสั่ง apt-get บน linux) โดยเราจะใช้ pip ในการติดตั้ง Django ต่อไป  
- สำหรับ Windows คำสั่ง pip จะถูกติดตั้งมาอยู่แล้วบน python version 3.5 ขึ้นไป  
- สำหรับ Linux ติดตั้งด้วยคำสั่ง $ sudo apt-get install python3-pip  
- สำหรับ Mac ทำตาม Link ด้านบนเพื่อติดตั้ง pip3  
เมื่อติดตั้งเสร็จสิ้นทดสอบด้วยการพิมพ์คำสั่ง $ pip3 ใน console

3. ติดตั้ง Django  
พิมพ์คำสั่ง $ pip3 install django==1.11.5  
แล้ว pip3 จะ download django เข้ามาติดตั้งในเครื่องให้โดยอัตโนมัติ

![](https://miro.medium.com/max/30/1*wChDOkON0eudIqPdBQ6rMA.png?q=20)

![](https://miro.medium.com/max/802/1*wChDOkON0eudIqPdBQ6rMA.png)

ตัวอย่างการติดตั้ง Django

4. ตรวจสอบการติดตั้ง โดยพิมพ์คำสั่ง $ django-admin ตามรูปด้านล่าง

![](https://miro.medium.com/max/30/1*AQN9l6v7KgvP_61mE83i1Q.png?q=20)

![](https://miro.medium.com/max/593/1*AQN9l6v7KgvP_61mE83i1Q.png)

ตัวอย่างการเรียกคำสั่ง django-admin เพื่อแสดง Django version ที่ติดตั้ง

NOTE: สำหรับ Linux user อาจเจอ Error

> The program ‘django-admin’ is currently not installed. You can install it by typing:
> 
> sudo apt install python-django-common

ซึ่งหมายความว่าคำสั่ง django-admin ยังไม่ได้อยู่ใน PATH environment variable ให้ค้นหา Path ของ django-admin ด้วยคำสั่ง $ find / -name django-admin.py  
ซึ่งโดยปกติแล้ว path จะอยู่ที่ /home/<user>/.local/bin/django-admin.py เช่น

![](https://miro.medium.com/max/30/1*tX6_CTF10J7o4lf_2CZ3eg.png?q=20)

![](https://miro.medium.com/max/953/1*tX6_CTF10J7o4lf_2CZ3eg.png)

ตัวอย่างการเรียกคำสั่ง django-admin บน Linux

----------

# สร้าง Django Project

Browse ไปยัง Folder ที่ต้องการเก็บ project จากนั้น เริ่มสร้าง project ชื่อ “my_library” (ห้องสมุดของฉัน) ด้วยคำสั่ง

> $ django-admin startproject my_library

จะทำให้ได้โฟลเดอร์ my_library ซึ่งด้านในจะเก็บไฟล์ project ของ Django ดังนี้

![](https://miro.medium.com/max/30/1*IKPrTzaqWj_vg3jXVwYtzQ.png?q=20)

![](https://miro.medium.com/max/421/1*IKPrTzaqWj_vg3jXVwYtzQ.png)

โครงสร้างโฟลเดอร์ของ Django Project

1.  manage.py คือไฟล์ script สำหรับรันคำสั่งต่างๆ ที่เกี่ยวข้องกับ Django โดยปกติไฟล์นี้จะไม่ถูกแก้ไขใด ๆ ทั้งสิ้น
2.  __init__.py คือไฟล์ว่างๆ (ลองเปิดด้วย text editor ดูได้นะครับ) ไฟล์นี้มีไว้เพื่อให้ภาษา Python รู้ว่าโฟลเดอร์ที่อยู่นี้เป็นโฟลเดอร์ที่ใช้เก็บ Python Package โดยปกติไฟล์นี้จะถูกปล่อยเป็นไฟล์ว่าง ๆ ไว้แต่เราสามารถใส่ Python script เข้าไปได้เช่นกันแต่จะไม่ขอพูดถึงรายละเอียดในส่วนนี้ในบทความนี้ โดยรายละเอียดเพิ่มเติมของไฟล์นี้สามารถศึกษาได้จาก  [ที่นี่](https://docs.python.org/3/tutorial/modules.html#packages)
3.  settings.py คือไฟล์ที่ใช้เก็บ configuration ทั้งหมดของ project เอาไว้ เช่น การตั้งค่า Database, Timezone, Logging เป็นต้น ซึ่งค่าที่เก็บในนี้จะอยู่ในรูปแบบ key — value ซึ่งไฟล์นี้จะเป็นไฟล์แรกที่ Django เข้ามาอ่านเมื่อเริ่มการทำงานของ web server
4.  urls.py คือไฟล์ที่ใช้เก็บการ routing ของ HTTP request ซึ่งจะกล่าวถึงในหัวข้อถัดไป
5.  wsgi.py คือไฟล์ที่ใช้เก็บข้อมูลของ Django project ของเรา ใช้สำหรับการ deploy project เมื่อต้องการเชื่อมต่อกับ Web Server สำหรับรายละเอียดการ deploy สามารถอ่านเพิ่มเติมได้  [ที่นี่](https://docs.djangoproject.com/en/1.11/howto/deployment/wsgi/)  หรือ  [ที่นี่](http://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html)

ทดลองรัน Django Project ที่ port 8000 ด้วยคำส่ัง

> $ py manage.py runserver 0.0.0.0:8000

หรือ สำหรับ Linux ให้รันคำสั่ง

> $ python3 manage.py runserver 0.0.0.0:8000

![](https://miro.medium.com/max/30/1*e1t07l5xxsUfWhKhUZMSqQ.png?q=20)

![](https://miro.medium.com/max/1396/1*e1t07l5xxsUfWhKhUZMSqQ.png)

ตัวอย่างการรัน Django project ครั้งแรก

ซึ่งคำสั่งที่ใช้จะแบ่งเป็น

![](https://miro.medium.com/max/30/1*HKnHpxit1dLDAK7eIJULpg.png?q=20)

![](https://miro.medium.com/max/551/1*HKnHpxit1dLDAK7eIJULpg.png)

คำสั่งที่ใช้สั่งรัน Django Project

1.  py manage.py คือการสั่งรัน Python script ในไฟล์ manage.py ซึ่งเป็นคำสั่งเริ่มต้นในการรัน Django command ทุกคำสั่ง
2.  runserver คือ parameter เพื่อบอกว่าต้องการ start web server ขึ้นมา
3.  0.0.0.0:8000 คือ parameter ของ web server ที่เราจะสร้างขึ้นมา โดย 0.0.0.0 หมายถึงให้ web server ของเรา bind กับทุก ๆ IP ในเครื่องของเรา และ 8000 คือ port ที่ต้องการรัน

หลังจากรัน Django project สำเร็จ สามารถทดลองใช้ web browser เปิดเข้าหน้าเวปของเราได้ที่  [http://localhost:8000](http://localhost:8000/)  จะได้ผลลัพธ์ตามภาพด้านล่าง

![](https://miro.medium.com/max/30/1*HigMIXl3S8KXCf_PbQTsGQ.png?q=20)

![](https://miro.medium.com/max/1265/1*HigMIXl3S8KXCf_PbQTsGQ.png)

หน้า web ที่เห็นหลังจากสร้าง Django project และรันสำเร็จ

การรันคำสั่ง runserver จะส่งผลให้ Django ไปอ่าน configuration ในไฟล์ settings.py แล้วเริ่ม start web server ด้วย configuration เหล่านั้น โดยค่า config ที่อยู่ในไฟล์ settings.py มีรายละเอียดดังต่อไปนี้

1.  BASE_DIR คือตัวแปรที่เก็บ absolute path ไปหา Django project ของเรา ซึ่งโดยปกติข้อมูลส่วนนี้จะถูกเขียนอยู่ในรูปแบบของ Python script ที่ใช้อ้าง path มาถึงไฟล์ settings.py ตัวนี้ (สามารถทดลองโดยการ copy code ดังกล่าวมา save ไว้ในไฟล์ python ที่สร้างมาใหม่แล้วลองรันดูผลลัพธ์ได้)
2.  SECRET_KEY คือตัวแปรที่ใช้เก็บ hash text ใช้สำหรับการเข้ารหัสสิ่งต่าง ๆ ใน Django project เช่น session, cookies, password เป็นต้น ดังนั้นจึงไม่ควรเปลี่ยนค่านี้ และเก็บไว้เป็นความลับไม่ copy ไปแสดงในที่อื่น (โดยปกติค่านี้จะไม่ถูกแก้ไขหรือใช้งานอยู่แล้ว จะถูกใช้งานโดยอัตโนมัติเอง)
3.  DEBUG คือตัวแปรที่ใช้บอก Django ว่ารันใน mode debug หรือไม่ ซึ่งใน mode debug นี้ Django จะแสดง Error stack traceทั้งหมดออกมาในหน้าจอ web browser เพื่อให้ developer เห็นบรรทัดที่ code error แล้วเข้าแก้ไขได้ทันที
4.  ALLOWED_HOSTS คือตัวแปรที่ใช้เก็บชื่อ domain name ของ web site เรา โดยจะเก็บในรูปแบบ list ของ string เช่น [‘www.mylibrary.com’, ‘128.199.148.2XX’] เหตุผลที่ต้องระบุชื่อของ host อย่างเจาะจงเพื่อนำไปสร้าง host header ใน HTTP request เพื่อใช้ป้องกัน Cross Site Scripting attack ที่มีการส่ง host ปลอมมาหลอก server เราได้
5.  INSTALLED_APPS คือตัวแปรที่ใช้เก็บ Django Application ทั้งหมดที่ project นี้จะรู้จัก ซึ่งโดย default Django จะ add default Django Application บางตัวเข้ามาอยู่แล้ว
6.  MIDDLEWARE คือ plugin ที่ถูกใช้งานโดย Django เพื่อใช้ในงานด้านต่าง ๆ เช่น django.contrib.auth.middleware.AuthenticationMiddleware ถูกใช้สำหรับการจัดการ user ที่ authenticated กับระบบเข้ากับ HTTP request โดยผ่านทาง session ที่ user นั้น ๆ login อยู่เป็นต้น ซึ่งโดยปกติ Django จะมีการ add middleware ที่จำเป็นมาให้อยู่แล้ว
7.  ROOT_URLCONF คือตัวแปรที่ใช้เก็บ path ไปหาไฟล์ urls.py ซึ่งเป็นไฟล์แรกที่ Django เริ่มทำงานเมื่อได้รับ HTTP request
8.  TEMPLATES คือตัวแปรที่เก็บ configuration ของ Template โดย Template คือสิ่งที่รับผิดชอบในการ render หน้าเวป HTML + javascript ออกมาแล้วส่งกลับไปให้ web browser ซึ่งจะกล่าวถึงในหัวข้อถัดไป
9.  WSGI_APPLICATION คือตัวแปรที่ใช้เก็บ path ไปหาตัวแปร wsgi application ซึ่งถูกใช้ในการ deploy ระบบใน environment จริง เมื่อต้องการเชื่อมต่อ Django เข้ากับ web server ต่าง ๆ
10.  DATABASES คือตัวแปรที่เก็บ configuration ต่าง ๆ ของ ฐานข้อมูล เช่น ชนิดของฐานข้อมูล, username, password, ชื่อ database เป็นต้น โดย default Django จะใช้ sqlite3 ซึ่งเป็นฐานข้อมูลชนิดไฟล์ในการทำงาน
11.  LANGUAGE_CODE คือตัวแปรที่ใช้เก็บภาษา default ที่ระบบจะแสดงผล
12.  TIME_ZONE ใช้เก็บ timezone ตามปกติ
13.  USE_I18N คือตัวแปรที่ใช้บอกว่าระบบรองรับ I[18N (Internationalization)](https://en.wikipedia.org/wiki/Internationalization_and_localization)หรือไม่ ซึ่ง I18N คือระบบการแปลภาษาในหน้าเวปไซด์ให้รองรับหลาย ๆ ภาษา หลักการทำงานคือ Django จะสร้างไฟล์ขึ้นมาเป็น list ของ text ทั้งหมดในหน้าเวปเรา แล้วให้เราแปล text เหล่านี้ให้อยู่ในภาษาอื่น ๆ เท่าที่เราต้องการจะ support แล้ว Django จะนำ text ที่แปลแล้วมาแสดงแก่ผู้ใช้งานอีกทีหนึ่ง
14.  USE_L10N คือตัวแปรที่บอกว่า web server ของเรา support L10N (Localization) หรือไม่ ซึ่ง L10N จะแตกต่างกับ I18N คือ I18N จะครอบคลุมถึงการแปลภาษาบนหน้าจอเท่านั้น ส่วน L10N จะมีส่วนไปถึงการแสดงผลต่าง ๆ เช่น รูปแบบการแสดงวันที่, การแสดงหน่วยของเงิน เป็นต้น
15.  USE_TZ คือตัวแปรที่ใช้เก็บว่า web server รองรับ Time zone หรือไม่ หากตั้งค่าเป็น false ระบบจะไม่สนใจค่า time zone และใช้เวลาตามเครื่อง server เป็นหลักโดยไม่มีการทดเวลา เหมาะสำหรับการพัฒนาเวปไซด์ที่มีผู้ใช้งานเป็นคนไทย และไม่จำเป็นต้องใช้กับต่างประเทศ
16.  STATIC_URL คือตัวแปรที่ใช้เก็บ web url ไปยัง folder ที่ใช้เก็บ static ไฟล์ต่าง ๆ เช่น  [http://www.mylibrary.com/static/](http://www.mylibrary.com/static/)  เป็นต้น
17.  STATIC_ROOT ตัวแปรนี้ไม่ได้ถูกสร้างมาโดย default เป็นตัวแปรที่ใช้สำหรับเก็บ path ที่เราไว้เก็บไฟล์ static ต่าง ๆ เช่น ไฟล์ javascript หรือ css

----------

# สร้าง Django Application

Django framework แนะนำให้แบ่งการพัฒนา web application ของเราออกเป็น module ย่อย ๆ แทนที่จะเก็บใน folder project ใหญ่ ๆ เพียงตัวเดียว โดย module ย่อย ๆ เหล่านี้เรียกว่า Django Application ซึ่งข้อกำหนดในการแบ่ง Django Application นั้น ไม่มีแบบแผนที่ตายตัว ขึ้นอยู่กับความเหมาะสมของแต่ละ project เช่น project my_library (ห้องสมุดของฉัน) อาจสามารถแบ่ง Django Application ออกเป็น

-   book_management ใช้สำหรับจัดการหนังสือในห้องสมุด เช่น การลงทะเบียนหนังสือ, การค้นหาหนังสือ, การจัดการยืมคืน เป็นต้น
-   human_resource ใช้สำหรับจัดการพนักงานที่ทำงานในห้องสมุดแห่งนี้ เช่น การลงทะเบียนพนักงาน, การจัดกะการทำงาน, การลงเวลาเข้าออกพนักงาน
-   account ใช้สำหรับเก็บบัญชีรายรับ, รายจ่ายของห้องสมุดแห่งนี้ เป็นต้น

สำหรับคำสั่งที่ใช้ในการสร้าง Django Application ที่ชื่อ book_management คือ

> $ py manage.py startapp book_management

![](https://miro.medium.com/max/25/1*dS_HNG168HBIr2lSn4qSOA.png?q=20)

![](https://miro.medium.com/max/507/1*dS_HNG168HBIr2lSn4qSOA.png)

โครงสร้างโฟลเดอร์ของ Django Application

โดยแต่ละไฟล์จะค่อย ๆ อธิบายผ่านบทความนี้ไปเรื่อย ๆ ครับ

ความต้องการขั้นต่ำที่สุดของ Django คือไฟล์ urls.py และ views.py

เริ่มจากไฟล์ views.py เป็นไฟล์ที่ใช้เก็บ logic ของ web application คอยควบคุมสิ่งที่รับมาจาก client web browser (HTTP parameters ต่าง ๆ) และควบคุมสิ่งที่จะตอบกลับไปยัง client web browser

ทดลองเปิดไฟล์ views.py ด้วย text editor แล้วเพิ่ม function ลงไปครับ

![](https://miro.medium.com/max/30/1*CZJhv6X5xhGUIXjcjxxWqw.png?q=20)

![](https://miro.medium.com/max/903/1*CZJhv6X5xhGUIXjcjxxWqw.png)

ตัวอย่างไฟล์ views.py

จากนั้นแก้ไขไฟล์ urls.py ให้เป็นดังรูป

![](https://miro.medium.com/max/30/1*P6uwP9JY4k4BUO2OWzN7YQ.png?q=20)

![](https://miro.medium.com/max/575/1*P6uwP9JY4k4BUO2OWzN7YQ.png)

ตัวอย่างไฟล์ urls.py

จากนั้นรัน Django อีกครั้ง แล้วเปิด web browser แล้วเข้าหน้าเวป  [http://localhost:8000/](http://localhost:8000/)my_index/ จะเห็นว่าหน้าจอที่แสดงผลเปลี่ยนเป็นดังรูปด้านล่างนี้

![](https://miro.medium.com/max/30/1*DlPT5Vsq81cBcKexAcKtSA.png?q=20)

![](https://miro.medium.com/max/433/1*DlPT5Vsq81cBcKexAcKtSA.png)

ตัวอย่างหน้า Web Page แรก

สิ่งที่เกิดขึ้นภายในการทำงานของ Django สามารถอธิบายได้ด้วยภาพดังต่อไปนี้

![](https://miro.medium.com/max/30/1*uIXD6s3_p2D2CfvBe8zjMw.png?q=20)

![](https://miro.medium.com/max/691/1*uIXD6s3_p2D2CfvBe8zjMw.png)

การทำงานของ Django เมื่อได้รับ HTTP Request จาก Web Browser

เมื่อได้รับ HTTP Request จาก Web Browser มาแล้ว Django จะเริ่มทำงานโดยเริ่มจากไฟล์ urls.py ซึ่งหน้าที่หลักของไฟล์นี้คือการทำ URL Pattern Matching เพื่อดูว่า user request มาที่ URL อะไร จากนั้นจึงค่อยเรียก Python Script ที่ถูก match เพื่อขึ้นมาทำงาน

![](https://miro.medium.com/max/30/1*iRF5HaYse65yGKAPOM_6mg.png?q=20)

![](https://miro.medium.com/max/415/1*iRF5HaYse65yGKAPOM_6mg.png)

อธิบายการทำงานของ urls.py

จากรูปจะเห็นว่าข้อมูลใน urls.py ถูกแบ่งออกเป็นสองส่วนนั่นคือ

1.  r’^my_index/$’ ส่วนนี้เป็น String ที่ใช้ระบุถึง  [Regular Expression](https://en.wikipedia.org/wiki/Regular_expression)  ที่จะใช้ match กับ URL ที่ผู้ใช้กรอกมาใน Web Browser  
    NOTE: ตัว r ด้านหน้า String ใน Python หมายถึง “Raw String Literal” คือให้มอง String ทั้งหมดโดย ignore สัญลักษณ์พิเศษ นั่นคือ backslash (\) ทำให้ Python มอง backslash ว่าเป็นตัวอักษรธรรมดาตัวหนึ่งไม่ใช่ escape character ดังนั้น r’\n’ จะไม่มีผลให้ขึ้นบรรทัดใหม่แต่จะหมายถึงตัวอักษรว่า \n จริง ๆ
2.  views.index คือ Python Script ที่อ้างไปถึงไฟล์ views.py ในโฟลเดอร์ book_management และไปยัง function ที่ชื่อ index ซึ่งจะเห็นว่าในไฟล์ views.py จะมีการเรียก function HttpResponse() เพื่อ return HTML text กลับไปแสดงผลบนหน้าจอ

![](https://miro.medium.com/max/30/1*r3SfcWUDjhQ2nz6X50ZoYw.png?q=20)

![](https://miro.medium.com/max/842/1*r3SfcWUDjhQ2nz6X50ZoYw.png)

อธิบายการทำงานไฟล์ views.py

1.  เป็นส่วนที่ใช้ import function ชื่อ render และ HttpResponse เข้ามาใช้งานใน Script ของเรา
2.  การประกาศ function ของ Python เป็น function ชื่อ index โดยรับ parameter เป็น request ซึ่ง parameter นี้มีชนิดตัวแปรเป็น  [HttpRequest Object](https://docs.djangoproject.com/en/1.11/ref/request-response/#httprequest-objects)  ซึ่งภายในตัวแปรนี้จะเก็บข้อมูลต่าง ๆ ของ HTTP เอาไว้ เช่น HTTP parameter, method, content type, body, หรือ path เป็นต้น
3.  ประกาศตัวแปรชนิด  [HttpResponse](https://docs.djangoproject.com/en/1.11/ref/request-response/#httpresponse-objects) ซึ่งจากตัวอย่างเราจะส่ง body ของ response เป็น HTML ง่าย ๆ กลับไปแสดงผลยัง Web Browser

----------

# Django Template

จากตัวอย่างในหัวข้อก่อนหน้าจะเห็นว่าเราสามารถส่ง HTML กลับไปยัง Web Browser ได้โดยผ่านทาง views.py แต่หากเราต้องการส่งหน้า HTML ที่มีความซับซ้อนมากกว่านี้ เช่น มีการแนบไฟล์ Javascript, CSS, หรือภาพ หรือแม้แต่หน้า web site แบบ AngularJS หรือ React กลับไปแสดงผลบน Web Browser จะมีความยุ่งยากมากหากใช้วิธีนี้่ที่ต้องเปลี่ยน library เหล่านั้นเป็น text เพื่อกลับไปแสดงผล ซึ่ง Django มีวิธีที่ใช้ในการส่งหน้า Web Page ที่มีความซับซ้อนโดยผ่านทาง Template Engine

![](https://miro.medium.com/max/30/1*GiAJufWRRCjAKuzBfOdQBA.png?q=20)

![](https://miro.medium.com/max/1199/1*GiAJufWRRCjAKuzBfOdQBA.png)

ตัวอย่างอธิบายการทำงานของ Django Template

จากรูปจะเห็นว่าในการทำงานของ Template นั้นเริ่มจากทางผู้พัฒนาต้องสร้างไฟล์ HTML Template ขึ้นมา ซึ่งสิ่งทีทำให้ไฟล์ HTML นี้ต่างจากไฟล์ HTML ทั่วไปคือจะมีการฝัง Django Tag เข้าไปด้วย โดยในตัวอย่างคือการใช้  _{{var1}}_ หมายถึงการสร้างตัวแปรของ Django ขึ้น จากนั้นเมื่อ Django โหลดไฟล์ Template นี้ขึ้นมาสามารถ pass ค่า ของตัวแปรเข้าไปสู่ไฟล์นี้ได้ หลังจากนั้นจึงได้ไฟล์ HTML ที่สมบูรณ์พร้อมส่งกลับไปแสดงผลยัง Web Browser ต่อไป

Django Tag ที่สามารถใช้งานได้มีหลากหลาย เช่น การส่งผ่านตัวแปรธรรมดาดังตัวอย่างด้านบน, การใช้ if/else, การใช้ for loop ซึ่งรายละเอียดของ Django Tag ทั้งหมดสามารถ  [อ่านเพิ่มเติมได้ที่นี่](https://docs.djangoproject.com/en/1.11/ref/templates/builtins/)

เริ่มการทดลองนี้โดยการสร้าง Folder Template และสร้างไฟล์ index.html

![](https://miro.medium.com/max/27/1*tjlxYHB5qJlHeEo85IE54A.png?q=20)

![](https://miro.medium.com/max/909/1*tjlxYHB5qJlHeEo85IE54A.png)

สร้างโฟลเดอร์ชื่อ templates และสร้างไฟล์ index.html ในนั้น

![](https://miro.medium.com/max/30/1*QGM6ox_q_AkCxPjm8S7QdQ.png?q=20)

![](https://miro.medium.com/max/336/1*QGM6ox_q_AkCxPjm8S7QdQ.png)

code ในไฟล์ index.html

จากนั้นแก้ไขไฟล์ settings.py โดยการเพิ่ม ค่าให้กับตัวแปร DIRS ที่อยู่ภายใต้ TEMPLATES configuration ซึ่ง DIRS จะเป็นตัวบอกว่าไฟล์ HTML template ของเราถูกเก็บไว้ที่ไหนบ้าง

![](https://miro.medium.com/max/30/1*yYlblbeK3jvmGrSbsA2Zjw.png?q=20)

![](https://miro.medium.com/max/835/1*yYlblbeK3jvmGrSbsA2Zjw.png)

ไฟล์ settings.py ที่ถูกแก้ไขเพื่อให้ Django รู้จัก Folder Template

จากนั้นแก้ไขไฟล์ views.py โดยเพิ่มเติม code ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*84wA3kQLLwiipYncmySiZA.png?q=20)

![](https://miro.medium.com/max/691/1*84wA3kQLLwiipYncmySiZA.png)

ไฟล์ views.py ที่ใช้ในการโหลด HTML Template ชื่อ index.html แล้วผ่านค่าตัวแปร var1 ลงไป

1.  เพิ่ม import ตัวแปร loader
2.  ประกาศตัวแปรชื่อ header_str ให้เป็นชนิด String และมีข้อความดังปรากฎในรูป
3.  โหลด template ไฟล์ชื่อ index.html โดย Django จะพยายามไปหาจาก path ที่เรากรอกไว้ใน DIRS
4.  ประกาศตัวแปร context เป็นชนิด dictionary (dictionary คือ datatype ที่ใช้เก็บตัวแปรในรูปแบบของ key, value) โดยมีค่า key เป็น  _var1_ ซึ่งเป็นชื่อตัวแปรที่ประกาศใน index.html และ value คือตัวแปร  _header_str_
5.  เรียกฟังก์ชั่น render เพื่อ generate HTML ไฟล์ออกมาเพื่อส่งให้กับ Client

เปิด Web Browser แล้ว Browse ไปยัง  [http://localhost:8000/my_index/](http://localhost:8000/my_index/)

![](https://miro.medium.com/max/30/1*RZvhDssB_XZy-xj0A4dV2w.png?q=20)

![](https://miro.medium.com/max/351/1*RZvhDssB_XZy-xj0A4dV2w.png)

ตัวอย่างผลลัพธ์ของหน้าจอ HTML

เราสามารถย่อ code ที่ใช้ในการ load template ด้วยฟังก์ชั่น render ได้ดังรูปต่อไปนี้

![](https://miro.medium.com/max/30/1*eewUccYs-Oe8etYGTeAJWA.png?q=20)

![](https://miro.medium.com/max/545/1*eewUccYs-Oe8etYGTeAJWA.png)

การเรียกใช้ฟังก์ชั่น render เพื่อย่อ code ที่ใช้ในการ load Django Template

**การโหลด Javascript, CSS, หรือรูปภาพมาใช้งานบนหน้า web page**

กรณีที่เราต้องการใส่ Javascript, CSS หรือรูปเข้าไปเพื่อแสดงผลในหน้าเวป สามารถทำได้โดยผ่าน static (ที่เรียกว่า static เพราะไฟล์ JS, CSS, images เป็นไฟล์ Library ที่คงที่ ไม่มีการเปลี่ยนแปลง) โดยการใช้งาน static feature ใน Django นั้นต้องเริ่มจากไฟล์ settings.py ตรวจสอบว่ามี 2 บรรทัดนี้อยู่ในไฟล์

![](https://miro.medium.com/max/30/1*MT1HdXXRG4FmkfGNfeJFdQ.png?q=20)

![](https://miro.medium.com/max/425/1*MT1HdXXRG4FmkfGNfeJFdQ.png)

Configuration ที่ทำให้เกิด Feature Static

จากนั้นเพิ่ม Folder ชื่อ static ภายใต้ Folder book_management และสร้างไฟล์ style.css ขึ้นมา ซึ่ง Django จะไปหาไฟล์ static ตาม path static ที่อยู่ภายใต้ Django Application folder โดยอัตโนมัติ

![](https://miro.medium.com/max/27/1*KHwr4_f3ZCqaQGM04BPdiA.png?q=20)

![](https://miro.medium.com/max/637/1*KHwr4_f3ZCqaQGM04BPdiA.png)

สร้างโฟลเดอร์ static และ style.css

![](https://miro.medium.com/max/30/1*p_w54kBo4k-dZhxDLn_tpg.png?q=20)

![](https://miro.medium.com/max/365/1*p_w54kBo4k-dZhxDLn_tpg.png)

แก้ไขไฟล์ style.css โดยเพิ่มข้อความดังต่อไปนี้ (เป็นการเปลี่ยนพื้นหลังให้เป็นสีเหลือง)

จากนั้นแก้ไขไฟล์ index.html โดยเพิ่มบรรทัดดังต่อไปนี้เข้าไป

![](https://miro.medium.com/max/30/1*VPwdlFGSNRxefexUIHoF7Q.png?q=20)

![](https://miro.medium.com/max/853/1*VPwdlFGSNRxefexUIHoF7Q.png)

1.  หมายถึงการ load library static ของ Django เข้าไปใน web browser
2.  การเรียกใช้ CSS ภายในหน้าเวป โดยให้สังเกตุ tag href จะมีการเรียกใช้ Django syntax ชื่อ static

จากนั้น browse ไปที่  [http://localhost:8000/my_index/](http://localhost:8000/my_index/)  จะได้ผลลัพธ์ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*9w1Tmxm3pG7oZNgxAE93xQ.png?q=20)

![](https://miro.medium.com/max/482/1*9w1Tmxm3pG7oZNgxAE93xQ.png)

ภาพผลลัพธ์การ load static ไฟล์จาก Django

จากตัวอย่างข้างต้นสามารถใช้วิธีเดียวกันนี้ไปประยุกต์ใช้กับการโหลด Javascript และรูปภาพได้ เช่น

-   <img src=“{% static ‘background.png’ %}”/> เพื่อ โหลดรูปขึ้นมาแสดงผล
-   <script src=“{% static ‘myscript.js’ %}”/> เพื่อโหลด Javascript Library เข้ามาใช้งาน

----------

# การเชื่อมต่อฐานข้อมูล

การเข้าถึงฐานข้อมูลของ Django นั้นโดยทั่วไปจะไม่ใช้ SQL statement ตรง ๆ แต่จะถูกกระทำผ่านสิ่งที่เรียกว่า  [Object Relational Mappings (ORM)](https://en.wikipedia.org/wiki/Object-relational_mapping)  ซึ่ง ORM จะเป็นซ่อนคำสั่งของ SQL statement ทั้งหมดออกจากการพัฒนา แต่จะให้ผู้พัฒนาเข้าถึงฐานข้อมูลผ่านทาง class — object แทน (class/object เหมือนใน OOP ทั่วไป)โดย class จะเป็นตัวแทนของ Table ในฐานข้อมูล และ object จะเป็นตัวแทนของข้อมูลในฐานข้อมูล (Record)

ข้อดีของการใช้ ORM คือ syntax สามารถอ่านได้ง่ายกว่า SQL statement, และเราสามารถเปลี่ยนฐานข้อมูลได้โดยง่าย เช่น จากเดิมใช้ SQLite3 ต้องการเปลี่ยนเป็น MySQL หรือ Postgres ก็สามารถทำได้ทันที (อาจมีบางคำสั่งไม่ compatible กันซะทีเดียว ต้องมีการทดสอบให้ดีหลังเปลี่ยนฐานข้อมูลแล้วนะครับ)

ฐานข้อมูลที่จะใช้ในการทดสอบในครั้งนี้คือ SQLite3 ซึ่งเป็นฐานข้อมูลชนิดไฟล์ ซึ่งถูกตั้งค่าไว้เป็น default สำหรับ Django เราสามารถเปลี่ยนแปลงค่านี้ได้ทีหลังในไฟล์ settings.py

![](https://miro.medium.com/max/30/1*tcVpxsYYBwHQ_yjw4JnmDQ.png?q=20)

![](https://miro.medium.com/max/581/1*tcVpxsYYBwHQ_yjw4JnmDQ.png)

ไฟล์ settings.py แสดงการตั้งค่าฐานข้อมูล SQLite3 ซึ่งติดตั้งมาเป็นค่า default

ในหัวข้อนี้เราจะทดลองสร้างฐานข้อมูลที่เก็บข้อมูลของหนังสือ (Book) โดยหนังสือแต่ละเล่มจะถูกจัดอยู่ในหมวดหมู่ (Category) ต่างๆ ดังตัวอย่างต่อไปนี้

![](https://miro.medium.com/max/21/1*xUXIh83DXSnFDWyNKvOX3Q.png?q=20)

![](https://miro.medium.com/max/192/1*xUXIh83DXSnFDWyNKvOX3Q.png)

ตัวอย่างฐานข้อมูลที่ต้องการสร้าง

ซึ่งสามารถทำได้โดยการแก้ไขไฟล์ models.py ในโฟลเดอร์ book_management ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*9__OAHm_yXTgjZ7I0AVO0A.png?q=20)

![](https://miro.medium.com/max/832/1*9__OAHm_yXTgjZ7I0AVO0A.png)

ตัวอย่างไฟล์ models.py สำหรับสร้างฐานข้อมูลที่มี table ชื่อ Book และ Category

1.  Import  [models object](https://docs.djangoproject.com/en/1.11/ref/models/instances/#model-instance-reference)  ซึ่งตัว models นี้เป็นพื้นฐานสำหรับการทำให้ class ของเรามีรูปแบบที่ ORM สามารถรู้จักได้
2.  ประกาศ class ชื่อ Category ซึ่งสืบทอด (inherit) มาจาก class models.Model ส่วนนี้จะเป็นการบอกว่าให้สร้าง table ชื่อ Category ขึ้นในฐานข้อมูล
3.  ประกาศตัวแปรชื่อ name เป็นชนิด CharField มีความยาวสูงสุด 255 ตัวอักษร ส่วนนี้จะเหมือนกับการประกาศ Database Field ชื่อ name มีชนิดเป็น varchar 255 นั่นเอง
4.  ประกาศ class ชื่อ Book เป็นการสร้าง table ชื่อ Book ขึ้นมา
5.  ประกาศตัวแปร title เป็นชนิด CharField
6.  ประกาศตัวแปร publish_date เป็นชนิด date time ใช้เก็บวันที่ตีพิมพ์
7.  ประกาศตัวแปร category เป็นตัวแปรที่มีความสัมพันธ์ Foreign Key ไปหา table Category โดย parameter ที่ชื่อ on_delete=models.CASCADE หมายถึงการบอกว่าหาก Category Object ถูกลบไป Django จะตามไปลบ Book ทุกตัวที่มี Reference ถึง Category นี้ด้วย

สำหรับรายละเอียดชนิดของตัวแปร (Database Field) ทั้งหมดที่ Django support สามารถอ่านเพิ่มเติมได้  [ที่นี่](https://docs.djangoproject.com/en/1.11/ref/models/fields/)

แก้ไขไฟล์ settings.py เพื่อให้ Django project รู้ว่ามี Django Application ที่มีฐานข้อมูลได้โดยเพิ่ม ‘book_management’ เข้าไปในส่วนของ INSTALLED_APPS ดังแสดงในรูปด้านล่าง (อย่าลืมใส่ลูกน้ำ (,) ไว้หลังบรรทัด ‘django.contrib.staticfiles’ ด้วยนะครับ) โดยการเขียนอย่างนี้หมายถึงตัวแปร INSTALLED_APPS จะเป็นตัวแปรที่เก็บ list ของ string เอาไว้

![](https://miro.medium.com/max/30/1*MV5bBBM9BIbT6N3_KIBSNQ.png?q=20)

![](https://miro.medium.com/max/462/1*MV5bBBM9BIbT6N3_KIBSNQ.png)

เพิ่ม Django Application ให้กับ Django Project รู้จัก

ในการสร้างฐานข้อมูลจริง ๆ นั้น Django จำเป็นต้อง generate script ออกมาชุดหนึ่ง เรียกว่า Migration File ไว้ใช้สำหรับการสร้างฐานข้อมูลจริง ประโยชน์ของ Migration File ทีสร้างขึ้นมานี้เพื่อให้ Django Application สามารถ track การเปลี่ยนแปลงของฐานข้อมูลได้ตลอดเวลาที่มีการเปลี่ยนแปลง models.py ซึ่ง Django สามารถเปลี่ยน schema ของฐานข้อมูลไปมาได้ หรือจะย้อนกลับไปใช้ schema เก่าได้อย่างง่ายดาย (ในความเป็นจริงหากฐานข้อมูลมีความซับซ้อนมาก ๆ กระบวนการย้อน schema กลับไปก็เป็นสิ่งที่ยากเหมือนกันครับ)

![](https://miro.medium.com/max/30/1*v0AkBMFZ9KIEWIUhagQB-A.png?q=20)

![](https://miro.medium.com/max/763/1*v0AkBMFZ9KIEWIUhagQB-A.png)

การทำงานของ Django ORM เพื่อใช้สร้าง Database Schema

โดยคำสั่งที่ใช้ในการสร้าง Migration File คือ

> $ py manage.py makemigrations

![](https://miro.medium.com/max/30/1*2apuuS7NRAOEN57MWRkwig.png?q=20)

![](https://miro.medium.com/max/933/1*2apuuS7NRAOEN57MWRkwig.png)

ตัวอย่างการรันคำสั่ง makemigrations

หลังจากรันคำสั่งนี้จะส่งผลให้เกิดไฟล์ใหม่ขึ้นมาภายใต้โฟลเดอร์ book_management/migrations คือไฟล์ 0001_initial.py

![](https://miro.medium.com/max/25/1*ixjy-pJAzZ4YgmnRut0LwQ.png?q=20)

![](https://miro.medium.com/max/658/1*ixjy-pJAzZ4YgmnRut0LwQ.png)

สำหรับ Migration File ที่สร้างขึ้นมานี้หากลองเปิดดูจะเห็นว่าเป็นชุดคำสั่งของ Python ที่ใช้สำหรับเปลี่ยนแปลง Schema ในฐานข้อมูล โดยปกติแล้วผู้พัฒนาไม่จำเป็นต้องแก้ไขไฟล์นี้ แต่มีบางกรณีเช่นกันที่ต้องเข้ามาแก้ไข เช่น ต้องการลบ table A พร้อมกับย้ายข้อมูลบางส่วนไปยัง table B เป็นต้น

จากนั้นสั่งให้ Django สร้างฐานข้อมูลด้วยคำสั่ง

> $ py manage.py migrate

![](https://miro.medium.com/max/30/1*PykZ9lJ53q5MF8ZnGrTVpw.png?q=20)

![](https://miro.medium.com/max/1072/1*PykZ9lJ53q5MF8ZnGrTVpw.png)

ตัวอย่างการรันคำสั่ง migrate เพื่อสร้างฐานข้อมูล

หลังจากรันไฟล์นี้แล้วเราจะได้ไฟล์ใหม่ชื่อ db.sqlite3 ซึ่งเป็นไฟล์ฐานข้อมูลที่มี table ของ Book และ Category อยู่ภายใน และ Django จะทำการสร้าง Table Default อื่นๆ ขึ้นมาด้วย เช่น Table User, role สำหรับการทำ Authentication เป็นต้น

![](https://miro.medium.com/max/24/1*G6GR9lUlAIacGLy8wGvitg.png?q=20)

![](https://miro.medium.com/max/361/1*G6GR9lUlAIacGLy8wGvitg.png)

โครงสร้างฐานข้อมูลที่ถูกสร้างขึ้นโดย Django

----------

# Django Shell

Django Shell คือ python shell แบบหนึ่งซึ่งสามารถเข้าใช้งานฐานข้อมูลได้ ซึ่งเป็น feature ที่สะดวกมากในการเข้าตรวจสอบ debug ฐานข้อมูล หรือทดสอบใส่ข้อมูลเข้าไปในฐานข้อมูลโดยตรง โดยเราสามารถเข้าถึง Django Shell ด้วยคำสั่ง

> $ py manage.py shell

![](https://miro.medium.com/max/30/1*2FZr4Nh1mPRHqxY4_MWvVA.png?q=20)

![](https://miro.medium.com/max/1257/1*2FZr4Nh1mPRHqxY4_MWvVA.png)

ตัวอย่าง Django Shell

ขั้นตอนต่อไปเป็นการ import table ของฐานข้อมูลให้กับ shell รู้จัก เพื่อเตรียมตัวทำงานกับ table เหล่านี้ต่อไป

> from book_management.models import Category, Book

จากนั้นทดลองสร้าง Category ของหนังสือ ชื่อ “Horror” ด้วยคำสั่ง

> horror_category = Category(name=’Horror’)  
> horror_category.save()

![](https://miro.medium.com/max/30/1*FoxEn7TP-7iExO7sgVzlEg.png?q=20)

![](https://miro.medium.com/max/883/1*FoxEn7TP-7iExO7sgVzlEg.png)

แสดงขั้นตอนการสร้าง Category Horror ในฐานข้อมูล

จะเห็นว่าการสร้าง Record ใน Database Table นั้นสามารถทำได้อย่างง่าย คล้ายกับการสร้าง object ของ class ตามปกติ โดยในบรรทัดแรกจะเป็นคำสั่งที่ใช้ในการสร้าง object ชื่อ horror_category จาก class Category โดยมี parameter name เป็น Horror และบรรทัดที่สองคำสั่ง save() เป็นฟังก์ชั่นที่ให้ Django เปิดการเชื่อมต่อกับฐานข้อมูลและ save Record ลงฐานข้อมูลจริง

![](https://miro.medium.com/max/30/1*dir4eOah1shNdTxGCd0Kow.png?q=20)

![](https://miro.medium.com/max/549/1*dir4eOah1shNdTxGCd0Kow.png)

ทดสอบ Browse ฐานข้อมูลจริงเพื่อดูข้อมูลในฐานข้อมูล

จากรูปจะเห็นว่าในฐานข้อมูลจริงนั้น Django ได้ใส่ Record ที่ชื่อ Horror เข้าไปในฐานข้อมูล และสังเกตุ Field ชื่อ id เป็น Field Default ที่ถูกสร้างขึ้นโดย Django เพื่อใช้เป็น internal key สำหรับเป็น primary key ของ table นี้ เนื่องจากในทุก ๆ table ในฐานข้อมูล Django จะบังคับให้มี primary key อย่างน้อย 1 ตัว ดังนั้นหากเรากำหนด primary key ตอนประกาศ class จะทำให้ Field id นี้หายไป

ทดลองดึงข้อมูลออกจากฐานข้อมูลด้วยคำสั่ง

> c_list = Category.objects.filter(name=’Horror’)  
> c_list[0].name

![](https://miro.medium.com/max/30/1*ZE3mCkv58w_Jvfszf10CuA.png?q=20)

![](https://miro.medium.com/max/541/1*ZE3mCkv58w_Jvfszf10CuA.png)

ผลลัพธ์การดึง Category ออกจากฐานข้อมูล

![](https://miro.medium.com/max/30/1*eYi3-1DBoR1TiuyjXj99Og.png?q=20)

![](https://miro.medium.com/max/485/1*eYi3-1DBoR1TiuyjXj99Og.png)

1.  ประกาศตัวแปรชื่อ c_list ไว้รอรับค่าจากการเรียกฟังก์ชั่น
2.  Category.objects จะ return object ชนิด  [Manager](https://docs.djangoproject.com/en/1.11/topics/db/managers/)  ออกมา ซึ่งเป็น object ที่ใช้เริ่มต้นในการทำ Database operation ต่าง ๆ ต่อไป
3.  ฟังก์ชั่น filter คือฟังก์ชั่นที่ใช้ในการค้นหาข้อมูลในฐานข้อมูล เทียบเท่ากับคำสั่ง SELECT ในภาษา SQL ธรรมดา ซึ่งจากในตัวอย่างเราสามารถแปลงเป็น SQL statement ได้ว่า SELECT * FROM Category WHERE name=’horror’ นั่นเอง สิ่งที่ return กลับมาจากฟังก์ชั่น filter คือ  [QuerySet](https://docs.djangoproject.com/en/1.11/ref/models/querysets/) object ซึ่งเป็น list ของ object (Record ในฐานข้อมูล) ที่ได้จากคำสั่งต่างๆ นั่นเอง สำหรับรายละเอียดคำสั่ง Query อื่น ๆ เช่น order_by, like สามารถอ่านเพิ่มเติมได้จาก  [ที่นี่](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#queryset-api)

เราสามารถนำความรู้ที่ได้จากส่วนนี้มาใช้ร่วมกับไฟล์ template และ views.py เพื่อส่งผลลัพธ์ที่ได้จากฐานข้อมูลกลับไปให้ผู้ใช้งานได้เห็นได้ เริ่มจากทดลองแก้ไขไฟล์ templates/index.html ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*jdM0GQpShaF_cX855ESa2g.png?q=20)

![](https://miro.medium.com/max/521/1*jdM0GQpShaF_cX855ESa2g.png)

แก้ไขไฟล์ index.html เพื่อแสดงผลการนับ Category object และ Book object จากฐานข้อมูล

จากนั้นแก้ไขไฟล์ views.py ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*xBKMTIZ2PQMxsmeEyHsaZg.png?q=20)

![](https://miro.medium.com/max/418/1*xBKMTIZ2PQMxsmeEyHsaZg.png)

ไฟล์ views.py ที่แก้ไขเพื่อแสดงค่าการนับ Category และ Book ในฐานข้อมูล

![](https://miro.medium.com/max/30/1*C-kv3AdJpvFwHobZ7uWV3w.png?q=20)

![](https://miro.medium.com/max/306/1*C-kv3AdJpvFwHobZ7uWV3w.png)

1.  len() เป็น function build-in ของ Python โดยรับค่าตัวแปรเป็น list แล้วจะ return มาเป็นจำนวน element ทั้งหมดที่อยู่ใน list โดยจากตัวอย่างเราได้ส่งผลลัพธ์ของการ Query หรือ QuerySet เข้าไป ทำให้ len return ค่าของจำนวน Record ทั้งหมดใน QuerySet นี้ออกมา
2.  all() เป็น Manager Function ที่ใช้สำหรับ Select ทุกอย่างออกมาจาก Table ซึ่งจากคำสั่งด้านบนสามารถแปลงเป็น SQL Statement ได้ว่า SELECT * FROM Category นั่นเอง

จากนั้นทดลอง Browse หน้าเวปไปที่  [http://localhost:8000/my_index/](http://localhost:8000/my_index/)  จะได้ผลลัพธ์ดังรูปต่อไปนี้

![](https://miro.medium.com/max/30/1*qForVDRn2mo9gVnbylTuSQ.png?q=20)

![](https://miro.medium.com/max/367/1*qForVDRn2mo9gVnbylTuSQ.png)

----------

# Django admin site

อีกหนึ่ง Feature เด่นสำหรับ Django คือหน้า Web Page ซึ่งเป็นหน้าสำหรับใช้ในการทำ Database CRUD operation (Create, Read, Update, Delete) เหมาะสำหรับใช้เป็นหลังบ้านสำหรับ Web Admin ใช้บริหารงานต่าง ๆ โดยไม่ต้องเข้าถึงฐานข้อมูลโดยตรง หรือสามารถใช้ในการ debug ข้อมูลได้อย่างรวดเร็วอีกด้วย และยิ่งไปกว่านั้น Django Admin ยังสามารถปรับแต่งแก้ไขให้แสดงรายละเอียดตามที่ต้องการได้หลากหลาย เช่น ต้องการใส่ search box, ใส่ filter เปลี่ยนการแสดงผล เช่น Object Book ต้องการแสดงแค่ชื่อของหนังสือเพียงอย่างเดียว เป็นต้น

การใช้งาน Django Admin นั้นขอให้ตรวจสอบไฟล์ settings.py และแก้ไขไฟล์ urls.py ให้มีค่าตามที่แสดงในรูปด้านล่างนี้

![](https://miro.medium.com/max/30/1*yFuhpCStxOLsJcYlpdh_oQ.png?q=20)

![](https://miro.medium.com/max/314/1*yFuhpCStxOLsJcYlpdh_oQ.png)

ไฟล์ settings.py โดยปกติค่าเหล่านี้จะใส่มาให้โดย default อยู่แล้ว

![](https://miro.medium.com/max/30/1*5Nekrq1fU2jkgcOenl1YcQ.png?q=20)

![](https://miro.medium.com/max/339/1*5Nekrq1fU2jkgcOenl1YcQ.png)

ไฟล์ urls.py แก้ไขโดยเพิ่มบรรทัดที่ highlight ด้วยกรอบสีแดงทั้งสองบรรทัด

จากนั้นลองใช้ web browser เข้าไปที่ URL :  [http://localhost:8000/admin/](http://localhost:8000/admin/)  จะได้ผลลัพธ์ดังรูปต่อไปนี้

![](https://miro.medium.com/max/30/1*NqdGI5dsnQo9e_M4vuyzAQ.png?q=20)

![](https://miro.medium.com/max/413/1*NqdGI5dsnQo9e_M4vuyzAQ.png)

จะเห็นว่าเรายังไม่สามารถเข้าใช้งานหน้า Admin ได้เนื่องจากติด Authentication ให้ทำการเพิ่ม user ด้วยคำสั่งดังรูปต่อไปนี้

![](https://miro.medium.com/max/30/1*NagloDeR6ma_NPL0zqnpLw.png?q=20)

![](https://miro.medium.com/max/1182/1*NagloDeR6ma_NPL0zqnpLw.png)

การสร้าง Super User เพื่อเข้าถึงหน้า Django admin site

จากนั้นกลับไป Login เพื่อเข้าสู่หน้าจอ Django admin site

![](https://miro.medium.com/max/30/1*x-dxACxty8WyQCzjibIfHQ.png?q=20)

![](https://miro.medium.com/max/1884/1*x-dxACxty8WyQCzjibIfHQ.png)

จากรูปจะเห็นว่าเราสามารถแก้ไขได้เพียงแค่ Table ที่เกี่ยวกับ user และ group แต่จะไม่เห็น Table Book หรือ Category เนื่องจาก Django admin ยังไม่รู้จัก Table ทั้งสองของเรา ซึ่งเราสามารถทำให้ Django รู้จัก Table ของเราได้โดยผ่านทางไฟล์ admin.py

![](https://miro.medium.com/max/25/1*uS2hUne8CYBh6ClgtyTGLw.png?q=20)

![](https://miro.medium.com/max/658/1*uS2hUne8CYBh6ClgtyTGLw.png)

![](https://miro.medium.com/max/30/1*EdAibG1Sm1AoNhyQNfRrwQ.png?q=20)

![](https://miro.medium.com/max/418/1*EdAibG1Sm1AoNhyQNfRrwQ.png)

แก้ไขไฟล์ admin.py โดยเพิ่ม สองบรรทัดนี้เข้าไป

จากนั้นเปิดหน้า web admin ใหม่อีกครั้งจะเห็น Book และ Category ขึ้นมา

![](https://miro.medium.com/max/30/1*RIs5q8rvu6i-TUjHgqqD8w.png?q=20)

![](https://miro.medium.com/max/677/1*RIs5q8rvu6i-TUjHgqqD8w.png)

![](https://miro.medium.com/max/30/1*USO-3DPxIDJS9tLs9rO7TA.png?q=20)

![](https://miro.medium.com/max/1320/1*USO-3DPxIDJS9tLs9rO7TA.png)

![](https://miro.medium.com/max/30/1*rPNfxTyhvDWKblXExkSOxA.png?q=20)

![](https://miro.medium.com/max/1858/1*rPNfxTyhvDWKblXExkSOxA.png)

จะเห็นว่าการแสดงผลของ Category จะพิมพ์คำว่า Category Object ออกมา เนื่องจาก Django ไม่ทราบว่าเมื่อ object ของ class Category ถูกแปลงเป็น String แล้วจะแสดงผลอย่างไร สามารถแก้ไขตรงนี้ได้โดยการ override function โดยการแก้ไขไฟล์ models.py ดังต่อไปนี้

![](https://miro.medium.com/max/30/1*AbOIqeI6iif_fwpEJSoB3g.png?q=20)

![](https://miro.medium.com/max/555/1*AbOIqeI6iif_fwpEJSoB3g.png)

การประกาศฟังก์ชั่นภายใน class ของ python จะถูกบังคับให้ใส่ตัวแปรชื่อ self มาเสมอ ซึ่งตัวแปร self จะหมายถึง object ของตัวเอง (เหมือนกับ keyword “this” ใน java หรือ C#) ส่วนฟังก์ชั่นที่ประกาศเพิ่มคือ __str__ จะเหมือนกับฟังก์ชั่น toString() ใน Java นั่นเอง

![](https://miro.medium.com/max/30/1*xt8c0x0VTKbxPDcBfqdZNA.png?q=20)

![](https://miro.medium.com/max/1301/1*xt8c0x0VTKbxPDcBfqdZNA.png)

![](https://miro.medium.com/max/30/1*eeNlsINlgXd08dG8sCSkPg.png?q=20)

![](https://miro.medium.com/max/1305/1*eeNlsINlgXd08dG8sCSkPg.png)




> [Source :](https://codeburst.io/%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%9E%E0%B8%B1%E0%B8%92%E0%B8%99%E0%B8%B2-web-application-%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%A0%E0%B8%B2%E0%B8%A9%E0%B8%B2-python-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-django-framework-38ce132ac706).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNTIyNzAyMDFdfQ==
-->