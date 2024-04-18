---
title: Programmers Java Lv.0 (34) - 최댓값 만들기 1
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
## **최댓값 만들기 1**

<br />

---

<br/>

###### **문제 설명**

정수 배열 `numbers`가 매개변수로 주어집니다. `numbers`의 원소 중 두 개를 곱해 만들 수 있는 최댓값을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 0 ≤ `numbers`의 원소 ≤ 10,000
- 2 ≤ `numbers`의 길이 ≤ 100

---

##### **입출력 예**

|numbers|result|
|---|---|
|[1, 2, 3, 4, 5]|20|
|[0, 31, 24, 10, 1, 9]|744|

---

##### **입출력 예 설명**

입출력 예 #1

- 두 수의 곱중 최댓값은 4 * 5 = 20 입니다.

입출력 예 #1

- 두 수의 곱중 최댓값은 31 * 24 = 744 입니다.

<br />

---

<br/>

## **Solution**

> 주어진 배열을 정렬해서 가장 큰 수와 그 다음 큰 수를 곱하면 최대값입니다. 

```java
import java.util.*;
class Solution {
    public int solution(int[] numbers) {
        Arrays.sort(numbers);
                    
        return numbers[numbers.length-1] * numbers[numbers.length-2];
    }
}
```