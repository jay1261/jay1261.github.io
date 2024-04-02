---
title: Programmers Java Lv.0 (19) - 짝수의 합
author: jay
date: 2024-04-01
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **짝수의 합**

<br />

---

<br/>

###### **문제 설명**

정수 `n`이 주어질 때, `n`이하의 짝수를 모두 더한 값을 return 하도록 solution 함수를 작성해주세요.

---

##### **제한사항**

0 < `n` ≤ 1000

---

##### **입출력 예**

|n|result|
|---|---|
|10|30|
|4|6|

---

##### **입출력 예 설명**

입출력 예 #1

- `n`이 10이므로 2 + 4 + 6 + 8 + 10 = 30을 return 합니다.

입출력 예 #2

- `n`이 4이므로 2 + 4 = 6을 return 합니다.


<br />

---

<br/>

## **Solution**

> 반복문의 i 를 2씩 더해서 짝수를 모두 더했습니다.

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = 0; i <= n; i+=2){
            answer += i;
        }
        return answer;
    }
}
```