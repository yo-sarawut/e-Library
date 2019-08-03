5 Concepts พื้นฐานของภาษา R
====================

## 1. Variables

การสร้างตัวแปร หรือที่ใน R เรียกว่า variable assignment การสร้างตัวแปรใน R ใช้ operator  `<-`  หรือ  `=`  ก็ได้ (แต่ pure R programmer ต้องใช้  `<-`  เท่านั้น 555+) ถ้าต้องการลบตัวแปร ใช้ฟังชั่น  `rm(variable_name)`

Tip – R เป็นภาษาที่เราเรียกว่า Object Oriented Programming เราสามารถสร้าง object และกำหนด class ของ object นั้นๆได้ ลองดูฟังชั่น  `class()`  หัวข้อถัดไป

```
## assign new variables
x <- 100
y <- 200
print(x + y)

income_old <- 50000
income_new <- income_old * (1.1 ** 2)
print(income_new)
```

## 2. Data Types

ตัวแปรใน R จะมี data type ติดตัวมันด้วย ตัวหลักๆที่เราใช้ในงาน data analysis เป็นประจำคือ numeric, character, logical, date และ factor เราสามารถใช้ฟังชั่น  `class()`  เพื่อตรวจสอบ type ใน console ได้เลย

Tip – logical ใน R หรือที่ภาษาอื่นๆเรียกกันว่า Boolean จะเขียนแค่ T, F เลยก็ได้ (ไม่ต้องเขียนเต็มๆว่า TRUE, FALSE) ถ้าเราเปลี่ยน logical เป็น numeric TRUE จะมีค่าเท่ากับหนึ่งและ FALSE มีค่าเท่ากับศูนย์

```
## create four variables
id <- 100
customer_name <- "Captain Marvel"
status_single <- TRUE
date_of_birth <- as.Date("1975-09-30")
gender <- as.factor("female")

## check data type
class(id)             ## numeric
class(customer_name)  ## character
class(status_single)  ## logical
class(date_of_birth)  ## date
class(gender)         ## factor
```

## 3. Data Structures

Data structures คือการนำ data type มาประกอบร่างเป็นโครงสร้างที่ใหญ่ขึ้น ตัวหลักๆที่เราใช้ใน R มี 4 ตัวคือ vector, matrix, list และ data frame โดย data structures แต่ละแบบจะมีวิธีการใช้งานที่แตกต่างกัน

ตัวอย่างเช่น vector เป็น one-dimensional array เก็บข้อมูลได้แค่ประเภทเดียว (single data type) ส่วน matrix เป็น two-dimensional array แต่ data structure ที่เราใช้เยอะที่สุดสำหรับการวิเคราะห์ข้อมูลใน R คือ data frame i.e. หน้าตาเหมือน Excel table ตัวแปรแต่ละตัวเป็น column และ row คือ observations

```
## vector
id <- 1:5
friends <- c("Iron Man", "Spider Man", "Thor", "Hulk", "Captain")
ages <- c(45, 18, 30, 42, 80)
super_power <- c(FALSE, TRUE, TRUE, TRUE, FALSE)

## matrix
m <- matrix(1:25, ncol = 5)

## list
my_list <- list(id, friends, ages, super_power, m)

## data frame
df <- data.frame(id, friends, ages, super_power)
```

Tip – ฟังชั่นที่เรานิยมใช้กับ data frame เช่น  `str()`,  `summary()`,  `head()`,  `tail()`,  `subset()`  และฟังชั่นหลักของ package dplyr สำหรับทำ data transformation

![](https://i0.wp.com/datarockie.com/wp-content/uploads/2019/07/image-39-e1563888582630.png?resize=780%2C407&ssl=1)

ตัวอย่าง data frame ใน R

## 4. Control Flow

Control flow เป็น concept ที่สำคัญมากของการเขียนโปรแกรมทุกภาษาและใน R ก็เช่นเดียวกัน เราใช้ keywords if-else, for, while เพื่อเขียนเงื่อนไขและ loop ตามลำดับ

Tip – R มีฟังชั่น  `ifelse()`  และ  `case_when()`  เพื่อใช้แทนการเขียน if-else block และมีฟังชั่นตระกูล  `apply()`และ  `map()`  แทนการเขียน loop ฟังชั่นพวกนี้มีสอนใน  [Data Analyst Bootcamp](https://datarockie.com/data-analyst-bootcamp/)  ของเราด้วย  

```
## if-else
score <- 90
if (score > 50) {
  print("passed")
} else {
  print("failed")
}

## for loop
students <- c("Anna", "John", "Snow")
for (s in students) {
  print(paste("hello!", s))
}

## while loop
n <- 5
while (n > 0) {
  print("hello world")
  n <- n - 1
}
```

ความรู้เกี่ยวกับ control flow มีประโยชน์มาก โดยเฉพาะอย่างยิ่งเวลาที่เราต้องเขียน function ไว้ใช้งานเอง ถ้าเราเข้าใจการทำงานของ if-else, for และ while เราสามารถสร้างฟังชั่นใหม่ได้อย่างไม่มีขีดจำกัด

## 5. Functions

Function คือ reusable piece of code ที่เราสามารถเรียกใช้งานซ้ำได้เรื่อยๆ และ R คือหนึ่งใน functional programming languages ที่มีฟังชั่นเป็นหัวใจสำคัญ (เหมือนที่เราเกริ่นใน motto)

ด้านล่างเป็น template สำหรับเขียนฟังชั่นไว้ใช้งานเองใน R โดยฟังชั่นจะมีหรือไม่มี input ก็ได้ (R เรียก input ของฟังชั่นว่า argument) วิธีการเขียนฟังชั่นเราใช้  `function_name <- function()`  เพื่อสร้างฟังชั่นใหม่ ขั้นตอนการทำงานของฟังชั่นจะถูกเขียนเป็นขั้นตอนใน { } และ code ไลน์สุดท้ายใน { } จะเป็น output ของฟังชั่นนั้นๆ

Tip – ฟังชั่นที่เราเขียนขึ้นมาใหม่ถือว่าเป็น object หนึ่งใน R environment เหมือนกัน สำหรับฟังชั่นของ base R ทั้งหมด ถ้าเราอยากรู้ว่าฟังชั่นไหนทำงานยังไง แค่พิมพ์  `help(function_name)`  เพื่ออ่านวิธีการใช้งานได้เลย

```
## function with argument
add_two <- function(x){
  x + 2
}

## function with default argument
cube <- function(x, power = 3){
  x ** power
}

## function without argument
greeting <- function(){
  name <- readline("What's your name? ")
  print(paste("Hello", name))
}

## test functions
add_two(20)
cube(5)
cube(5, power = 4)
greeting()
```



อัพเดทวันที่ 23 ก.ค. 2562 – R มีฟังชั่นให้เราใช้งานแตะหลัก 2.6 ล้านฟังชั่น (มากกว่า 17,000 packages) เพื่อนๆสามารถค้นหาและอ่านวิธีการทำงานของฟังชั่นทั้งหมดได้ที่เว็บไซต์  [R documentation](https://www.rdocumentation.org/trends)


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3NDM4MzAwNl19
-->