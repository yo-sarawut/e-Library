
ทำ Web Scraping ด้วย BeautifulSoup
===

สำหรับ Blog นี้เราจะมาดูวิธีการทำ Web scraping ด้วย Python3 และ BeautifulSoup ในระดับ Basic  :)
![enter image description here](https://miro.medium.com/max/900/1*DNTLycFqmcfwB5iNMCvPFg.jpeg)
ก่อนที่เราจะเริ่มทำ web scraping เรามาเรียนรู้พื้นฐานเรื่อง website กันก่อนดีกว่า
## Componenet of web page
เมื่อเราเข้าไปที่ web page ซัก url นึงแล้ว web browser ของเราก็จะทำการ request ไปที่ web server เราจะเรียกการ request ประเภทนี้ว่า GET request เนื่องจากเรา request ไปที่ server แล้วเราก็จะได้ file จาก server กลับมาเพื่อที่จะบอกกับ web browser นี้ว่าเราจะแสดงหน้า web page ของเราอย่างไร ซึ่งเนื้อหาใน file ที่กลับมาก็จะมีส่วนประกอบคร่าวๆ ดังนี้
- **HTML** : เป็นเนื้อหาหลักของหน้านั้นๆ
- **CSS** : เป็นตัวจัดการตกแต่ง HTML ของเราให้สวยงาม ดูดีขึ้น
- **JS** : เป็นตัวจัดการ interactive ของ HTML ของเราให้ดีขึ้น
- **Image** : รูปภาพใน format เช่น JPG , PNG สำหรับแสดงบน web
หลังจาก web browser ได้รับดังกล่าวมาแล้ว ก็จะทำการ render ออกมาสวยงามตามที่เราเห็นกันเป็นปกติ

### HTML
HyperText Markup Language (HTML) คือ ภาษาสำหรับสร้าง web page ไม่ใช่ภาษา programming เหมือน python โดยตัว HTML จะเป็นตัวบอก web browser ว่าจะต้องทำการวาดโครงสร้างหน้าตาออกมาเป็นอย่างไร

เอาล่ะ เรามาทำความเข้าใจตัว HTML กันอย่างรวดเร็วกันดีกว่า HTML ประกอบไปด้วย tag <> โดยจะเริ่มด้วย <html> ซึ่งจะเป็นตัวบอก browser ว่าภายใต้สิ่งนี้คือสิ่งที่เราต้องการจะวาด ถ้าเราลองสร้าง file html เราก็จะได้ประมาณนี้
```html
<html>
</html>
```
ต่อมาภายใน <html> เราสามารถใส่ tag head และ tag body เพื่อแยกส่วน content ต่างๆในหน้า web page ของเราได้
```html
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```
ตอนนี้เราจะเพิ่มเนื้อหาใน web page ของเราด้วย tag p โดย p คือ paragraph
และทำการใส่ css class และใส่ id ดังนี้
```html
<html>
    <head>
    </head>
    <body>
        <p class="bold-paragraph">
          Here's a paragraph of text!
          <a href="https://www.google.com" id="link1">Google</a>
        </p>
        <p class="bold-paragraph extra-large">
          Here's a second paragraph of text!
          <a href="https://www.python.org" class="link2">Python</a>
        </p>
    </body>
</html>
```
เราก็จะได้หน้า web page ของเราประมาณนี้
![enter image description here](https://miro.medium.com/max/435/1*BY-qiEr-txcZhe8vZqAUjw.png)


## Request Library
ขั้นแรกของการทำ web scraping คือเราต้องทำการ request ไปที่ url ที่เราต้องการจะทำการ scrap ซึ่งเราสามารถใช้ Python library ที่ชื่อว่า request โดยเจ้า lib ตัวนี้จะทำการ GET request ไปที่ web server ของ url ที่เราระบุ และจำทำการ download content ของ web page นั้นมาให้เรา ป่ะๆ ลองทำกันดีกว่า
ทำการ install lib ใน cmd ด้วย pip install request จากนั้นก็เขียน code ตามนี้
```py
import requests  
page = requests.get("http://dataquestio.github.io/web-scraping-pages/simple.html") 
print(page)

# <Response [200]> 
```
เราจะได้ output เป็น `<Response [200]>` ซึ่งก็คือ `request success`
ซึ่งตัวเลข status_code ที่ขึ้นต้นด้วย 2 คือ success แต่หากขึ้นต้นด้วย 4 5 คือ error สามารถดูรายละเอียดเพิ่มเติมเรื่อง `request status` code ได้ที่นี่ [click](https://www.restapitutorial.com/httpstatuscodes.html)
ถ้าเราลอง `print(page.content)` เราจะเห็นได้ว่าตัว content ที่เราได้มานั้นดูเข้าใจได้ยาก ดังรูป
```html
b'<!DOCTYPE html>\n<html>\n <head>\n <title>A simple example page</title>\n</head>\n<body>\n<p>Here is some simple content for this page.</p>\n </body>\n</html>'
```
## BeautifulSoup
และแล้วก็ถึงเวลาของพระเอกของเรา เจ้า BeautifulSoup เนี่ยจะมาทำการ parse content ที่เรา download ได้มา ให้มันสวยงามเข้าใจได้ง่ายมากขึ้น ลองกันเลยดีกว่า
ทำการ install pip install beautifulsoup4 จากนั้นก็เขียน code ตามนี้

เราจะได้ output สวยงาม ตามนี้
```html
<!DOCTYPE html>  
<html> 
<head> 
<title>A simple example page</title>
</head> 
<body> 
<p>Here is some simple content for this page.</p> 
</body> 
</html>
```
### ค้นหา Tags ทั้งหมดบน Content
หากเราได้ content จาก web page ที่เราต้องการมาแล้ว แล้วเราต้องการหา tag p ทั้งหมดที่อยู่บนนั้น เราสามารถทำได้โดยใช้คำสั่ง `find_all()` เช่น
`print(soup.find_all('p'))` ต่อจาก ตัวอย่างก่อนหน้า จะได้ list ออกมาตามนี้
`[<p>Here is some simple content for this page.</p>]`
จะเห็นได้ว่าเจ้า find_all() เนี่ยมัน return ออกมาเป็น list ให้เรา เราจึงสามารถ get position ของ list ได้ด้วย `soup.find_all('p')[0].getText()` ก็จะได้ผลลัพธ์ตามนี้ `Here is some simple content for this page.`

### ค้นหา Tags ทั้งหมดบน Content ด้วย Class หรือ Id
ลองสร้าง web page ด้วย html ใหม่โดยมีการใส่ class และ id ใหม่ ตามนี้
```html
<html>
    <head>
        <title>A simple example page</title>
    </head>
    <body>
        <div>
            <p class="inner-text first-item" id="first">
                First paragraph.
            </p>
            <p class="inner-text">
                Second paragraph.
            </p>
        </div>
        <p class="outer-text first-item" id="second">
            <b>
                First outer paragraph.
            </b>
        </p>
        <p class="outer-text">
            <b>
                Second outer paragraph.
            </b>
        </p>
    </body>
</html>
```
แต่ ณ ที่นี้จากเราสามารถยิง url ไปลองได้ที่ https://dataquestio.github.io/web-scraping-pages/ids_and_classes.html โอเคไปเขียน code ลองดึง tag ที่มี` id = first` ออกมาแสดง ลองเขียน code ตามนี้ดู
```py
soup.find_all(id="first")
```
เราก็จะได้ผลลัพธ์ของ tag ที่มี id = first ออกมาตามนี้
```py
[<p class="inner-text first-item" id="first">
                 First paragraph.
             </p>]
  ```
ต่อมาเราจะลองทำการหา tag p ที่มี class outer-tex โดยทำการเขียน code ดังนี้
```py
soup.find_all(‘p’, class_=’outer-text’)
```
เราก็จะได้ผลลัพธ์ของ tag ที่มี class outer-text ออกมาตามนี้
```py
[<p class="outer-text first-item" id="second">
 <b>
                 First outer paragraph.
             </b>
 </p>, <p class="outer-text">
 <b>
                 Second outer paragraph.
             </b>
 </p>]
 ```
มาถึงตรงจุดนี้เราก็จะทำการดึง content จาก web page หรือที่เรียกว่า web scraping กันได้แล้ว อีกทั้งยังสามารถแยกตาม tag , id , class ของ content นั้นได้ด้วย
จบไปแล้วสำหรับ basic การทำ web scraping แบบ baby walk ถ้าติดขัดตรงไหน หรือมีอะไรจะแนะนำ comment หรือ inbox มาได้โดยตรงเลยนะครับ :P
Reference : [Python Web Scraping Tutorial using BeautifulSoup](https://www.dataquest.io/blog/web-scraping-tutorial-python/)


> [Source : ](https://medium.com/equinox-blog/%E0%B8%A5%E0%B8%AD%E0%B8%87%E0%B8%97%E0%B8%B3-web-scraping-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-beautifulsoup-%E0%B8%81%E0%B8%B1%E0%B8%99%E0%B9%80%E0%B8%96%E0%B8%AD%E0%B8%B0-b58dc0e1775a).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODgwOTI5ODZdfQ==
-->