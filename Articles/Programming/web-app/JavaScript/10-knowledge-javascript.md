
# 10 เรื่องน่ารู้ตอบข้อสงสัย JavaScript

ในการเขียนภาษา JavaScript นั้นมีทั้งสิ่งที่เหมือนและแตกต่างกับภาษาโปรแกรมอื่นๆ สำหรับคนที่ใช้งาน JavaScript ไม่ว่าจะเพิ่งเริ่มศึกษาหรือใช้มานานแล้ว ก็อาจจะยังมีบางเรื่องที่สงสัยหรือยังไม่รู้เกี่ยวกับ JavaScript อยู่ เราจึงรวบรวม 10 เรื่องน่ารู้เกี่ยวกับ JavaScriptมาให้ได้ลองอ่านกัน

### 1.  **การประกาศตัวแปร Var, Let, Const ใช้แบบไหน**

ในการเขียนโค้ด การประกาศตัวแปรก็เป็นสิ่งแรกๆ ที่น่าจะเจอในการเริ่มต้นศึกษาภาษานั้นๆ ใน JavaScript ก็เช่นกัน สำหรับคนที่เริ่มศึกษา JavaSctipt น่าจะเคยเห็นผ่านตามาบ้างก็คือ var, let และ const เพื่อการนำไปใช้งานอย่างถูกต้อง ลองมาดูกันว่าการประกาศแต่ละแบบนั้นต่างกันอย่างไรบ้าง
```js
function run() {
    const myNum = 191;
    var one = "One";
    let two = "Two";
    {
        var three = "Three";
        let four = "Four";
    }
    console.log(one);    //Output: One
    console.log(two);    //Output: Two
    console.log(three);  //Output: Three
    console.log(four);   //Uncaught ReferenceError
}
run();
```
-   var – สำหรับการประกาศค่าด้วย var นั้น น่าจะเป็นแบบที่ทุกเคยเห็นกันแน่นอน ซึ่งการใช้ var นั้นเคยเป็นหลักในการประกาศตัวแปรมาก่อนที่ ES6 จะออกมา ซึ่งการประกาศด้วย var นั้นจะเป็นแบบ function scope เมื่อประกาศตัวแปรแล้วจะสมารถนำไปใช้ได้ภายในฟังก์ชันนั้นได้ทั้งหมด
-   let – เป็นการประกาศตัวแปรที่ออกมาพร้อมกันกับ const ซึ่งมาพร้อมกับอัพเดต ES6 เพื่อช่วยให้การเขียน JavaScript นั้นง่ายขึ้น โดย let เมื่อประกาศแล้วตัวแปรจะมีค่าอยู่แค่ภายใน block scope คือแค่ภายในเครื่องหมาย { และ } ทำให้ไม่เกิดปัญหาการอ้างอิงตัวแปรเก่า เช่น การใช้ตัวแปรใน loop ค่างๆ ที่ต้องการประกาศค่าขึ้นมาใหม่
-   const – ใช้สำหรับประกาศค่าตัวแปรที่ไม่ต้องการให้เปลี่ยนแปลงค่าได้ เพราะเมื่อประกาศค่าไปแล้วจะไม่สามรถแก้ไขค่านั้นซ้ำได้ โดย const นั้นทำงานภายใน block scope เหมือนกันกับ let

### 2. ชนิดของตัวแปร

JavaScript เป็น dynamic data type คือตัวแปรหนึ่งตัวนั้น สามารถกำหนดค่าที่ชนิดแตกต่างกันให้กับตัวแปรนั้นๆได้
```js
var x =  10; console.log(x);  //Output: 10 x =  "hello"; console.log(x);  //Output: hello x =  [1,  2,  3]; console.log(x);  //Output: [1,2,3]
```
จะเห็นว่าในตอนแรกนั้นตัวแปร x นั้นถูกกำหนดค่า string ไว้ แต่ภายหลังก็สามารถกำหนดค่าด้วย number หรือ array ให้กับตัวแปร x ได้เช่นกัน ในด้านหนึ่งนึงนี่คือความง่ายในการเขียนโค้ด แต่เมื่อโค้ดมีความซับซ้อนขึ้น หรือในการนำไปใช้ในโปรเจ็กใหญ่ๆ การที่ไม่ระบุชนิดของตัวแปรก็อาจจะกลายเป็นความยุ่งยากในการพัฒนาได้ ซึ่งถ้าอยู่ในจุดนั้นคงต้องหาทางเลือกอื่น เช่นการเปลี่ยนไปใช้ TypeScript ในการพัฒนาแทน

