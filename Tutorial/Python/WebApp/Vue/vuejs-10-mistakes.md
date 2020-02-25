10 สิ่งที่คนเริ่มต้นใช้ Vue.js ควรรู้
====
ช่วงที่ผมหัดเขียน Vue.js ใหม่ ๆ ผมได้เจอปัญหาหลาย ๆ อย่าง ผมจึงพยายามเอามารวมไว้ เผื่อคนที่กำลังหัดเขียน Vue.js อยู่แล้วเจอปัญหาเดียวกัน จะได้เอา solution ที่ผมลองผิดลองถูกไปใช้ได้เลย หรือใครมี solution ที่ดีก็นี้ก็แนะนำผมได้นะครับ เพราะผมก็พึ่งหัดเขียน Vue.js เหมือนกัน

## 1. อย่าคำนวณใน template

ใครที่เคยเขียน Angular มา บางคนจะติดนิสัยชอบเขียนโค้ดคำนวณใน template เช่น {{ list.splice(1, 2).reverse() }} แต่ใน Vue.js template จะเป็นแค่ส่วนที่แสดงข้อมูลอย่างเดียว ถ้าจะคำนวณให้ใส่ใน computed แทน เช่น

<template>  
  <p v-for="x in result">{{ x }}</p>  
</template>  
<script>  
  export default {  
    data () {  
      return { list: [1, 2, 3, 4] }  
    },  
    computed: {  
      result () {  
        return this.list.splice(1, 2).reverse()  
      }  
    }  
  }  
</script>

และ filter สามารถใช้ได้เฉพาะใน text interpolations เท่านั้น เช่น

{{ x | toUpper }}

แต่แบบนี้ไม่สามารถใช้ได้

<p v-html="x | toUpper"></p>  
<p v-for="x in list | limitBy(10)"></p>

ดังนั้น เราจึงต้องใช้ computed แทน

## 2. ใช้ ref แทน id

ใน Vue.js มีคำสั่ง ref ให้ใช้งานใน DOM แทนการใช้ id ทำให้สามารถใช้แทน jQuery ได้ และเร็วกว่าด้วย

