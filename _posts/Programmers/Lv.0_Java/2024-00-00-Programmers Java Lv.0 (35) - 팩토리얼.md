---
title: Programmers Java Lv.0 (35) - 팩토리얼
author: jay
date: 2024-04-18
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **팩토리얼**

<br />

---

<br/>

###### **문제 설명**

`i`팩토리얼 (i!)은 1부터 i까지 정수의 곱을 의미합니다. 예를들어 5! = 5 * 4 * 3 * 2 * 1 = 120 입니다. 정수 n이 주어질 때 다음 조건을 만족하는 가장 큰 정수 i를 return 하도록 solution 함수를 완성해주세요.

- i! ≤ n

---

##### **제한사항**

- 0 < `n` ≤ 3,628,800

---

##### **입출력 예**

|n|result|
|---|---|
|3628800|10|
|7|3|

---

##### **입출력 예 설명**

입출력 예 #1

- 10! = 3,628,800입니다. `n`이 3628800이므로 최대 팩토리얼인 10을 return 합니다.

입출력 예 #2

- 3! = 6, 4! = 24입니다. `n`이 7이므로, 7 이하의 최대 팩토리얼인 3을 return 합니다.

<br />

---

<br/>

## **Solution**

> 주어진 n을 1부터 숫자를 늘려가며 나누어주고, n이 1보다 작아지는 시점에 `i - 1` 을 return 해줬습니다.

```java
class Solution {
    public int solution(int n) {
        int i = 1;
        while(true){
            n = n / i;
            if (n < 1){
                return i-1;
            }
            i++;
        }
    }
}
```