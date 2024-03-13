---
title: SQL Grammer (7) - Subquery
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (7) - Subquery**
<br />

### **Subquery**
<br />

여러번의 연산을 수행해야할 때, 조건문에 연산 결과를 사용하거나 조건에 Query결과를 사용하고 싶을 때 쓸 수 있는 문법입니다. 복잡한 쿼리문을 효율적으로 작성할 수 있습니다. 기본 구조는 아래와 같습니다.

```sql
select column1, test
from (
	#subquery
	select column1, column2 as test
	from table1
) subq
```

---
#### **예시**
<br/>

ex 1) 음식점의 총 주문수량과 주문금액을 연산하고, 주문수량을 기반으로 수수료 할인율 구하기 
- 할인조건: 수량 5개 이하-> 10%, 수량 15개 초과 & 총 주문금액 300000이상 - 0.5%, 이외 1%

```sql
select restaurant_name,  
       case when sum_quantity<=5 then 10  
            when sum_quantity>15 and total_price>=300000 then 0.5  
            else 1 end as "수수료 할인률"  
from(  
select restaurant_name,  
       sum(quantity) as sum_quantity,  
       sum(price) as total_price  
from food_orders  
group by 1  
) a;
```

| restaurant_name           | 수수료 할인률 |
| ------------------------- | ------- |
| Hangawi                   | 10.0    |
| Blue Ribbon Sushi Izakaya | 0.5     |
| Cafe Habana               | 1.0     |
| Blue Ribbon Fried Chicken | 0.5     |
| Dirty Bird to Go          | 1.0     |

<br/>
<br/>

 ex 2) 음식 타입별 총 주문수량과 음식점 수를 연산하고, 주문 수량과 음식점 수 별 수수료율 산정하기
- 음식점수 5개이상, 주문수 30개이상 - 0.05%
- 5개이상 30개미만 - 0.08%
- 5개미만, 30개이상 - 1%       
- 5개미만, 30개미만 - 2%

```sql
select cuisine_type,  
        total_quantity,  
        count_restaurant,  
        case when count_restaurant>=5 and total_quantity>= 30 then 0.005  
            when count_restaurant>=5 and total_quantity< 30 then 0.008  
            when count_restaurant<5 and total_quantity>= 30 then 0.01  
            when count_restaurant<5 and total_quantity<= 30 then 0.02  
            end rate  
from  
(select cuisine_type,  
        sum(quantity) as 'total_quantity',  
        count(distinct restaurant_name) 'count_restaurant'  
 from food_orders  
 group by 1  
 ) a;
```



| cuisine_type | total_quantity | count_restaurant | rate      |
| ------------ | -------------- | ---------------- | --------- |
| American     | 1763           | 41               | 0.005<br> |
| Chinese      | 635            | 16               | 0.005     |
| French       | 57             | 3                | 0.010     |
| Indian       | 186            | 14               | 0.005     |
| Italian      | 900            | 31               | 0.005     |

