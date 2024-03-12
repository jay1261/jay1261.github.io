---
title: SQL Grammer (6) - If, Case, Cast
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (6) - If, Case, Cast**
<br />

### **If**
<br />

조건에 따라 다른 방법을 적용해 값을 얻고 싶을 때 If문을 사용합니다. `if(조건, 참일 때 실행, 거짓일 때 실행)`의 형태로 사용합니다. 음식의 타입이 "Korean"이면 한식, 아니면 기타를 출력하는 예시입니다.

```sql
select restaurant_name,  
       cuisine_type "원래 음식 타입",  
       if(cuisine_type='Korean', '한식', '기타') "음식 타입"  
from food_orders;
```

|Hangawi|Korean|한식|
|Blue Ribbon Sushi Izakaya|Japanese|기타|
|Cafe Habana|Mexican|기타|
|Blue Ribbon Fried Chicken|American|기타|
|Dirty Bird to Go|American|기타|


---

### **Case**
<br />

조건을 지정하다보면 두개 이상의 조건을 지정해야 할 경우가 있는데, 이러한 때에는 case문이 더 효율적입니다. 

```sql
case when '조건1' then '값1'
     when '조건2' then '값2' 
     ...
     else '값3'
end
```

의 형태로 사용할 수 있습니다.  

ex) 10세 이상 30세 미만의 고의 나이와 성로 그룹 나누기(이름도 같이 출력)
```sql
select case when age between 10 and 19 and gender='male' then '10대 남성'  
            when age between 10 and 19 and gender='female' then '10대 여성'  
            when age between 20 and 29 and gender='male' then '20대 남성'  
            when age between 20 and 29 and gender='female' then '20대 여성'  
            end as "고객 분류",  
            name, age, gender  
from customers  
where age between 10 and 29;
```

|고객 분류|name|age|gender|
|10대 남성|김도진|15|male|
|10대 여성|정지은|15|female|
|20대 남성|김하호|21|male|
|10대 여성|이채원|16|female|
|10대 여성|박민연|12|female|


---

### Cast

Type에 관련한 문제가 발생했을 때 데이터베이스의 값의 `타입을 변경`해 줄 수 있는 문법입니다. 

문자 -> 숫자 or 숫자 -> 문자 등
`cast(컬럼 as 타입)`의 형태로 사용가능합니다.