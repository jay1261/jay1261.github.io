---
title: SQL Grammer (Replace, Substring, Concat)
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## SQL Grammer (Replace, Substring, Concat)
<br />
### Replace
<br />
특정 문자를 변경하고자 할 때 사용합니다. `Replace(바꿀컬럼, 현재 값, 바꿀 값)` 의 형태로 사용할 수 있습니다.

```sql
ex)
SELECT restaurant_name AS "원래 이름",  
       REPLACE (restaurant_name, 'Blue', 'Pink')  
FROM food_orders  
WHERE restaurant_name LIKE '%Blue Ribbon%'
```

이렇게 하면 기존에 'Blue' 였던 문자가 Pink로 바뀌게 됩니다.


|원래이름|바뀐이름|
|Blue Ribbon Sushi Izakaya|Pink Ribbon Sushi Izakaya|
|Blue Ribbon Fried Chicken|Pink Ribbon Fried Chicken|
|Blue Ribbon Fried Chicken|Pink Ribbon Fried Chicken|
|Blue Ribbon Sushi Izakaya|Pink Ribbon Sushi Izakaya|
|Blue Ribbon Sushi|Pink Ribbon Sushi|
|Blue Ribbon Sushi|Pink Ribbon Sushi|


---

### Substring
<br />

특정 문자만 골라서 조회할 수 있는 문법입니다. `substr(조회할 컬럼, 시작 위치, 글자 수)`의 형태로 사용 가능합니다. 전체 주소에서 앞의 두글자만 추출하고 싶을 때 쓸 수 있습니다 ("서울특별시"에서 "서울"만 추출). 글자 수를 입력하지 않으면 시작위치에서 끝까지 출력됩니다.

```sql
SELECT addr as "원래주소",SUBSTR(addr, 1,2) FROM food_orders
```

|서울특별시 종로구 팔판|서울|
|경기도 광주시 퇴촌면|경기|
|경기도 용인시 처인구 양지면 식금리|경기|
|경기도 인천시 간석동|경기|
|경기도 평택군 고덕면 문곡리|경기|


---

### Concat
<br />

여러 컬럼에 나눠져있는 문자를 합쳐야할 때 사용할 수 있는 문법입니다. `concat(붙이고 싶은 값1, 붙이고 싶은 값2, ...)` 의 형태로 사용 가능합니다. "서울특별시", "음식점" 형태의 값을 `[서울] 음식점명`으로 변경하고 싶을 때 사용할 수 있습니다.

```sql
SELECT restaurant_name as "원래이름",  
       CONCAT('[', SUBSTR(addr,1,2), '] ', restaurant_name)  
FROM  food_orders  
WHERE addr like '%서울%';
```

|Hangawi|[서울] Hangawi|
|Barbounia|[서울] Barbounia|
|Empanada Mama (closed)|[서울] Empanada Mama (closed)|
|The Meatball Shop|[서울] The Meatball Shop|
|Blue Ribbon Sushi|[서울] Blue Ribbon Sushi|
|The Meatball Shop|[서울] The Meatball Shop|


---

### 연습문제

- [지역(시도)] 음식점이름(음식종류) 컬럼을 만들고, 총 주문건수 구하기

```sql
SELECT concat('[' , substr(addr,1,2) ,'] ', restaurant_name, '(', cuisine_type, ')') as "음식점 상세",  
       count(1) as "총 주문건수"  
from food_orders  
group by restaurant_name;
```

- 출력 결과


|[서울] Hangawi(Korean)|2|
|[경기] Blue Ribbon Sushi Izakaya(Japanese)|29|
|[경기] Cafe Habana(Mexican)|16|
|[경기] Blue Ribbon Fried Chicken(American)|96|
|[경기] Dirty Bird to Go(American)|4|
|[경기] Tamarind TriBeCa(Indian)|27|
|...|...|
