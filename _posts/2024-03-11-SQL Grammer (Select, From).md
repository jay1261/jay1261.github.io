---
title: SQL Grammer (Select, From)
author: jay
date: 2024-03-11
categories:
  - MySQL
  - SQL Grammer
tags:
  - Algorithm
  - SwiftAlgorithm
---
## SQL Grammer (Select, From)
<Br>
### SQL 이란?
<Br>
`SQL`은 `Structured Query Language`의 약자이며 직역하자면 구조화된 질의 언어 라는 의미입니다. 관계형 데이터베이스에서 데이터를 관리하고 처리하기 위해 사용되는 비절차적인 언어입니다.
<Br>
SQL 문장에는 다음 3가지 종류가 있습니다.
- 데이터 정의어(Data Definition Language)
- 데이터 조작어(Data Manipulation Language)
- 데이터 제어어(Data Control Language)

---
### Select
<Br>
Select는 SQL에서 가장 많이 사용되는 구문입니다. 데이터를 가져오는 기본 명령어로, 데이터를 조회하는 모든 Query에 사용됩니다. 단순하게 데이터베이스가 엑셀처럼 행과 열(row) 열(column)이 있다고 했을 때, 열(column)을 선택한다고 생각할 수 있습니다.

```sql
#모든 열을 선택
SELECT * 
```
<Br>

---
### From
<Br>
From은 데이터베이스 안에서 데이터를 가져올 테이블을 특정해주는 문법입니다. 
<Br>
```sql
SELECT * FROM customer
```
<Br>
> 이에 따라 위의 sql문을 해석하면, 현재 데이터베이스의 customer 테이블의 모든 열을 가져오는 코드가 됩니다.

- 출력 예시

| customer_id | name | email                |
| ----------- | ---- | -------------------- |
| 337525      | 조현아  | xzvnliwj@hanmail.com |
| 358141      | 장민호  | byuvhegb@hanmail.com |
| 66393       | 김도진  | dzelcyxr@daum.net    |


