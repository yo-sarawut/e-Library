# 10 Tips & Tricks ที่ช่วยให้คุณใช้งาน Python ได้รวดเร็วขึ้น

![enter image description here](https://revelwood.com/wp-content/uploads/2019/09/header-blog-tips-53019141.jpg)

ภาษา Python ถือเป็นภาษา Programming ที่มีการใช้งานเติบโตขึ้นอย่างรวดเร็ว แม้แต่ Netflix, IBM รวมทั้งอีกหลายแห่งก็ใช้ Python ในบทความนี้จึงมาบอกถึง 10 Tips & Tricks ที่ช่วยให้คุณใช้งาน Python ได้รวดเร็วขึ้น มาให้ได้เรียนรู้กัน

**1. Concatenating Strings**

เมื่อคุณต้องการเชื่อมต่อ\(Concatenate\) List ของ Strings คุณสามารถทำได้โดยใช้ For Loop โดยเพิ่มเข้าไปทีละ Element แต่อย่างไรก็ตาม วิธีนี้อาจจะไม่ค่อยมีประสิทธิภาพมากนัก โดยเฉพาะถ้า List นั้นยาวมาก ๆ ใน Python นั้น String ถือเป็น Immutable ดังนั้น String ด้านซ้ายและขวา จะถูก Copy ไปยัง String ใหม่ด้วยสำหรับการ Concatenate แต่ละครั้ง

วิธีที่ดีกว่าการใช้ For Loop ก็คือ การใช้ฟังก์ชั่น _**join\(\)**_ ดังที่แสดงด้านล่าง:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Concatination.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Concatination.png)

**2. ใช้** **List Comprehensions**

List Comprehensions ถูกใช้สำหรับการสร้าง List ใหม่จาก iterables อื่น ๆ เมื่อ List Comprehensions ทำการ Return Lists, พวกมันประกอบด้วย วงเล็บ \(Brackets\) ที่บรรจุ Expression ซึ่งจะถูก Execute สำหรับแต่ละ Element ไปพร้อมกับ For Loop เพื่อ Iterate แต่ละ Element การที่ List Comprehensions ใช้งานได้เร็วกว่า ก็เพราะมันจะถูกปรับให้เหมาะสำหรับ Python Interpreter ซึ่งจะทำให้เห็นถึง Pattern ที่คาดเดาได้ในระหว่างการวน Loop

จากตัวอย่างนี้ เป็นการให้หา ค่ายกกำลัง 2 ของตัวเลข 5 ตัว โดยใช้ List Comprehensions

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ListComprehension01.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ListComprehension01.png)

ในตัวอย่างนี้ เราจะมาหาตัวเลขที่ซ้ำกันจาก 2 Lists โดยใช้ List Comprehensions

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ListComprehension02.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ListComprehension02.png)

**3. Iterate ด้วย enumerate\(\)**

Enumerate\(\) Method จะเพิ่มตัว Counter เข้าไปยัง iterable และ Return พวกมันกลับมาในรูปแบบของ Enumerate Object

คราวนี้ เราลองมาแก้ปัญหาของ [Fizz Buzz Problem](https://en.wikipedia.org/wiki/Fizz_buzz) กันดู โดยเขียน Program ที่ Print ตัวเลขใน List ออกมา โดยหากตัวเลขนั้นหารด้วย 3 ลงตัวให้ Print คำว่า “fizz” แทนที่ตัวเลขนั้น หากหาร 5 ลงตัวให้ Print คำว่า “buzz” และหากตัวเลขใดหารทั้ง 3 และ 5 ลงตัวให้ Print คำว่า “fizzbuzz” ออกมา

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/IterateWithEnumerate.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/IterateWithEnumerate.png)

**4. ใช้** **ZIP เมื่อต้องทำงานกับ Lists**

สมมติว่า คุณได้รับมอบหมายงานให้รวมหลาย ๆ Lists ที่มีความยาวเท่ากันเข้าด้วยกัน และ Print ผลลัพธ์ออกมา และการใช้ _**zip\(\)**_ ก็เป็นวิธีที่ดีกว่าที่จะได้ผลลัพธ์ที่ต้องการ ดังที่แสดงใน Code ด้านล่าง:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Zip.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Zip.png)

