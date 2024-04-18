---
title: Programmers Java Lv.0 (2) - 최빈값 구하기
author: jay
date: 2024-03-26
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **최빈값 구하기**

<br />

---

<br/>
###### **문제 설명**

최빈값은 주어진 값 중에서 가장 자주 나오는 값을 의미합니다. 정수 배열 `array`가 매개변수로 주어질 때, 최빈값을 return 하도록 solution 함수를 완성해보세요. 최빈값이 여러 개면 -1을 return 합니다.

---

##### **제한사항**

- 0 < `array`의 길이 < 100
- 0 ≤ `array`의 원소 < 1000

---

##### **입출력 예**

|array|result|
|---|---|
|[1, 2, 3, 3, 3, 4]|3|
|[1, 1, 2, 2]|-1|
|[1]|1|

---

##### **입출력 예 설명**

입출력 예 #1

- [1, 2, 3, 3, 3, 4]에서 1은 1개 2는 1개 3은 3개 4는 1개로 최빈값은 3입니다.

입출력 예 #2

- [1, 1, 2, 2]에서 1은 2개 2는 2개로 최빈값이 1, 2입니다. 최빈값이 여러 개이므로 -1을 return 합니다.

입출력 예 #3

- [1]에는 1만 있으므로 최빈값은 1입니다.

<br />

---

<br/>
## **Solution** 
<br/>

> HashMap을 사용해서 배열을 돌면서 각 숫자별 나온 횟수를 저장하고, 그 값이 현재까지 나온 값중 가장 높은 값일 경우에 max와, 해당 숫자를 업데이트 해줍니다. 이후 answer를 반환합니다.

```java
import java.util.*;

class Solution {
    public int solution(int[] array) {
       Map<Integer, Integer> map = new HashMap<>();
        int max = 0;
        int answer = 0;

        for (int i = 0; i < array.length; i++) {
            Integer temp = map.getOrDefault(array[i], 0) + 1;
            map.put(array[i], temp);

            if (max < temp) {
                max = temp;
                answer = array[i];
            } else if (max == temp) {
                answer = -1;
            }
        }

        return answer;
    }
}
```