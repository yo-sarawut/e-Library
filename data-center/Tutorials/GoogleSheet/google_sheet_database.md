
วิธีการใช้ Google Sheets เป็นฐานข้อมูล
==

Google Sheets เป็นหนึ่งใน Google Apps ซึ่งเป็น Application Suite ของ Google ประกอบด้วย

![](https://lh3.googleusercontent.com/LCvRPOqvEDw0cB-CGm1onZ78Eov-T0TQKyi2MtfYynf0S0__Mh-IvD-kncuy1Dcdria19YL6kXikF6-9gbpcJP0fsd0zgLLy3VVXISlUyfs5XtcRUQBMtp8K5OPMXGcQ)

ในการใช้งานทั่วไป Google Apps สามารถตอบสนองการใช้งานได้เป็นอย่างดี แต่เมื่อต้องการทำกิจกรรมบางอย่างที่นอกเหนือไปจากการใช้งานพื้นฐาน ผู้ใช้สามารถพัฒนาเพิ่มเติมได้เอง ด้วย Google Apps Script

Google Apps Script เป็น Scripting Language ที่อยู่บนพื้นฐานของภาษา JavaScript สามารถใช้งานได้และพัฒนาต่อยอดได้ทันทีโดยไม่ต้องติดตั้งอะไรเพิ่มเติมอีกแล้ว สามารถเรียกใช้ Google Service ต่างๆได้มากมาย รวมถึง Google Sheets เพื่อสร้าง เมนูพิเศษ หรือ Macro เพื่อให้การทำงานที่ทำหลายๆขั้นตอนลดลงเหลือเพียงแค่คลิกเดียว อีกทั้งยังสามารถตั้งเวลาให้ทำงานอัตโนมัติ หรือ ตั้ง Trigger เพื่อให้ทำงานเมื่อเกิด Action ต่างๆได้อีกด้วย

Google Apps Script มี 3 ชนิด ได้แค่ Standalone, Bound to Google Apps และ Web App ซึ่งจะสามารถใช้งานร่วมกับ Google Sites ได้อีกด้วย (Sites Gadget) รายละเอียดสามารถอ่านเพิ่มเติมได้ที่  [Google Apps Script](https://developers.google.com/apps-script/)

ในที่นี้ จะแสดงตัวอย่างการประยุกต์ใช้ Google Apps Script แบบ Standalone เพื่อพัฒนาให้ Google Sheets ทำหน้าที่เป็นฐานข้อมูล และจะนำไปสู่การต่อยอดเป็น  [วิธีการใช้ Google Sheets เป็นระบบเฝ้าระวังเว็บไซต์ (Website Monitoring) จากภายนอกองค์กร](https://docs.google.com/a/psu.ac.th/document/d/1n2t9nYVcVUo2E9RtSfG4d15K98v2LSOfck2vzMhf3eQ/edit) เพื่อตรวจสอบระยะเวลาในการตอบสนอง ( Response Time) ของเว็บไซต์ ได้อีกด้วย

วิธีการใช้งาน Google Apps Script แบบ Standalone

1.  ใน Google Drive คลิก New > More > Connect more apps![](https://lh5.googleusercontent.com/ijiAGDa3aTwHGcRLyp5AA1bJYEfHXVUoKRF0PNKC0NKK1cokxckdUWYZXLopq0aXbIwHOLBl_KtIjzLMRndnHSE5UqboCuoVTRYD7gVaoZ6HIPN1FEwEGNORM02od9MT)

2.  ในชื่อ search ใส่คำว่า script แล้วกด Enter  
    จะพบ Google Apps Script แล้วกดปุ่ม Connect  
    ![](https://lh4.googleusercontent.com/c_xYkFC_o2Kpx7SzNlLg7BUfaEmbi7Ew7PnoPW0eQH37LCCbLewiprLtJbCiGzkfn3O5N6BGlSnEJk-b1WbxK87osqPbVAq7Ds64BeFfuqyeapkxfoJT-EXqWdNWyn6L)
3.  จากนั้น ใน Google Drive ให้คลิกที่ New > More > Google Apps Script  
    ![](https://lh4.googleusercontent.com/JLYpWjT0EgVRwDdb7YPTZGQrrtOpYk6WXHZYNoqeaf-MuOeopUFQLB72Us-km_WgHNojhPz3fuovNPzYUgBnZL3g2smmJtW8t3GocYTmoMs1lrjQ536cUl6uzW40fPfD)
4.  จากนั้นให้คลิก Close ได้เลย  
    ![](https://lh4.googleusercontent.com/TZSU87NzgN8jL2jRi4_9uDjB3gNMCZVn7AKSoutnqdNoWZDX_gXU1TjznKBJ92JQa88MC6f2UUiIBXTUbNMJ17Kjl788mZyyj_F-ZsznruEDho5rasCFxlOFwKDumHT5)
5.  จะได้พื้นที่โปรเจค (Project) ในการพัฒนา Google Apps Script โดยในแต่ละโปรเจคจะประกอบไปด้วยหลายๆไฟล์ Google Apps Script ได้  ![](https://lh3.googleusercontent.com/DAFIMfoNrfMoj7e_yPN2C2xP91IiCCmibucL1fNdz9y7LnhKqJaAKceAWAi7xFv0Lmw4lUSBqmO76AHH-T-lvZxxGl3TiBZ-7uJLfciczJGb1cAD-aHbWlXffAlRqGxi)

ในการพัฒนา Google Apps Script นั้น จะต้องเขียนในรูปแบบของฟังก์ชั่น (Function) เพื่อให้สะดวกในการใช้งานต่างๆ

ตัวอย่างเช่น มี Google Sheets อยู่ใน Google Drive ดังภาพ

![](https://lh5.googleusercontent.com/5iGLojQ-rKwex49cypFU17st8qcrYeQeRnzzIIHKfjKwBmKksVbLd2v3oXO5TTrd32sHYiVsaOW6tfbXelvbtNai216-JWR50I3GyyhCFjPbnTAecPTVQ9Hy6uKiZJgr)

มีรายละเอียดดังนี้

1.  ชื่อของ SpreadSheet คือ “ฐานข้อมูลของฉัน”
2.  ประกอบไปด้วย Sheet ชื่อ “Sheet1” และ “Log”
3.  มี URL คือ  
    https://docs.google.com/a/psu.ac.th/spreadsheets/d/1HJmyqiBYC_AEATmdUWakLgHFyYGqSqeqSA8xEw-8o-c/edit

ต่อไปเป็นขั้นตอนการเขียน Google Apps Script เพื่อติดต่อกับ Google Sheet ข้างต้น เพื่อเขียนข้อมูลลงไป โดยตั้งชื่อโปรเจคนี้ว่า ProjectMyDB ตั้งชื่อไฟล์ว่า SheetDB.gs และตั้งชื่อฟังก์ชั่น “editSheet” ดังภาพ

![](https://lh3.googleusercontent.com/ntjmnBA8f-yJMTlUq8_4J7__Mm3SejHfn5Mu-47UegL3Fz8OeVf6htOzrK4uAoQtntBIQXHt_dXj2iJV8JSVZt9SyOQea_hh80UyoG175-rsYNsZX5FnElUk-0ObCej5)

ขั้นตอนการทำงานของฟังก์ชั่น editSheet

1.  สร้างตัวแปร ss รับค่าจากการเปิด SpreadSheet จาก URL ข้างต้นด้วยคำสั่ง
```bash
var ss = SpreadsheetApp.openByUrl('https://docs.google.com/a/psu.ac.th/spreadsheets/d/1HJmyqiBYC_AEATmdUWakLgHFyYGqSqeqSA8xEw-8o-c/edit');
```

2.  สั่งให้ SpreadSheet ดังกล่าว Active ด้วยคำสั่ง
```bash    
    SpreadsheetApp.setActiveSpreadsheet(ss);
  ```  

3.  เนื่องจากในแต่ละ SpreadSheet ประกอบด้วยหลาย Sheet จึงต้องระบุว่า จะทำงานกับ Active Sheet ชื่อ “Sheet1” ด้วยคำสั่ง
    
    SpreadsheetApp.setActiveSheet(ss.getSheetByName("Sheet1"));
    

4.  สร้างตัวแปร activeSheet เพื่อกำหนดว่ากำลังทำงาน Active Sheet ด้วยคำสั่ง
    
    var activeSheet=ss.getActiveSheet();
    

5.  เมื่อต้องการเขียนค่า “Hello World” ลงใน Active Sheet ที่ Cell “C3” ใช้คำสั่ง
    
    activeSheet.getRange("C3").setValue("Hello World");
    

6.  หากต้องการเขียนค่าทีละหลายๆ Cell หรือเป็น Range ต้องสร้างข้อมูลชนิด Array 2 มิติขึ้นมา แล้วจึงเขียนค่าลงไป กรณีต้องการใส่ค่าในช่วง “A1:C1” ใช้คำสั่ง
    
    var values =[  ["คณกรณ์","หอศิริธรรม","'3720024"]  ];
    activeSheet.getRange("A1:C1").setValues(values);
    

7.  หากต้องการเขียนค่าในช่วง “A2:A4” ใช้คำสั่ง
    
    values = [ ["เกรียงไกร"],["หนูทองคำ"],["'4220020"] ];
    activeSheet.getRange("A2:A4").setValues(values);
    

8.  เมื่อจะเก็บข้อมูลจริงๆ วิธีการข้างต้นจะไม่สะดวก เพราะจะต้องทราบว่าแถวสุดท้ายแล้วเพิ่มค่าแถวไปทีละหนึ่ง ซึ่งสามารถใช้วิธีการ Append Row กล่าวคือเขียนค่าลงไปในแถวถัดจากแถวล่าสุดที่มีข้อมูลได้ ในตัวอย่างนี้ จะสลับไปใช้ Sheet ชื่อ “Log” แล้วใส่ค่าลงไปด้วยคำสั่ง
    
    SpreadsheetApp.setActiveSheet(ss.getSheetByName("Log"));
    activeSheet=ss.getActiveSheet();
    var timestamp = new Date();
    activeSheet.appendRow([timestamp, 200 , 300]);
    timestamp = new Date();
    activeSheet.appendRow([timestamp, 200 , 456]);
    

จากนั้น Save ข้อมูล แล้วสั่ง Run โดยเลือกฟังก์ชั่นชื่อ editSheet ดังภาพ  
![](https://lh4.googleusercontent.com/6SNGQ3vMuwGtm-53ZQq_hs2AvHwYcV0iEDaEme6sWVAviezX_gSAkEajV-n2Lv5cFq5mjjbVzyeRtPbxnxi3IL-TkljKRY1ElBgc3N2HMd3429zM4HEa8C89lAyhYxld)

ในการใช้งานครั้งแรก จะปรากฏหน้าต่าง Consent ขึ้นมาเพื่อขอสิทธิ์ในการเข้าใช้ไฟล์

ผลที่ได้จากการทำงานคือ

![](https://lh4.googleusercontent.com/sJBGWhnrF7WrJBtgM9nJhoZpbVf1YckUz9MCgpTZJOTsxFLsfUw1sISgrLd-eDmN7Dt9mEVOFMo12UK6d140lPSML0ZgomSecfA9rnIUru9zqHnA0EMW3w9J9U1mfte8)

และ

![](https://lh6.googleusercontent.com/BumIrm1mQ5AeBE9zVct0aZGB8dV4SqMVvHIRZpi5WHUISUtHJlukHWThjbnfZ1QLy7e9ErHA_ctRLonyNh7bbeeNLhLTAhXLWsypZ7AgEny5R3hmPn84cKIrVKQM8LCj)

จะเห็นได้ว่าสามารถใช้ Google Apps Script เพื่อเขียนค่าใน Google Sheets เพื่อเป็นฐานข้อมูลได้ และสามารถประยุกต์ใช้งานอื่นๆได้อีกมากมาย



> Reference : https://sysadmin.psu.ac.th/2014/10/10/googleappsscript-googlesheets-database/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwMjExNzUyMV19
-->