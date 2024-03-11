---
title: SQL Grammer (Where, Between, In, Like)
author: jay
date: 2024-03-11
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## SQL Grammer (Where, Between, In, Like)
<br>
### **Where**
<br>
데이터 중에 특정 조건으로 필터링을 해야할 때 사용하는 문법입니다. "나이가 20살 이상인 사람"과 같은 경우의 데이터를 구할 때 사용합니다.
```sql
ex)
SELECT * FROM customer WHERE age>=20
```

 `Where`를 사용할 때 기본적인 비교 연산자로는 `=, <>, <, <=, >, >=`이 있습니다

| 연산자 | 의미    |
| --- | ------ |
| =   | 같다    |
| <>  | 같지않다   |
| >   | 크다     |
| >=  | 크거나 같다 |
| <   | 작다     |
| <=  | 작거나 같다 |


---
### **Between**
<br>
a와 b값의 사이에 있는 값을 가져올 때 사용합니다. a와 b 사이에 AND를 사용해 줍니다.

```sql
ex)
SELECT * FROM customer WHERE age BETWEEN 20 and 30
```
<br>

---
### **In**
<br>

포함하는 조건을 줄 때 사용합니다. "나이가(20, 21, 27)살인 사람"을 필터링할 때 사용합니다.

```sql
SELECT * FROM customer WHERE age IN(20, 21, 27)
```
<br>

---
### **Like**
<br>
완전히 똑같지는 않지만 비슷한 값을 찾을 때 사용할 수 있습니다. 예를들어 이름이 'OO현'인 사람을 찾을때 사용할 수 있습니다. Like연산자와 `%, _`가 같이 사용되는데, 이 문자들을 `WildCard`라고 합니다. `%`는 `0,1 또는 하나 이상의 character`를 나타냅니다. `_`는 `하나의 character`를 나타냅니다.
```sql
SELECT * FROM customer WHERE name LIKE "%현"
SELECT * FROM customer WHERE name LIKE "_현_"
```
결과를 출력해보면 
1. 김예현, 이동현...
2. 김현재, 이현호...
가 될 수 있습니다.





