# create-blog-hugo

### [\[Develop\] สร้าง Blog แบบคลู ๆ ด้วย Markdown](https://bozzlab.github.io/post/hugo-blog/)

![](https://bozzlab.github.io/img/hugo.png)

## สร้างบล็อคด้วย Markdown + Hugo

> เกริ่นก่อนว่า เขียนไว้ก่อนลืม ถ้าลองทำตามแล้วติดขัดตรงไหน google can help ครับ แต่ถ้าใครเบื่อ medium สิ่งนี้ก็ยังน่าสนใจอยู่ครับ
>
> ถ้าใครเคยเขียนหรือรู้จัก Markdown หรือเคยเขียนเว็บมาแค่ HTML ก็ทำตามได้แล้วครับ gg ez มาก ๆ

### Step แรก Install + Setup Project ก่อนนะครับ

ก่อนอื่นเราต้องสร้าง folder project กันก่อนนะครับ

```text
mkdir hugo
```

Copy

หลังจากนั้น install hugo โดยสามารถเข้าไปได้ที่ [Click](https://gohugo.io/getting-started/installing/) เพื่ออ่าน Docs ซึ่งแต่ละ OS จะไม่เหมือนกัน โดยในบทความนี้จะอ้างอิงจาก Ubuntu นะครับ

```text
sudo apt-get install hugo
```

Copy

หลังจากที่ทำการ install แล้วลองเช็ค version ดูครับ

```text
hugo version
```

Copy

![image](https://bozzlab.github.io/img/hugo-p1.png)

โอเค ทีนี้ เราก็จะเริ่มสร้างกันเลย โดยพิมพ์ cmd ตามด้านล่างนี้ hugo จะทำการ generate engine ออกมาให้เราใช้ใน directory ของเรา

```text
hugo new site my-first-blog
```

Copy

![image](https://bozzlab.github.io/img/hugo-p2.png)

ต่อจากนั้นเราก็จะเห็นว่า มี folder เกิดขึ้นมาใหม่ใน project เรา ซึ่งมันก็คือ blog ของเรานั้นเอง

![image](https://bozzlab.github.io/img/hugo-p3.png)

ถ้าเข้าไปจะเห็น structure ต่าง ๆ

![image](https://bozzlab.github.io/img/hugo-p4.png)

> ซึ่งถ้าใครเคยผ่านการเขียนเว็บมา ก็บอกเลยว่าต่อจากนี้มันจะง่ายมาก ๆ หรือต่อให้ไม่เคยเขียนมา ก็ยังง่ายอยู่ดี โถ่เอ้ย

โดยผมจะไม่อธิบายนะครับว่า แต่ละส่วนทำหน้าที่หรือทำงานยังไง เพราะผมขี้เกียจ จริงๆ เขียนไว้กันลืมเฉย ๆ

อันที่จริง ชื่อ folder ค่อนข้างตรงอยู่แล้ว ถ้าติดตรงไหนก็คอมเม้นถามได้ แล้วผมก็จะไปตอบ ถ้าผมไม่ขี้เกียจ

### Step สอง Download + Install Theme

* ก่อนจะไปเข้าการเขียนบล็อค ให้ไปเลือก Theme ก่อน  [คลิกที่นี้ เพื่อไปเลือก theme](https://themes.gohugo.io/)

> ซึ่งจริง ๆ ตรงนี้ข้ามไปก็ได้ครับ ถ้าขี้เกียจ ใครอยากข้าม step ให้ไปลองสร้าง post ได้เลยครัช

![image](https://bozzlab.github.io/img/hugo-theme.png)

เลือกได้ตามใจชอบ  
พอเลือกได้แล้วก็ Clone จาก github มาได้เลยครับ

* ก่อนอื่นอย่าลืม git init

  ```text
  git init 
  git submodule add https://github.com/htdvisser/hugo-base16-theme.git themes/base16  
  echo 'theme = "base16"' >> config.toml
  ```

  Copy

cmd ด้านบน คือ git init แล้วเพื่อให้เราใช้ git ได้และเพื่อสร้างความง่อยให้ตัวเอง

เราไม่จำต้องที่ต้องเข้าโฟลเดอร์ theme แล้วไป clone theme ลงมา เราสามารถทำได้ในทันที โดยใช้ git submodule add ตามด้วย git theme ที่เราเลือก แล้ว directory ที่จะไปอยู๋

มากไปกว่านั้น แล้ว engine จะรู้ได้ยังไงว่ามี theme ใหม่มา เราใช้ echo ให้เป็นประโยชน์ โดยการบอกมันซะ ตรงๆ เลย

> config ทุกอย่างจะอยู่ในไฟล์ config.toml นะครับ ห้ามลบเด็ดขาด ลบได้แหละ แต่สร้างใหม่ด้วย

### Step สาม สร้าง Post

ที่นี้เราจะลองเพิ่ม post เข้าไปในเว็บของเราก่อน โดยการสั่ง cmd ให้ hugo generate

```text
hugo new post/my-first-post.md
```

Copy

จากนั้นให้ลองเข้าไปดูที่ content/post

![image](https://bozzlab.github.io/img/hugo-list-blog-1.png)

จะเห็นว่ามีชื่อไฟล์ markdown ที่เราสร้างไว้ ซึ่งเราสามรถใช้ editor เพื่อเปิดมันดูได้ โดยของผมเป็น vscode ตอนแรกจะใช้ vim แต่ไม่ดีกว่า sad ไป

![image](https://bozzlab.github.io/img/hugo-blog-1.png)

จะเห็นได้ว่ามี syntax ให้มาเป็น default เช่น วันเดือนปี หัวข้อ ชื่อคนเขียน โดยสามารถเพิ่มได้อีก เช่นพวกรูป tag อะไรต่าง ๆ ผมลืมไปแล้ว

> ก่อนที่เราจะเวิ่นเว้อระบายความในใจลงบล็อค ให้ลองไป test ก่อนว่า ไอที่ทำมาทั้งหมดเนี่ย มันใช้ได้ไหม ไอคนเขียนมั่วรึเปล่า

### Step Arsenal ทำการลอง Run Server

โอเค ลองมาเช็คกันก่อนว่า เว็บเราสามารถใช้ได้ไหม

```text
hugo server -D
```

* หลังจาก run server ให้ลองเข้าไป port ที่ hugo เปิดให้เรา อันนี้ถ้าใครทำตาม แล้วได้ port ไม่เหมือนกัน ไม่ต้องแปลกใจ เพราะผมใช้ port เยอะ มากจนไม่รู้ว่าต้องเปิดและปิดตัวไหน

![image](https://bozzlab.github.io/img/hugo-serv.png)

* โดยแต่ละเครื่องอาจจะไม่เหมือน ซึ่ง default ถ้าผมจำไม่ผิดจะเป็น :1313 ซึ่งถ้าผิด ก็ผิดแหละ เพราะผมจำไม่ได้ คาดหวังอะไรวะ

> หลังจากนั้นก็เข้าไป port เลย

![image](https://bozzlab.github.io/img/hugo-runweb.png)

จะเห็นได้ว่า โอเคเว็บสามารถใช้งานได้แล้ว

ลองตกแต่งสักหน่อย ก็เข้าไปตาม path นั้นเลย

```text
vi layouts/partials/hero.html
```

ถ้าสมมุติไม่มีใน folder หลักของเรา ก็ให้ก็อป layouts จาก theme มาใส่ใน path layouts/ ของ project เราเลยนะครับ

![image](https://bozzlab.github.io/img/hugo-cm.png)

* ถึงตรงนี้คิดว่า น่าจะได้พอสมควรแล้ว อันที่จริงผมขี้เกียจเขียนต่อ คือท่าต่อไป ก็ตกแต่งตามใจชอบเลยครับ จะ css + js อันนี้ก็แล้วแต่ความสามารถ หรือจะ add-ons ก็ลองดูว่า theme ที่เราเลือกมารองรับไหม

> ส่วนเรื่อง build + deploy เอาไว้ part ต่อไปนะครับ ตอนนี้ขี้เกียจแล้ว แต่บอกเลยว่าง่ายมาก ๆ ๆ ๆ ๆ ๆ ๆ

* ส่วนถ้าใครยังงงอยู่ว่า Hugo คืออะไร ก็คือ คนที่ร้อง 99 problem ทั้งร้องทั้งแต่งเอง ต้องเหงาแค่ไหน คิดดู

> สำหรับใครที่อยากต่อเนื่อง มีบทความเพิ่มเติมครับ

### [Build + Deploy Hugo โดยใช้ Host บน GitHub Pages](https://bozzlab.github.io/post/hugo-build/)

> [ที่มาบทความ : ](https://bozzlab.github.io/post/hugo-blog/).

