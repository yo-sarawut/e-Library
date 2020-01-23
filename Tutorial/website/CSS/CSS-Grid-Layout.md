CSS Grid Layout
===

CSS Grid Layout คืออะไร? รู้จักมาตรฐานการออกแบบเลย์เอาท์ใน 2 มิติกันเถอะ!

[บทความโดยNuttavut Thongjor](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4)
23 เมษายน 2560

CSS ไม่ใช่เรื่องง่าย ต่อให้ยกเจ้าหน้าที่ทั้งกรมศิลปากรมาช่วย งานออกแบบหน้าเว็บด้วย CSS ก็ไม่ได้ง่ายจนทำให้ชาวโปรแกรมเมอร์ **หน้าใส** ขึ้น

ด้วยความซับซ้อนของหน้าเว็บ Flexbox จึงถือกำเนิดเพื่อให้การจัดเลย์เอาท์ยืดหยุ่นมากขึ้น ด้วยพลานุภาพแห่ง Flexbox เราจึงสามารถจัดเรียง Element ต่างๆ จากบนลงล่างหรือจากซ้ายไปขวาได้อย่างง่ายดาย `float` หรอ? คุ้นๆชื่อนะ แต่ตอนนี้ลืมไปแล้ว~

ด้วยความที่ Flexbox ออกแบบมาเพื่อใช้จัดการเลย์เอาท์ในทิศทางเดียว กอปรกับความซับซ้อนของหน้าเว็บที่มากขึ้น ลำพัง Flexbox จึงไม่เพียงพออีกต่อไป…

กว่า 5 ปีตั้งแต่วันที่ไมโครซอฟต์เสนอมาตรฐานใหม่ในการจัดเลย์เอาท์ 2 มิติ ตอนนี้เราพร้อมแล้วที่จะทดลองใช้มาตรฐานที่ชื่อว่า **CSS Grid Layout**

## สารบัญ