<template>  
  <form>  
    <input ref="file" type="file" style="display: none;">  
    <button [@click](http://twitter.com/click)="selectFile">Select File</button>  
  </form>  
</template>  
<script>  
  export default {  
    methods: {  
      selectFile () {  
        this.$refs.file.click()  
      }  
    }  
  }  
</script>

หรือจะเขียนไปใน DOM เลยก็ได้ ถ้าเป็นคำสั่งง่าย ๆ อย่างการ click

<template>  
  <form>  
    <input ref="file" type="file" style="display: none;">  
    <button [@click](http://twitter.com/click)="$refs.file.click()">Select File</button>  
  </form>  
</template>

## 3. mounted ไม่ได้ guarantee ว่า this.$el จะอยู่ใน DOM

เวลาที่เราจะเรียกใช้ jQuery กับ Vue.js ต้องรอให้ this.$el หรือ this.$refs เข้าไปใน DOM ก่อนถึงจะเรียกได้ ใน Vue.js 1 มี ready hook เพื่อบอกว่า component ready แล้ว แต่ใน Vue.js 2 นั้นไม่มี ready ให้ใช้ มีแต่ mounted ให้ใช้แทน ดังนั้นถ้าต้องการใช้ jQuery แล้วจะต้องรอให้ mounted จบก่อน

export default {  
  mounted () {  
    this.$nextTick(() => {  
      $(this.$el).accordion()  
    })  
  }  
}

## 4. อย่าลืม call jQuery หลัง update data ด้วย

เวลาที่เรา update data แล้ว DOM ถูก render ใหม่ ต้อง call jQuery ใหม่ด้วย

export default {  
  props: [‘rating’],  
  mounted () {  
    this.$nextTick(this.updateDOM)  
  },  
  updated () {  
    this.updateDOM()  
  },  
  methods: {  
    updateDOM() {  
      $(this.$refs.rating).rating()  
    }  
  }  
}

## 5. ใช้ <router-link> แทน <a> เวลา navigate ภายในเว็บ

เราจะใช้ <a> เฉพาะ navigate ออกไปที่อื่น เพราะถ้าใช้ <a> navigate ในเว็บจะทำให้เว็บถูกโหลดใหม่

<template>  
  <div>  
    <a :href="`/user/${userId}`">User {{ userId }}</a>  
    <router-link :to="`/user/${userId}`">User {{ userId }}</router-link>  
  </div>  
</template>

## 6. check data ทุกครั้งเวลาแสดงผล

Vue.js ไม่เหมือน Angular ที่ถ้า data เป็น null หรือ undefined มันจะข้ามไปเลย แต่ใน Vue.js จะ error

<template>  
  <div v-if="data">  
    <h1>{{ data.title }}</h1>  
  </div>  
</template>  
<script>  
  export default {  
    data () { return { data: null } },  
    created () {  
      setTimeout(() => {  
        this.data = { title: 'test' }  
      }, 5000)  
    }  
  }  
</script>

จากตัวอย่างถ้าไม่ใส่ v-if จะมี error ตอนที่ data ยังเป็น null อยู่

## 7. Reuse Component

เนื่องจาก Vue.js จะใช้ Component เดิม เช่น เราอยู่ในหน้า /user/10 แล้วเราจะเปลี่ยนไปหน้า /user/11 Vue.js จะไม่สร้าง Component ใหม่

<template>  
  <div v-if="data">  
    <h1>{{ data.name }}</h1>  
    <router-link :to="`/user/${data.id - 1}`">Prev</router-link>  
    <router-link :to="`/user/${data.id + 1}`">Next</router-link>  
  </div>  
</template>  
<script>  
  import { User } from '../services'  
  export default {  
    data () {  
      return { data: null }  
    },  
    created () {  
      User.get(this.$route.params.id)  
        .subscribe(  
          (data) => {  
            this.data = data  
          }  
        )  
    }  
  }  
</script>

ถ้าลองรันดูจะเห็นว่าเวลาเรากดปุ่ม Prev หรือ Next, URL ของเว็บจะเปลี่ยน แต่ data ยังเป็นค่าเดิม เพราะ Vue.js ไม่ได้สร้าง Component ใหม่ ดังนั้นเราต้อง watch ว่าเมื่อไร route เปลี่ยน

export default {  
  data () {  
    return { data: null }  
  },  
  created () {  
    this.init()  
  },  
  watch: {  
    $route () {  
      this.init()  
    }  
  },  
  methods: {  
    init () {  
      User.get(this.$route.params.id)  
        .subscribe(  
          (data) => {  
            this.data = data  
          }  
        )  
    }  
  }  
}

## 8. Submit form ต้อง prevent ด้วย

<form @submit="signIn"></form>

จากโค้ดข้างบน เวลา form ถูก submit หน้าเว็บจะถูก refresh ดังนั้นเราต้อง prevent ไม่ให้ใช้ behavior ของ onsubmit

<form @submit.prevent="signIn"></form>

## 9. ระวัง path ตอนสร้าง router

ตอนสร้าง router ใน Vue.js จะไม่เหมือนกับ library ตัวอื่น เช่น

const router = new VueRouter({  
  mode: 'history',  
  routes: [  
    { path: '/home', component: Layout,  
      children: [  
        { path: '', component: Home },  
        { path: '/profile', component: Profile },  
        { path: 'list', component: List }  
      ]  
    }  
  }  
})

เราจะได้ routes ที่เป็น  
/home => Home  
/home/list => List  
/profile => Profile  
แต่ /home/profile ไม่มี

## 10. One-way data-binding

ใน Vue.js 2 เวลาส่ง data ผ่าน props จะเป็นแบบ one-way เท่านั้น ดังนั้นถ้าเราแก้ค่าใน component ข้างล่าง ค่าใน component ข้างบนจะไม่เปลี่ยนตาม เราจึงต้องใช้ emit ในการส่งค่าแทน

// FormData component  
<template>  
  <div>  
    <input v-model="data">  
    <button [@click](http://twitter.com/click)="$emit('submit', data)">Submit</button>  
  </div>  
</template>  
//---------------  
<template>  
  <div>  
    <form-data @submit="save"></form-data>  
  </div>  
</template>

หรือใครจะ advance กว่านี้ก็สามารถใช้กับ v-model ได้เลย โดยการ $emit(‘value’, $event.target.value) component ข้างบนก็สามารถใช้ <my-comp v-model=”data”></my-comp> ได้เลย

> [Source : ](https://medium.com/acoshift/vuejs-10-mistakes-ae2968e1156e).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2OTk4NTcwMl19
-->