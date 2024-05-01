---
title: Programmers Java Lv.0 (11) - 배열 뒤집기
author: jay
date: 2024-03-29
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **배열 뒤집기**

<br />

---

<br/>
###### **문제 설명**

정수가 들어 있는 배열 `num_list`가 매개변수로 주어집니다. `num_list`의 원소의 순서를 거꾸로 뒤집은 배열을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 1 ≤ `num_list`의 길이 ≤ 1,000
- 0 ≤ `num_list`의 원소 ≤ 1,000

---

##### **입출력 예**

|num_list|result|
|---|---|
|[1, 2, 3, 4, 5]|[5, 4, 3, 2, 1]|
|[1, 1, 1, 1, 1, 2]|[2, 1, 1, 1, 1, 1]|
|[1, 0, 1, 1, 1, 3, 5]|[5, 3, 1, 1, 1, 0, 1]|

---

##### **입출력 예 설명**

입출력 예 #1

- `num_list`가 [1, 2, 3, 4, 5]이므로 순서를 거꾸로 뒤집은 배열 [5, 4, 3, 2, 1]을 return합니다.

입출력 예 #2

- `num_list`가 [1, 1, 1, 1, 1, 2]이므로 순서를 거꾸로 뒤집은 배열 [2, 1, 1, 1, 1, 1]을 return합니다.

입출력 예 #3

- `num_list`가 [1, 0, 1, 1, 1, 3, 5]이므로 순서를 거꾸로 뒤집은 배열 [5, 3, 1, 1, 1, 0, 1]을 return합니다.


<br />

---

<br/>

## **Solution**

> 주어진 배열의 길이를 구하고, 그 길이만큼 새로운 배열을 만들었습니다. 반복문을 돌면서 기존 배열은 뒤에서부터 값을 새로운 배열의 앞부터 넣어주었습니다.

```java
class Solution {
    public int[] solution(int[] num_list) {
        int length = num_list.length;
        int[] answer = new int[length];
        for(int i = 0; i < length; i++){
            answer[i] = num_list[length-i-1];
        }
        
        return answer;
    }
}
```


> Java에 `Stream` 라이브러리를 사용하는게 중요한데, `LongStream`을 사용해서 문제를 푼 답안을 찾게되었습니다. 

```java
import java.util.stream.LongStream;

class Solution {
    public int[] solution(int[] num_list) {
        return LongStream.range(1, num_list.length + 1)
                .mapToInt(i -> num_list[(int) (num_list.length - i)])
                .toArray();
    }
}
```
<br/>

> 해당 답안을 참고하여 `IntStream`을 이용해서 문제를 다시 풀어보았습니다.

```java
import java.util.stream.IntStream;

class Solution {
    public int[] solution(int[] num_list) {
        int length = num_list.length;
        return IntStream.range(1, length + 1)
            .map(i -> num_list[length - i])
            .toArray();
    }
}
```