**5. ใช้** **itertools**

Python itertools Module เป็นหนึ่งใน Tools ที่ใช้สำหรับจัดการกับ Iterators โดย itertools มีเครื่องมือหลายอย่างสำหรับการสร้าง iterable Sequences ของ Input Data iterable ในที่นี้จะขอใช้ _**itertools.combinations\(\)**_ เป็นตัวอย่าง โดย _**itertools.combinations\(\)**_ จะถูกใช้สำหรับการสร้าง Combinations ซึ่งยังเป็นการรวมกลุ่มที่เป็นไปได้ทั้งหมดของ Input Values

ขอยกตัวอย่าง ที่ใช้กันจริง ๆ เพื่อทำให้ประเด็นข้างต้นชัดเจนยิ่งขึ้น โดยสมมติว่า มีทีม 4 ทีมที่แข่งขันกันอยู่ และทุกทีมจะทำการแข่งขันกับทีมอื่นที่เหลือ งานของคุณก็คือ การสร้างความเป็นไปได้ทั้งหมดที่แต่ละทีมจะทำการแข่งขันกัน

ลองดูที่ Code ด้านล่าง:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Itertool.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/Itertool.png)

สิ่งสำคัญที่ควรสังเกตคือ ลำดับของค่า นั้นไม่สำคัญ เนื่องจาก \('Team 1', 'Team 2'\) และ \('Team 2', 'Team 1'\) ถือว่ามีความหมายเหมือนกัน ดังนั้นจะทำการแสดงเพียงหนึ่งครั้งเท่านั้นใน Output และในทำนองเดียวกัน เราสามารถใช้ _**itertools.permutations\(\)**_ ได้เช่นเดียวกันกับฟังก์ชั่นอื่น ๆ จาก Module

**6. ใช้** **Python Collections**

Python Collections เป็น Container Data Types ไม่ว่าจะเป็น Lists, Sets, Tuples, Dictionary ซึ่ง Collections Module ได้จัดเตรียม Datatypes ที่มีประสิทธิภาพสูงเอาไว้ให้แล้ว มันสามารถช่วยปรับปรุงให้ Code ของคุณสามารถทำทุกอย่างได้ง่ายขึ้นและ Clean ยิ่งขึ้น แถมยังมีฟังก์ชั่นมากมายให้ใช้ เพื่อให้เห็นภาพชัดเจนยิ่งขึ้น จะขอยกตัวอย่างในการใช้ฟังก์ชัน _**Counter\(\)**_

ฟังก์ชัน _**Counter\(\)**_ จะรับ iterable เข้ามา \(เช่น List หรือ Tuple\) แล้วทำการ Return Counter Dictionary กลับมา โดย Key ของ Dictionary จะเป็น Element ที่ไม่ซ้ำกันที่มีอยู่ใน iterable และค่าของแต่ละ Key จะนับจำนวนของ Element ที่มีอยู่ใน iterable

ในการสร้าง Counter Object ให้ส่งผ่านฟังก์ชัน iterable\(list\) ไปยังฟังก์ชั่น Counter\(\) ตามที่แสดงใน Code ด้านล่างนี้

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonCollection.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonCollection.png)

**7. Convert 2 Lists ไปยัง Dictionary**

สมมติว่าเรามี List อยู่ 2 Lists โดย List แรกประกอบด้วย ชื่อของนักเรียน ส่วน List ที่สองประกอบด้วย คะแนนที่พวกเขาทำได้ เรามาดูกันว่า จะสามารถแปลงจากทั้ง 2 List ไปเป็น Dictionary เดียวได้อย่างไร เราสามารถใช้ฟังก์ชั่น zip ในการทำสิ่งนั้นได้โดยใช้ Code ตามที่แสดงอยู่ด้านล่างนี้:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ConvertList.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ConvertList.png)

**8. ใช้** **Python Generators**