-   [สารบัญ](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%AA%E0%B8%B2%E0%B8%A3%E0%B8%9A%E0%B8%B1%E0%B8%8D)
-   [ทำไมต้อง CSS Grid Layout](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%97%E0%B8%B3%E0%B9%84%E0%B8%A1%E0%B8%95%E0%B9%89%E0%B8%AD%E0%B8%87-CSS-Grid-Layout)
-   [องค์ประกอบของ Grid Layout](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%AD%E0%B8%87%E0%B8%84%E0%B9%8C%E0%B8%9B%E0%B8%A3%E0%B8%B0%E0%B8%81%E0%B8%AD%E0%B8%9A%E0%B8%82%E0%B8%AD%E0%B8%87-Grid-Layout)
-   [การออกแบบเลย์เอาท์ด้วย CSS Grid Layout](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%AD%E0%B8%AD%E0%B8%81%E0%B9%81%E0%B8%9A%E0%B8%9A%E0%B9%80%E0%B8%A5%E0%B8%A2%E0%B9%8C%E0%B9%80%E0%B8%AD%E0%B8%B2%E0%B8%97%E0%B9%8C%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-CSS-Grid-Layout)
-   [แบ่งพื้นที่ด้วย Grid Layout](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B9%81%E0%B8%9A%E0%B9%88%E0%B8%87%E0%B8%9E%E0%B8%B7%E0%B9%89%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-Grid-Layout)
-   [Fraction Unit (fr)](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#Fraction-Unit-(fr))
-   [ตั้งชื่อให้ Grid Line เพื่อความเข้าใจโค้ดที่มากขึ้น](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B8%8A%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B9%83%E0%B8%AB%E0%B9%89-Grid-Line-%E0%B9%80%E0%B8%9E%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B8%84%E0%B8%A7%E0%B8%B2%E0%B8%A1%E0%B9%80%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B9%83%E0%B8%88%E0%B9%82%E0%B8%84%E0%B9%89%E0%B8%94%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%A1%E0%B8%B2%E0%B8%81%E0%B8%82%E0%B8%B6%E0%B9%89%E0%B8%99)
-   [Grid Template Areas](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#Grid-Template-Areas)
-   [Browser Support](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#Browser-Support)
-   [สรุป](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B8%AA%E0%B8%A3%E0%B8%B8%E0%B8%9B)
-   [เอกสารอ้างอิง](https://www.babelcoder.com/blog/posts/css-grid-layout?fbclid=IwAR0rRDqGCdxV4NC-RmpMkMMvSf27VnLcOdtIV6kk4y-ZzudB4UbRyHBAMn4#%E0%B9%80%E0%B8%AD%E0%B8%81%E0%B8%AA%E0%B8%B2%E0%B8%A3%E0%B8%AD%E0%B9%89%E0%B8%B2%E0%B8%87%E0%B8%AD%E0%B8%B4%E0%B8%87)

## ทำไมต้อง CSS Grid Layout

ตอนพระเจ้าสร้าง Flexbox พระเจ้าได้ใส่ยีนพิเศษที่ทำให้มันสามารถแสดงเนื้อหาให้ไหลไปทิศทางเดียว…

สมมติหน้าเพจของเราประกอบด้วย Header, Sidebar, Main และ Footer โดยแต่ละส่วนของเราจะแสดงผลเรียงกันจากบนลงล่าง

```html
<div class="container">
  <header class="header">
    Header
  </header>
  <aside class="sidebar">
    Sidebar
  </aside>
  <section class="main">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
    Ut vitae facilisis quam, nec consectetur urna. 
    Aliquam elementum nibh metus, eget lobortis lacus aliquet eu.
  </section>
  <footer class="footer">
    Footer
  </footer>
</div>

```

อาศัยความสามารถของ Flexbox ที่ทำงานได้ดีใน 1 มิติ (ในที่นี้คือมิติแนวตั้ง, จากบนลงล่าง) เราจึงสามารถเขียน CSS เพื่อแสดงผลได้ดังนี้

```css
.container {
  display: flex;
  /* ให้แกนหลักเป็นแนวตั้ง ทิศทางการไหลจึงไหลจากบนลงล่าง */
  flex-direction: column;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.header, .sidebar, .main, .footer {
  padding: 10px;
}

.header { 
  background: #8CC152; 
}

.main { 
  background: #F6BB42;
}

.sidebar { 
  background: #E9573F; 
}

.footer { 
  background: #D770AD; 
}

```

![Flexbox One Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-single-dimentional.PNG)

เพราะพฤติกรรมสัตว์ป่าของ Flexbox ที่ทำงานได้ดีในมิติเดียว หากเราต้องออกแบบเลย์เอาท์ให้มีทั้งสองมิติ เช่น ให้ทิศทางการไหลปกติเป็นจากบนลงล่าง ยกเว้น Sidebar และ Main ที่ไหลจากซ้ายไปขวา ความต้องการเช่นนี้ยังแก้ปัญหาด้วย Flexbox ได้หรือไม่?

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-dimentional.PNG)

มันจะไปยากอะไรหละ ถ้าเรารู้ว่ากล่องที่บรรจุอีลีเมนต์ต่างๆของเราวางตัวในทิศทางเดียว เราก็แค่สร้างกล่องสองใบ กล่องแรกจะวางตัวแนวขวาง ทำให้อีลีเมนต์ภายในกล่องไหลจากซ้ายไปขวาในทิศทางเดียว กล่องใบนี้จะบรรจุ Sidebar และ Main ส่วนกล่องอีกใบของเราจะวางตัวแนวตั้ง ทำให้อีลีเมนต์ต่างๆไหลจากบนลงล่าง กล่องนี้จะบรรจุ Header, กล่องใบแรก และ Footer นั่นเอง

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-box.PNG)

ด้วยวิธีการนี้เราต้องเพิ่มกล่องมาครอบ Sidebar และ Main ของเราเพิ่มอีกหนึ่งชั้น ดังนี้

```html
<!-- นี่คือกล่องใบที่สองของเรา --!>
<div class="container">
  <header class="header">
    Header
  </header>
  <!-- นี่คือกล่องใบแรกของเรา --!>
  <div class="content">
    <aside class="sidebar">
      Sidebar
    </aside>
    <section class="main">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
      Ut vitae facilisis quam, nec consectetur urna. 
      Aliquam elementum nibh metus, eget lobortis lacus aliquet eu.
    </section>
  </div>
  <footer class="footer">
    Footer
  </footer>
</div>

```

และเราสามารถจัดสไตล์ได้ดังนี้

```css
/*
  container เป็นกล่องใบที่สองของเรา
  ที่จะวางตัวจากบนลงล่าง
*/
.container {
  display: flex;
  /* อีลีเมนต์ต่างๆในกล่องนี้จะมีทิศทางเดียว คือจากบนลงล่าง */
  flex-direction: column;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.header, .sidebar, .main, .footer {
  padding: 10px;
}

.content {
  display: flex;
  /* 
    ในขณะที่ Sidebar และ Main ที่อยู่ในกล่องใบที่สองนี้
    จะมีทิศทางจากซ้ายไปขวา
  */
  flex-direction: row;
}

.header { 
  background: #8CC152; 
}

.main { 
  background: #F6BB42; 
  flex: 3;
}

.sidebar { 
  background: #E9573F; 
  flex: 1;
}

.footer { 
  background: #D770AD; 
}

```

ช้าก่อน… จากรูปภาพเราก็สามารถมองว่าเป็นการจัดเลย์เอาท์แบบทิศทางเดียวได้นะ นั่นคือมีทิศทางการไหลจากซ้ายไปขวาไงหละ เพียงแต่ Header กินพื้นที่ซะ 100% แล้ว ส่วนอื่นเลยต้องปัดตกไปบรรทัดใหม่ พอมาถึงแถวที่สอง เราอาจมองว่า 33% เป็นพื้นที่ของ Sidebar โดยส่วนที่เหลือของแถวที่สองจะเป็นของ Main และบรรทัดท้ายสุดพื้นที่ทั้งหมดเป็นของ Footer

เมื่อการไหลของสิ่งของในกล่องถูกมองเป็นทิศทางเดียว จึงไม่มีความจำเป็นต้องสร้างกล่องพิเศษไว้ใส่ Sidebar และ Main อีกต่อไป…

```html
<div class="container">
  <header class="header">
    Header
  </header>
  <aside class="sidebar">
    Sidebar
  </aside>
  <section class="main">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
    Ut vitae facilisis quam, nec consectetur urna. 
    Aliquam elementum nibh metus, eget lobortis lacus aliquet eu.
  </section>
  <footer class="footer">
    Footer
  </footer>
</div>

```

เมื่อแนวคิดการวางตัวของอีลีเมนต์เปลี่ยน CSS ของเราก็เปลี่ยนตามเช่นกัน

```css
.container {
  display: flex;
  /* อีลีเมนต์ของเรามีการวางตัวจากซ้ายไปขวา */
  flex-flow: row wrap;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.container > * {
  padding: 10px;
}

.header { 
  background: #8CC152; 
  /* โดยส่วน header ของเราจะกินพื้นที่ 100% พอดี (flex-basis เป็น 100%) */
  flex: 1 100%;
}

.main { 
  background: #F6BB42; 
  /* ในขณะที่ main จะมีพื้นที่ราว 3/4 ส่วน */
  flex: 3;
}

.sidebar { 
  background: #E9573F; 
  /* และพื้นที่ของ Sidebar เป็น 1 ใน 4 */
  flex: 1;
}

.footer { 
  background: #D770AD; 
  /* footer จะมีพื้นที่ 100% เฉกเช่นที่ header เป็น */
  flex: 1 100%;
}

```

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-dimentional.PNG)

ไม่ว่าวิธีการแก้ปัญหาของเราจะใช้วิธีที่ 1 หรือ 2 หากการจัดวางเลย์เอาท์ของเรามีลักษณะเป็นสองมิติ มันก็ยากอยู่ดีที่จะแก้ปัญหาด้วยวิธีของ Flexbox

ลองจินตนาการเพิ่มเติมครับ หากเรามี `div` ก้อนนึง เราต้องการนำอีลีเมนต์ก้องนี้ไปวางไว้แถวที่ 5 โดยเรียงจากซ้ายมือมาเป็นลำดับที่ 3 แบบนี้สามารถแก้ปัญหาด้วย Flexbox ได้ไหม? คำตอบก็คือได้ แต่ไม่ได้แบบง่ายๆใช่ไหมละเพราะนั่นไม่ใช่สิ่งที่พระเจ้าสร้างให้ Flexbox เป็น

CSS Grid Layout เป็นมาตรฐานที่สร้างขึ้นมาเพื่อจัดการเลย์เอาท์สองมิติ มาตรฐานนี้ไม่ได้เกิดขึ้นมาเพื่อฆ่า Flexbox นะครับ หากแต่เข้ามาเพื่อเติมเต็มให้การวางเลย์เอาต์ในสองมิติของเราสมบูรณ์ขึ้น

## องค์ประกอบของ Grid Layout

…เมื่อ Designer วาดแบบอย่างสวยงามมาให้ พี่แกเก็บทุกเม็ดนึกว่าตัวเองเป็นจิตรกรชื่อดังแบบปิกัสโซรึไง เห็นใจ Front-end แบบตูบ้าง เห็นดีไซน์ทีไรอยากดื่มวีต้าแล้วรีบเข้านอนทุกที~

CSS Grid Layout ช่วยให้งานออกแบบเว็บง่ายขึ้นด้วยการแบ่งพื้นที่ออกเป็นส่วนๆ พื้นที่หน้าจอจะถูกแบ่งได้ก็ต่อเมื่อมีเส้นตัดผ่านจากบนลงล่างและจากซ้ายไปขวาเกิดเป็นลักษณะตารางที่เรียกว่า Grid

![Grid Design](https://www.w3.org/TR/css3-grid-layout/images/basic-form.png)

หากเปรียบเลย์เอาท์ของเราเป็นกล่อง เราจะเรียกกล่องใบนี้ว่าเป็น **Grid Container** ที่มีสิ่งของข้างในเป็น **Grid Item** วางตัวไหลไปตามการจัดวางแบบ Grid ของเรา แต่ละเส้นที่ตัดผ่านพื้นที่ต่างๆภายในกล่องของเราจะเรียกว่า **Grid Line**

![Grid Lines](https://www.w3.org/TR/css3-grid-layout/images/grid-lines.png)

เมื่อมีเส้นตรงตัดผ่านกันไปมาจึงทำให้เกิดพื้นที่ย่อยๆขึ้นมา พื้นที่ซึ่งเกิดจากการตัดผ่านของ Grid Line สองเส้นที่ใกล้กันเรียกว่า **Grid Track**

![Grid Tracks](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-tracks.PNG)

จากภาพข้างต้น พบว่ามี Grid Line ที่ 2 และ 3 ตัดผ่านทำให้เกิดพื้นที่สีเขียว พื้นที่สีเขียวนี้จึงเรียกว่า Grid Track นอกจากเส้น Grid Line จะตัดผ่านแนวนอนได้แล้ว มันยังสามารถตัดผ่านแนวตั้งได้เช่นกัน เราจึงอาจกล่าวได้ว่า Grid Track ก็คือ **Grid Column** (คอลัมภ์) หรือ **Grid Row** (แถว) นั่นเอง

แล้วพื้นที่ที่เกิดจากการตัดกันของ Grid Column กับ Grid Row ละจะเรียกว่าอะไร? **Grid Cell** คือคำตอบสำหรับคำถามนี้ครับ

![Grid Cells](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-cells.PNG)

เมื่อเรามี Grid Cell แล้วใยจะรวม Grid Cell ข้างๆขยายอาณาเขตให้เป็น Grid Area ไม่ได้?

**Grid Area** คือพื้นที่ที่เกิดจากการรวม Grid Cell ที่อยู่ติดๆกันเข้าด้วยกัน โดย Grid Area จะมีเส้น Grid Line 4 เส้นล้อมรอบมันอยู่

![Grid Area](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-area.PNG)

แม้จะเข้าใจองค์ประกอบพื้นฐานของ Grid Layout แล้ว หากไม่ลงมือสร้างมันขึ้นมาชาตินี้คงตายตาไม่หลับ…

## การออกแบบเลย์เอาท์ด้วย CSS Grid Layout

ต้นบทความเราได้เกริ่นไปว่าการออกแบบเลย์เอาท์ในสองมิติด้วย Flexbox เป็นเรื่องยาก เราจะลองแปลงเลย์เอาท์ของเราเสียใหม่ด้วยวิธีการของ CSS Grid Layout กัน

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-dimentional.PNG)

จากเลย์เอาท์ข้างต้น หากเราเปลี่ยนมุมมองให้พื้นที่ของเราประกอบขึ้นมาจาก Grid Items ภาพในหัวจะสว่างจ้าออกมาเป็นรูปนี้ครับ

![Grid Design](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-design.PNG)

Grid Item แต่ละตัวของเราไม่จำเป็นต้องอยู่บน Cell เดียวเท่านั้น เราพบว่าส่วนของ Header และ Footer ครอบคลุมพื้นที่ของ 2 Grid Cells ในขณะที่ Sidebar และ Main ใช้พื้นที่ไปแค่ Grid Cell เดียว

Grid Cell แต่ละตัวไม่จำเป็นต้องมีขนาดเท่ากัน เราพบว่าพื้นที่ของ Main นั้นกินอาณาเขตกว้างสุด นั่นคือมีขนาดของ Grid Cell ใหญ่สุดนั่นเอง

## แบ่งพื้นที่ด้วย Grid Layout

ขั้นตอนหลังจากออกแบบตามแนวทางของ Grid Layout นั่นคือ การลงมือเขียน CSS ยังไงหละ! โดยมีขั้นตอนต่างๆดังนี้

-   **ขั้นตอนที่ 1**: กำหนด Grid Container ซะก่อนด้วยการใส่  `display: grid`
-   **ขั้นตอนที่ 2**: กำหนดจำนวนแถวและจำนวนหลักพร้อมขนาด
-   **ขั้นตอนที่ 3**: วาง Grid Item แต่ละตัวของเราลงบนเลย์เอาท์

เพราะเราทราบว่า Grid ของเราจะประกอบด้วย 3 แถวกับ 2 คอลัมภ์ เราจึงประกาศ CSS ของเราดังนี้

```css
.container {
  /* 
    ประกาศให้เป็น Grid Container 
    display ของเรานอกเหนือจาก grid แล้ว
    ยังสามารถใช้ inline-grid และ subgrid ได้ด้วย
    เราจละที่จะพูดถึงในบทความนี้
  */
  display: grid;
  /*
    โดย Grid ของเราแบ่งออกเป็น 3 แถว
    แถวที่1: สูง 50px
    แถวที่2: สูง 200px
    แถวที่3: สูง 50px
  */
  grid-template-rows: 50px 200px 50px;
  /*
    ให้ Grid ของเราแบ่งออกเป็น 2 คอลัมภ์
    คอลัมภ์ 1: กว้าง 200px
    คอลัมภ์ 2: กว้าง 500px
  */
  grid-template-columns: 200px 500px;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.container > * {
  padding: 10px;
}

.header { 
  background: #8CC152; 
}

.main { 
  background: #F6BB42; 
}

.sidebar { 
  background: #E9573F; 
}

.footer { 
  background: #D770AD; 
}

```

![Grid Container](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-container.PNG)

นี่หรือเมืองพุทธ! หลังจากทดสอบโปรแกรม เรากลับพบว่าเพียงการกำหนดให้ Grid ของเราประกอบด้วย 3 แถว 2 หลักนั้นไม่พอ เพราะเรายังไม่ได้กำหนดว่าไอเทมแต่ละตัวต้องวางตัวอยู่ตำแหน่งไหนบ้าง เช่น Header และ Footer ต้องวางตัวในแนวนอนจาก Grid Line แนวตั้งเส้นที่ 1 ไปสิ้นสุดเส้นที่ 3

![Grid Design](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-design.PNG)

```css
.header { 
  background: #8CC152; 
  /*
    Header ต้องเริ่มจาก Line1 แล้วไปสิ้นสุดที่ Line 3
    โปรดสังเกต เราใช้คำว่า grid-column
    แสดงว่าเส้นที่พิจารณาคือ Grid Line แนวตั้ง ซึ่งเป็นเส้นแบ่งคอลัมภ์นั่นเอง
  */
  grid-column-start: 1;
  /* พื้นที่ของ Header จะไปสิ้นสุดที่ Grid Line แนวตั้งเส้นที่ 3 */
  grid-column-end: 3;
}

.footer { 
  background: #D770AD; 
  grid-column-start: 1;
  grid-column-end: 3;
}

```

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-dimentional.PNG)

เราใช้ `grid-column-start` และ `grid-column-end` เพื่อกำหนดจุดเริ่มต้นของพื้นที่โดยอิงจาก Grid Line แนวตั้ง หากต้องการอิงจาก Grid Line แนวนอน เราต้องใช้ `grid-row-start` และ `grid-row-end` แทน

เพราะโปรแกรมเมอร์นั้นขี้เกียจ จะมานั่งพิมพ์ทั้ง start และ end ทำไม รวบรัดไปเลยแล้วเขียนแค่ `grid-column` ซะซิ!

```css
.header { 
  background: #8CC152; 
  grid-column: 1 / 3;
}

.footer { 
  background: #D770AD; 
  grid-column: 1 / 3;
}

```

กรณีที่ Grid ของเราประกอบด้วย Grid Line น้อยเส้น เราก็ยังพอนับกันไหวใช่ไหมครับว่าเส้นสุดท้ายคือหมายเลขอะไร แต่ไม่ใช่สำหรับ Grid Line หลายเส้น เหตุนี้ Grid Line เส้นสุดท้ายจึงอ้างอิงได้ด้วยเลข -1 และไล่ย้อนขึ้นไปทางซ้ายในเลขติดลบที่น้อยลง คือ -2, -3, -4…

```css
.header { 
  background: #8CC152; 
  /* -1 หมายถึง Grid Line เส้นขวาสุด */
  grid-column: 1 / -1;
}

.footer { 
  background: #D770AD; 
  grid-column: 1 / -1;
}

```

หากเพื่อนๆคิดว่าการใช้ `grid-column-end` เป็น -1 ยังไม่อินดี้พอ เราสามารถใช้ `span` เพื่อเป็นการบอกว่าต้องการให้ Grid Item นี้กินอาณาบริเวณไปอีกกี่ Grid Track

```css
.header { 
  background: #8CC152; 
  /* span 2 หมายถึงให้ header กินพื้นที่ไป 2 Grid Column Track */
  grid-column: 1 / span 2;
}

.footer { 
  background: #D770AD; 
  grid-column: 1 / span 2;
}

```

## Fraction Unit (fr)

หัวข้อก่อนหน้าเราได้ประกาศให้แถวและหลักของเรามีความสูงและความกว้าง

```css
.container {
  display: grid;
  grid-template-rows: 50px 200px 50px;
  grid-template-columns: 200px 500px;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

```

จะดีกว่าไหมถ้าเราสามารถประกาศความกว้างของเราแบบสัดส่วนได้ เช่น ให้คอลัมภ์ที่ 2 มีขนาดเป็น 3 ใน 4 ส่วนของพื้นที่ทั้งหมด? หน่วยที่ยืดหยุ่นนี้เราเรียกว่า Fraction Unit หรือ fr

```css
.container {
  display: grid;
  /*
    แถวแรกจะมีความสูงเป็น 1 ใน 5 ของความสูงทั้งหมด
    แถวสองจะมีความสูงเป็น 3 ใน 5 ของความสูงทั้งหมด
    แถวสามจะมีความสูงเป็น 1 ใน 5 ของความสูงทั้งหมด
  */
  grid-template-rows: 1fr 3fr 1fr;
  /*
    หลักแรกจะมีความกว้างเป็น 1 ใน 4 ของความกว้างทั้งหมด
    หลักสองจะมีความกว้างเป็น 3 ใน 4 ของความกว้างทั้งหมด
  */
  grid-template-columns: 1fr 3fr;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

```

Fraction Unit จะคำนวณจากพื้นที่ว่างที่เหลือ หากเราระบุเป็น `200px 1fr 3fr` ความหมายคือมันจะนำพื้นที่ทั้งหมดหักออกไป 200px ก่อน จึงจะเริ่มแบ่งพื้นที่ออกเป็น 4 ส่วนแล้วแจกให้ 1fr กับ 3fr ต่อไป

## ตั้งชื่อให้ Grid Line เพื่อความเข้าใจโค้ดที่มากขึ้น

การที่เราบอกว่า Header ของเราจะมีพื้นที่อยู่ตั้งแต่ `1 / -1` เรายังพอเข้าใจได้ว่าส่วนของ Header กินอาณาบริเวณทั้งแถว แล้วถ้ามีอีลีเมนต์อื่นที่บอกว่า `grid-column: 3 / 6` แบบนี้หละความหมายของมันคืออะไร?

เป็นการยากที่จะจินตนาการพื้นที่ด้วยการบอกว่า Grid Item นั้นมีพื้นที่อยู่ระหว่างเส้นไหนถึงเส้นไหน ด้วยเหตุนี้เราจึงควรระบุเป็นชื่อซะมากกว่า เมื่อต้องการประกาศว่า Grid Item ของเราอยู่บนพื้นที่ไหนก็จะใช้ชื่อนั้นเป็นตัวสื่อความหมาย เช่น เราบอกว่า Header เรามีพื้นที่อยู่ระหว่าง `sidebar-start` ถึง `main-end` แบบนี้จะเข้าใจง่ายกว่า

![Named Grid Lines](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/named-grid-line.PNG)

```css
.container {
  display: grid;
  grid-template-rows: 
    [header-start] 1fr [header-end content-start] 3fr [content-end footer-start] 1fr [footer-end];
  grid-template-columns: 
    [sidebar-start] 1fr [sidebar-end main-start] 3fr [main-end];
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.header { 
  background: #8CC152; 
  grid-column: sidebar-start / main-end;
}

.footer { 
  background: #D770AD; 
  grid-column: sidebar-start / main-end;
}

```

## Grid Template Areas

แม้การประกาศชื่อ Grid Line จะทำให้โค้ดเราเข้าใจได้ง่ายขึ้น แต่มันจะฟินกว่าไหมถ้าเราสามารถกำหนดพื้นที่ด้วยชื่อได้เลย?

`grid-template-areas` ทำให้เราสามารถประกาศชื่อของพื้นที่ใน Grid ของเราได้ หากเราอยากวาง Grid Item ตัวไหนไว้บนพื้นที่ใด เราแค่ประกาศ `grid-area` ไว้กับ Grid Item นั้น แค่นี้เป็นอันเรียบร้อย~

```css
.container {
  display: grid;
  /*
    แถวแรกของเราเป็นพื้นที่ของ header ทั้งสองคอลัมภ์
    แถวที่สอง คอลัมภ์แรกเป็นพื้นที่ของ sidebar ส่วนคอลัมภ์ที่สองเป็นพื้นที่ของ main
    แถวสุดท้าย พื้นที่ทั้งหมดเป็นของ footer
  */
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.container > * {
  padding: 10px;
}

.header { 
  background: #8CC152; 
  /* ที่เหลือก็แค่บอกว่า Grid Item แต่ละตัวจะวางไว้บนพื้นที่ชื่ออะไร */
  grid-area: header;
}

.main { 
  background: #F6BB42; 
  grid-area: main;
}

.sidebar { 
  background: #E9573F; 
  grid-area: sidebar;
}

.footer { 
  background: #D770AD; 
  grid-area: footer;
}

```

ช้าก่อน… แม้ว่าเลย์เอาท์ของเราจะเข้าที่เข้าทางแล้ว แต่เรายังไม่ได้จัดการความกว้างและความสูงของแต่ละ Grid Cell เลยนะ เพิ่ม `grid-template-columns` และ `grid-template-rows` เข้าไปเสียซิ!

```css
.container {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: 1fr 3fr 1fr;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

```

แหม… จะมานั่งประกาศทั้ง `grid-template-columns`, `grid-template-rows` และ `grid-template-areas` ทำไม เสียเวลาจะตาย โปรแกรมเมอร์หน้าใสๆแบบเราต้องใช้ `grid-template` ซิ แบบนี้~

```css
.container {
  display: grid;
  /* มันคือ <grid-template-rows> / <grid-template-columns> */
  grid-template:
    "header header" 1fr
    "sidebar main" 3fr
    "footer footer" 1fr
    / 1fr 3fr;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

```

Perfect! ค่อยทำงานสมค่าแรงขั้นต่ำ 300 บาทต่อวันหน่อย~ ตอนนี้หน้าตาเลย์เอาท์อันสวยงามของเราก็เป็นผู้เป็นคนแบบที่มันควรเป็นแล้ว

![Flexbox Two Direction](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/flexbox-two-dimentional.PNG)

และเพื่อความสวยงาม เราจะเพิ่มช่องไฟระหว่าง Cell ด้วย `grid-gap` ดังนี้

```css
.container {
  display: grid;
  grid-template:
    "header header" 1fr
    "sidebar main" 3fr
    "footer footer" 1fr
    / 1fr 3fr;
  grid-gap: 10px;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

```

![Grid Gap](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/grid-gap.PNG)

และนี่คือโค้ด CSS สุดท้ายจากความพยายามของเราในบทความนี้

```css
.container {
  display: grid;
  grid-template:
    "header header" 1fr
    "sidebar main" 3fr
    "footer footer" 1fr
    / 1fr 3fr;
  grid-gap: 10px;
  color: #FFF;
  font-weight: bold;
  text-align: center;
}

.container > * {
  padding: 10px;
}

.header { 
  background: #8CC152; 
  grid-area: header;
}

.main { 
  background: #F6BB42; 
  grid-area: main;
}

.sidebar { 
  background: #E9573F; 
  grid-area: sidebar;
}

.footer { 
  background: #D770AD; 
  grid-area: footer;
}

```

## Browser Support

CSS Grid Layout นั้นยังไม่พร้อมที่จะทำงานบนทุกเบราเซอร์ เป็นเรื่องน่าขันมากครับที่ Edge จากไมโครซอฟต์ผู้ริเริ่มเสนอ CSS Grid Layout กลับไม่สามารถใช้งานมาตรฐานใหม่นี้ได้ (ยังคงใช้ Spec เก่าอยู่, มีแผนที่จะพัฒนามาตรฐานใหม่เร็วๆนี้) แหมขนาดผู้เสนอมาตรฐานเองยังไม่รองรับ แล้วคิดเหรอว่าเบราเซอร์ทั้งตลาดจะซัพพอร์ตหมด

ไปดูกันดีกว่าครับว่าเบราเซอร์ในท้องตลาด มีใครสนับสนุนการใช้งาน CSS Grid Layout แล้วบ้าง

![ฺBrowser Support](https://s3-ap-southeast-1.amazonaws.com/babelcoder/articles/images/css-grid-layout/browser-support.PNG)

## สรุป

CSS Grid Layout ไม่ได้มาแทน Flexbox นะครับ ทั้งสองตัวนี้มีบทบาทที่ต่างกัน กล่าวคือ Flexbox จะเหมาะกับการจัดเรียงในหนึ่งมิติ ในขณะที่ CSS Grid คู่ควรแก่การจัดวางในสองทิศทาง

บทความนี้เป็นเพียงจุดเริ่มต้นการใช้งาน CSS Grid Layout เพื่อนๆที่สนใจสามารถท่อง Google เพื่อดูตัวอย่างมากมายในอินเตอร์เน็ตได้ครับ

## เอกสารอ้างอิง

_CSS Grid Layout_. Retrieved April, 23, 2017, from [http://caniuse.com/#feat=css-grid](http://caniuse.com/#feat=css-grid)

W3C (2017). _CSS Grid Layout Module Level 1_. Retrieved April, 23, 2017, from [https://www.w3.org/TR/css3-grid-layout/](https://www.w3.org/TR/css3-grid-layout/)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDE5Mzg0MzBdfQ==
-->