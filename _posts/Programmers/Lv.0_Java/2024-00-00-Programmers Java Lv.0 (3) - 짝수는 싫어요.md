---
title: Programmers Java Lv.0 (3) - 짝수는 싫어요
author: jay
date: 2024-03-26
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **짝수는 싫어요**

<br />

---

<br/>

###### 문제 설명

정수 `n`이 매개변수로 주어질 때, `n` 이하의 홀수가 오름차순으로 담긴 배열을 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 100

---

##### 입출력 예

|n|result|
|---|---|
|10|[1, 3, 5, 7, 9]|
|15|[1, 3, 5, 7, 9, 11, 13, 15]|

---

##### 입출력 예 설명

입출력 #1

- 10 이하의 홀수가 담긴 배열 [1, 3, 5, 7, 9]를 return합니다.

입출력 #1

- 15 이하의 홀수가 담긴 배열 [1, 3, 5, 7, 9, 11, 13, 15]를 return합니다.

<br />

---

<br/>

## **Solution**

> ArrayList를 사용했으며, for문으로 i를 1부터 2씩 증가시키며 array에 add했습니다. 이후 ArrayList를 array로 변환하여 출력했습니다.

```java
import java.util.*;

class Solution {
    public int[] solution(int n) {
        ArrayList<Integer> array = new ArrayList<>();
        
        for (int i = 1; i <= n; i+=2){
            array.add(i);
        }
        
        return array.stream().mapToInt(x->x).toArray();
    }
}
```