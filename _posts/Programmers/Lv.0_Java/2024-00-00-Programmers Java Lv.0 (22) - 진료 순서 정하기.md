---
title: Programmers Java Lv.0 (22) - 진료 순서 정하기
author: jay
date: 2024-04-02
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **진료 순서 정하기**

<br />

---

<br/>
###### **문제 설명**

외과의사 머쓱이는 응급실에 온 환자의 응급도를 기준으로 진료 순서를 정하려고 합니다. 정수 배열 `emergency`가 매개변수로 주어질 때 응급도가 높은 순서대로 진료 순서를 정한 배열을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 중복된 원소는 없습니다.
- 1 ≤ `emergency`의 길이 ≤ 10
- 1 ≤ `emergency`의 원소 ≤ 100

---

##### **입출력 예**

|emergency|result|
|---|---|
|[3, 76, 24]|[3, 1, 2]|
|[1, 2, 3, 4, 5, 6, 7]|[7, 6, 5, 4, 3, 2, 1]|
|[30, 10, 23, 6, 100]|[2, 4, 3, 5, 1]|

---

##### **입출력 예 설명**

입출력 예 #1

- `emergency`가 [3, 76, 24]이므로 응급도의 크기 순서대로 번호를 매긴 [3, 1, 2]를 return합니다.

입출력 예 #2

- `emergency`가 [1, 2, 3, 4, 5, 6, 7]이므로 응급도의 크기 순서대로 번호를 매긴 [7, 6, 5, 4, 3, 2, 1]를 return합니다.

입출력 예 #3

- `emergency`가 [30, 10, 23, 6, 100]이므로 응급도의 크기 순서대로 번호를 매긴 [2, 4, 3, 5, 1]를 return합니다.

<br />

---

<br/>

## **Solution**

> emergency를 정렬하고, 정렬된 요소를 key로, index를 value로 `HashMap`에 추가합니다. 그리고 emergency를 다시 돌면서 요소별로 해당하는 순위를 answer에 넣어서 문제를 풀었습니다.

```java
import java.util.*;

class Solution {
    public int[] solution(int[] emergency) {
        int[] answer = new int[emergency.length];
        int[] sorted = Arrays.stream(emergency).sorted().toArray();
        
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < sorted.length; i++){  
            map.put(sorted[i], i);
        }
        
        for(int i = 0; i < emergency.length; i++){  
           answer[i] = emergency.length - map.getOrDefault(emergency[i],0);
        }
        
        return answer;
    }
}
```