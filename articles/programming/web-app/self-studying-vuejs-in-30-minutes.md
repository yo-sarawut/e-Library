
# แนวทางการศึกษา Vue.js ด้วยตัวเองใน 30 นาที

![enter image description here](https://i0.wp.com/www.khomkrit.com/wp-content/uploads/2020/09/Screen-Shot-2020-09-25-at-09.59.06.png?w=830&ssl=1)

การเริ่มศึกษาอะไรสักอย่าง สำหรับบางคนแล้วอาจต้องการแค่ขอให้เริ่มได้อย่างเร็วๆ ให้เห็นภาพรวมให้ได้ก่อน เพื่อให้ตัวเองจับต้นชนปลายได้ถูก แล้วหลังจากนั้นจึงสามารถศึกษาเองต่อได้ ซึ่งจะมาช้ามากๆ ก็ตอนเริ่มต้นแรกๆ นี่แหละ ผมจึงลองสรุปสาระสำคัญ _สำหรับผู้ที่ต้องการเริ่มต้น Vue.js ด้วยตัวเองอย่างเร็วๆ_ มาให้อ่านกัน และหวังว่าจะทำให้ผู้อ่านสามารถจับต้นชนปลาย มองเห็นภาพรวมของ [Vue.js](https://vuejs.org/) ได้อย่างรวดเร็ว โดย**เลือก**ทิ้งสาระสำคัญเชิงลึกหลายส่วนไป อย่างไรก็ตามหากสนใจสามารถหาอ่านเพิ่มเติมต่อได้ใน [Official Guide](https://vuejs.org/v2/guide/) ของ Vue.js เองต่อไป

**เนื้อหา**

[1.  ติดตั้ง npm](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#tid_tang_npm)

[2.  ติดตั้ง Vue CLI 3 และ Vue CLI Service Global](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#tid_tang_Vue_CLI_3_laea_Vue_CLI_Service_Global)

[3.  Instant Prototype](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Instant_Prototype)

[3.1.  template](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#template)

[3.2.  script](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#script)

[3.3.  style](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#style)

[4.  แสดงเนื้อหา](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#saedng_neuxha)

[5.  Vue Instance](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vue_Instance)

[5.1.  data](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#data)

[5.2.  computed](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#computed)

[6.  Vue Life Cycle](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vue_Life_Cycle)

[7.  Directive](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Directive)

[7.1.  v-for](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#v-for)

[7.2.  v-if และ v-else](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#v-if_laea_v-else)

[7.3.  v-on](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#v-on)

[7.4.  v-bind](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#v-bind)

[8.  Vue Instance (ต่อ)](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vue_Instance_tx)

[8.1.  methods](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#methods)

[8.2.  Components](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Components)

[8.3.  ส่งค่าเข้าไปใน component](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#sng_kha_kheapi_ni_component)

[8.4.  ส่งค่าออกมาจาก component](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#sng_kha_xxk_ma_cak_component)

[8.5.  การอ้างถึง element](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#kar_xang_thung_element)

[9.  สรุปครึ่งทางแรก](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#srup_khrung_thang_raek)

[10.  สร้าง Project ด้วย Vue CLI 3](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#srang_Project_dwy_Vue_CLI_3)

[11.  Vue Router](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vue_Router)

[12.  App.vue](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Appvue)

[13.  Vuex](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vuex)

[13.1.  state](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#state)

[13.2.  mutations](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#mutations)

[13.3.  actions](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#actions)

[13.4.  getters](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#getters)

เนื้อหา

-   ติดตั้งเครื่องมือในการใช้งาน [Vue.js](https://vuejs.org/) – npm และ [Vue CLI](https://cli.vuejs.org/)
-   สร้างเว็บแอปฯ ด้วยไฟล์ .vue – [Instant Prototype](https://cli.vuejs.org/guide/prototyping.html)
-   รู้จัก Vue Instance
    -   เก็บข้อมูลด้วย Data
    -   คำนวนข้อมูลก่อนออกมาใช้ด้วย computed
    -   Lifecycle
        -   ถูกสร้าง – `created()`
        -   ถูก attatch เข้าใน DOM – `mounted()`
    -   ลูป, เงื่อนไข, ดักจับ event ด้วย Directive
        -   v-for, v-if, v-else, v-on, v-bind
    -   การสร้าง และใช้งาน methods
-   แบ่งส่วนหน้าจอเป็นชิ้นๆ ด้วย – components
    -   ส่งค่าเข้าออกจาก component ด้วย props, slot, $emit
-   อ้างถึง element ใน DOM
    -   $refs, ref
-   อธิบายการกำหนด path/routing โดยใช้ [Vue-Router](https://router.vuejs.org/)
-   อธิบายการเก็บสถานะขอแอปด้วย Vuex

## ติดตั้ง npm

โหลด node.js จากที่นี่ [https://nodejs.org/en/](https://nodejs.org/en/) มาติดตั้งให้เสร็จสรรพ

## ติดตั้ง Vue CLI 3 และ Vue CLI Service Global

เปิด command line แล้วพิมพ์คำสั่งต่อไปนี้

```
$ sudo npm install -g @vue/cli
$ sudo npm install -g @vue/cli-service-global
```

หลังจากติดตั้งเครื่องมือดังกล่าวเสร็จ เราก็พร้อมลงมือทำแอปด้วย Vue.js แล้ว

## Instant Prototype

เราจะใช้ไฟล์ `.vue` ในการทำ app ไฟล์นี้แต่ละไฟล์ก็คือ Vue Instance ตัวหนึ่งที่จะถูก Vue runtime เรียกใช้ในระหว่างการรันโปรแกรม โดยไฟล์นี้จะประกอบด้วย 3 ส่วนหลัก แต่ละส่วนก็คือ tag HTML ต่างๆ ดังนี้

### template

ใช้สำหรับใส่เนื้อหาที่ต้องการแสดงในหน้าเว็บ โดยหลักแล้วจะประกอบไปด้วยแท็ก HTML

### script

ใช้สำหรับเขียน script เพื่อควบคุมส่วนต่างๆ ของแอป หรือควบคุมเนื้อหาใน `<template></template>` อีกที

### style

ใช้สำหรับกำหนด style ให้กับเนื้อหาใน `<template></template>`

จากทั้ง 3 ส่วนที่กล่าวมา จะพบว่า แต่ละส่วนก็คือ ส่วนแสดงผล ส่วนควบคุมการแสดงผลและการคำนวน และส่วนกำหนดลักษณะของการแสดงผลนั่นเอง

## แสดงเนื้อหา

เริ่มจากการสร้างไฟล์ `Person.vue` ขึ้นมา ซึ่งไฟล์นี้ก็คือ Vue Instance 1 ตัวที่เราสร้างขึ้นมา จากนั้นให้ใส่ ส่วนที่ 1 ที่กล่าวไปตอนแรก โดยมีเนื้อหาดังนี้

```html
<template>
  <h1>Hello Vue</h1>
</template>
```

จากนั้นรันดูผลลัพธ์

```
$ vue serve Person.vue
```

จะเห็นว่าหน้าจอแสดงข้อความ Hello Vue ออกมา หากเราต้องการแสดงเนื้อหาอะไรบนหน้าจอ เราจะเอามาเขียนไว้ในแท็กนี้ทั้งหมด โดยมีกฎเหล็กของส่วนที่ 1 นี้ก็คือ จะมี root element ได้เพียง 1 อันเท่านั้น

## Vue Instance

Vue Instance จะมี attribute ต่างๆ ที่ต้องรู้ เริ่มจาก `data` ก่อน โดย attribute ตัวนี้จะใช้สำหรับเก็บ data ต่างๆ ที่ Vue Intance ใช้งาน โดย attribute ต่างๆ ทุกตัวของ Vue Instance เราจะเขียนโค้ดไว้ใน `<script></script>` ดังนี้

### data

```js
<script>
  export default {
    data() { 
      return {
        firstname: 'Will',
        lastname: 'Smith',
        age: 20,
        colors: ['red', 'gree', 'blug']
      }
    }
  }
</script>
```

เราจะใช้ `{{}}` สำหรับนำข้อมูลใน data ไปแสดงผล ดังนี้

```html
<template>
  <div>
    <p>firstname: {{ firstname }}</p>
    <p>lastname: {{ lastname }}</p>
    <p>age: {{ age }}</p>
    <p>colors: {{ colors }}</p>
  </div>
</template>
```

### computed

attribute ตัวต่อไปของ Vue Instance ที่ควรรู้จักคือ `computed` โดย attribute ตัวนี้มักถูกใช้เวลาเราต้องการต้องการคำนวนค่าของ data ก่อนนำออกมาใช้งาน เช่น เราต้องการใช้ชื่อเต็ม แทนที่เราจะเขียน ทั้ง firstname และ lastname ก็สามารถเขียน `fullname` เพียงอย่างเดียวก็ได้หากเรากำหนด `fullname` ไว้ใน `computed` attribute ดังนี้

```js
<script>
  export default {
    data() { 
      ...
    },
    computed: {
      fullname() {
        return this.firstname + ' ' + this.lastname
      }
    }
  }
</script>
```

และเราสามารถเขียน `<template></template>` โดยใช้ fullname แทน firstname และ lastname ได้ใหม่แบบนี้

```html
<template>
  <div>
    <p>fullname: {{ fullname }}</p>
    <p>age: {{ age }}</p>
    <p>colors: {{ colors }}</p>
  </div>
</template>
```

## Vue Life Cycle

ช่วงชีวิตของ Vue Instance จะมีจังหวะ hook ต่างๆ ให้เราสามารถเข้าไปแทรกจังหวะได้ เช่น `created()`, `mounted()` ดังนี้

```js
<script>
  export default {
    data() { 
      ...
    },
    computed: {
      ...
    },
    created() {
      console.log('created')
    },
    mounted() {
      console.log('mounted')
    }
  }
</script>
```

สามารถดู Hook ต่างๆ ได้ที่นี่ [Vue Lifecycle Diagram](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram)

นอกจากนี้ ยังมี attribute ต่างๆ ที่ควรทำความรู้จักเพิ่มเติมอีก เช่น `methods` และ `components` แต่ก่อนที่เราจะทำความรู้จักกับมัน เรามาทำความรู้จักกับ Directive กันก่อน

## Directive

### v-for

ใช้สำหรับสร้าง element ซ้ำๆ ตามจำนวนรอบที่เราต้องการ เช่น เราต้องการให้แสดง colors ใน data attribute ออกมาเป็น list แทนที่จะพิมพ์เป็น array object ออกมา แปลว่าเราต้องการทำซ้ำแท็ก `<li>` ดังนี้

```html
<template>
  <div>
    <p>fullname: {{ fullname }}</p>
    <p>age: {{ age }}</p>
    <p>colors:
      <ul>
        <li v-for="color in colors">{{ color }}</li>
      </ul>
    </p>
  </div>
</template>
```

จากโค้ดจะเห็นว่า หากเราต้องการให้แท็กไหนถูกสร้างขึ้นซ้ำๆ เราก็ไปใช้ `v-for` กับแท็กนั้น

### v-if และ v-else

ใช้สำหรับเลือกว่าจะแสดง หรือไม่แสดง element ที่กำหนดหรือไม่ โดยจะแตกต่างจากการซ่อนหรือไม่ซ่อนโดยที่ การซ่อนคือการที่ element นั้นๆ ถูกสร้างขึ้นมาแล้วแต่ไม่แสดงให้เราเห็น ส่วน การแสดงหรือไม่แสดงโดย `v-if` นั้นคือการที่ element นั้นยังไม่ถูกสร้างขึ้นมาเลยตั้งแต่แรก แต่จะถูกสร้างขึ้นมาก็ต่อเมื่อเข้าเงื่อนไขเท่านั้น ในทางตรงกันข้ามหากไม่เข้าเงื่อนไข element จะถูกทำลายทิ้งไปเลย ไม่ใช่การซ่อนไม่ให้เห็น ยกตัวอย่างเช่น เราต้องการให้แสดง/ไม่แสดง `old` เมื่ออายุของ Person มากกว่า 20 และหากไม่ใช่ให้แสดง `young` ดังนี้

```html
<template>
  <div>
    <p>fullname: {{ fullname }}</p>
    <p>age: {{ age }}</p>
    <p v-if="age > 20"> old </p>
    <p v-else> young </p>
    <p>colors:
      <ul>
        <li v-for="color in colors">{{ color }}</li>
      </ul>
    </p>
  </div>
</template>
```

### v-on

ใช้สำหรับดักจับ event ต่างๆ ที่เกิดขึ้น เช่น ดักจับว่ามีการ click ที่ element นั้นๆ หรือไม่ เราก็จะใช้ v-on:click หรือหากต้องการดักจับ event focus เราก็จะใช้ v-on:focus หรือ v-on:submit เป็นต้น ยกตัวอย่างการใช้ `v-on:click` ได้ดังนี้

```html
<template>
  <div>
    <p>fullname: {{ fullname }}</p>
    <p>age: {{ age }}</p>
    <p v-if="age > 20"> old </p>
    <p v-else> young </p>
    <p>colors:
      <ul>
        <li v-for="color in colors">{{ color }}</li>
      </ul>
    </p>
    <button v-on:click="age++">Increase Age</button>
    <button v-on:click="age--">Decrease Age</button>
  </div>
</template>
```

จากโค้ดตัวอย่างเมื่อ `click` ที่ปุ่มแล้วค่าของ `age` จะถูกแก้ไข ให้ลองกดปุ่ม เพิ่ม ลด อายุแล้วสังเกตค่าของ Age ที่หน้าจอ รวมถึงสังเกตแท็กที่เรากำหนดเงื่อนไขด้วย `v-if` ว่ามันจะถูกอัพเดทโดยอัตโนมัติเมื่อค่าของ age เปลี่ยนไป

การดักจับ event ต่างๆ เราสามารถเขียนแบบสั้นๆ ได้ด้วยการใช้ `@` เช่น `@click="age++"`

### v-bind

คือการเชื่อมค่าเข้ากับ property ของแท็ก เช่น เชื่อมค่าของ data เข้ากับ property `src` ของ `<img>` โดย property ที่เราเชื่อมค่าเข้าไปจะต้องใส่เครื่องหมาย `:` ไว้ข้างหน้าด้วย ดังนี้ (และให้ลองเอาเครื่องหมาย `:` ออกดู)

```html
<template>
  <p><img :src="profileImage"/></p>
</template>
<script>
  data() { 
      return {
        profileImage: 'https://farm6.staticflickr.com/5622/25359356909_0e07150a22_s.jpg'
      }
    },
</script>
```

## Vue Instance (ต่อ)

### methods

กลับมาที่ Vue Instance กันต่อที่ attributes methods ของ Vue Instance เราสามารถประกาศว่า Vue Instance ตัวนี้มี method อะไรให้ใช้บ้างได้โดยการกำหนดค่าให้ atteribute `methods` ดังนี้

```html
<template>
  <div>
    ...
    <p>age: {{ age }}</p>
    ...
    <button @click="increaseAge">Increase Age</button>
    <button @click="decreaseAge">Decrease Age</button>
  </div>
</template>
<script>
  export default {
    ...
    methods: {
      increaseAge() {
        this.age++
      },
      decreaseAge() {
        this.age--
      }
    }
  }
</script>
```

จากโค้ดตัวอย่าง เราสร้าง method เพิ่ม และลด อายุ และแก้โค้ดใน `<template>` ให้มาเรียก method ทั้ง 2 ตัวนี้แทนเมื่อมีการ `click` ที่ปุ่ม

### Components

attribute ตัวต่อไปของ Vue Instance ที่จะแนะนำก็คือ `components` ซึ่งจะช่วยให้เราสามารถสร้าง Vue Instance ตัวอื่นๆ แล้วนำมาใช้ร่วมกันได้ โดยเราจะเรียกแต่ละไฟล์ว่า component เริ่มจากการสร้างไฟล์ชื่อ `Create.vue` แล้วให้ใส่เนื้อหาดังนี้

```html
<template>
  <form>
  <div class="form-group">
    <label >Input new Color</label>
    <input type="text" class="form-control" placeholder="Enter color">
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
</template>
```

เราสามารถเรียกใช้ component `Create.vue` ในไฟล์ `Person.vue` ได้โดยกำหนดค่าให้กับ attribute components ดังนี้

```js
<script>
  import Create from './Create.vue'
  export default {
    data() { 
      ...
    },
    computed: {
      ...
    },
    methods: {
      ...
    },
    components: {
      AppCreate: Create
    }
  }
</script>
```

จากโค้ดด้านบนจะเห็นว่าเราต้อง import `Create.vue` เข้ามาใช้งานก่อน จากนั้นไปประกาศไว้ใน attribute `components` โดย AppCreate เราจะตั้งเป็นชื่ออะไรก็ได้ ซึ่งชื่อนี้จะถูกใช้สร้างเป็นแท็กให้เราสามารถนำมาใช้งานได้ใน `<template>` กรณีที่ยกมา ถ้าใช้ชื่อ `AppCreate` แล้ว Vue จะสร้างแท็ก `<appCreate>` มาให้เราใช้ ได้ดังนี้

```html
<template>
  <div>
    <app-create></app-create>
    ...
  </div>
</template>
```

### ส่งค่าเข้าไปใน component

เราสามารถส่งค่าจาก `Person.vue` เข้าไปใน component `Create.vue` ได้ โดยการแก้ไขไฟล์ `Person.vue` ตอนที่เราเรียกใช้ `<app-create></app-create>` ดังนี้

```html
<template>
  <div>
    <app-create hint="Color">Enter your favorite color</app-create>
    ...
  </div>
</template>
```

ต่อไปเราก็มาอ่านค่าที่อยู่ระหว่างแท็ก `<app-create></app-create>` และอ่านค่าของ property `hint` ที่เราส่งเข้าไป โดยเข้าไปแก้ไขไฟล์ Create.vue ดังนี้

```html
<template>
  <form>
  <div class="form-group">
    <h1><slot></slot></h1>
    <label>Input new Color</label>
    <input type="text" class="form-control" :placeholder="hint">
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
</template>
```

จากโค้ดด้านบน เราจะใช้แท็ก `<slot></slot>` เพื่อบอกว่าให้นำเนื้อหาที่อยู่ระหว่างแท็ก (ที่เราเรียกใช้ในไฟล์ Person.vue) ซึ่งในที่นี้ก็คือ Enter your favorite color นำมาวางไว้ตรงนี้ และใช้ค่าของ property `hint` (ซึ่งก็คือ Color) ที่ได้รับมากับ attribute placeholder ของ `<input>`

แต่ก่อนที่เราจะรับ `hint` เข้ามาใน component ได้ เราจำเป็นต้องนิยามว่า component Create.vue นี้มี attribute ชื่อ `hint` ซะก่อน ดังนี้

```js
<script>
export default {
  props: ['hint'],
  ...
}
</script>
```

### ส่งค่าออกมาจาก component

สิ่งที่เราต้องการก็คือสร้าง color ใหม่ใน `Create.vue` และส่งสีที่สร้างขึ้นใหม่นี้กลับออกมาให้ `Person.vue` อัพเดทค่าบนหน้าจอ

เริ่มจากการแก้ไขไฟล์ `Create.vue` ก่อนดังนี้

```html
<template>
  <form @submit.prevent="saveColor"> // (1)
  <div class="form-group">
    <h1><slot></slot></h1>
    <label>Input new Color</label>
    <input type="text" class="form-control" :placeholder="hint" v-model="color"> // (2)
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
</template>
<script>
export default {
  props: ['hint'],
  data() {
    return {
      color: '' // (3)
    }
  },
  methods: {
    saveColor() { // (4)
      this.$emit('createColor', this.color)
    }
  }
}
</script>
```

จากโค้ดด้านบน เราแก้ไขทั้งหมด 4 จุดดังนี้

1.  ดัก event `submit` ไว้ที่แท็ก `<form>` พร้อมกับใส่ event modifier ชื่อ `prevent` โดยที่ event modifier ตัวนี้ทำหน้าที่ป้องกันไม่ให้ page reload ใหม่เมื่อมีการกดปุ่ม submit
2.  ใช้ directive `v-model` โดยที่ directive ตัวนี้ทำหน้าชื่อ เชื่อมค่าของ form input ต่างๆ เข้ากับ data แบบ 2-way binding ซึ่งหมายความว่า หากค่าใน data เปลี่ยน ค่าของ form input ก็จะเปลียนตาม ในทางตรงกันข้ามถ้าค่าของ form input เปลี่ยน ค่าของ data ก็จะเปลี่ยนตามเช่นกัน (ลองเปลี่ยนค่าของ `color` ใน data ดูจะพบว่าค่าใน form input จะเปลี่นตามทันที)
3.  ประกาศ `color` ไว้ใน data เอาไว้เชื่อมกับ form input ด้วย `v-model` ในข้อ 2
4.  สร้าง method `saveColor()` ซึ่งจะถูกเรียกใช้เมื่อมี event `submit` ที่เรา handle ไว้ในข้อ 1 โดย method นี้จะเรียกใช้ function `$emit()` ให้ทำหน้าที่ส่ง event ชื่อ `createColor` ออกมาพร้อมกับพารามิเตอร์อีกตัว โดยค่าของพารามิเตอร์นี้ก็คือ color นั่นเอง

จากนั้นกลับไปแก้ไขไฟล์ `Person.vue` ให้รอรับข้อมูลที่ถูกส่งออกมาจาก `Create.vue` โดยหลักการก็คือ ดักจับ event ชื่อ `createColor` ที่ถูกส่งออกมาจาก `<app-create>` โดยฟังก์ชั่น `$emit()` นั่นเอง ดังนี้

```html
<template>
  <div>
    <app-create hint="Color" @createColor="addColor">Enter your favorite color</app-create> // (1)
    ...
  </div>
</template>
<script>
  import Create from './Create.vue'
  export default {
    data() { 
      ...
      }
    },
    computed: {
      ...
    },
    methods: {
      ...
      addColor(color) {
        this.colors.push(color) // (2)
      }
    },
    components: {
      AppCreate: Create
    }
  }
</script>
```

จุดที่ 1 เราเพิ่มให้แท็ก `<app-create>` ดักจับ event `createColor` และเมื่อมี event นี้เกิดขึ้นให้เรียกใช้ method ชื่อ `addColor()` ที่เราสร้างไว้ที่จุดที่ 2

### การอ้างถึง element

หากเราต้องการให้ cursor ไป focus อยู่ที่ textfield ของ Create.vue ให้พร้อมกรอกข้อมูลเลยตั้งแต่เปิดหน้าจอมาเราสามารถทำได้โดยแก้ไขไฟล์ Create.vue โดยการอ้างถึง element ที่ต้องการ แล้วเรียกฟังก์ชั่น `focus()` ดังนี้

```html
<template>
...
  <input ref="inputColor" type="text" class="form-control" :placeholder="hint" v-model="color"> // (1)
...
</template>
<script>
  ...
  },
  mounted() { // (2)
    this.$refs.inputColor.focus()
  }
</script>
```

จากโค้ดด้านบนเราแก้ไข 2 จุดดังนี้

1.  เพิ่ม attribute ชื่อ `ref` พร้อมกับกำหนดค่าให้ ซึ่งค่านี้จะกลายไปเป็นชื่อที่เราเอาไว้ใช้อ้างถึงใน script
2.  อ้างถึง element โดยใช้ `this.$refs` โดยการเพิ่ม code ลงไปใน hook ชื่อ `mounted()` และสั่งให้ `focus()` ทันทีที่ถูก mount element ลงใน DOM

## สรุปครึ่งทางแรก

มาถึงตรงนี้เราก็น่าจะพอเห็นภาพรวมของการเขียนเว็บแอปด้วย Vue.js กันบ้างแล้ว โดยเนื้อหาหลักจะเป็นเรื่องเกี่ยวกับ Vue Instance, Directive และ Component

ตอนต่อไปเราจะมาพูดถึงหัวข้อสำคัญอีก 2 เรื่องที่จำเป็นต้องรู้ ก็คือ Vue-Router และ Vuex

## สร้าง Project ด้วย Vue CLI 3

มาเริ่มกันต่อเกี่ยวกับ [Vue-Router](https://router.vuejs.org/) ก่อนเลย ด้วยการสร้างโปรเจ็คจาก Vue CLI ขึ้นมาใหม่ด้วยคำสั่งนี้

```
$ vue create my-project
```

ให้เลือก Manually select features ตามรูปด้านล่าง

```
Vue CLI v3.0.1
? Please pick a preset:
  Router+Vuex (vue-router, vuex, babel)
  Babel+Router+Vuex+Linter (vue-router, vuex, babel, eslint)
  default (babel, eslint)
❯ Manually select features

```

ให้เลือก Babel, Router, Vuex, Linter / Formatter ในขั้นตอนนี้ เวลาจะเลือกให้กดปุ่ม space bar เพื่อเลือก พอเลือกเสร็จแล้วถึงจะกด Enter

```
Vue CLI v3.0.1
? Please pick a preset: Manually select features
? Check the features needed for your project:
 ◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
 ◉ Router
❯◉ Vuex
 ◯ CSS Pre-processors
 ◉ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing


```

จากนั้นให้ตั้งค่าตามนี้

```
Vue CLI v3.0.1
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, Router, Vuex, Linter
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Standard
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? (Use arrow keys)
❯ In dedicated config files
  In package.json
```

เราจะได้ folder ชื่อ my-project มา จากนั้นให้เข้าไปใน folder นี้แล้วรันคำสั่ง

```
$ npm run serve
```

## Vue Router

ในเบื้องต้นให้คิดว่าเราใช้ vue router ในการกำหนดว่า เมื่อ user เข้ามาที่ path ไหน แล้วจะแสดงอะไรให้ user ดู และนอกจากนี้ยังมี hook ต่างๆ ให้เราได้ใช้งานกันอีก ไม่ว่าจะเป็นการ intercept ก่อนเข้ามาที่ path นี้หรือหลังจากที่ user ออกจาก path ที่เรากำหนดไว้ก็ได้

ใน directory `src` ไฟล์ที่เราสนใจคือไฟล์ `router.js` และ attribute ที่เราสนใจในไฟล์นี้คือ `routes` โดยเราจะพบว่า `routes` เก็บค่าเป็น array ของ object ซึ่งแต่ละ object นั้นก็คือการนิยาม router แต่ละตัวนั่นเอง ว่าถ้า user เข้ามาที่ path ไหนแล้วจะให้โหลด component ไหนเข้ามาแสดง

```js
    {
      path: '/',
      name: 'home',
      component: Home
    }

```

นอกจาก attribute ทั้ง 3 ตัวที่ถูก generate มาให้เราตั้งแต่แรก เราก็ยังสามารถ config อย่างอื่นให้กับ route แต่ละอันเพิ่มได้อีก เช่น

-   [Dynamic Route Maching](https://router.vuejs.org/guide/essentials/dynamic-matching.html) – ทำให้เราสามารถกำหนด route maching โดยไม่ต้องกำหนดชื่อ path เป็นค่าคงที่ก็ได้ เช่น ถ้าเรากำหนด route เป็น `/user/:id`

```js
    {
      path: '/user/:id',
      name: 'user-detail',
      component: User
    }
```

เวลามีคนเรียก path มาที่ `/user/123` เราก็สามารถอ่านค่านี้ได้เลยจากใน Vue Instant ว่า `this.$route.params.id` แล้วจะได้ค่า `123` มาใช้งาน

หัวข้ออื่นๆ ที่น่าสนใจหากต้องการลองเล่นอะไรเพิ่มเติมเกี่ยวสกับ Vue Router ผมแนะนำให้เริ่มอ่านจากหัวข้อเหล่านี้ต่อ

-   [Nested Route](https://router.vuejs.org/guide/essentials/nested-routes.html)
-   [Programmatic Navigation](https://router.vuejs.org/guide/essentials/navigation.html) – ช่วยให้เราเขียนโค้ดส่งให้ user ไปยังหน้าจอต่างๆ ได้ตามเงื่อนไขต่างๆ ที่เกิดขึ้นในโปรแกรมของเรา
-   [Navigation Gaurd](https://router.vuejs.org/guide/advanced/navigation-guards.html) – ช่วยให้เราทำอะไรก่อนหลังการเข้ามาที่ route ได้ เช่นการตรวจสอบว่าถ้าเปิดมาที่ path นี้แล้วยังไม่ให้ login เราก็จะ redirect ไปที่หน้า login เป็นต้น แต่ที่ต้องจำไว้อย่างหนึ่งก็คือการ การเปลี่ยน query หรือเปลี่ยน parameter ตอนเรียก URL นั้นจะไม่ trigger navigation guard และหากต้องการรู้ว่า parameter หรือ query เปลี่ยนให้เลี่ยงไป[ใช้ `watch` ของ Vue Instance](https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes) แทน

## App.vue

ต่อไปเราจะมาดูที่เนื้อหาในไฟล์ App.vue กัน จากที่ Vue CLI 3 scaffold project มาให้เรา เราจะได้ไฟล์นี้มา และไฟล์นี้ถูกกำหนดให้เป็นเป็นไฟล์ที่เป็นหน้าจอแรกหรือหน้าจอหลักที่ถูกแสดงขึ้นมาบนเว็บ ส่วนที่ว่าทำไมไฟล์นี้ถึงเป็นไฟล์แรกนั้น ให้เข้าไปดูเนื้อหาในไฟล์ `main.js` จะเห็นว่า Vue Instance ถูกสร้างขึ้นมา พร้อมกับกำหนด router และ สั่งให้ render component ชื่อ App และ mount มันเข้ากับ element ที่มี id = `app` ส่วน element ไหนมี id = `app` นั้นให้ลองเปิดดูไฟล์ `/public/index.html` ซึ่งเรื่องราวที่มาที่ไปทั้งหมด สามารถอ่านเพิ่มเติมต่อได้ใน [Official Guide ของ Vue.js](https://vuejs.org/v2/guide/)

`App.vue` ไฟล์นี้มีเนื้อหาเกี่ยวข้องกับ Vue Router ดังนี้

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |  // (1)
      <router-link to="/about">About</router-link>  // (2)
    </div>
    <router-view/>  // (3)
  </div>
</template>
```

จากโค้ดที่ยกมาแบ่งอธิบายได้ 3 จุด ดังนี้

จุดที่ (1) และจุดที่ (2) ปกติแล้วเวลาเราจะสร้าง link ให้ไปยัง path ต่างๆ ที่เรากำหนดไว้ใน router เราจะใช้แท็ก `<router-link>`

ตามตัวอย่าง router link ตัวแรกจะ link ไปที่ `/` ส่วน router link ตัวที่สองจะ link ไปที่ `/about` ซึ่งแต่ละ path ที่ link ไปนั้นจะไปโหลด component ไหนให้ลองกลับไปดูเนื้อหาในไฟล์ `router.js`

แท็ก `<router-link>` จะสร้างแท็ก `<a>` มาให้เรา พร้อมกับกำหนดว่าจะให้ link ไปที่ path ใด ซึ่งเราสามารถกำหนดค่าต่างๆ เพิ่มให้กับ `<router-link>` ได้อีก เช่น แทนที่เราจะกำหนดเป็น path ไปก็สามารถกำหนดเป็นชื่อของ route ก็ได้ดังนี้

```js
<router-link :to="{ name: 'home' }>Home</router-link>
```

จุดที่ (3) คือแท็ก `<router-view>` เอาไว้กำหนดว่า เมื่อ component นี้ถูกแสดง (ในที่นี้คือ App.vue) แล้วให้นำ component ที่ match กับ route ที่เรากำหนดค่าไว้ใน `router.js` มาแสดงแทนที่แท็ก `<router-view>` ตรงนี้

**อ่านเพิ่ม**

-   [Lazy Loading Routes](https://router.vuejs.org/guide/advanced/lazy-loading.html) – บาง component เรายังไม่อยากให้โหลดมาตั้งแต่ตอนแรก เราสามารถกำหนดได้ว่าให้โหลดมาตอนไหนในภายหลังได้ ว่าจะโหลดมาเฉพาะ component โดดๆ หรือโหลดมาพร้อมกับ component อื่นๆ โดยกำหนด chunk file ให้กับมันได้อีกที

## Vuex

[Vuex](https://vuex.vuejs.org/) คือ state management pattern + library ช่วยให้เราเก็บข้อมูลต่างๆ ในแอปของเราไว้ที่เดียวกัน ให้เราเรียกใช้ และเข้าถึงมันได้ง่าย ซึ่งเจ้า Vuex นี้ยังถูก integrate เข้ากับ [Vue Devtool](https://github.com/vuejs/vue-devtools) ให้เราสามารถเข้าไปดู state ต่างๆ ได้ง่าย และยังควบคุมสถานะต่างๆ ได้โดยไม่ต้อง config อะไรเลย

สามารถโหลด [Vue Dev Tool Chrome Extension ได้ที่นี่](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en) มันเป็น extension ที่ทุกคนควรใช้ ทำให้เรา debug Vue Application ได้ง่ายขึ้นมากๆ ทำให้เราสามารถดูสถานะต่างๆ แก้ไขค่าในตัวแปร ดูตัวแปรที่มีให้เราใช้ ณ​ ขณะนั้นๆ ฯลฯ ได้ผ่าน Vue Dev Tool

ในระหว่างที่ลองเล่นกับ Vuex แนะนำว่าควรเปิด Vue Dev Tool Extension ควบคู่ไปด้วย จะช่วยทำให้เราเข้าใจมากขึ้น

หลังจากที่เรา Scaffold Vue Project มาแล้วเราสามารถตามไปดูร่องรอยของ Vuex ได้ที่ 2 ไฟล์นี้ เริ่มจาก `/src/main.js` – มีการกำหนด `store` ให้ตั้งแต่ตอนสร้าง Vue instance โดยใช้ค่าที่ export มาจาก `/src/store` ดังนี้

```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```

จากนั้นเราลองตามไปดูในไฟล์ `/src/store.js` ก็จะพบว่าไฟล์นี้ export Vuex.Store instance ออกไป พร้อมกับกำหนด property ต่างๆ ใน Vuex ได้แก่ `state`, `mutations`, `actions` ดังนี้

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {

  },
  mutations: {

  },
  actions: {

  }
})
```

จุดที่เราต้องสนใจต่อจากนี้ก็คือไฟล์ `/src/store.js` ที่เราจะใช้เป็นที่เก็บ state ของแอปเรา มาเริ่มดูกันทีละ attribute กันต่อดังนี้

### state

Vuex เป็น **single state tree** หมายความว่าใน Application ของเรานั้นจะมี state ได้เพียงอันเดียวเท่านั้นเป็น **single source of truth** ซึ่งช่วยให้เราทำ snapshot เพื่อ debug แอปของเราได้ง่าย

เริ่มจากลองกำหนดค่าให้กับ state

```
state: {
  items: ['a']
}
```

เราสามารถอ้างถึงค่านี้จากที่ไหนก็ได้ในแอป เช่น

```
methods: {
  addTodo() {
    this.$store.state.items.push('b')
  },
  deleteItem(index) {
    this.$store.state.items.splice(index, 1)
  }
}
```

### mutations

ทีนี้เราจะย้าย logic จากที่เคยเรียกตรงๆ จากที่อื่นเข้ามาไว้ใน store ของเรา โดยกฏเหล็กข้อหนึ่งของ mutations ก็คือ mutation handler functions จะต้องเป็น synchronous เท่านั้น ([เหตุผล](https://vuex.vuejs.org/guide/mutations.html#mutations-must-be-synchronous))

ลองเพิ่มเนื้อหาใน mutation ดังนี้

```
mutations: {
  'ADD_ITEM' (state, payload) {
    state.items.push(payload.item)
  }
}
```

จากโค้ดเราจะมี mutation ชื่อ `ADD_ITEM` เอาไว้ให้เรียกใช้ได้จากที่ไหนก็ได้ในแอปเช่นกัน เช่น

```
addTodo() {
  this.$store.commit('ADD_ITEM', { item: 'b'})
},
```

### actions

คล้ายกับ mutations แต่สิ่งที่ต่างออกไปก็คือ

-   แทนที่จะแก้ไข data ที่ state ตรงๆ ก็จะใช้วิธี commit mutation แทน
-   โค้ดใน action สามารถเป็น aynschronous ได้

ใน action ก็จะรับ payload เข้ามาแล้วสั่ง commit mutation อีกที ดังนี้

```
actions: {
  addItem({ commit }, payload) {
    commit('ADD_ITEM', payload)
  }
}
```

และวิธีเรียกใช้งาน actions ทำได้ดังนี้

```js
addTodo() {
  this.$store.dispatch('addItem', { item: this.item })
},
```

### getters

นอกจาก attribute state, mutations, action ที่เราได้มาตั้งแต่ตอนแรกแล้ว ยังมีอีกตัวก็คือ `getters` เรามักใช้ getters ในกรณีที่เราต้องการคำนวนค่าของ state ก่อนนำออกมาใช้งาน ก็คือเราจะไม่อ้างไปถึง state ตรงๆ นั่นแหละ ไม่ว่าจะกำหนดค่า (ผ่าน action) และการดึงค่าออกมาเราก็จะทำผ่าน getters ตัวอย่างเช่น เราต้องการนับว่า items มีกี่อันแล้วใน state เราจะทำแบบนี้

```js
getters: {
  todoCount(state) {
    return state.items.length
  }
}
```

แล้วเวลาเรียกใช้เราก็สามารถเรียกใช้ได้แบบนี้

```
let itemCounts = this.$store.getters.todoCount
```

แต่โดยมากแล้วเราจะไม่อ้างถึง `this.$store` ตรงๆ แบบนี้เพื่อ commit mutation, get state หรืออะไรก็แล้วแต่เกี่ยวกับ store แต่จะส่งข้อมูลเข้าออก state ผ่าน `mapActions`, `mapGetters` แทน (อย่างไรก็ตาม ยังมี [mapMutations](https://vuex.vuejs.org/guide/mutations.html#committing-mutations-in-components) และ [mapState](https://vuex.vuejs.org/guide/state.html#the-mapstate-helper)) ดังนี้

```js
<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  computed: {
    ...mapGetters({
      todoCount: 'todoCount'
    })
  },
  methods: {
    ...mapActions({
      addItem: 'addItem'
    }),
    addTodo() {
      this.addItem({item: 'b'})
    }
  }
}
</script>
```

โดย `mapActions` จะ return ออกมาเป็น actions ทั้งหมดที่เรามีใน store และเช่นเดียวกัน `mapGetters` จะ return getters ทั้ืหงมดที่เรามีออกมาให้เราใช้ โดยเราสามารถระบุ actions หรือ getters ที่ต้องการนำมาใช้ได้ตามโค้ดตัวอย่างด้านบน จะทำให้ vue instance ตัวนี้มองเห็น computed attribute ตัวอื่นๆ และมองเห็น method ตัวอื่นๆ เพิ่มเติม ซึ่งสามารถเรียกใช้ได้ตามปกติ

อ่านเพิ่ม

-   [Dispatching Actions in Components](https://vuex.vuejs.org/guide/actions.html#dispatching-actions-in-components)
-   [The mapGetters Helper](https://vuex.vuejs.org/guide/getters.html#the-mapgetters-helper)

มาถึงตรงนี้ เราก็ได้ทำความรู้จักกับ Vue.js กันมาประมาณหนึ่งแล้ว ตั้งแต่ Vue Instance, Directive, Component, Vue Router และ Vuex หวังว่าบทความนี้จะช่วยให้สามารถเริ่มต้น Vue.js ได้อย่างรวดเร็ว สำหรับคนที่ต้องการความรวดเร็วในการเริ่มต้นได้ไม่น้อย


> [Source : ](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE1NTQ5NDQxXX0=
-->