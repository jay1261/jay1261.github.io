---
title: Programmers Java Lv.0 (29) - 2차원으로 만들기
author: jay
date: 2024-04-16
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **2차원으로 만들기**

<br />

---

<br/>

###### **문제 설명**

정수 배열 `num_list`와 정수 `n`이 매개변수로 주어집니다. `num_list`를 다음 설명과 같이 2차원 배열로 바꿔 return하도록 solution 함수를 완성해주세요.

`num_list`가 [1, 2, 3, 4, 5, 6, 7, 8] 로 길이가 8이고 `n`이 2이므로 `num_list`를 2 * 4 배열로 다음과 같이 변경합니다. 2차원으로 바꿀 때에는 num_list의 원소들을 앞에서부터 n개씩 나눠 2차원 배열로 변경합니다.

|num_list|n|result|
|---|---|---|
|[1, 2, 3, 4, 5, 6, 7, 8]|2|[[1, 2], [3, 4], [5, 6], [7, 8]]|

---

##### **제한사항**

- `num_list`의 길이는 `n`의 배 수개입니다.
- 0 ≤ `num_list`의 길이 ≤ 150
- 2 ≤ `n` < `num_list`의 길이

---

##### **입출력 예**

|num_list|n|result|
|---|---|---|
|[1, 2, 3, 4, 5, 6, 7, 8]|2|[[1, 2], [3, 4], [5, 6], [7, 8]]|
|[100, 95, 2, 4, 5, 6, 18, 33, 948]|3|[[100, 95, 2], [4, 5, 6], [18, 33, 948]]|

---

##### **입출력 예 설명**

입출력 예 #1

- `num_list`가 [1, 2, 3, 4, 5, 6, 7, 8] 로 길이가 8이고 `n`이 2이므로 2 * 4 배열로 변경한 [[1, 2], [3, 4], [5, 6], [7, 8]] 을 return합니다.

입출력 예 #2

- `num_list`가 [100, 95, 2, 4, 5, 6, 18, 33, 948] 로 길이가 9이고 `n`이 3이므로 3 * 3 배열로 변경한 [[100, 95, 2], [4, 5, 6], [18, 33, 948]] 을 return합니다.


<br />

---

<br/>

## Solution

> 주어진 `num_list의 길이`만큼 for문을 돌면서 `i%n` 의 값이 0이 될 때 answer의 행을 1씩 이동하게 하고, 열 또한 `i%n`의 값에따라 이동시키며 num_list의 값들을 차례로 대입해주었습니다.

```java
class Solution {
    public int[][] solution(int[] num_list, int n) {
        int[][] answer = new int[num_list.length/n][n];

        int index = -1;
        for (int i = 0; i < num_list.length; i++){
            if(i % n == 0){
                index++;
            }
            answer[index][i%n] = num_list[i];
        }
        
        return answer;
    }
}
```