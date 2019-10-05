
24 เคล็ดลับ การใช้งาน Python
===

Python เป็นอีกหนึ่งภาษา Programming ที่ได้รับความนิยม ถูกนำไปใช้ในการเขียน Program ได้หลากหลายประเภท โดยไม่ได้จำกัดอยู่ที่งานเฉพาะทางใดทางหนึ่ง ไม่ว่าจะเป็นการพัฒนา Web หรือด้าน Data Science และ Machine Learning เป็นต้น จึงทำให้มีการนำไปใช้กันอย่างแพร่หลาย วันนี้เรามาดู 24 เคล็ดลับ การใช้งาน Python ที่จะช่วยให้คุณประหยัดเวลาและทำงานได้สะดวกขึ้น โดยดูตัวอย่างการใช้งานในแต่ละหัวข้อกันได้เลย

## **1. Unpacking Array Items**

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/01.png)(http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/01.png)

## **2. Swapping Variables**

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/02.png)(http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/02.png)

**3. Profile And Stats Of Your Code**

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/03.png)(http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/03.png)

**4. Repeat String**

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/04.png)(http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/04.png)

**5. Slicing**

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/05.png)(http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/05.png)

**6. Reversing**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/06.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/06.png)

**7. Negative Index**

ถ้าคุณต้องการที่จะเริ่มต้นจาก Character ตัวสุดท้าย สามารถใช้ Negative Index ได้

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/07.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/07.png)

**8. Intersect Sets**

กรณีต้องการดึงสมาชิกที่ซ้ำกันของทั้ง 2 Sets

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/08.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/08.png)

**9. Difference In Sets**

กรณีต้องการดึงสมาชิกของ Set ที่ไม่เป็นสมาชิกของอีก Set หนึ่ง (ในตัวอย่างนี้ ต้องการดึงสมาชิกของ a ที่ไม่ซ้ำกับสมาชิกของ b)

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/09.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/09.png)

**10. Union Of Collections**

กรณีต้องการดึงสมาชิกทั้งหมดของทั้ง 2 Sets

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/10.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/10.png)

**11. Optional Arguments**

เราสามารถส่งผ่าน Optional Argument โดยระบุค่า Default ให้กับ Argument ได้:

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/11.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/11.png)

**12. Unknown Arguments Using**  ***arguments**

หาก Function ของคุณสามารถรับ Argument จำนวนเท่าใดก็ได้ ให้เพิ่ม * ไว้ที่ด้านหน้าของชื่อ Parameter:

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/12.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/12.png)

**13. Dictionary As Arguments Using**  ****arguments**

จะช่วยให้คุณสามารถส่งผ่านจำนวน Keyword Arguments ที่แตกต่างกันไปยัง Function  
นอกจากนี้ คุณยังสามารถส่งผ่านค่า Dictionary เป็น Keyword Arguments ได้:

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/13.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/13.png)

**14. Function With Multiple Outputs**

ใช้ในกรณีที่ Function ต้องการ Return Outputs หลาย ๆ ค่า:

![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/14.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/14.png)

**15. One Liner For Loops**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/15.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/15.png)

**16. Combining Lists Using Zip**

-   ใช้หลาย ๆ Collection แล้ว Return เป็น Collection ใหม่
-   Collection ใหม่ จะมี Items ที่แต่ละ Item ประกอบด้วย 1 Element จากแต่ละ Collection ที่ถูก Input เข้ามา
-   ช่วยให้เราสามารถ Transverse ได้หลาย Collection ในเวลาเดียวกัน

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/16.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/16.png)

**17. Free up Memory**

เราสามารถเคลียร์หน่วยความจำ (Garbage Collection) แบบ Manual ได้ตามต้องการ

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/17.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/17.png)

**18. Using Decorators**

-   Decorators สามารถเพิ่ม Function การทำงานให้กับ Code ได้ มันเป็น Function ที่เรียก Object / Function อื่น ๆ ด้วยเหตุนี้ พวกมันจึง Return Object ที่จะถูกเรียกใช้ในภายหลังจากที่ Decorated Function ถูก Invoked
-   Decorates ก็เปรียบเหมือนการใช้แนวคิดของ Aspect-Oriented Programming
-   เราสามารถ Wrap Class/Function จากนั้น Code นั้นจะถูก Executed เมื่อใดก็ตามที่ Function ถูกเรียกใช้

_(ตัวอย่างนี้ แสดงถึงวิธีการ_ _Print ชื่อ Function นี่เป็นเพียงตัวอย่าง Code เพื่อแสดงให้เห็นถึงวิธีที่คุณสามารถเรียกใช้ Decorator คุณสามารถใช้ Decorator เพื่อเรียก Loggers ของคุณ, perform security operations เป็นต้น)_

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/18_1.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/18_1.png)

และเมื่อเราใช้มันใน Function จะเป็นลักษณะดังนี้:

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/18_2.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/18_2.png)

**19. Unzipping**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/19.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/19.png)

**20. Joining Collection**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/20.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/20.png)

**21. Memory Footprint Of An Object**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/21.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/21.png)

**22. Print Current Directory**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/22.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/22.png)

**23. Print Imported Modules**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/23.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/23.png)

**24. Get Current Process Id**

[![](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/24.png)](http://images.techstarthailand.com/images/blog/Article2019/TopPythonTips/24.png)

**ที่มา:** [**_https://medium.com/_**](https://medium.com/fintechexplained/top-python-tips-tricks-dd996b807865)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1ODExMjg2OV19
-->