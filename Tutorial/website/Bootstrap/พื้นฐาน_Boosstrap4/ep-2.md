# สรุปการใช้งาน Bootstrap 4 แบบพื้นฐาน ตอนที่ 2

![enter image description here](https://benzneststudios.com/blog/wp-content/uploads/2018/11/cover2-1.png)

## Table

สร้างไฟล์ใหม่ชื่อ portal.html  
ใส่โค้ดพื้นฐาน html ลงไปแล้วก็เพิ่ม bootstrap.css ด้วย
```html
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"  content="width=device-width, initial-scale=1.0">

<meta http-equiv="X-UA-Compatible"  content="ie=edge">

<title>Portal</title>

<link rel="stylesheet"  href="css/bootstrap.min.css"  />

</head>

<body>

<div class="container">

<div class="row">

<div class="col">

</div>

</div>

</div>

</body>

</html>
```
ใส่ตารางลงไปใน container


```html
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"  content="width=device-width, initial-scale=1.0">

<meta http-equiv="X-UA-Compatible"  content="ie=edge">

<title>Portal</title>

<link rel="stylesheet"  href="css/bootstrap.min.css"  />

</head>

<body>

<div class="container">

<div class="row">

<div class="col">

<h1>Portal</h1>

<table>

<thead>

<tr>

<th>No...</th>

<th>Name</th>

<th>Status</th>

<th>Age</th>

<th>Address</th>

<th>Department</th>

</tr>

</thead>

<tbody>

<tr>

<td>1</td>

<td>Benz</td>

<td>Normal</td>

<td>35</td>

<td>Bangkok  10000</td>

<td>IT</td>

</tr>

<tr>

<td>2</td>

<td>Namnueng</td>

<td>NA</td>

<td>35</td>

<td>Bangkok  10000</td>

<td>IT</td>

</tr>

<tr>

<td>3</td>

<td>Pare</td>

<td>NA</td>

<td>35</td>

<td>Bangkok  10000</td>

<td>IT</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</body>

</html>
```
จะได้แบบนี้

![40](https://benzneststudios.com/blog/wp-content/uploads/2018/11/40.png)

Bootstrap มี class ชื่อว่า table ทำให้ตารางสวยขึ้น

```html
<table class="table">
```
![41](https://benzneststudios.com/blog/wp-content/uploads/2018/11/41.png)

ปรับแต่งหัวตารางโดยใช้ utility class คือ bg- และ text-


```html
<table class="table">

<thead>

<tr class="bg-primary text-white">

...
```
![42](https://benzneststudios.com/blog/wp-content/uploads/2018/11/42.png)

ทำให้ตารางสลับสี ใช้ table-striped เพิ่มเข้าไป


```html
<table class="table table-striped">
```
![43](https://benzneststudios.com/blog/wp-content/uploads/2018/11/43.png)

ทำให้ตารางเลื่อสีไปตาม cursor ใช้ table-hover เพิ่มเข้าไป


```html
<table class="table table-hover">
```
![g5](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g5.gif)

ใส่ขอบให้ตารางใช้ table-bordered
```html
<table class="table table-hover table-bordered">
```
![44](https://benzneststudios.com/blog/wp-content/uploads/2018/11/44.png)

ลองย่อหน้าต่างให้เล็กเป็นมุมมองมือถือ จะพบว่าตารางไม่รองรับ responsive

[![46a](https://benzneststudios.com/blog/wp-content/uploads/2018/11/46a.png)

วิธีการแก้ก็คือเอาตารางไปใส่ใน div class **table-responsive**


```html
<div class="table-responsive">

<table class="table table-hover table-bordered">

...

</table>

</div>
```
มันจะสามารถเลื่อน ซ้ายขวาได้

![g6](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g6.gif)

ใน VS Code ตรงไหนโค้ดยาวก็ย่อโค้ดได้นะ

[![47](https://benzneststudios.com/blog/wp-content/uploads/2018/11/47.png)

### Source code

[https://gist.github.com/benznest/d7b07ec41ffef49429ec4c95112c1dcb](https://gist.github.com/benznest/d7b07ec41ffef49429ec4c95112c1dcb)

## Form

สร้างไฟล์ใหม่ login.html จะลองทำหน้า login กัน อย่าลืมเพิ่ม boostrap.css เข้ามาด้วย

ฟอร์มล้อคอินที่จะทำ หน้าตาประมาณนี้

![50](https://benzneststudios.com/blog/wp-content/uploads/2018/11/50.png)

ลองใส่ฟอร์มล็อกอิน แบบง่ายๆ


```html
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"  content="width=device-width, initial-scale=1.0">

<meta http-equiv="X-UA-Compatible"  content="ie=edge">

<title>Portal</title>

<link rel="stylesheet"  href="css/bootstrap.min.css"  />

</head>

<body>

<div class="container">

<div class="row">

<div class="col">

<form action="#">

<label for="usernmae">Username:  </label>

<input type="text"  id="username"  name="username">

<label for="pwd">Password:  </label>

<input type="password"  id="pwd"  name="pwd">

<button type="submit">Sign in</button>

</form>

</div>

</div>

</div>

</div>

</body>

</html>
```
![48](https://benzneststudios.com/blog/wp-content/uploads/2018/11/48.png)

ให้ใช้ class  **form-group**  จัดการแถวของฟอร์ม


```html
<form action="#">

<div class="form-group">

<label for="usernmae">Username:  </label>

<input type="text"  id="username"  name="username">

</div>

<div class="form-group">

<label for="pwd">Password:  </label>

<input type="password"  id="pwd"  name="pwd">

</div>

<button type="submit">Login</button>

</form>
```
![49](https://benzneststudios.com/blog/wp-content/uploads/2018/11/49.png)

ใช้ class  **form-control**  ให้กับ input เพื่อให้มันรองรับ responsive และความสวยงาม


```html
<input class="form-control"  type="text"  id="username"  name="username">
```
![51](https://benzneststudios.com/blog/wp-content/uploads/2018/11/51.png)
ส่วนปุ่มใช้ class ชื่อว่า  **btn** และอยากได้ส้มๆก็ใส่ **btn-warning**


```html
<button class="btn btn-warning text-white"  type="submit">Login</button>
```
![52](https://benzneststudios.com/blog/wp-content/uploads/2018/11/52.png)

ถ้าต้องการให้ปุ่มแสดงตามขนาดจอ ก็ใช้ **btn-block**


```html
<button class="btn btn-block btn-warning text-white"  type="submit">Login</button>
```
![53](https://benzneststudios.com/blog/wp-content/uploads/2018/11/53.png)

ถ้าต้องการให้แสดงแบบแถวเดียวใช้ **form-inline**
```html

<form action="#"  class="form-inline">
```
![54](https://benzneststudios.com/blog/wp-content/uploads/2018/11/54.png)

ฟอร์มมันชิดไป ไม่สวยก็สามารถใช้ class margin มาร่วมได้


```html

<form action="#"  class="form-inline mt-3">

<div class="form-group">

<label class="mr-2"  for="usernmae">Username:  </label>

<input class="form-control mr-3"  type="text"  id="username"  name="username">

</div>

<div class="form-group">

<label class="mr-2"  for="pwd">Password:  </label>

<input class="form-control mr-3"  type="password"  id="pwd"  name="pwd">

</div>

<button class="btn btn-warning text-white"  type="submit">Login</button>

</form>
```
![55](https://benzneststudios.com/blog/wp-content/uploads/2018/11/55.png)

### Source code

[https://gist.github.com/benznest/1d77e1a799253e5546b8d4c836cd2f1c](https://gist.github.com/benznest/1d77e1a799253e5546b8d4c836cd2f1c)

## Card

อีกอันที่ใช้บ่อยๆ คือ card มันคือการทำเนื้อหาเป็นบล็อกๆ

สร้างไฟล์ใหม่ชื่อว่า news.html ทำ grid ไว้ 2 คอลัมภ์


```html

<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport"  content="width=device-width, initial-scale=1.0">

<meta http-equiv="X-UA-Compatible"  content="ie=edge">

<title>News</title>

<link rel="stylesheet"  href="css/bootstrap.min.css"  />

</head>

<body>

<div class="container">

<div class="row">

<div class="col">

<!--  Col  1  -->

</div>

<div class="col">

<!--  Col  2  -->

</div>

</div>

</div>

</body>

</html>
```
Card โครงสร้างจะเป็นประมาณนี้


```html

<div class="container">

<div class="row">

<div class="col">

<div class="card">

<div class="card-header">

<h4>Hot news</h4>

</div>

<div class="card-body">

<p>Lorem ipsum dolor,  sit amet consectetur adipisicing elit.  Dolorem minus accusantium rerum suscipit,  commodi sapiente,  saepe doloremque beatae quod architecto voluptatibus.  Nobis ratione excepturi omnis incidunt laboriosam quidem quae quibusdam!</p>

</div>

<div class="card-footer">

By Benznest

</div>

</div>

</div>

<div class="col">

<!--  Col  2  -->

</div>

</div>

</div>
```
![58](https://benzneststudios.com/blog/wp-content/uploads/2018/11/58.png)

![56](https://benzneststudios.com/blog/wp-content/uploads/2018/11/56.png)

สามารถจัดแต่งโดยใช้ utilities class ได้ตามปกติ เช่น bg และ text
```html
<div class="card-header bg-danger text-white">
```
![57](https://benzneststudios.com/blog/wp-content/uploads/2018/11/57.png)

สามารถนำรูปมาเป็น Header ได้ โดยใช้ class ชือว่า **card-img-top**

```html

<div class="row">

<div class="col">

...

</div>

<div class="col">

<div class="card">

<img class="card-img-top"  src="img/staffs/staff4.jpg"  >

<div class="card-body">

<h4 class="card-title">Our Staff</h4>

<p  class="card-text">Lorem ipsum dolor sit amet consectetur adipisicing elit.  Dolores excepturi modi voluptate animi repellat?  Animi accusantium numquam iste non voluptatem ipsum totam,  odio sequi.  Fuga amet qui vitae atque.  Illo.</p>

</div>

</div>

</div>

</div>
```
![59](https://benzneststudios.com/blog/wp-content/uploads/2018/11/59.png)

เพิ่มปุ่มใน card ให้ดูสวยงาม


```html
<a  href="#"  class="btn btn-primary">Read more</a>
```
![60](https://benzneststudios.com/blog/wp-content/uploads/2018/11/60.png)

ซึ่งถ้าจะทำสวยๆ ก็ต้องมีรูป และเนื้อหาที่เหมาะสมกัน

![61](https://benzneststudios.com/blog/wp-content/uploads/2018/11/61.png)

สามารถนำรูปมาวางด้านล่างแทนได้ โดยใช้ class ชื่อว่า  **card-img-bottom**


```html
<div class="card-body">

...

</div>
```
![62](https://benzneststudios.com/blog/wp-content/uploads/2018/11/62.png)

### Source code

[https://gist.github.com/benznest/bb45d6f0affd79d462a837055408f3c8](https://gist.github.com/benznest/bb45d6f0affd79d462a837055408f3c8)

## การใช้ Media

การนำคลิป youtube embed มาใช้ใน bootstrap  
ไปที่ youtube คลิกขวาที่คลิป > Copy embed code

![63a](https://benzneststudios.com/blog/wp-content/uploads/2018/11/63a.png)

มันจะเป็น iframe  ถ้ามี width height ให้ลบออก  เพราะ เราจะทำให้ responsive


```html
<iframe src="https://www.youtube.com/embed/5nLWk7kzXgI?ecver=1"

frameborder="0"  allow="accelerometer; autoplay; encrypted-media;

gyroscope; picture-in-picture"  allowfullscreen></iframe>
```
เพิ่ม `<div> `ครอบตัว video โดยเพิ่ม class ชื่อว่า  **embed-responsive embed-responsive-4by3  
**4by3 คือขนาด 4:3 สามารถใช้ตัวอื่นได้เช่น 16by9, 21by9, 1by1และที่ iframe เพิ่ม class ชื่อว่า **embed-responsive-item**

โดยจะลองเพิ่มแถวเข้าไปต่อจากเดิม

1

2

3

4

5

6

7

8

9

10

<div class="row mt-5">

<div class="col">

<h3>Video gallery</h3>

<div class="embed-responsive embed-responsive-4by3">

<iframe class="embed-responsive-item"  src="https://www.youtube.com/embed/5nLWk7kzXgI?ecver=1"  frameborder="0"  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"  allowfullscreen></iframe>

</div>

</div>

</div>

[![64](https://benzneststudios.com/blog/wp-content/uploads/2018/11/64.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/64.png "64")

ลองเพิ่มคอมลัมภ์อีกอันเพื่อทำ photo gallery ด้านขวาของ video  
ซึ่งสามารถใช้ class ชื่อว่า  **media** การทำงานของมันจะเรียงไปแนวนอน

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

<div class="row mt-5">

<div class="col-md-6">

...

</div>

<div class="col-md-6">

<h3>Photo gallery</h3>

<div class="media">

<img class="w-50"  src="img/content/office10.jpg">

<div class="media-body pl-3">

<p>Lorem,  ipsum dolor sit amet consectetur adipisicing elit.  Neque aliquam nisi officiis aut

beatae.  Voluptas,  aliquid!  Nostrum quam architecto  </p>

</div>

</div>

</div>

</div>

[![65](https://benzneststudios.com/blog/wp-content/uploads/2018/11/65.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/65.png "65")

การจะเพิ่มแถวของเนื้อหาที่ใช้ class media สามารถใช้  <ul class=”list-unstyled”>  และ <li> เข้ามาได้

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

<div class="col-md-6">

<h3>Photo gallery</h3>

<ul class="list-unstyled">

<li>

<div class="media">

<img class="w-50"  src="img/content/office1.jpg">

<div class="media-body pl-3">

<p>Lorem,  ipsum dolor sit amet consectetur adipisicing elit.  Neque aliquam nisi

officiis aut

beatae.  Voluptas,  aliquid!  Nostrum quam architecto  </p>

</div>

</div>

</li>

<li>

<div class="media">

<img class="w-50"  src="img/content/office3.jpg">

<div class="media-body pl-3">

<p>Lorem,  ipsum dolor sit amet consectetur adipisicing elit.  Neque aliquam nisi

officiis aut

beatae.  Voluptas,  aliquid!  Nostrum quam architecto  </p>

</div>

</div>

</li>

<li>

<div class="media">

<img class="w-50"  src="img/content/office2.jpg">

<div class="media-body pl-3">

<p>Lorem,  ipsum dolor sit amet consectetur adipisicing elit.  Neque aliquam nisi

officiis aut

beatae.  Voluptas,  aliquid!  Nostrum quam architecto  </p>

</div>

</div>

</li>

</ul>

</div>

[![66](https://benzneststudios.com/blog/wp-content/uploads/2018/11/66.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/66.png "66")

### Source code

[https://gist.github.com/benznest/17e5753cff346c5ed5ba8f4689377801](https://gist.github.com/benznest/17e5753cff346c5ed5ba8f4689377801)

## Navigation

เพิ่ม row ไปที่บนสุดของ container ข้างในใช้ list คือ <ul><li> … </li></ul>

1

2

3

4

5

6

7

8

9

10

<body>

<div class="container">

<div class="row">

<div class="col">

<ul><li><a  href="#">Home</a></li></ul>

</div>

</div>

...

ใน bootstrap จะใช้  
class ชื่อ nav ใน <ul>  
class ชื่อ nav-item ใน <li>  
class ชื่อ nav-link ใน <a> ที่เป็นป้ายลิงค์

1

2

3

4

5

6

7

8

9

10

11

12

<div class="row pt-3 pb-3">

<div class="col">

<ul class="nav">

<li class="nav-item"><a  class="nav-link"  href="#">Home</a></li>

<li class="nav-item"><a  class="nav-link"  href="#">Service</a></li>

<li class="nav-item"><a  class="nav-link"  href="#">About</a></li>

<li class="nav-item"><a  class="nav-link"  href="#">Contact</a></li>

</ul>

</div>

</div>

[![67](https://benzneststudios.com/blog/wp-content/uploads/2018/11/67.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/67.png "67")

เพิ่ม ให้เมนูนึงถูกเลือกใช้ class ชื่อว่า  **active**

1

2

3

<li class="nav-item"><a  class="nav-link active"  href="#">Home</a></li>

เพิ่ม class  **nav-pills**  ให้กับ <ul>

1

2

3

<ul class="nav nav-pills">

[![68](https://benzneststudios.com/blog/wp-content/uploads/2018/11/68.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/68.png "68")

หรือจะใช้ class **nav-tabs**

1

2

3

<ul class="nav nav-tabs">

[![69](https://benzneststudios.com/blog/wp-content/uploads/2018/11/69.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/69.png "69")

รายละเอียด

[https://getbootstrap.com/docs/4.1/components/navs/](https://getbootstrap.com/docs/4.1/components/navs/)

## การใช้ Javascript ของ Bootstrap

Bootstrap ต้องใช้ library เพิ่มคือ jquery กับ popper ถึงจะใช้งานได้เต็มประสิทธิภาพ ซึ่ง bootstrap ไม่มีติดมาให้ เพราะ ติด license จำเป็นต้องไปดาวน์ดหลดมาจากต้นทางผู้พัฒนา  
ให้ดาวน์โหลด jquery js กับ popper js มาติดตั้งไว้ในโปรเจค ในโฟลดเดอร์ js

[![71](https://benzneststudios.com/blog/wp-content/uploads/2018/11/71.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/71.png "71")

เพิ่ม jquery , popper , bootstrap ไปที่ท้าย body โดยใช้คำสั่ง <script></script>  
โดยให้ jquery และ popper อยู่ด้านบนของ bootstrap.js เพราะการอ่านโค้ดจะอ่านจากบนลงล่าง วึ่ง bootstrap เรียกใช้งาน jquery  
จึงจำเป็นต้องอ่าน jquery มาก่อนนั่นเอง

1

2

3

4

5

6

7

8

9

...

<script src="js/jquery-3.3.1.min.js"></script>

<script src="js/popper_1_14_3.min.js"></script>

<script src="js/bootstrap.min.js"></script>

</body>

</html>

ถ้าใส่ผิด สามารถ Inspect ดูที่เมนู console

[![72](https://benzneststudios.com/blog/wp-content/uploads/2018/11/72.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/72.png "72")

## การทำ dropdown

เพิ่ม dropdown ให้เมนู ได้ โดยใช้  **dropdown-menu**

1

2

3

4

5

6

7

8

9

10

11

<li class="nav-item dropdown">

<a  class="nav-link dropdown-toggle"  href="#"  data-toggle="dropdown">Service</a>

<div class="dropdown-menu">

<a  class="dropdown-item"  href="#">App</a>

<a  class="dropdown-item"  href="#">Website</a>

<a  class="dropdown-item"  href="#">Desktop</a>

<a  class="dropdown-item"  href="#">IoT</a>

</div>

</li>

[![73](https://benzneststudios.com/blog/wp-content/uploads/2018/11/73.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/73.png "73")

ปัญหาที่ตามมาคือ เมนูแบบนี้ไม่รองรับ responsive ดังนั้นต้องไปใช้ Navbar แบบใหม่

[![74](https://benzneststudios.com/blog/wp-content/uploads/2018/11/74.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/74.png "74")

## ติตดั้ง extension

ติดตั้ง Bootstrap v4 Snippets

[![70](https://benzneststudios.com/blog/wp-content/uploads/2018/11/70.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/70.png "70")

## Navbar responsive

พิมพ์ b-navbar มันจะ generate โค้ดมาให้

[![g7](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g7.gif)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g7.gif "g7")

ซึ่งเยอะมาก เรามีหน้าที่แก้เนื้อหาก็พอ นี่คือการใช้เครื่องมือให้เป็นประโยชน์

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

<nav class="navbar navbar-expand-lg navbar-light bg-light fixed-top">

<a  class="navbar-brand">Benznest's  blog</a>

<button class="navbar-toggler"  data-target="#my-nav"  data-toggle="collapse">

<span class="navbar-toggler-icon"></span>

</button>

<div id="my-nav"  class="collapse navbar-collapse">

<ul class="navbar-nav mr-auto">

<li class="nav-item"><a  class="nav-link active"  href="#">Home</a></li>

<li class="nav-item dropdown">

<a  class="nav-link dropdown-toggle"  href="#"  data-toggle="dropdown">Service</a>

<div class="dropdown-menu">

<a  class="dropdown-item"  href="#">App</a>

<a  class="dropdown-item"  href="#">Website</a>

<a  class="dropdown-item"  href="#">Desktop</a>

<a  class="dropdown-item"  href="#">IoT</a>

<a  class="dropdown-item"  href="#">Android</a>

<a  class="dropdown-item"  href="#">iOS</a>

<a  class="dropdown-item"  href="#">Windows</a>

<a  class="dropdown-item"  href="#">Linux</a>

</div>

</li>

<li class="nav-item"><a  class="nav-link"  href="#">About</a></li>

<li class="nav-item"><a  class="nav-link"  href="#">Contact</a></li>

</ul>

</div>

</nav>

Navbar อันใหม่จะรองรับ responsive

[![75](https://benzneststudios.com/blog/wp-content/uploads/2018/11/75.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/75.png "75")

[![76](https://benzneststudios.com/blog/wp-content/uploads/2018/11/76.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/76.png "76")[![77](https://benzneststudios.com/blog/wp-content/uploads/2018/11/77.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/77.png "77")

ปรับสีของ Navbar โดยใช้ class uitility

1

2

3

4

<nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top">

<a  class="navbar-brand text-white">Benznest's  blog</a>

[![78](https://benzneststudios.com/blog/wp-content/uploads/2018/11/78.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/78.png "78")

และเนื่องจาก Navbar มันใช้ Fix-top มันจะทำให้กินเนื้อด้านบน ก็ให้เนื้อหาของเราเว้นว่างด้านบนนิดนึง โดยใช้ pt-5 ก็คือ padding top 5 rem

1

2

3

4

5

6

...

</nav>

<div class="container pt-5">

...

## แนะนำ Bootswatch

bootswatch เป็นเว็บที่รวมแหล่งธีม css ของ bootstrap มาไว้ในที่เดียว เราสามารถดาวน์โหลดธีมที่ชอบมาใช้ได้ ซึ่งมันคือ css ของ bootstrap ดังนั้นสามารถนำมาใช้กับ bootstrap ได้เลย

[https://bootswatch.com/](https://bootswatch.com/)

กดดาวน์โหลดธีมที่ชอบ แล้วจะได้ไฟล์ .css

[![79](https://benzneststudios.com/blog/wp-content/uploads/2018/11/79.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/79.png "79")

เอาไฟล์ .css ไปไว้ในโฟลเดอร์ css แนะนำเปลี่ยนชื่อเป็นชื่อธีม ไม่ควรใช้ชื่อ bootstrap ทับอันเดิม

[![81](https://benzneststudios.com/blog/wp-content/uploads/2018/11/81.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/81.png "81")

ใน html ให้เปลี่ยนการใช้ bootstrap.min.css มาใช้ธีมอันใหม่

1

2

3

<link rel="stylesheet"  href="css/minty.min.css"  />

Refresh หน้าเว็บ

[![80](https://benzneststudios.com/blog/wp-content/uploads/2018/11/80.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/80.png "80")

## การใช้ Carousel

carousel คือ ตัวสไลด์รูปภาพ  
ใช้โค้ดลัด พิมพ์ว่า b-carousel เลือก carousel-full

[![g8](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g8.gif)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g8.gif "g8")

จากนั้นก็ปรับแต่ง carousel จะมีสามส่วน คือ  
indicator ที่เป็นจุด ว่ารูปภาพเราคือรูปไหน  
Slide คือรูปภาพ  
Button คือปุ่มซ้าย ขวา

active คืออันที่ถูกเลือกอยู่

[![82](https://benzneststudios.com/blog/wp-content/uploads/2018/11/82.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/82.png "82")

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

<div class="container-fluid mt-5 p-0">

<div id="my-carousel"  class="carousel slide"  data-ride="carousel"  data-interval="500">

<ol class="carousel-indicators"  >

<li class="active"  data-target="#my-carousel"  data-slide-to="0"></li>

<li class=""  data-target="#my-carousel"  data-slide-to="1"></li>

<li class=""  data-target="#my-carousel"  data-slide-to="2"></li>

</ol>

<div class="carousel-inner">

<div class="carousel-item active">

<img class="d-block w-100"  src="img/banner/banner3.jpg">

<div class="carousel-caption d-none d-md-block">

<h5>Hello  ,  world</h5>

<p>Lorem ipsum dolor sit amet consectetur adipisicing elit.  Ullam aliquid doloremque,  </p>

</div>

</div>

<div class="carousel-item">

<img class="d-block w-100"  src="img/banner/banner4.jpg">

<div class="carousel-caption d-none d-md-block">

<h5>Hello  ,  world</h5>

<p>Lorem ipsum dolor sit amet consectetur adipisicing elit.  Ullam aliquid doloremque,  </p>

</div>

</div>

<div class="carousel-item">

<img class="d-block w-100"  src="img/banner/banner5.jpg">

<div class="carousel-caption d-none d-md-block">

<h5>Hello  ,  world</h5>

<p>Lorem ipsum dolor sit amet consectetur adipisicing elit.  Ullam aliquid doloremque,  </p>

</div>

</div>

</div>

<a  class="carousel-control-prev"  href="#my-carousel"  data-slide="prev">

<span class="carousel-control-prev-icon"></span>

</a>

<a  class="carousel-control-next"  href="#my-carousel"  data-slide="next">

<span class="carousel-control-next-icon"></span>

</a>

</div>

การปรับเวลาในการเลื่อนอัตโนมัติ ทำได้โดยใช้ data-interval หน่วยเป็นมิลลิวินาที

1

2

3

4

<div id="my-carousel"  class="carousel slide"  data-ride="carousel"

data-interval="500">

[![83](https://benzneststudios.com/blog/wp-content/uploads/2018/11/83.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/83.png "83")

### Source code

[https://gist.github.com/benznest/a2c5683a2f19ddd26617415821a2b141](https://gist.github.com/benznest/a2c5683a2f19ddd26617415821a2b141)

## Modal

Modal คือป๊อบอัพแบบสวยๆ อันนี้ก็ใช้บ่อยมากๆ  
ใช้โค้ดลัดสร้าง Modal คือพิมพ์ว่ b-modal แล้วเลือก modal-full

[![g10](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g10.gif)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g10.gif "g10")

Modal ปกติมันจะถูกซ่อนเอาไว้ รอให้เรียกใช้งาน  
ให้เพิ่ม id ให้กับ div modal หลัก

1

2

3

<div class="modal fade"  id="myModal">

ปรับแต่ง modal ตามใจ โดยภายในก็แบ่งเป็น header, content , footer

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

<div class="modal fade"  id="myModal">

<div class="modal-dialog">

<div class="modal-content">

<div class="modal-header">

<h5 class="modal-title">Hello Modal</h5>

<button class="close"  data-dismiss="modal">

<span>&times;</span>

</button>

</div>

<div class="modal-body">

<p>Content</p>

</div>

<div class="modal-footer">

<a  class="btn btn-danger text-white"  data-dismiss="modal">Close</a>

<a  class="btn btn-success text-white"  data-dismiss="modal">Save</a>

</div>

</div>

</div>

</div>

ปุ่มไหนที่อยากให้กดแล้วแสดง modal ก็เพิ่ม  **data-toggle=”modal” data-target=”#myModal”  
**โดย target คือ id ของ modal

1

2

3

<a  class="btn btn-primary text-white"  data-toggle="modal"  data-target="#myModal">Read more</a>

[![84](https://benzneststudios.com/blog/wp-content/uploads/2018/11/84.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/84.png "84")

## แนะนำ bootsnipp

bootsnipp จะเป็นเว็บที่รวม code หรือ component ต่างๆ เอาไว้สำหรับ bootstrap

[https://bootsnipp.com](https://bootsnipp.com/)

เช่นอยากลองใช้ตัวที่ชื่อว่า Timeline vertical ในเว็บของเรา

[![85](https://benzneststudios.com/blog/wp-content/uploads/2018/11/85.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/85.png "85")

กดเข้าไป ข้างในจะมีรายละเอียด เช่น HTML , CSS

[![87](https://benzneststudios.com/blog/wp-content/uploads/2018/11/87.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/87.png "87")

ให้ copy โค้ด HTML มาไว้ในที่ต้องการ และ copy CSS ของมันมาด้วย โดยเอาไปวางไว้ใน custom.css ของเรา

จากนั้น มาเพิ่ม custom.css

1

2

3

4

5

6

...

<link rel="stylesheet"  href="css/custom.css"  />

</head>

...

[![86](https://benzneststudios.com/blog/wp-content/uploads/2018/11/86.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/86.png "86")

## แนะนำ Startbootstrap.com

ตัวนี้เป็นแหล่งรวมธีมของ Bootstrap แบบมาทั้ง pack เลย เช่น ธีมสำหรับทำเว็บบริษัท ธีมสำหรับแสดงผลงาน

[https://startbootstrap.com/](https://startbootstrap.com/)

[![88](https://benzneststudios.com/blog/wp-content/uploads/2018/11/88.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/88.png "88")

## การใช้ class display

อันนี้เป็นความสามารถใหม่ใน ฺbootstrap4 เช่น อยากให้หน้าจอใหญ่แสดง Carousel แต่ในจอเล็กให้ซ่อน  
ใน Bootstrap 4 สามารถใช้ class d-

1

2

3

<div class="container-fluid mt-5 p-0 d-none d-sm-none d-md-block">

[![g12](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g12.gif)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/g12.gif "g12")

## Media query

Media query คือการระบุเงื่อนไขเจาะจงสำหรับ css เช่น ถ้าหน้าจอขนาดมากกว่า 700px ให้ h1 , h2, h3 ขนาด 1 rem

1

2

3

4

5

6

7

@media  (max-width:700px){

h1,h2,h3{

font-size:1rem;

}

}

## สิ่งที่ใช้ร่วมกับ Bootstrap ไม่ได้

เช่น คู่แข่ง ชื่อว่า Foundation เพราะใช้ชื่อ class เหมือนกัน ตัว Foundation มีความสามารถมากกว่า Bootstrap ทำอะไร Advance ได้มากกว่า แต่ก็ต้องเรียนรู้มากกว่า

[![39](https://benzneststudios.com/blog/wp-content/uploads/2018/11/39.png)](https://benzneststudios.com/blog/wp-content/uploads/2018/11/39.png "39")

## สรุป

บทความนี้ก็พาไปทำ component ที่ใช้งานบ่อย เช่น Table , Form , Carousel , Modal , Navbar รวมทั้งแนะนำเว็บที่เกี่ยวกับ bootstrap ที่จะช่วยให้ใช้งานได้ง่ายขึ้นอีกด้วย


> Written with [StackEdit](https://benzneststudios.com/blog/web/bootstrap-4-basic-part-2/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5MDU1MDVdfQ==
-->