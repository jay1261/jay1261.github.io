---
title: Programmers Java Lv.0 (31) - 배열 회전시키기
author: jay
date: 2024-04-17
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **배열 회전시키기**

<br />

---

<br/>

###### **문제 설명**

정수가 담긴 배열 `numbers`와 문자열 `direction`가 매개변수로 주어집니다. 배열 `numbers`의 원소를 `direction`방향으로 한 칸씩 회전시킨 배열을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 3 ≤ `numbers`의 길이 ≤ 20
- `direction`은 "left" 와 "right" 둘 중 하나입니다.

---

##### **입출력 예**

|numbers|direction|result|
|---|---|---|
|[1, 2, 3]|"right"|[3, 1, 2]|
|[4, 455, 6, 4, -1, 45, 6]|"left"|[455, 6, 4, -1, 45, 6, 4]|

---

##### **입출력 예 설명**

입출력 예 #1

- `numbers` 가 [1, 2, 3]이고 `direction`이 "right" 이므로 오른쪽으로 한 칸씩 회전시킨 [3, 1, 2]를 return합니다.

입출력 예 #2

- `numbers` 가 [4, 455, 6, 4, -1, 45, 6]이고 `direction`이 "left" 이므로 왼쪽으로 한 칸씩 회전시킨 [455, 6, 4, -1, 45, 6, 4]를 return합니다.


<br />

---

<br/>

## Solution

> direction이 left일 때, 0번째 요소를 제외하고 나머지를 answer의 0부터 차례대로 담습니다. 마지막으로 0번째 요소를 answer의 맨 뒤에 넣어줍니다.
> <br/>
> direction이 right일 때는 반대로, 마지막 요소를 제외한 나머지를 answer의 1번째부터 담습니다. 이후 마지막 요소를 맨앞에 추가하고 return합니다.

```java
class Solution {
    public int[] solution(int[] numbers, String direction) {
        int[] answer = new int[numbers.length];
        if (direction.equals("left")){
            for (int i = 0; i < numbers.length - 1; i++){
                answer[i] = numbers[i+1];
            }
            answer[numbers.length-1] = numbers[0];
        }
        else {
            for (int i = 0; i < numbers.length - 1; i++){
                answer[i+1] = numbers[i];
            }
            answer[0] = numbers[numbers.length-1];
        }
        
        return answer;
    }
}
```