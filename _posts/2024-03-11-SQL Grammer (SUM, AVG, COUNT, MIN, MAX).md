---
title: SQL Grammer (SUM, AVG, COUNT, MIN, MAX)
author: jay
date: 2024-03-11
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (SUM, AVG, COUNT, MIN, MAX)**
<br>
### **SUM**

선택된 열과 범위의 합계를 반환해줍니다. 예시처럼 customer의 테이블안에 있는 모든 값들의 나이를 더한 값을 얻고 싶을 때 쓸 수 있습니다.
```sql
ex)
SELECT SUM(age) FROM customers
```

---

### **AVG**

sum과 같은 방법으로 사용 가능하며, 평균 값을 구할 때 사용합니다. customer 테이블 안의 age의 평균값을 구하고 싶다면 다음과 같이 사용할 수 있습니다.
```sql
SELECT AVG(age) FROM customers
```


---

### **COUNT**

데이터의 개수를 구하는데 사용할 수 있습니다. ()안에 `1`이나 `*`을 입력하면 해당 테이블의 전체 카운트를 가져옵니다. distinct를 사용하면 중복되지 않는 값을 반환합니다. 예시를 보면 customer_id가 중복되지 않는 값을 반환합니다.
```sql
SELECT COUNT(1) FROM customers
SELECT COUNT(*) FROM customers
SELECT COUNT(*),COUNT(DISTINCT customer_id) FROM food_orders
```

---

### **MIN**

선택된 범위 내에서 최소값을 가져오는 문법입니다. "나이가 가장 어린사람"을 찾고 싶을 때 사용 가능합니다.

```sql
SELECT MIN(age) FROM customers
```

---

### **MAX**

선택된 범위 내에서 최대값을 가져오는 문법입니다. "나이가 가장 많은사람"을 찾고 싶을 때 사용 가능합니다.

```sql
SELECT MAX(age) FROM customers
```
