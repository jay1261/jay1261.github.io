---
title: SQL Grammer (Group By, Order By)
author: jay
date: 2024-03-12
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (Group By, Order By)**
<br />
### **Group By**
<br />
데이터를 범주별로 연산된 결과를 얻고 싶을 때 주로 사용합니다. Count, AVG, Sum등의 함수들과 주로 같이 사용되며, 예를들어 나라별 음식 판매의 합산 금액을 구하고 싶을때 사용할 수 있습니다.
<br />
```sql
ex)
select cuisine_type,
       sum(price) sum_of_price
from food_orders
group by cuisine_type
```

- 출력


| cuisine_type | sum_of_price |
| ------------ | ------------ |
| Korean       | 182020       |
| Japanese     | 7663130      |
| Mexican      | 1303850      |
| American     | 9530780      |


---

### **Order By**
<br>
지정한 칼럼을 기준으로 정렬된 값을 얻고 싶을 때 사용하는 문법입니다. 기본 오름차순으로 정렬되며 desc를 사용하면 내림차순으로 정렬할 수 있습니다. Group by의 예시의 바로 아래에 `order by sum(price)`를 입력해줌으로써 합산된 가격의 오름차순으로 정렬된 값을 얻을 수 있습니다. 내림차순은 `order by sum(price) desc`를 입력해주면 됩니다.

```sql
ex)
select cuisine_type,
       sum(price) sum_of_price
from food_orders
group by cuisine_type
order by sum(price) 
```

- 출력

| cuisine_type | sum_of_price |
| ------------ | ------------ |
| Vietnamese   | 90180        |
| Korean       | 182020       |
| Spanish      | 227930       |
| Southern     | 328110       |
| French       | 356290       |

