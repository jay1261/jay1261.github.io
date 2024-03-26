---
title: SQL Grammer (9) - Null, Coalesce
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - MySQL
---
## **SQL Grammer (9) - Null, Coalesce**

<br />

---

<br/>



### **Null**
<br />

값이 없을 때 `Null` 을 이용한다. 숫자 계산같은 함수를 사용할 때 알아두면 좋은 점이 있는데, Null로 처리한 것과 다른 문자로 처리된 경우 계산값이 다르게 나올 수 있다는 것이다.
MySQL에서는 사용할 수 없는 값이 연산으로 들어오면 자동으로 0으로 간주한다. Avg로 평균을 구하는데 하나의 값이 0으로 들어가면서 자릿수는 차지해버려 평균값을 깎아먹는 역할을 하게된다. 하지만 Null로 되어있다면 완전히 제외되어서 계산에 포함되지 않는다.

ex)
```sql
select restaurant_name,  
       avg(rating) average_of_rating,  
       avg(if(rating<>'Not given', rating, null)) average_of_rating2  
from food_orders  
group by 1;
```

rating이라는 테이블에는 없는 값이 null이 아니라 'Not given'이라는 문자로 처리되어 있다. 이 때 2번째줄 처럼 avg를 사용하면 자동으로 'Not given'을 0으로 처리하여 연산한다. 하지만 3번째 줄 처럼 'Not given'을 null로 변환해서 처리한다면 0으로 간주하지 않고 아예 계산 목록에서 제외시켜 버려서 3번째 값의 숫자가 더 크게 나온다.

- 원래 데이터

| restaurant_name           | rating    |
| ------------------------- | --------- |
| Hangawi                   | Not given |
| Blue Ribbon Sushi Izakaya | Not given |
| Cafe Habana               | 5         |
| Blue Ribbon Fried Chicken | 3         |


- 출력 결과

| restaurant_name           | average_of_rating  | average_of_rating2 |
| ------------------------- | ------------------ | ------------------ |
| Blue Ribbon Sushi Izakaya | 2.689655172413793  | 4.333333333333333  |
| Cafe Habana               | 2.9375             | 4.2727272727272725 |
| Blue Ribbon Fried Chicken | 2.8854166666666665 | 4.328125           |



<br />

---

<br/>



### Coalesce

조회한 값이 null 이고, 이를 대신해 다른 값으로 사용하고 싶을 때 쓸 수 있습니다. `coalesce(컬럼, 대체값)`의 형태로 사용할 수 있습니다. 아래 예시는 null인 값들만 가져와서, "null 제거" 컬럼에 대체된 20이라는 값을 넣어주는 예시입니다.

```sql
select b.name,  
       b.age,  
       coalesce(b.age, 20) "null 제거"  
from food_orders a  
         left join customers b on a.customer_id = b.customer_id  
where b.age is null;
```


| name | age  | null 제거 |
| ---- | ---- | ------- |
| Null | Null | 20      |
| Null | Null | 20      |
| Null | Null | 20      |
| Null | Null | 20      |
