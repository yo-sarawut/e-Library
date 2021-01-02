
# เรียน VuePress ด้วยตัวเองใน 30 นาที

[VuePress](https://vuepress.vuejs.org/) ช่วยให้เราสร้าง static website สำหรับ document ต่างๆ ได้อย่างง่ายดาย มี Default Theme ที่มีฟีเจอร์เพียงพอและพร้อมต่อการทำ online document เช่น Search, Sidebar, ScrollSpy, รวมถึง Markdown Extension ที่ทีม VuePress ทำเตรียมมาให้เราใช้ อีกทั้งเรายังสามารถ embed VueComponent ลงไปในไฟล์ markdown ตรงๆ ได้อีกด้วย และที่สำคัญคือ เรายังสามารถโฟกัสที่การเขียนเอกสารด้วย markdown เพียงอย่างเดียวได้ตลอดการเขียนเอกสารเลย แม้เบื้องหลังจะเป็น Vue.js ก็ตาม มากไปกว่านั้น ต่อให้เราไม่มีความรู้เกี่ยวกับ Vue.js เลยก็สามารถสร้างเอกสารออนไลน์สวยๆ ฟีเจอร์ครบครันได้อย่างง่ายดาย!

หลังจากที่ติดตามข่าวของ [VuePress](https://vuepress.vuejs.org/) อยู่เป็นระยะ และผมก็ยังไม่ได้จะจริงจังกับมันมากนักจนท้ายที่สุด เมื่อไม่นานมานี้ VuePress เปิดตัวเวอร์ชั่น 1.x อย่างเป็นทางการหลังจากที่ทำกันมาได้ประมาณปีกว่าๆ (เริ่มทำตั้งแต่เมษายน 2018) ประกอบกับที่พักหลังผมหันมาใช้ [Vue.js](https://vuejs.org/) ทำโปรเจ็คจริงจังมากขึ้นเรื่อยๆ ก็เลยคิดว่าถึงเวลาแล้วที่ต้องลองไปเล่น VuePress ดูสักทีให้เห็นภาพรวมคร่าวๆ ว่ามันใช้ยังไง และเป็นอย่างไรเมื่อเทียบกับ [Jekyll](https://jekyllrb.com/) static site generator อีกตัวที่ผมใช้มาโดยตลอดก่อนหน้านี้

## VuePress คืออะไร?

[VuePress](https://vuepress.vuejs.org/) คือ static site generator แบบเดียวกับ [Jekyll](https://jekyllrb.com/) โดยมีขุมพลังเบื้องหลังเป็น [Vue.js](https://vuejs.org/) เขียนด้วย [Markdown](https://en.wikipedia.org/wiki/Markdown) เป็นหลัก (สาเหตุที่ผมใช้คำว่าเป็นหลัก เพราะเราสามารถแทรก VueComponent ลงไปในไฟล์ Markdown ได้เลย) สามารถทำความเข้าใจและนำมาใช้ได้อย่างรวดเร็ว จุดเด่นอยู่ที่เราสามารถแทรก [VueComponent](https://vuejs.org/v2/guide/components.html) ลงไปใน Markdown ได้, มี markdown extension อีกทั้งมี [Default Theme](https://www.npmjs.com/package/@vuepress/theme-default) ที่พร้อมและเพียงพอสำหรับการนำมาใช้เขียน document ออนไลน์ ซึ่งหากคนที่ใช้ Vue.js เป็นอยู่แล้วจะยิ่งใช้ VuePress ได้อย่างเต็มประสิทธิ์ภาพได้ยิ่งขึ้น

## ลองใช้ VuePress

ติดตั้งผ่าน npm ได้ดังนี้

>ในขั้นตอนการติดตั้ง VuePress ถ้าติด permission บางอย่างลองดู[ที่นี่](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) อาจช่วยได้

```js
npm install -g vuepress

# สร้าง markdown ไฟล์
echo '# Hello VuePress' > README.md

# เริ่มใช้งาน
vuepress dev
```

ใช่แล้ว มันง่ายแค่นั้น แค่สร้างไฟล์ `README.md` เพียง 1 ไฟล์แล้วก็รัน `vuepress dev` ก็ได้เว็บมาแล้ว! เมื่อเราเข้าไปที่ localhost จะพบว่าไฟล์ `README.md` ถูกแปลงเป็นไฟล์ index.html ให้เราใช้งาน

และหากต้องการ deploy ก็สั่งสร้าง build ไฟล์ได้ดังนี้ เราจะได้ directory `.vuepress/dist` ที่ข้างในบรรจุ site พร้อม deploy

```js
vuepress build
```

## หัวใจของ VuePress

หัวใจของ VuePress นั้นคือ folder ชื่อ `.vuepress` เพราะเราจะใช้บรรจุไฟล์ resource สำคัญต่างๆ ที่จะถูกนำมาใช้สร้างเว็บไซต์ให้เรา เช่น web configuration, VueComponent, Public Files, Template และ Theme เป็นต้น โดย folder นี้จะสร้างไว้ข้างๆ กับไฟล์ `README.md` ที่เราสร้างไว้ตอนแรกเลย

## แก้ไข Default Theme

มาลองดูการแก้ไขบางอย่างที่สำคัญๆ กันก่อน ซึ่งมีโอกาสแก้แน่ๆ อยู่แล้วทุกครั้งที่ใช้ VuePress อย่างแรกเลยก็คือ `config.js` ให้ลองสร้างไฟล์ config.js ไว้ใน folder `.vuepress` จากนั้นเข้าไปแก้ไขไฟล์ดังนี้ โดย export config ออกมา และตัวอย่างต่อไปนี้เป็นการกำหนด title และ description ให้ Web ของเรา

```js
module.exports = {
  title: 'My Blog',
  description: 'Just write a blog',
}
```

กลับไปดูที่เว็บจะพบว่า Navigation Bar จะแสดง `title` ที่เรากำหนดค่าในไฟล์ `config.js` เรามาดูการ config ที่สำคัญอีกอันหนึ่งต่อกันเลย ซึ่งก็คือการเพิ่มเมนู Navigation Bar

นอกจากเราจะเขียน config ไฟล์เป็น json แล้วเรายังสามารถเขียนเป็น .yml และ .toml ได้อีกด้วย

### เพิ่มเมนูให้ Navigation Bar

เริ่มแรก Navigation Bar เราจะมีแค่ช่องสำหรับค้นหา หากเราต้องการเพิ่มเมนูเข้าไปสำหรับ link ไปยังหน้าต่างๆ ของเว็บ สามารถเขียน config ได้ดังนี้

```js
module.exports = {
  themeConfig: {
    nav: [
      { text: 'Home', link: '/' },
      { text: 'Blog', link: '/blog/' },
      { text: 'Archive', link: '/archive' },
      { text: 'Contact', items: [
        { text: 'Twitter', link: 'http://www.twitter.com' },
        { text: 'Facebook', link: 'http://www.facebook.com' },
        { text: 'LinkedIn', link: 'http://www.linkedin.com' },
        { text: 'Flickr', link: 'http://www.flickr.com' },
      ]}
    ]
  }
}
```

บรรทัดที่ 4 – กำหนด link ไปยัง root directory `/README.md`

บรรทัดที่ 5 – กำหนด link ไปยัง directory ชื่อ blog ซึ่ง VuePress จะมองหาไฟล์ชื่อ /blog/README.md สำหรับสร้างเป็นไฟล์ index.html ดังนั้นเราจำเป็นต้องสร้างไฟล์ README.md ไว้เสมอ ไม่อย่างนั้นเมื่อกด link ไปจะเจอ 404

บรรทัดที่ 6 – กำหนด link ไปหาไฟล์ชื่อ archive.md

บรรทัดที่ 7 – สร้าง submenu

อ่านเพิ่มเกี่ยวกับ [Navbar](https://vuepress.vuejs.org/default-theme-config/#navbar)

### สร้าง Sidebar

ในไฟล์ `.md` เราสามารถใส่ front matter เพื่อให้ VuePress สร้าง sidebar ให้หน้านั้นๆ แบบอัตโนมัติโดยอิงจาก h1 และ h2 ในไฟล์ ซึ่งเราจะเขียน front matter นี้ไว้ด้านบนสุดของไฟล์ markdown ดังนี้

```js
---
sidebar: auto
---
```

แต่หากอยากสร้าง Sidebar เอง ก็ให้เข้าไปแก้ไขไฟล์ `config.js` ดังนี้

```js
module.exports = {
  themeConfig: {
    sidebar: [
      '/',
      '/page-a',
      ['/page-b', 'Explicit link text']
    ]
  }
}
```

บรรทัดที่ 4 – แสดง link ไปยัง root directory `/README.md`

บรรทัดที่ 5 – แสดง link ไปยังไฟล์ `/page-a.md`

บรรทัดที่ 6 – แสดง link ไปยังไฟล์ `/page-b.md` โดยให้แสดงชื่อ link เป็นคำว่า Explicit link text

อ่านเพิ่มเติมเกี่ยวกับ [Sidebar](https://vuepress.vuejs.org/default-theme-config/#sidebar)

### Render บางหน้าด้วย Layout เฉพาะ

ปกติ content ของไฟล์ `.md` จะถูก render ใน `<div class="page">` container ของ default theme layout หากเราต้องการสร้าง layout เอง เราสามารถสร้าง VueComponent สำหรับใช้เป็น layout ที่เราต้องการได้ โดยเราสามารถระบุ layout ที่เราต้องการใช้ในไฟล์ markdown นั้นๆ โดยเฉพาะได้โดยการกำหนดชื่อ layout ได้ที่ frontmatter ดังนี้

```js
---
layout: MyCustomLayout
---
```

VuePress จะตามไป render หน้านี้จากไฟล์ `.vuepress/components/MyCustomLayout.vue` โดยเนื้อหาในไฟล์ markdown ที่ใช้ layout นี้จะแทนที่ `<Content/>` ในไฟล์ `MyCustomLayout.vue` (คล้ายกับ `<router-view>`) เช่น

```js
<template>
  <div class="container">
    <Content/>
  </div>
</template>
```

การแก้ไข default theme ในส่วนอื่นๆ และรายละเอียดต่างๆ สามารถอ่านเพิ่มเติมได้ที่ [Default Theme Config](https://vuepress.vuejs.org/default-theme-config/#homepage)

## Public Files

นำไฟล์ที่ต้องการให้เข้าถึงได้ไปวางไว้ใน directory `.vuepress/public` เช่นไฟล์รูปภาพต่างๆ

## Markdown Extension

### Front Matter

คือส่วนหัวของไฟล์ `.md` โดยเราสามารถกำหนดค่าอะไรก็ได้ลงไปในนี้ และอ้างถึงมันได้ผ่านตัวแปร `$site`, `$page` (เราสามารถอ้างถึงตัวแปร 2 ตัวนี้จากที่ไหนในไฟล์ markdown หรือใน VueComponent ก็ได้) เช่น หากเราต้องการกำหนด `date` ให้ เราก็เขียนลงไปตรงๆ ไว้ด้านบนสุดของไฟล์แบบนี้

```js
---
date: 2019-10-15 12:30:11
---
```

และเมื่อเราลองอ่านค่าของตัวแปร `$site` หรือ `$page` ออกมา (เขียนลงไปในไฟล์ `.md` ตรงๆ ได้เลย) จะเห็น attribute ต่างๆ ที่เรากำหนดไว้ใน `frontmatter`

```js
{{ $site }}
{{ $page }}
```

### Table of Contents

เขียนแค่นี้ เราจะได้ table of contents ของทั้งหน้า โดยจะถูกสร้างอัตโนมัติจาก `h2`, `h3`

```js
[[toc]]
```

### Custom Containers

```js
::: tip สาาะน่ารู้
This is a tip
:::

```

`tip` คือชื่อของ container นอกจากนี้ยังมี `warning` และ `danger` ให้เราได้ใช้อีก

### Line Highlighting in Code Blocks

ใส่ตัวเลขไว้หลังชนิดของโค้ด เช่น `{4}` และถ้าอยากได้ hilight หลายๆ บรรทัดให้ใส่เป็นช่วงแบบนี้ `{4-7}` ดังนี้

```js
  ``` js{4}
    export default {
      data () {
        return {
          msg: 'Highlighted!'
        }
      }
    }
  ```
```

แสดงเลขบรรทัดได้โดยการเขียน config เพิ่มในไฟล์ `config.js` ดังนี้

```
module.exports = {
  markdown: {
    lineNumbers: true
  }
}  
```

## ใช้ Vue Directive ในไฟล์ Markdown

เราสามารถใช้ Vue Directive ได้ เช่น

```
  <span v-for="i in 3">{{ i }} </span>
```

และอ้างถึงตัวแปร `$page` และ `$site` ได้เลยดังที่อธิบายไปด้านบน

### ใช้ Vue Component

ให้สร้างไฟล์ `.vue` (Vue Component) ไว้ใน `.vuepress/components/` และไฟล์นั้นจะกลายมาเป็น component ให้เราใช้ได้เลยในไฟล์ markdown เช่น เราสร้างไฟล์ `/vuepress/components/MyComponent.vue` เราก็สามารถเรียกใช้ได้แบบนี้เลย

```
<MyComponent/>
```

ความดีงามของความสามารถนี้ก็คือ เราสามารถสร้าง application เล็กๆ ในรูปของ VueComponent แล้วเอามาแสดงแทรกลงไปในไฟล์ markdown ได้เลย โดยที่เรายังติดตั้ง node package ต่างๆ ผ่าน npm เข้ามาใช้งานกับ VueComponent ได้ตามปกติ

> [Source : ](https://www.khomkrit.com/vuepress-in-30-minutes/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5NDk1NzY2XX0=
-->