### 3. เครื่องหมาย == กับ === ต่างกันยังไง ?

การสร้างอัลกอริทึมขึ้นมา operator สำหรับการเปรียบเทียบค่าพื้นฐานย่อมเป็นสิ่งจำเป็นที่มีอยู่ในโค้ด เช่น มากกว่า, น้อยกว่า, เท่ากัน หรือ ไม่เท่ากัน สำหรับเครื่องหมายที่ใช้ในการเปรียบเทียบความเท่ากันนั้น อาจจะเคยเห็นหรือเคยใช้ทั้ง == และ === มาแล้ว แต่อาจจะยังไม่เข้าใจว่ามันมีอะไรที่ต่างกัน
```js
var a =  10;  var b =  '10'; a == b // Output: true a === b // Output: false
```
-   == จะใช้สำหรับเปรียบเทียบความเท่ากัน (equality)
-   === ใช้ในการเปรียบเทียบความเหมือนกัน/เป็นอย่างเดียวกัน (identically)

ในการใช้งาน == นั้นจะทำการแปลงชนิดของตัวแปรเพื่อเปรียบเทียบกัน ในขณะที่ === จะไม่ทำการแปลงชนิดของข้อมูล แต่จะเปรียบเทียบทั้ง ชนิดของตัวแปร และค่าของตัวแปร โดยตรง

### 4. What Is ‘This’ ?

ในภาษาอื่นๆเช่น Java นั้น this จะใช้เพื่ออ้างอิงถึง Object ที่กำลังใช้งานอยู่ อย่างเช่น method ภายในคลาสที่ต้องการเรียกค่าตัวแปรภายในคลาสนั้น ก็สามารถระบุได้ด้วยการใช้ this แต่ในส่วนของ JavaScript นั้นจะต่างออกไป โดยจะเปลี่ยนไปตามบริบทที่ใช้งาน เช่น
```js
// สร้าง Object  var pet =  { name:  "Foo", weight:  15, info:  function()  {  return  "Name: "  +  this.name+  ", Weight: "  +  this.weight;  }  };
```
-   this ใน method จะอ้างอิงถึง Object ที่เป็นเจ้าของ เช่นเดียวกันกับภาษา OOP อื่น
```js
var x =  10;  function run()  {  var x =  20; console.log(x);  //Output: 20 console.log(this.x);  //Output: 10  } run();
```
-   this ใน function จะอ้างอิงถึง Window Object
```js
<button  onclick="console.log(this.tagName);"> Click Me </button> //Output: BUTTON
```
-   this ใน event handler จะอ้างอิงถึง HTML Element ที่เป็นตัวทำให้เกิด event นั้นๆ

### 5. Null กับ Undefined ต่างกันยังไง ?

สำหรับคนที่เคยเขียน JavaJcript น่าจะเคยเจอ error เกี่ยวกับ null และ undefined มาบ้าง ซึ่งทั้งสองอย่างก็ล้วนแต่เป็นปัญหาเกี่ยวกับตัวแปรเวลาเขียนโค้ดเหมือนๆกัน แล้วสองอย่างนี้แตกต่างกันตรงไหน?
```js
var myVarA; console.log(myVarA);  //Output: undefined  var myVarB =  null; console.log(myVarB);  //Output: null
```
-   Undefined นั้นหมายถึงว่าตัวแปรนั้นถูกประกาศเรียบร้อยแล้วแต่ยังไม่ได้กำหนดค่าให้ตัวแปร
-   Null นั้นเป็นค่าที่ใช้กำหนดให้กับตัวแปรเพื่อสื่อความหมายว่า ตัวแปรนั้นไม่มีค่าอะไร

นอกจากความหมายของทั้งสองตัวจะต่างกันแล้ว ยังมีข้อสังเกตอีกว่า undefined นั้นจะเป็นค่าเริ่มต้นที่โปรแกรมจะกำหนดให้ตัวแปรที่ถูกสร้างขึ้นแต่ยังไม่ได้กำหนดค่าเสมอ ส่วน null นั้นจะเป็นค่าที่โปรแกรมเมอร์เป็นคนกำหนดให้กับตัวแปร (รูปแกนทิชชู)

### 6. For / ForEach / For-In / For-Of แบบไหนใช้ยังไง ?

