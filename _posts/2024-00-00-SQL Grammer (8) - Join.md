---
title: SQL Grammer (8) - Join
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - MySQL
---
## **SQL Grammer (8) - Join**

<br />

---

<br/>



### **Join**
<br />

필요한 데이터가 서로 다른 테이블에 있을 때 사용할 수 있는 문법입니다. 공통 컬럼을 기준으로 두 테이블을 합쳐서 각각 테이블에서 필요한 데이터를 조회할 수 있습니다. 

#### Join의 종류
- `Inner Join`
	- 가장 많이 사용하는 조인으로, 두 테이블 모두에 있는 값만 조회하는 것을 말합니다.
- `OuterJoin` 
	- `left, right, full` 이 있으며 각각 왼쪽 테이블의 모든 값 조회, 오른쪽 테이블의 모든 값 조회, 모든 테이블의 모든 값 조회를 할 수 있습니다.
- `Cross Join` 
	- 한쪽 테이블의 모든 행과 다른쪽 테이블의 모든 행을 조인시키는 기능을 합니다. 전체 행 개수는 `두 테이블의 각 행의 개수를 곱한 수` 입니다.
- `Self Join`
	- 자체 조인은 자기 자신과 조인하므로 1개의 테이블을 사용합니다. 


<br />

---

<br/>



### **사용 예시** 
#### **예시 1**
- 한국 음식의 주문별 결제수단과 수수료율을 조회하기

<br />

```sql
select f.order_id,  
       f.restaurant_name,  
       f.price,  
       p.pay_type,  
       p.vat  
from food_orders f left join payments p on f.order_id=p.order_id  
where cuisine_type='Korean';
```

| order_id | restaurant_name           | price | pay_type | vat  |
| -------- | ------------------------- | ----- | -------- | ---- |
| 1477147  | Hangawi                   | 30750 | card     | 0.25 |
| 1476856  | Woorijip                  | 8250  | card     | 0.1  |
| 1477600  | Hangawi                   | 6740  | cash     | 0.25 |
| 1478363  | Cho Dang Gol              | 29250 | card     | 0.2  |
| 1477302  | Dons Bogam BBQ & Wine Bar | 12230 | card     | 0.2  |

#### **예시 2**
- 주문 가격과 수수료율을 곱하여 주문별 수수료 구하기  
- 조회 컬럼: 주문번호, 식당이름, 주문가격, 수수료율, 수수료) 수수료가 있는 경우만 조회

```sql
select f.order_id,  
       f.restaurant_name,  
       f.price,  
       p.vat,  
       (f.price * p.vat) as '수수료'  
from food_orders f inner join payments p on f.order_id=p.order_id
```


| order_id | restaurant_name           | price     | vat      | 수수료                    |
| -------- | ------------------------- | --------- | -------- | ---------------------- |
| 1477147  | Hangawi                   | 30750<br> | 0.25     | 7687.5<br>             |
| 1477685  | Blue Ribbon Sushi Izakaya | 12080     | 0.13<br> | 1570.3999423980713<br> |
| 1477070  | Cafe Habana               | 12230<br> | 0.1<br>  | 1223.0000182241201<br> |
| 1477334  | Blue Ribbon Fried Chicken | 29200     | 0.13<br> | 3795.99986076355<br>   |
| 1478249  | Dirty Bird to Go          | 11590<br> | 0.1<br>  | 1159.0000172704458<br> |

