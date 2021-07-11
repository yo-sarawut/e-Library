
Working Analog Clock using HTML CSS & JavaScript
==
![enter image description here](https://codingnepalweb.com/wp-content/uploads/2021/05/Working2BAnalog2BClock2Busing2BHTML2BCSS2Band2BJavascript.png)

## **Working Analog Clock in HTML CSS & JavaScript [Source Codes]**

To create this program (Working Analog Clock). First, you need to create two Files one HTML File and another one is CSS File. After creating these files just paste the following codes in your file.

First, create an HTML file with the name of index.html and paste the given codes in your HTML file. Remember, you’ve to create a file with .html extension.
```html
<!DOCTYPE html>
<!-- Created By CodingNepal -->
<html lang="en" dir="ltr">
   <head>
      <meta charset="utf-8">
      <title>Neumorphism Analog Clock | CodingNepal</title>
      <link rel="stylesheet" href="style.css">
   </head>
   <body>
      <div class="clock">
         <div class="center-nut"></div>
         <div class="center-nut2"></div>
         <div class="indicators">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
         </div>
         <div class="sec-hand">
            <div class="sec"></div>
         </div>
         <div class="min-hand">
            <div class="min"></div>
         </div>
         <div class="hr-hand">
            <div class="hr"></div>
         </div>
      </div>
      <script>
         const sec = document.querySelector(".sec");
         const min = document.querySelector(".min");
         const hr = document.querySelector(".hr");
         setInterval(function(){
           let time  = new Date();
           let secs = time.getSeconds() * 6;
           let mins = time.getMinutes() * 6;
           let hrs = time.getHours() * 30;
           sec.style.transform = `rotateZ(${secs}deg)`;
           min.style.transform = `rotateZ(${mins}deg)`;
           hr.style.transform = `rotateZ(${hrs+(mins/12)}deg)`;
         });
      </script>
   </body>
</html>
```
Second, create a CSS file with the name of style.css and paste the given codes in your CSS file. Remember, you’ve to create a file with .css extension.

```css

```











> Reference : https://www.codingnepalweb.com/working-analog-clock-javascript/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTM4MTI4NzZdfQ==
-->