ในการเขียนโปรแกรมยังไงก็คงหนีไม่พ้นการใช้ for loop เพราะใช้ในการทำซ้ำงานต่างๆ โดยหลักๆที่ภาษาโปรแกรมอื่นๆมีกันก็น่าจะเป็น for และ for each ที่แต่ละคนคงจะเคยคุ้นเคยกันแล้ว พอมาเป็น javascript ก็มีเช่นกัน แต่ถ้าใครได้ลองหาข้อมูลดูอาจจะได้เจอกับ for-in และ for-of ที่การใช้งานก็ดูคล้ายกันไปหมด แล้วทีนี้เราจะเลือกใช้ for แบบไหนตอนไหนดี
```js
let myArray =  [1,  2,  3]  for  (let index =  0; index < myArray.length; index++)  {  const element = myArray[index]; console.log(element);  }
```
```js
//Output  1  2  3
```
-   for – เริ่มที่ตัวพื้นฐาน สำหรับ for ตัวนี้ทุกคนต้องเคยใช้กันแน่นอน โดยจะเป็นการวนลูปตามค่า index ที่กำหนดไว้
```js
let myArray =  [1,  2,  3] myArray.forEach(element =>  { console.log(element);  });
```
```js
//Output  1  2  3
```
-   forEach – มาถึงตัวนี้ก็น่าจะรู้จักการทำงานของมันที่เหมือนกันกับภาษาอื่นๆ คือใช้เพื่อเข้าถึงข้อมูลใน Array ต่างๆ โดยที่เราไม่ต้องประกาศค่า index ในการวนลูปเอง แต่ forEach จะเข้าถึงข้อมูลใน Array ตั้งแต่ตำแหน่งแรกจนถึงสุดท้ายให้เรา
```js
var dog =  { name:  "Yoyo", color:  "black", age:  2  }  for  (const key in dog)  {  if  (dog.hasOwnProperty(key))  {  const element = dog[key]; console.log(key +  " : "  + element);  }  }
```
```
//Output name :  Yoyo color : black
```js
age :  2

-   for…in – สำหรับ for-in ของ javascript นั้นใช้สำหรับวนลูป Object ซึ่งจะได้เป็นชื่อ properties ของ Object นั้นๆ หรือก็คือ key นั่นเอง

// Array  var myArray =  [1,  2,  3];  for  (const iterator of myArray)  { console.log(iterator);  }

//Output  1  2  3

// String  var str =  "hello";  for  (const iterator of str)  { console.log(iterator);  }

//Output h
e
l
l
o

-   for…of – ตัวสุดท้ายกับ for…of ตัวนี้จะใช้งานได้กับ iterable object หมายความว่าอะไรก็ตามที่สามารถวนลูปได้ จะสามารถใช้ for…of ได้นั่นเอง เช่น array, set หรือแม้แต่ string ก็สามารถใช้ได้

นี่เป็นเพียงแค่การวนลูปด้วย for ต่างๆเท่านั้น ยังไม่นับรวม while อีก จึงขึ้นอยู่กับการใช้งาน ว่าจะเลือกใช้อันไหนให้เหมาะสมกับความต้องการของเรา

### 7. Use Strict คืออะไร ?

หลายคนที่เคยได้อ่านโค้ด JavaScript น่าจะเคยผ่านตากับ use strict ที่อยู่บรรทัดแรกของโค้ดมากันบ้าง แต่อาจจะไม่รู้ว่ามันมีไว้เพื่ออะไร use strict มีไว้เพื่อระบุว่าโค้ดในส่วนนั้นจะทำงานใน strict mode ซึ่งจะทำให้ใช้ตัวแปรที่ยังไม่ได้ประกาศไม่ได้ เนื่องจากใน javascript นั้นหากเรียกใช้ตัวแปรโดยไม่ได้ประกาศ var/let/const นำหน้าชื่อตัวแปร ตัวแปรนั้นจะถูกกำหนดเป็น global variables ดังนั้นเพื่อป้องกันความผิดพลาดในการประกาศค่าตัวแปรเราจึงสามารถใช้ use strict ได้

