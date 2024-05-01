---
title: Programmers Java Lv.0 (4) - 피자 나눠먹기 1
author: jay
date: 2024-03-28
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **피자 나눠먹기 1**

<br />

---

<br/>

###### **문제 설명**

머쓱이네 피자가게는 피자를 일곱 조각으로 잘라 줍니다. 피자를 나눠먹을 사람의 수 `n`이 주어질 때, 모든 사람이 피자를 한 조각 이상 먹기 위해 필요한 피자의 수를 return 하는 solution 함수를 완성해보세요.

---

##### **제한사항**

- 1 ≤ `n` ≤ 100

---

##### **입출력 예**

|n|result|
|---|---|
|7|1|
|1|1|
|15|3|

---

##### **입출력 예 설명**

입출력 예 #1

- 7명이 최소 한 조각씩 먹기 위해서 최소 1판이 필요합니다.

입출력 예 #2

- 1명은 최소 한 조각을 먹기 위해 1판이 필요합니다.

입출력 예 #3

- 15명이 최소 한 조각씩 먹기 위해서 최소 3판이 필요합니다.



<br />

---

<br/>

## **Solution**
<br/>
> 인원수 `n`이 `7조각`으로 딱 나눠 떨어질 때에는 `n/7`, 아닐 때에는 `n/7 +1` 로 풀었습니다. 

```java
class Solution {
    public int solution(int n) {
        int answer = n % 7 == 0 ? n/7 : (n/7) + 1;
        return answer;
    }
}
```