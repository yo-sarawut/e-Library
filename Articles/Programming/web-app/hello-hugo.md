Goodbye wordpress, Hello Hugo
===
![enter image description here](https://backendology.com/public/images/hugo.png)

สวัสดีครับ กลับมาอีกครั้งหลังจากหายไปไม่ได้เขียน Blog นานมากๆ กลับมาครั้งนี้มีการเปลี่ยนแปลงหลายอย่างครับ

ชื่อเว็บเปลี่ยนจากเดิม www.thitiblog.com เป็น thiti.dev แล้วในตอนนี้ และเปลี่ยนจากเดิมที่ใช้ Wordpress มาเป็น  [Hugo](https://gohugo.io/)  ก็จะมาเล่าให้ฟังว่า Hugo มันคืออะไร ดีอย่างไง ทําไมถึงหันมาใช้ Hugo

# [](https://thiti.dev/post/1/#hugo-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3)Hugo คืออะไร

Hugo(static site generator) เป็นเครื่องมือสําหรับสร้างเว็บ Page ที่เป็น Static file ล้วนๆ ไม่ต้องมี Database มีเฉพาะไฟล์ html, css, javascript, image ที่จริงก็มีอีกหลายเจ้า แต่ Hugo จะมีจุดเด่นในเรื่องของความเร็ว และความยืดหยุ่นในการใช้งาน

# [](https://thiti.dev/post/1/#hugo-%E0%B8%94%E0%B8%B5%E0%B8%AD%E0%B8%A2%E0%B9%88%E0%B8%B2%E0%B8%87%E0%B9%84%E0%B8%A3)Hugo ดีอย่างไร

-   เมื่อเป็นเว็บแบบ Static file ทำให้สามารถใช้ Static File Hosting ธรรมดาได้เลย ซึ่งจะมีราคาที่ถูก และบางที่ก็ฟรี
-   เนื่องจาก ไม่ต้องใช้ Database และไม่มีการประมวลผลในส่วนของ Backend เพียงแค่โยนไฟล์ออกไปเท่านั้น ทำให้เว็บเร็วมากๆ
-   ทำ SEO ได้ดียิ่งขึ้น เนื่องจากเป็นเว็บ แบบ Static file
-   หมดปัญหาเรื่องการโดน Hack เพราะเว็บทั้งเว็บเป็น Static file

# [](https://thiti.dev/post/1/#%E0%B8%82%E0%B9%89%E0%B8%AD%E0%B8%88%E0%B9%8D%E0%B8%B2%E0%B8%81%E0%B8%B1%E0%B8%94%E0%B8%82%E0%B8%AD%E0%B8%87-hugo)ข้อจํากัดของ Hugo

-   ไม่สามารถทําเว็บที่มีการเก็บข้อมูลได้ เนื่องจากไม่มี Backend และ Database
-   จะต้องมี Hugo ในเครื่องที่ต้องการแก้ไขหรือ เพิ่ม Content
-   เมื่อมีการ Update content จะต้อง Built ก่อนทําให้ Content จะไม่ถูก Update ในทันที

# [](https://thiti.dev/post/1/#%E0%B8%AA%E0%B8%A3%E0%B8%B8%E0%B8%9B-hugo-%E0%B9%80%E0%B8%AB%E0%B8%A1%E0%B8%B2%E0%B8%B0%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%AA%E0%B8%A3%E0%B9%89%E0%B8%B2%E0%B8%87%E0%B9%80%E0%B8%A7%E0%B9%87%E0%B8%9A%E0%B9%81%E0%B8%9A%E0%B8%9A%E0%B9%84%E0%B8%AB%E0%B8%99)สรุป Hugo เหมาะกับการสร้างเว็บแบบไหน

Hugo เป็น Tool สําหรับสร้างเว็บที่เป็น Static website ดังนั้นเว็บที่เหมาะจะเป็นเว็บประเภทเน้นให้บริการ Content เป็นหลัก เช่น Web blog, เว็บแนะนําสินค้า, โรงเรียน ส่วนใหญ่เว็บพวกนี้จะแสดงผลเพียงเนื้อหาอย่างเดียว อาจจะมีการ embedded forms ต่างๆ ได้ เช่น Facebook comment, Form ส่งเมล์ติดต่อสอบถาม, google analytic ฯลฯ จะง่ายในการใช้งาน และจัดการเป็นอย่างมาก

หลังจากที่ได้ลองเล่น ก็พบว่าเหมาะกับ Web blog ของผมเป็นอย่างมาก เพราะง่ายต่อการจัดการ ระบบไม่ซับซ้อนเกินความจําเป็นสําหรับเว็บที่เน้นนําเสนอข้อมูลเพียงอย่างเดียว และที่สําคัญเป็นมิดรกับ SEO ส่วนในเรื่อง Performance ก็ดีมากเพราะเป็น Static website เราสามารถนําเว็บของเราไปวางที่ Host ไหนก็ได้ ราคาถูก หรือไม่ก็ฟรี อย่างเช่น Google firebase hosting, netlify ฯลฯ ตอนนี้ผมจึงย้ายมาใช้งาน Hugo เป็นที่เรียบร้อย :) ถ้าท่านทําลังมองหาหรือ จะทํา Website ประเภทนี้อยู่ ก็เป็นตัวเลือกที่ดีเลยครับ



>  [Source](https://thiti.dev/post/1/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgwOTE2MTMwN119
-->