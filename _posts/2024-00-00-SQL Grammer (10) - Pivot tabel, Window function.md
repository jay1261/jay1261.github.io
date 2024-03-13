---
title: SQL Grammer (10) - Pivot tabel, Window function
author: jay
date: 2024-03-13
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (10) - Pivot tabel, Window function**
<br />

### **Pivot tabel**
<br />

2개 이상의 기준으로 데이터를 집계할 때, 보기 쉽게 배열하여 보여주는 것을 의미합니다. 집계 기준을 행의 기준으로 잡고, 구분 컬럼으로 데이터를 보여줄 수 있습니다. 

```sql
select restaurant_name,  
       max(if(hh='15', cnt_order, 0)) "15",  
       max(if(hh='16', cnt_order, 0)) "16",  
       max(if(hh='17', cnt_order, 0)) "17",  
       max(if(hh='18', cnt_order, 0)) "18",  
       max(if(hh='19', cnt_order, 0)) "19",  
       max(if(hh='20', cnt_order, 0)) "20"  
from  
(  
select a.restaurant_name,  
       substring(b.time, 1, 2) hh,  
       count(1) cnt_order  
from food_orders a inner join payments b on a.order_id=b.order_id  
where substring(b.time, 1, 2) between 15 and 20  
group by 1, 2  
) a  
group by 1  
order by 7 desc;
```

이렇게 하면 음식점 별, 시간대별 주문 건수를 한눈에 확인할 수 있게 데이터를 조회할 수 있습니다.


| restaurant_name           | 15  | 16  | 17  | 18  | 19  | 20  |
| ------------------------- | --- | --- | --- | --- | --- | --- |
| Shake Shack               | 13  | 7   | 6   | 9   | 3   | 9   |
| The Meatball Shop         | 4   | 2   | 7   | 3   | 4   | 9   |
| Blue Ribbon Fried Chicken | 5   | 4   | 2   | 4   | 4   | 5   |

---

### **Window function**
<br/>
각 행의 관계를 정의하기 위한 함수로, 그룹 내의 연산을 쉽게 만들어주는 함수입니다. 예를 들어 한식 식당 중에서 주문건수가 많은 순으로 순위를 매기고 싶은 경우에 사용할 수 있습니다.

기본 구조는 `window_function(argument) over (partition by 기준 칼럼, order by 정렬 기준)`의 형태로 쓰입니다. 

```sql
select cuisine_type,  
       restaurant_name,  
       order_count,  
       rn "순위"  
from  
(  
select cuisine_type,  
       restaurant_name,  
       rank() over (partition by cuisine_type order by order_count desc) rn,  
       order_count  
from  
(  
select cuisine_type, restaurant_name, count(1) order_count  
from food_orders  
group by 1, 2  
) a  
) b  
where rn<=3  
order by 1, 4;
```

Rank()를 사용해 음식의 타입별로 레스토랑들의 주문건수 순위를 볼 수 있습니다.

| cuisine_type | restaurant_name             | order_count | 순위  |
| ------------ | --------------------------- | ----------- | --- |
| American     | Shake Shack                 | 219         | 1   |
| American     | Blue Ribbon Fried Chicken   | 96          | 2   |
| American     | Five Guys Burgers and Fries | 29          | 3   |
| Chinese      | RedFarm Broadway            | 59          | 1   |
| Chinese      | RedFarm Hudson              | 55          | 2   |
| Chinese      | Han Dynasty                 | 46          | 3   |
