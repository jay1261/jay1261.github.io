---
title: SQL Grammer (11) - Date
author: jay
date: 2024-03-13
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## **SQL Grammer (11) - Date**
<br />

### **Date**
<br />
년, 월, 일, 시, 분, 초 등의 값을 모두 갖고 있으며, 목적에 따라 월, 주, 일 등으로 포맷을 변경할 수 있습니다.
데이터에 날짜를 지정하거나, 조건에 날짜를 사용해야할 때 유용합니다. 
- date_format
	- 년: Y(4자리) , y(2자리)
	- 월: M,m
	- 일: d, e
	- 요일: w

```sql
select date(date) date_type,  
       date_format(date(date), '%Y') "년",  
       date_format(date(date), '%m') "월",  
       date_format(date(date), '%d') "일",  
       date_format(date(date), '%w') "요일"  
from payments
```


| date_type  | 년    | 월   | 일   | 요일  |
| ---------- | ---- | --- | --- | --- |
| 1978-08-23 | 1978 | 08  | 23  | 3   |
| 1974-03-24 | 1974 | 03  | 24  | 0   |
| 2008-05-16 | 2008 | 05  | 16  | 5   |
| 1973-09-27 | 1973 | 09  | 27  | 4   |
