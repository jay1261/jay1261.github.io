---
title: Programmers Java Lv.0 (20) - 배열 자르기
author: jay
date: 2024-04-01
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **배열 자르기**

<br />

---

<br/>

###### **문제 설명**

정수 배열 `numbers`와 정수 `num1`, `num2`가 매개변수로 주어질 때, `numbers`의 `num1`번 째 인덱스부터 `num2`번째 인덱스까지 자른 정수 배열을 return 하도록 solution 함수를 완성해보세요.

---

##### **제한사항**

- 2 ≤ `numbers`의 길이 ≤ 30
- 0 ≤ `numbers`의 원소 ≤ 1,000
- 0 ≤`num1` < `num2` < `numbers`의 길이

---

##### **입출력 예**

|numbers|num1|num2|result|
|---|---|---|---|
|[1, 2, 3, 4, 5]|1|3|[2, 3, 4]|
|[1, 3, 5]|1|2|[3, 5]|

---

##### **입출력 예 설명**

입출력 예 #1

- [1, 2, 3, 4, 5]의 1번째 인덱스 2부터 3번째 인덱스 4 까지 자른 [2, 3, 4]를 return 합니다.

입출력 예 #2

- [1, 3, 5]의 1번째 인덱스 3부터 2번째 인덱스 5까지 자른 [3, 5]를 return 합니다.

<br />

---

<br/>

## **Solution**

> `num2 - num1 + 1`로 배열의 크기를 정하고, 반복문을 num1...num2 까지 돌면서 새로 선언한 배열에 값을 하나씩 넣어주는 방식으로 문제를 풀었습니다.

```java
class Solution {
    public int[] solution(int[] numbers, int num1, int num2) {
        int[] answer = new int[num2-num1+1];
        
        for (int i = num1; i<=num2; i++){
            answer[i-num1] = numbers[i];
        }
        return answer;
    }
}
```

> `Arrays.copyOfRange(기존 배열, 시작 인덱스, 끝 인덱스`라는 함수를 이용하면 코드를 간략하게 구현할 수 있습니다.

```java
import java.util.*;

class Solution {
    public int[] solution(int[] numbers, int num1, int num2) {
        return Arrays.copyOfRange(numbers, num1, num2 + 1);
    }
}
```