function myFunction1 ()  { x =  6; console.log(x);  //Output: 6  } myFunction1()

function myFunction2 ()  {  "use strict"; y =  7; console.log(y);  //Uncaught ReferenceError: y is not defined  } myFunction2()

### 8. Arrow Function ( => ) คืออะไร ?

สำหรับคนที่เพิ่งเริ่มศึกษา JavaScript เวลาค้นหาข้อมูลอาจจะเจอกับเครื่องหมาย => ที่มีคนมาตอบตามกระทู้คำถามต่างๆเช่นใน Stack Overflow แล้วงงว่ามันคืออะไร ชื่อของเครื่องหมายนี้ก็ตามหัวข้อนี้เลยคือ Arrow Function เป็นสิ่งที่มาพร้อมกับ ES6 เพื่อให้สามารถเขียนฟังก์ชันได้สั้นลง

// แบบปกติ sayHi =  function()  {  return  "Hi Human";  }

// แบบใช้ Arrow Function sayHi =  ()  =>  {  return  "Hi Human";  }

### 9. String จะใช้ ‘ ’ , “ ” หรือ ` ` ?

การประกาศค่าให้กับตัวแปรชนิด string ใน JavaScript เราน่าจะเคยเห็นหรือใช้ทั้ง ‘ ’ (single quote) และ “ ” (double quote) ซึ่งทำงานได้เหมือนกันทุกประการ ขึ้นอยู่กับความชอบของแต่ละคน โดยจุดที่แตกต่างกันคือ

var str =  'Hello it\'s me'; console.log(str);  //Output: Hello it's me

-   single quote – ต้องใช้ Escape character สำหรับพิมพ์ single quote

var str =  "Hello from the \"other\" side"; console.log(str);  //Output: Hello from the "other" side

-   double quote – ต้องใช้ Escape character สำหรับพิมพ์ double quote

จากสองแบบข้างต้นก็จะทำให้ความยากง่ายในการประกาศค่าตัวแปร string ต่างกันออกไปขึ้นอยู่กับว่าเป็นประโยคแบบไหน เราก็สามารถเลือกใช้ตามความเหมาะสมได้ แต่ยังมีอีกเครื่องหมายนึงที่ใช้ประกาศค่า string ได้ ก็คือ ` ` (backtick) ก็คือเครื่องหมายที่อยู่ปุ่มเดียวกันกับปุ่มตัวหนอนที่มักใช้สำหรับเปลี่ยนภาษากันนั่นเอง ส่วนการนำไปใช้งานนั้น

str =  `Hello it's me from the "other" side`; console.log(str);  //Output: Hello it's me from the "other" side

-   backtick – ไม่ต้องใช้ Escape character ในเวลาที่พิมพ์ทั้ง single quote และ double quote

จะเห็นได้ว่าการใช้ backtick นั้นช่วยให้การประกาศค่า string นั้นทำได้ง่ายขึ้น และโค้ดอ่านได้ง่าย แต่ท้ายที่สุกแล้วก็วนกลับไปที่ความถนัดของแต่ละคนหรือสไตล์ที่คนในทีมเลือกใช้กัน ที่จะเป็นตัวตัดสินว่าเราจะเลือกใช้รูปแบบไหนในการเขียนโค้ดของเราออกมา

### 10. Boolean ใน Javascript อะไรบ้างที่เป็น True หรือเป็น False

ใน javascript นั้นค่าความจริงหรือ Boolean นั้นมี 2 ค่าด้วยกันนั่นคือ true และ false แต่นอกจากสองอย่างนี้แล้วสิ่งอื่นๆก็ล้วนนำมาเป็นค่าความจริงได้ โดยหลักการมีง่ายๆคือ

console.log(Boolean("hello"));  // true console.log(Boolean(5));  // true console.log(Boolean(9.99));  // true console.log(Boolean(1  +  2  +  3  +  4  +  5));  // true

-   อะไรก็ตามที่ “มีค่า” จะนับเป็น true เช่น “hello”, 5, 9.99, 1+2+3+4+5

console.log(Boolean(""));  // false console.log(Boolean(0));  // false console.log(Boolean(-0));  // false console.log(Boolean(null));  // false console.log(Boolean(undefined));  // false

-   ส่วนอะไรก็ตามที่ “ไม่มีค่า” จะนับเป็น false เช่น “”, 0, -0, null, undefined

**อ้างอิง**

JavaScript Tutorial, available in  
https://www.w3schools.com/js/, 2020.

JavaScript reference, available in  
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference, 2020.

เรื่องของ this ใน JavaScript และวิธีการใช้ bind, call, apply, available in  
https://www.tamemo.com/post/118/what-is-js-this-bind-call-apply/


> Written with [StackEdit](https://www.borntodev.com/2020/01/06/10-%E0%B9%80%E0%B8%A3%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B8%87%E0%B8%99%E0%B9%88%E0%B8%B2%E0%B8%A3%E0%B8%B9%E0%B9%89-javascript/?fbclid=IwAR1V0oMlnI4gMBj72bhjLyBz5kxVE_jkgGiUMuPcHy9A49QJJJts5vcQLj0).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxODEwOTYyNF19
-->