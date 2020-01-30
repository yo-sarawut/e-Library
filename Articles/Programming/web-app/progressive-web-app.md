Progressive Web App คืออะไร และ มาลองกันแบบง่ายๆ วันเดียวเสร็จ
===
[Source:](https://medium.com/@timeff/%E0%B9%82%E0%B8%AD%E0%B9%89%E0%B9%80%E0%B8%A2-progressive-web-app-%E0%B8%A1%E0%B8%B2%E0%B8%A5%E0%B8%AD%E0%B8%87%E0%B9%81%E0%B8%9A%E0%B8%9A%E0%B8%87%E0%B9%88%E0%B8%B2%E0%B8%A2%E0%B9%86-%E0%B8%A7%E0%B8%B1%E0%B8%99%E0%B9%80%E0%B8%94%E0%B8%B5%E0%B8%A2%E0%B8%A7%E0%B9%80%E0%B8%AA%E0%B8%A3%E0%B9%87%E0%B8%88-b7a2be52ae5b)

![enter image description here](https://miro.medium.com/max/1440/1*fgLCG_rSLORMz3aVuJEe5w.jpeg)

ฮัลโหลๆ สวัสดีครับ ช่วงนี้หายไปนาน แอบไปศึกษา Front-end framework อยู่หลายตัว จนไปเจอกับของเล่นใหม่เรียกว่า Progressive Web App หรือเรียกสั้นๆว่า PWA นั่นเอง ซึ่งประจวบเหมาะกับทาง Google ผู้ผลักดันเทคโนโลยีนี้ก็ได้มา Roadshow แสดงความเทพที่กรุงเทพกันไปหยกๆ ก็เลยถือโอกาสใช้พลังความมั่วส่วนตัว ขอมาเขียนเรื่องนี้ ดีไม่ดี ผิดพลาดตรงไหน ติชมได้เน่อ เริ่มกันเลย …

> บทความนี้เกิดจากเนื้อหาหลายๆส่วนจากทั้งในงาน Roadshow เอง รวมถึงการมั่วซั่วของผู้เขียนนะครับ ดู Reference ได้ท้ายบทความ

# หัวข้อในวันนี้

1.  อะไรคือ PWA
2.  ทำไมต้อง PWA
3.  เบื้องหลังการทำงานของ PWA เป็นอย่างไร
4.  มาลองทำ PWA เล่นๆกันดู

# อะไรคือ เจ้า Progressive Web App ?

![](https://miro.medium.com/max/30/1*NgXhx6T6gx6YrbCTD0oB3w.png?q=20)

![](https://miro.medium.com/max/3440/1*NgXhx6T6gx6YrbCTD0oB3w.png)

Source:  [http://www.letsnurture.com/blog/progressive-web-app-an-application-in-a-webpage.html](http://www.letsnurture.com/blog/progressive-web-app-an-application-in-a-webpage.html)

เจ้านี่คือเทคโนโลยีที่จะทำให้เว็บของเราเนี่ย มีความใกล้เคียงกับ App ในมือถือมากขึ้น ทั้งความลื่นไหลในการใช้งาน, เข้าเมนูต่างๆอย่างง่ายดาย, การใช้งานเมื่ออยู่ใน Mode Offline, การทำ Push Notification ฯลฯ ในขณะเดียวกันก็เก็บข้อดีของเว็บไว้อาทิเช่น ความสดใหม่ของข้อมูล(อัพเดทกันได้ทันที ไม่ต้องไปอัพ App Store), ความเข้าถึงง่ายไม่ต้อง Install ให้ยุ่งยาก

แหม่ ดีอย่างงี้ จะให้อธิบายก็ไม่สู้ลองเล่นดูเอง ใครใช้ Android ขอให้หยิบมาถือขึ้นมาแล้วเข้าไปที่ aliexpress.com กันเลยครับ

วิธีลงเจ้า PWA นี่ก็ง่ายๆ แค่อยู่ในหน้าเว็บแล้วกด Add To Home Screen….



![](https://miro.medium.com/max/250/1*vYfQT43mgPfSv_IOCo4GJg.jpeg)

**เรียบร้อย!** ท่านได้ลง Progressive Web App ลงเครื่องของท่านแล้วครับ

ทีนี้พอเราลองไปที่หน้า Homescreen ก็จะพบว่ามี Icon ของ Aliexpress สีแดงๆอยู่ ให้ท่านผู้อ่านลองกดเข้าไปปุ้ป ก็จะเห็นหน้า Splash Screen เก๋ๆ เป็นรูปโลโก้ App และ Background สีแดงฉาน เต็มจอ เก๋ๆ ตรงนี้เราก็จะเข้า App มาละครับ สังเกตว่าจะเป็น Feeling แบบ App ที่เราใช้กันเลย ไม่มี Address Bar ให้ยุ่งยาก รวมถึงสามารถกด Hamburger เมนูหรือไอ้เจ้าขีดสามขีดตรงซ้ายบน ให้โชว์เมนูออกมาได้อย่างสวยงาม

![](https://miro.medium.com/max/30/1*5faniMyOjNKR6EgLN_Hovw.png?q=20)

![](https://miro.medium.com/max/1000/1*5faniMyOjNKR6EgLN_Hovw.png)

Aliexpress.com

**ถ้าคิดว่าหมดแค่นี้…** ให้ทุกท่านลองปิดอินเตอร์เน็ตในมือถือดู แล้วเข้า App อีกทีครับผม… แต่น แต๊นนน สังเกตได้ว่าแอพยังทำงานได้ เมนูต่างๆยังอยู่ครบ เลยใช่ไหมครับ

นี่แหล่ะครับ PWA ที่เราจะพูดถึงกันในวันนี้ ซึ่งเรียกได้ว่าเป็นความพยายามแก้ปัญหา Post-App Era จากฝั่งค่าย​ Google นั่นเอง

# ทำไมต้อง PWA ? (Post-App Era กับความพยายามของ Google)

Section นี้ขอสรุปในแบบของผมจาก Keynote ในงานวัน Progressive Web App Roadshow ที่กรุงเทพนะครับ



![](https://miro.medium.com/max/607/1*rBrC06UDVTMwuVbdy78KbA.png)

Source: Progressive Web App Roadshow 2016

เรื่องมันมีอยู่ว่า จากการวิจัยของ  _comScore Mobile Metrix_ พบว่าในปัจจุบัน ค่าเฉลี่ยของการโหลดแอพใหม่ลงมือถือต่อเดือนมันอยู่ที่ 0 แล้วจริงๆ ลองคิดง่ายๆครับว่าในมือถือที่เราใช้กันอยู่ เดือนๆนึงโหลดอะไรมาเพิ่มบ้าง รวมถึงใช้กันจริงๆ ทุกวันเนี่ยกี่แอพกัน (ในงานวิจัยบอกว่า 80% ของเวลาที่ใช้มือถือ ใช้อยู่แค่ 3 แอพหลักๆ เท่านั้นเอง)

ในขณะที่มาดูข้อมูลการใช้งานเว็บไซต์ พบว่าผู้ใช้มือถือในหนึ่งเดือน เข้าเว็บไซต์ต่างๆกว่า 100 เว็บไซต์ Google เลยบอกว่าปล่อยไว้อย่างงี้ไม่ได้ละ จึงปิ๊งไอเดีย จะมายกเครื่องเว็บไซต์ของเรากัน ภายใต้แนวคิด…



![](https://miro.medium.com/max/593/1*3YW_iMX9BZExFmN1s04kmg.png)

Source: Progressive Web App Roadshow 2016

1.  Reliable - ไม่ใช่กดเปิด App ขึ้นมาแล้วเจอ Downasaur (ชื่อเล่นของตัวไดโนเสาร์ ที่เรามักเจอใน Chrome เวลาเน็ตขัดข้อง) ต้องทำงานได้แม้ในโหมด Offline
2.  Fast - มีงานวิจัยออกมาว่า Users กว่า 53% ถอดใจที่จะเข้าเว็บ หากเว็บใช้เวลาโหลดเกิน 3 วินาที ดังนั้นต้องทำไงก็ได้ ให้กดปุ้ปติดปั้ป พร้อมใช้งาน
3.  Engaging-แบ่งออกเป็น 3 หัวข้อย่อยๆ ได้แก่  
    3.1) Homescreen เข้าถึงง่าย สามารถกด Icon App ได้จาก Home screen  
    3.2) Immersive นักพัฒนาสามารถควบคุม Experience ของ User กำหนด รูปแบบหน้าตาของ App ว่าจะมี Address Bar ไหม เอาแนวตั้งแนวนอนได้  
    3.3) Notification อันนี้หล่อ คือสามารถ Push Notification ให้ User ได้แบบ App เลยนั่นเอง

# เบื้องหลังการทำงานของ PWA

ในการทำให้เว็บของเราเป็น PWA นั้น ผมขอแบ่งพระเอกออกเป็น 2 คนหลักๆครับคือ ServiceWorker กับ Manifest.json

1.  **ServiceWorker**



![](https://miro.medium.com/max/770/1*9-3hRYImNd7E-BGEyPuXvA.png)

Source: Progressive Web App Roadshow 2016

ServiceWorker หรือ SW เอาง่ายๆคือไฟล์ Cilent-side proxy ที่เราเขียนขึ้นมาด้วย JavaScript นี่แหล่ะครับ พอ Users เข้ามาเว็บเรา เราก็จะทำการ Install เจ้า SW นี่ลงไปในเครื่องของ User คนนั้นๆ

**หน้าที่ของ SW** ก็คือ กำหนดให้ Cache สิ่งต่างๆที่เราจำเป็นในเว็บของเราไว้ ซึ่งเราก็กำหนดได้ว่าจะให้ Cache ส่วนไหน ไม่ Cache ส่วนไหน



![](https://miro.medium.com/max/1249/1*zK795muTXWsQefMlUDWcTw.png)

Source:  [https://developers.google.com/web/fundamentals/getting-started/codelabs/your-first-pwapp/](https://developers.google.com/web/fundamentals/getting-started/codelabs/your-first-pwapp/)

ง่ายๆ ให้ลองมองเป็น App ครับ เราอาจจะบอกให้ SW แคช Header, ปุ่มต่างๆ ของเราไว้ เพื่อให้ครั้งต่อไปที่เข้าเว็บไม่ต้องเสียเวลามานั่งโหลดเจ้า Element เหล่านั้นใหม่ แต่ในส่วนเนื้อหาเนี่ยให้ไม่ต้องแคช ให้ดึงออกมาใหม่ทุกครั้ง หรือจะบอกให้ใช้ Strategy ต่างๆเช่น Cache Then Network คือ เข้าเว็บมาให้ดึงเนื้อหาจาก Cache ที่เก็บไว้ก่อน พอ Network โหลดเสร็จค่อยเอาเนื้อหาใหม่มา Re render เข้าไปอีกที

ซึ่งเจ้าตัวนี้ก็จะทำให้เว็บไซต์ของเราทำงานเร็วขึ้นปรู๊ดปร๊าด ผิดหูผิดตา รวมถึงสามารถทำงานในโหมด Offline ได้ด้วย เนื่องจากเรา Browser สามารถไปดึง Element บางส่วนที่เรากำหนดไว้จาก Cache มาใช้งานได้เลย (ลองเล่นตัวนี้ดูครับ  [https://airhorner.com/](https://airhorner.com/)  ทำงานได้ Offline เต็มรูปแบบเลย)



![](https://miro.medium.com/max/818/1*zDoTrUR1cTOQT3chmQqMRg.png)

Source: Progressive Web App Roadshow 2016

**ไม่หมดเพียงแค่นั้นครับ** อีกหนึ่งหน้าที่ที่สำคัญมากๆ ของ SW คือการทำ Push Notification นั่นเอง เนื่องจากเจ้า SW เนี่ยแม้เราทำการปิด Browser ของเราไปแล้ว แต่ OS ก็สามารถทำการปลุก SW ออกมาทำงานได้ ซึ่งก็ทำให้เราสามารถเขียน Code เพื่อรับ Message ที่ส่งมาได้

**2. Manifest.json**



![](https://miro.medium.com/max/1440/1*vaOPvP8lMkhnOdAcYQ181Q.jpeg)

Source:  [https://addyosmani.com/blog/getting-started-with-progressive-web-apps/](https://addyosmani.com/blog/getting-started-with-progressive-web-apps/)

เจ้าตัวนี้เป็นไฟล์ JSON เล็กๆที่เราใส่เข้าไปใน head ของ html ครับ หน้าที่ของมันมีมากมายอาทิเช่น

-   ทำให้เว็บของเรามี Icon สวยๆบน หน้า Home screen เมื่อ Users กด Add to homescreen เว็บของเรา
-   สามารถเปิดเว็บแบบ Full screen mode ไม่มี Address bar เมื่อ Users กดเข้ามาจากหน้า Homescreen
-   ควบคุมมุมมองแนวตั้ง แนวนอน ของ Users ได้
-   ระบุ สี และ Icon ที่จะใช้มาประกอบเป็น Splash screen (หน้าจอ ตอนกดแอพขึ้นมา ลองดูรูปข้างบนครับ อันขวาสุด)

**สำคัญอีกเรื่องเกือบลืมคือเว็บไซต์ของคุณจะใช้งานพวก Service Worker ได้จำเป็นต้องมี HTTPS นะครับ เรียกได้ว่าจะให้พลังที่ยิ่งใหญ่ไปเล่นกับเครื่อง Users ได้ขนาดนั้น เราก็ต้องรับผิดชอบชีวิต ทรัพย์สินเขาให้เรียบร้อย ไม่ใช่โดนดักตีหัวระหว่างทางนะครับ (เดี๋ยวนี้มี Cloudflare, Firebase ให้ลองเล่นกันฟรีๆแล้วนะครับ ซึ่งทำให้เราไปลองทำ HTTPS กันแบบฟรีๆแล้วนะครับ)**


# มาลองทำ PWA เล่นๆกันดู

เอาหล่ะ ถึงเวลามาลองทำเล่นกันดูแล้ว ในส่วนนี้ผมจะขอเรียบเรียงมาจาก[CodeLab](https://codelabs.developers.google.com/codelabs/your-first-pwapp/index.html)  ในวันงาน PWA RoadShow ของทาง Google นะครับ ละก็จะมีเสริมเติมแต่งไปบ้างประปรายตามทาง

1.  **ดาวน์โหลด Source Code, ติดตั้ง Web Server**

ตอนนี้ให้ทุกคนไปโหลด Source Code เบื่องต้นมากันก่อนครับที่  [https://github.com/googlecodelabs/your-first-pwapp/archive/master.zip](https://github.com/googlecodelabs/your-first-pwapp/archive/master.zip)  ได้เลย เมื่อ Unzip ออกมาจะได้ your-first-pwapp-master ออกมา สำหรับวันนี้เราจะเริ่มกันที่โฟลเดอร์ work นะครับ เป็นไฟล์ตั้งต้นของเรา

![](https://miro.medium.com/max/30/1*WZe1eNXoGuONwtmkoCwwPA.png?q=20)

![](https://miro.medium.com/max/582/1*WZe1eNXoGuONwtmkoCwwPA.png)

จากนั้นให้ทุกคนไปลง Web Server ให้เรียบร้อยก่อน Google ก็ให้ Tool ง่ายๆมา ลองเล่นได้ทาง  [https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en)



![](https://miro.medium.com/max/1226/1*1VA6orskiuy7ebnYgpR4QA.png)

Source: Progressive Web App Roadshow 2016

พอรันขึ้นมาก็กด Choose Folder เลือกโฟลเดอร์ work ของเรา แล้วกด Web Server URL(s) เข้าไปดูกันได้เลยครับ

**2. มาดูโครงสร้าง App ของเรากันหน่อย**



![](https://miro.medium.com/max/189/1*XH8wUS_k-hw9tGZTVBsFsA.png)

สำหรับ App ตัวนี้ก็เป็น Single Page App ที่แสดงข้อมูลสภาพอากาศจาก API ของ yahoo แบบง่ายๆครับ โดยมีไฟล์ JavaScript หลักคือ app.js นั่นเอง (JavaScript Plainๆจริง document.querySelector ไม่เจอกันตั้งนาน 555) ซึ่งก็จะมีโครงสร้างหลักๆดังนี้

**[Object] app**  เป็น Object หลักที่เก็บข้อมูลสำคัญของ App นี้ เออเกือบลืม เขาใช้ Pattern JavaScript แบบนึงเรียกว่า IIFE (immediately-invoked function expression) นะครับ ซึ่งมันจะทำให้ตัวแปรหรือ Function ที่เราประกาศข้างในเนี่ยไม่ไปรบกวน Environment Context อื่นๆ (เห็นมีพี่ท่านนึงเขียน รายละเอียดไว้  [ที่นี่](https://www.algorithmtut.com/javascript-design-pattern-%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%84%E0%B8%B8%E0%B8%93%E0%B8%95%E0%B9%89%E0%B8%AD%E0%B8%87%E0%B9%84%E0%B8%A7%E0%B9%89%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%97%E0%B8%B3%E0%B8%87/)  ครับ) ตรงนี้น่าศึกษาๆ

**Listener สองตัว** สำหรับปุ่ม Refresh กับ เพิ่มเมือง

**[Function] updateForecaseCard** ฟังก์ชันที่ทำหน้าที่เอาข้อมูลที่ได้จาก API มาแสดงผลบน Card ครับ

**[Function] getForecast** ฟังก์ชันที่ทำการดึงข้อมูลจาก API Endpoint ออกมา

**[Function] updateForecast** ฟังก์ชันที่ทำการ Loop เช็คการ์ดต่างๆแล้วสั่ง getForecast เพื่ออัพเดทข้อมูลสภาพอากาศ

**[Object] initialWeatherForecast** ข้อมูลเบื้องต้นที่เราจะใส่ไปหลอกๆ เป็นตัวตั้งต้นให้โปรแกรมแสดงผลออกมา

ทีนี้ขอให้ทุกท่านเริ่มโดยการ uncomment บรรทัดนี้ ในไฟล์ index.html
``` js
<!--<script src="scripts/app.js" async></script>-->
``` 
เพื่อรับพลังจาก app.js เข้ามา และ uncomment บรรทัดข้างล่างนี้ใน app.js ครับ
``` js
// app.updateForecastCard(initialWeatherForecast);
``` 
ซึ่งจะเป็นการสั่งให้นำข้อมูลหลอกๆ ของเราเนี่ยไปอัพเดทบนการ์ดสภาพอากาศของเราทำให้การโหลดแอพขึ้นมาครั้งแรก Cilent ไม่ต้องเสียเวลาไปดึงข้อมูล API เอง

_ตรงนี้ใน Production อาจจะทำการ Inject จาก Server ซึ่ง Base ตามตำแหน่งของ User ได้ครับ_

ตอนนี้แอพเราควรจะมีหน้าตาเป็นแบบนี้แล้วครับ (ตรงลูกศรสีแดง เผื่อบางท่านยังไม่ทราบว่าไอ้ Chrome Dev Tool สามารถจำลองรูปแบบหน้าจอเป็นมือถือรุ่นดังๆ ต่างๆได้นะครับ ลองเล่นดูสนุกดีครับ)



![](https://miro.medium.com/max/676/1*YWpKIfVQvHhXDBZ9yfrfqw.png)

**3. เก็บข้อมูลเมืองที่ Users ต้องการดูสภาพอากาศกัน**

ทีนี้ พอ Users ลองเล่น App ของเราเพิ่มเมืองใหม่เข้ามา เราจะทำอย่างไรเพื่อ Save ข้อมูลของ Users คนนั้นไว้ ให้ครั้งต่อไป เมื่อเข้าเว็บมาก็แสดงเมืองที่เขาเลือกออกมาเลย

![](https://miro.medium.com/max/28/1*LPUqCP_VuMk5AW_rEeFCqw.png?q=20)

![](https://miro.medium.com/max/528/1*LPUqCP_VuMk5AW_rEeFCqw.png)

ให้เพื่อนๆ ลองเปิด Chrome Dev Tools ขึ้นมาแล้วเลือกไปที่ Tab Application ครับ จะพบว่ามีตัวเลือก Storage ให้เราเล่นมากมาย ง่ายสุดก็จะเป็น  **Local Storage** ซึ่งเป็นวิธีการเก็บข้อมูลคล้ายๆ Cookies แต่เก็บได้มากกว่า พร้อมทั้งมี Browser ที่รองรับมากมายตั้งแต่ IE ยัน Opera

แต่ทว่าปัญหาของ  **Local Storage**  คือ

-   เก็บข้อมูลได้แค่แบบ String จะใช้ JSON ก็ทำการ parse, stringify เอา
-   ทำงานแบบ Synchronous หรือ Blocking ทีละอันนั่นเอง ซึ่งอาจเป็นปัญหา Performance ได้
-   ไม่ทำงานแบบ Transactional กล่าวคือ Write ไปสองอันพร้อมกัน อาจจะ Overwrite กันได้ จนเดาไม่ออกเลยว่าข้อมูลมันจะออกอันไหนออกมา

ยุ่งไปถึงนักพัฒนาต้องทำ Storage ยุคใหม่ๆ เช่น**IndexedDB,WebSQL** ที่ทำงานได้แบบ Asynchronous, Transactional, รวมถึงสามารถเก้บ Data แบบต่างๆเช่น JSON ได้นั่นเอง

![](https://miro.medium.com/max/30/1*lO6MJIZn4jJvd8-bvx85iw.png?q=20)

![](https://miro.medium.com/max/907/1*lO6MJIZn4jJvd8-bvx85iw.png)

เรื่องเหมือนจะจบดี แต่ปัญหาคือ Browser รุ่นเก่าๆ บางประเภทยังไม่ Support เจ้านี่เต็มรูปแบบ Google ก็เลยเสนอทางแก้มาคือให้เราใช้ localForage อันเป็น Library ที่ทำให้เราใช้งานเจ้า IndexedDB,WebSQL นี้ง่ายขึ้น รวมไปถึง Switch ไปใช้ localStorage ได้หาก Browser ของ User คนนั้นๆ ไม่ Support IndexedDB หรือ WebSQL

วิธีการใช้ localForage แบบบ้านๆ ง่ายๆ เพื่อความรวดเร็ว ก็ไปโหลด localforage.min.js มาเก็บไว้เลยละกันครับ

จากนั้นก็วาง เจ้านี่ในไฟล์ index.html เหนือบรรทัด script tag -> app.js เราได้เลยครับ
``` js
<script type="text/javascript" src="scripts/localforage.min.js"></script>
``` 
กลับมาที่ app.js ขั้นตอนของเราจะเป็นงี้คือ ทุกครั้งที่ Users เพิ่มเมืองเข้ามา เราจะ Push Object เมืองของเราเนี่ยเข้าไปที่ Array ที่ชื่อว่า app.selectedCities จากนั้นเราจะเรียก Function ใหม่ที่เราสร้างขึ้น ขอเรียกมันว่า app.saveForage() ซึ่งจะเป็นฟังก์ชันจับเจ้า Array app.selectedCities เนี่ยยัดเข้าไปใน localForage ของเราอีกที

มาสร้าง Function app.saveForage() กันก่อน ให้ทุกท่านหาบรรทัดที่ 199 จะเจออันนี้ครับ
```js 
// TODO add saveSelectedCities function here
``` 
แล้วทำการใส่ Code ส่วนนี้เข้าไปข้างล่าง
``` js
app.saveForage=function(){  
    localforage.setItem('selectedCities',app.selectedCities)  
    .then(function(value){  
      console.log('Save data: '+value);  
    })  
    .catch(function(error){  
      console.log('Saving data failed: '+error);  
    })  
  }
``` 
จากนั้นให้ไปที่บรรทัดที่ 53 เราจะเจอ
``` js
// TODO init the app.selectedCities array here
// TODO push the selected city to the array and save here
``` 
ตรงนี้เราจะเช็ค app.selectedCities ก่อนว่ามีไหม ถ้าไม่มีก็สร้างเป็น Array มาซะ

จากนั้นทำการ Push Object เมืองเข้าไปใน Array แล้วเซฟลง IndexedDB ซะ โดยการใส่ Code ชุดนี้ลงไปครับ
``` js
// TODO init the app.selectedCities array here  
    if (!app.selectedCities) {  
      app.selectedCities = [];  
    }
```
และ 
  ```js
// TODO push the selected city to the array and save here  
    app.selectedCities.push({key: key, label: label});  
    app.saveForage();
``` 
ต่อมาเราก็ต้องมีฟังก์ชันที่ Check ว่า Users คนนี้เคยเข้าเล่น App เราและเพิ่มเมืองเล่นไว้หรือยัง

เลื่อนไปข้างล่าง ตรงที่เราทำการ Inject Data ไว้ในขั้นตอนที่สองครับ แถวๆนี้
```js
// TODO uncomment line below to test app with fake data  
 app.updateForecastCard(initialWeatherForecast);// TODO add startup code here
```
ผมจะขออนุญาตเปลี่ยนเป็นฟังก์ชัน app.getForage เลยละกันครับตามนี้ (ลบเจ้า app.updateForecastCard(initialWeatherForecast) ออกไปเลย)
```js
app.getForage=function(){  
    localforage.getItem('selectedCities')  
    .then(function(value){  
      console.log(value);  
      if(value){  
        app.selectedCities=value;  
        app.selectedCities.forEach(function(city){  
          app.getForecast(city.key,city.label);  
        })  
      }else{  
        app.selectedCities = [{key: initialWeatherForecast.key, label: initialWeatherForecast.label}];  
        app.updateForecastCard(initialWeatherForecast);  
        app.saveForage()  
      }  
    })  
    .catch(function(error){  
      console.log('Getting data failed: '+error);  
    })  
  }app.getForage();
```
เจ้านี้ทำหน้าที่ไปดึงข้อมูลใน localForage ออกมาถ้าเจอ Item ที่มี key ว่า selectedCities ก็เอาข้อมูลออกมา getForecast แสดงผลบนแอพ ถ้าไม่เจอก็ทำการใช้ข้อมูล Inject ไปก่อนซะ

![](https://miro.medium.com/max/30/1*m_wp2Ha_A_uhBeY7ka9J-w.png?q=20)

![](https://miro.medium.com/max/639/1*m_wp2Ha_A_uhBeY7ka9J-w.png)

มาถึงตรง แอพเราก็น่าจะเก็บข้อมูลของ Users ได้แล้วครับ ลองปิด Browser แล้วเปิดใหม่ ข้อมูลก็ควรจะยังอยู่ครบนะครับ

**4. ติดตั้ง Service Worker**

ทีนี้มาถึงตาพระเอกคนแรกของเราละครับ เราจะทำการบอก app.js ของเราให้ทำการติดตั้ง Service Worker ลงบนเครื่องของ Users ให้เลื่อนลงไปล่างสุดจะเจอ

// TODO add service worker code here

ให้เราทำการใส่ Code ส่วนนี้ลงไปครับ
```js
if ('serviceWorker' in navigator) {  
    navigator.serviceWorker  
             .register('./service-worker.js')  
             .then(function() { console.log('Service Worker Registered'); });  
  }
```
เจ้านี่จะเป็นการบอกว่าถ้า Browser ของเรามี Support Service Worker ให้ทำการ Register service-worker.js ของเราซะ

พอใส่เสร็จแล้วก็ให้เราทำการสร้างไฟล์ service-worker.js ขึ้นมาใหม่อันนึงใน Root Directory ที่เดียวกับ index.html ของเราครับ แล้วก็ใส่ code นี้เข้าไป
```js
var cacheName = 'weatherPWA-step-6-1';  
var filesToCache = [  
  '/',  
  '/index.html',  
  '/scripts/app.js',  
  '/scripts/localforage.min.js',  
  '/styles/inline.css',  
  '/images/clear.png',  
  '/images/cloudy-scattered-showers.png',  
  '/images/cloudy.png',  
  '/images/fog.png',  
  '/images/ic_add_white_24px.svg',  
  '/images/ic_refresh_white_24px.svg',  
  '/images/partly-cloudy.png',  
  '/images/rain.png',  
  '/images/scattered-showers.png',  
  '/images/sleet.png',  
  '/images/snow.png',  
  '/images/thunderstorm.png',  
  '/images/wind.png'  
];self.addEventListener('install', function(e) {  
  console.log('[ServiceWorker] Install');  
  e.waitUntil(  
    caches.open(cacheName).then(function(cache) {  
      console.log('[ServiceWorker] Caching app shell');  
      return cache.addAll(filesToCache);  
    })  
  );  
});
```
ตรงนี้คือเราจะทำการ Install SW ลงไปเครื่องของ Users ครับ จากนั้นทำการเซฟไฟล์ Static ต่างๆที่เรากำหนดไว้ใน Array filesToCache เก็บลงไว้ใน Cache ของเครื่อง User

เราจะทำการเปิด Cache ด้วย caches.open ซึ่งในส่วนของ cacheName จะต้องกำหนดไว้เพื่อให้เราสามารถอัพเดทเวอร์ชั่นของของไฟล์ต่างๆได้ เดี๋ยวจะไปดูต่อกันครับว่าทำงานอย่างไร

จากนั้นจะทำการ Add ไฟล์ทั้งหมดลงใน Cache ด้วย cache.addAll นั่นเอง

_e.waitUntil เป็นตัวที่สั่งให้ Browser อย่าพึ่ง Terminate Service Worker ก่อนที่มันจะทำงานเสร็จ อ่านเพิ่มเติมเกี่ยวกับ Service Worker ได้_ [_ที่นี่_](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/lifecycle) _ครับ_

หลังจากติดตั้งแล้ว เราจะทำบอกให้ Service Worker เช็ค Version ของ App เรากรณีที่มีการเปลี่ยนแปลงไฟล์ที่เรา Cache ไปนะครับ โดยเราใส่ Code นี้เพิ่มเข้าไปซึ่งจะทำงานทุกครั้งที่มีการเปิดใช้ App
```js
self.addEventListener('activate', function(e) {  
   console.log('[ServiceWorker] Activate');  
   e.waitUntil(  
     caches.keys().then(function(keyList) {  
       return Promise.all(keyList.map(function(key) {  
         if (key !== cacheName) {  
           console.log('[ServiceWorker] Removing old cache', key);  
           return caches.delete(key);  
         }  
       }));  
     })  
   );  
   return self.clients.claim();  
 });
```
หลักการคือจะ Iterate key ของ cache แต่ละตัว ถ้ามันไม่ตรงกับ cacheName ที่เราตั้งไว้บนหัวไฟล์ก็จะทำการลบ cache เก่านั้นทิ้งไปครับผม ฉะนั้นเวลาเราอัพเดทเวอร์ชัน App ของเรา ก็อย่าลืมไปเปลี่ยน cacheName ด้วยนะครับ

![](https://miro.medium.com/max/30/1*m23fnqb3uj7guS3ONzQuUA.png?q=20)

![](https://miro.medium.com/max/546/1*m23fnqb3uj7guS3ONzQuUA.png)

มาถึงตรงนี้ ตรวจงานกันหน่อย น่าจะเจอหน้าตา Cache Storage เป็นแบบนี้แล้วนะครับ

ต่อจากนี้เราจะทำการบอก Service Worker ว่า ในการ fetch data เพื่อดึงข้อมูลเนี่ย ถ้า fetch ไปที่ url ที่มีการ cache ไว้แล้ว ให้ดึงข้อมูลจาก cache ได้เลย ซึ่งจะทำให้เราไม่ต้องมาโหลดเจ้าตัว app shell นี้ใหม่กันทุกรอบครับ ใส่ code ด้านล่างต่อได้เลย
```js
self.addEventListener('fetch', function(e) {  
  console.log('[ServiceWorker] Fetch', e.request.url);  
  e.respondWith(  
    caches.match(e.request).then(function(response) {  
      return response || fetch(e.request);  
    })  
  );  
});
```
ทีนี้ใน Chrome Dev Tool ลองกดเป็น Offline mode แล้ว refresh ดูได้เลยครับ :)

_หมายเหตุ เวลาเราแก้ service-worker.js เพื่อให้ Browser ของเราอัพเดทเป็น SW Worker ใหม่ ลบ Cache ลบ IndexedDB ให้หมด ให้กดเข้าไปที่ Clear storage ใน Tab Application ของ Chrome Dev Tool ด้วยนะครับ เดี๋ยวจะงงกันหมด_

**5.แคชข้อมูลสภาพอากาศ**

ทีนี้เพื่อให้แอพของเราสามารถทำงานในโหมด Offline ได้เต็มรูปแบบ รวมถึงทำตัวให้เหมือน App มือถือที่เราใช้กัน ที่เปิดขึ้นมาแล้ว โชว์ Data เก่าๆจาก Cache ก่อนระหว่างรอโหลด Data ใหม่ขึ้นมา

มาลุยกันเลยครับ ที่ service-worker.js เหมือนเดิม สร้างตัวแปรใหม่ขึ้นมา
```js
var dataCacheName = 'weatherData-v1';
```
แล้วให้ทำการแก้ไขตัว Listener ‘activate’ ของเรา ตรง if ให้กลายเป็นอย่างนี้แทนครับ เพื่อไม่ให้มันไปลบ Cache นี้ทิ้งไปซะได้
```js
if (key !== cacheName && key !== dataCacheName) {
```
จากนั้นก็ Update Listener ‘fetch’ ของเราใหม่เป็น
```js
self.addEventListener('fetch', function(e) {  
  console.log('[Service Worker] Fetch', e.request.url);  
  var dataUrl = 'https://query.yahooapis.com/v1/public/yql';  
  if (e.request.url.indexOf(dataUrl) > -1) {  
    e.respondWith(  
      caches.open(dataCacheName).then(function(cache) {  
        return fetch(e.request).then(function(response){  
          cache.put(e.request.url, response.clone());  
          return response;  
        });  
      })  
    );  
  } else {  
    e.respondWith(  
      caches.match(e.request).then(function(response) {  
        return response || fetch(e.request);  
      })  
    );  
  }  
});
```
ตรงนี้ใน CodeLab จะมีอธิบายไว้ดีครับ คือ ถ้าไอ้ url ที่ไป fetch มาเนี่ยดันไปมีส่วนที่ตรงกับ query.yahoo บลาๆนั่น ให้ทำการดึงข้อมูลจาก Network มา แล้วมาเก็บไว้ที่ Cache ก่อน จากนั้น Return ข้อมูลที่ได้มากลับไป

ส่วนถ้าไม่ตรงกับ query.yahoo เนี่ย ก็คือไอ้พวก App Shell ก็ไปดึงจาก Cache มาเลยนะดู้ด ถ้าไม่เจอค่อยไป fetch โหลดมา

เดี๋ยวๆ ยังไม่จบ ขอให้กลับไปที่ app.js ก่อนครับ บรรทัดที่ 170 เราจะเจอ

ให้ทำการใส่ Code นี้เข้าไป
```js
if ('caches' in window) {  
      caches.match(url).then(function(response) {  
        if (response) {  
          response.json().then(function updateFromCache(json) {  
            var results = json.query.results;  
            results.key = key;  
            results.label = label;  
            results.created = json.query.created;  
            app.updateForecastCard(results);  
          });  
        }  
      });  
    }
```
ตรงนี้มีความเท่คือ ถ้า SW เรามีการ cache เจ้าข้อมูลสภาพอากาศไว้แล้วเนี่ย ให้ดึงมาแสดงผลก่อนเลย ระหว่างที่รออัพเดทจากการ fetch network จริงเข้ามาครับ

_ตรงนี้มีการ Handle Extreme case ไว้จุดนึงคือ เราไม่รู้ว่าข้อมูลอันไหนมันสด ใหม่กว่ากัน (แต่ปกติ Network มามันก็ต้องใหม่กว่าแหล่ะ) อันนี้เป็น Case Study ไว้ ใน App.js เขามีการเขียนป้องกันให้เราตามนี้ไว้ครับ (ไม่ต้องใส่เพิ่มใดๆ แล้วครับ)_
```js
var cardLastUpdatedElem = card.querySelector('.card-last-updated');  
    var cardLastUpdated = cardLastUpdatedElem.textContent;  
    if (cardLastUpdated) {  
      cardLastUpdated = new Date(cardLastUpdated);  
      _// Bail if the card has more recent data then the data_  
      if (dataLastUpdated.getTime() < cardLastUpdated.getTime()) {  
        return;  
      }  
    }
```
ตรงนี้เราก็จะได้ PWA ที่สามารถทำงานรวดเร็วและใช้งานได้แม้ Offline อยู่แล้วหล่ะครับ อีกนิดเดียวจบแล้ว อึดใจเดียวครับ

**5. แต่งหน้าทาปาก App ด้วย Manifest.json**

พระเอกคนที่สองของเราที่จะทำหน้าที่บ่งบอกว่า App ของเราหน้าตาเป็นอย่างไรเมื่อ Users ทำการ Add to homescreen เราแก้ได้หมดเลยว่าจะเอา Logo แบบไหน full-screen โหมดไม่มี Address Bar หรือเปล่า

ลองกันไม่ยากครับ สร้างไฟล์ manifest.json ใน Root Directory ของเราแล้วแปะไปตามนี้ได้เลย
```js
{  
  "name": "Weather",  
  "short_name": "Weather",  
  "icons": [{  
    "src": "images/icons/icon-128x128.png",  
      "sizes": "128x128",  
      "type": "image/png"  
    }, {  
      "src": "images/icons/icon-144x144.png",  
      "sizes": "144x144",  
      "type": "image/png"  
    }, {  
      "src": "images/icons/icon-152x152.png",  
      "sizes": "152x152",  
      "type": "image/png"  
    }, {  
      "src": "images/icons/icon-192x192.png",  
      "sizes": "192x192",  
      "type": "image/png"  
    }, {  
      "src": "images/icons/icon-256x256.png",  
      "sizes": "256x256",  
      "type": "image/png"  
    }],  
  "start_url": "/index.html",  
  "display": "standalone",  
  "background_color": "#3E4EB8",  
  "theme_color": "#2F3BA2"  
}
```
จากนั้นก็ให้ไปที่ไฟล์ html ใน Section header ก็ใส่ตามนี้เข้าไปครับ
```json
<link rel="manifest" href="/manifest.json">
```
ยังไม่หมด Codelab ของ Google ใจดีให้ Meta Tag สำหรับ iOS และ Window มาด้วยครับ ตามนี้
```js
<meta name="apple-mobile-web-app-capable" content="yes">  
<meta name="apple-mobile-web-app-status-bar-style" content="black">  
<meta name="apple-mobile-web-app-title" content="Weather PWA">  
<link rel="apple-touch-icon" href="images/icons/icon-152x152.png"><meta name="msapplication-TileImage" content="images/icons/icon-144x144.png">  
<meta name="msapplication-TileColor" content="#2F3BA2">
```
เสร็จแล้วไปลอง Test กันใน Chrome Dev Tools ได้เลยหน้าตาแบบนี้

![](https://miro.medium.com/max/30/1*Gb1BZi6ceDaUiilZMNuzsw.png?q=20)

![](https://miro.medium.com/max/955/1*Gb1BZi6ceDaUiilZMNuzsw.png)

ฮู่ววว … จบแล้ววววว

# **สรุปกันหน่อย**

เป็นอย่างไรบ้างครับกับ PWA เอาจริงๆ ก็ถ้าเราทำเว็บ SPA ใช้พวก Angular, React, VueJS อยู่แล้ว เพิ่มอีกนิดหน่อยสบายๆเลย ไม่แน่ 1–2 ปีถัดไป มันอาจเป็น Technology ที่ Front-end ทุกคนต้องติดตัวไปกันหมด เหมือนสมัยก่อนที่เป็นกับ Responsive Design ก็ได้ครับ

เรื่องนึงที่สำคัญคือ Apple ยังไม่เอาด้วย ก็แน่หล่ะ รายได้ของ Apple มาจาก App Store ตั้งเยอะ จะให้มา Bypass ไปลง App กันตามหน้าเว็บเองก็กระไรอยู่ ก็ได้แต่ภาวนาครับ เอา Service Worker มาใส่ไว้หน่อยก็ยังดี

ยังมีส่วนอื่นๆที่น่าสนใจเกี่ยวกับ PWA อีกครับ ไม่ว่าจะเป็น Push Notification ที่ใครสนใจ Google ก็มีทำ CodeLab ไว้แล้ว กดไปลุยได้เลย ที่  [https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/)

อีกเรื่องที่น่าศึกษาไม่แพ้กันคือ Caching Strategy ต่างๆ ว่าส่วนไหนของ App ดึง Cache ส่วนไหน ดึง Network ดู Keynote วันงานได้ตรงนี้ครับ  [https://docs.google.com/presentation/d/1TJSaBfxiwm2pIsyQpd9PSbCuwqeKyqbKx4YGQFZRTfU/edit#slide=id.p103](https://docs.google.com/presentation/d/1TJSaBfxiwm2pIsyQpd9PSbCuwqeKyqbKx4YGQFZRTfU/edit#slide=id.p103)

วันนี้ก็ขอขอบคุณทุกท่านมากครับ ที่สละเวลามาอ่าน รู้สึกว่าได้ทบทวนตัวเองดี เวลาต้องเขียนบทความออกมา อาจจะมีข้อผิดพลาดบ้าง ก็ขอให้ติชมกันมาได้เลยครับ

# แถมๆ

Google มีทำ Library จัดการสร้าง Service Worker ให้เราแบบง่ายๆครับ ใช้ร่วมกับ Gulp ได้เลยเรียกว่า sw-precache  [https://github.com/GoogleChrome/sw-precache](https://github.com/GoogleChrome/sw-precache)  ลองไปเล่นมาแล้วรู้สึกชีวิตดีขึ้นเยอะครับ
```js
var gulp = require('gulp');  
var sw = require('sw-precache')gulp.task('service', function() {  
  sw.write('service-worker.js', {  
    staticFileGlobs: [  
    'scripts/**.js',  
    'styles/**.css',  
    'images/**.*',  
    '**.{html,ico}'  
  ],  
  stripPrefix:'.',  
  runtimeCaching:[{  
      urlPattern: /^https:\/\/publicdata-weather\.firebaseio\.com/,  
      handler:'networkFirst',  
      options:{  
          cache:{  
              name:'weatherData'  
          }  
      }  
  }]  
  }, function(){  
      console.log('Done Dude');  
  });  
});
```
ใส่ประมาณนี้ไป อยากใช้ Caching Strategy ไหน ใส่ใน handler แล้วให้มัน Build ให้แปปเดียวเสร็จ ตัวนี้แนะนำเลยครับ

# Source อ้างอิง

PWA RoadShow Full day Slide:  [https://drive.google.com/drive/folders/0B55wxScz_BJtV1lGbTBOYlhLTVk](https://drive.google.com/drive/folders/0B55wxScz_BJtV1lGbTBOYlhLTVk)

Your First Progressive Web App (Code Lab):  
[https://codelabs.developers.google.com/codelabs/your-first-pwapp/index.html#0](https://codelabs.developers.google.com/codelabs/your-first-pwapp/index.html#0)

Client-Side Storage:  [https://www.html5rocks.com/en/tutorials/offline/storage/](https://www.html5rocks.com/en/tutorials/offline/storage/)

Web Storage API:  
[https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)

Udacity: Intro to Progressive Web Apps:  
[https://www.udacity.com/course/intro-to-progressive-web-apps--ud811](https://www.udacity.com/course/intro-to-progressive-web-apps--ud811)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc4Mjk4OTgyNCwxODE1MjYyODldfQ==
-->