ฟังก์ชั่น Generator จะช่วยให้คุณสามารถ Declare ฟังก์ชั่นที่ทำงานเหมือน iterator ซึ่งมันอนุญาตให้ Programmer สามารถสร้าง iterator ได้อย่างรวดเร็ว, ง่าย และ Clean ขอยกตัวอย่างเพื่ออธิบายแนวคิดนี้ให้ชัดเจนขึ้น โดยสมมติว่า คุณต้องการหาผลรวมของ ค่ายกกำลังสอง ของตัวเลขตั้งแต่ 1 - 100000000

มันดูง่ายใช่ไหม? คุณสามารถทำสิ่งนี้ได้โดยใช้ List Comprehension แต่ปัญหาก็คือ มันเป็น Input ที่มีขนาดใหญ่มาก จากตัวอย่างนี้ ลองดูที่ Code ด้านล่าง:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonGenerator01.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonGenerator01.png)

ในการบวกจำนวนที่เราต้องการเข้าไปเรื่อย ๆ เราควรตระหนักว่า วิธีนี้ดูจะเป็นไปได้ยากเนื่องจากต้องใช้เวลาในการคำนวณสูง เพราะเหตุนี้เอง Python Generators จึงถูกสร้างขึ้นมาเพื่อแก้ไขปัญหานี้ ด้วยการแทนที่ “\[ \]” ด้วย “\( \)” เราก็จะเปลี่ยน List Comprehension เป็น Generator Expression แล้ว ตอนนี้เรามาคำนวณเวลากันใหม่:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonGenerator02.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/PythonGenerator02.png)

คุณจะเห็นว่า เวลาลดน้อยลงไป และมันจะยิ่งเห็นได้เด่นชัดยิ่งขึ้นสำหรับ Input ที่มีขนาดใหญ่มาก ๆ

**9. Return ค่าหลาย ๆ ค่าจาก Function**

Python มีความสามารถในการ Return ค่าได้หลายค่า \(Multiple Values\) จากการเรียกใช้ฟังก์ชั่น ในกรณีนี้ค่าที่ Return กลับมาควรเป็น List ของค่าที่คั่นด้วยเครื่องหมายจุลภาค \( , \) และจากนั้น Python จะสร้าง Tuple และ Return ค่านี้ให้กับ ตัวที่เรียกใช้มัน ดังตัวอย่างที่แสดงด้านล่าง:

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ReturnMiltipleValue.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/ReturnMiltipleValue.png)

**10. ใช้ฟังก์ชั่น** **sorted\(\)**

เมื่อพูดถึงการเรียงลำดับ \(Sort\) ใน Python ถือเป็นเรื่องที่ทำได้ไม่ยาก เพราะสามารถใช้ Built-in Method Sorted\(\) ที่จะช่วยทำสิ่งเหล่านั้นให้คุณ โดย _**sorted\(\)**_ จะทำการเรียงลำดับ \(ไม่ว่าจะเป็น List, Tuple\) และจะ Return List ที่ Element ถูกเรียงลำดับแล้วเสมอ ขอยกตัวอย่างการ Sort List ของตัวเลข จากน้อยไปมาก

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/SortFunction01.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/SortFunction01.png)

ลองอีกตัวอย่าง เป็นการ Sort List ของ String จากมากไปน้อย

[![](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/SortFunction02.png)](http://images.techstarthailand.com/images/blog/Article2020/10PythonTipsTricks/SortFunction02.png)

_**ที่มา**_**\*\***_:_ **\[**[https://towardsdatascience.com/](https://towardsdatascience.com/)\*\*\]\([https://towardsdatascience.com/10-python-tips-and-tricks-you-should-learn-today-a05c23a39dc5](https://towardsdatascience.com/10-python-tips-and-tricks-you-should-learn-today-a05c23a39dc5)\)

> [Source : ](https://www.techstarthailand.com/blog/detail/10-Python-Tips-and-Tricks-You-Should-Learn-Today/1205?fbclid=IwAR0PwneIt4WJb1FDvLBPMXq-Qs_Ek1OHJfjAyUMA3iaXfRD9DLhJNf4PKHI).

