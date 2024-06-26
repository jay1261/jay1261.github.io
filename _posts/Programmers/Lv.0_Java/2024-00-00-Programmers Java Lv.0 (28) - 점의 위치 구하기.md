---
title: Programmers Java Lv.0 (28) - 점의 위치 구하기
author: jay
date: 2024-04-16
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **점의 위치 구하기**

<br />

---

<br/>

###### **문제 설명**

사분면은 한 평면을 x축과 y축을 기준으로 나눈 네 부분입니다. 사분면은 아래와 같이 1부터 4까지 번호를매깁니다.  
![스크린샷 2022-07-07 오후 3.27.04 복사본.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/b58d4788-42fa-44fa-af50-481907e65473/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-07-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.27.04%20%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%A1%E1%84%87%E1%85%A9%E1%86%AB.png)

- x 좌표와 y 좌표가 모두 양수이면 제1사분면에 속합니다.
- x 좌표가 음수, y 좌표가 양수이면 제2사분면에 속합니다.
- x 좌표와 y 좌표가 모두 음수이면 제3사분면에 속합니다.
- x 좌표가 양수, y 좌표가 음수이면 제4사분면에 속합니다.

x 좌표 (x, y)를 차례대로 담은 정수 배열 `dot`이 매개변수로 주어집니다. 좌표 `dot`이 사분면 중 어디에 속하는지 1, 2, 3, 4 중 하나를 return 하도록 solution 함수를 완성해주세요.

---

#### **제한사항**

- `dot`의 길이 = 2
- `dot[0]`은 x좌표를, `dot[1]`은 y좌표를 나타냅니다
- -500 ≤ `dot`의 원소 ≤ 500
- `dot`의 원소는 0이 아닙니다.

---

#### **입출력 예**

|dot|result|
|---|---|
|[2, 4]|1|
|[-7, 9]|2|

---

#### **입출력 예 설명**

입출력 예 #1

- `dot`이 [2, 4]로 x 좌표와 y 좌표 모두 양수이므로 제 1 사분면에 속합니다. 따라서 1을 return 합니다.

입출력 예 #2

- `dot`이 [-7, 9]로 x 좌표가 음수, y 좌표가 양수이므로 제 2 사분면에 속합니다. 따라서 2를 return 합니다.

<br />

---

<br/>

## **Solution**

> if else문을 활용해서 x가 음수 or 양수일 때, y가 음수 or 양수일 때를 비교해서 문제를 풀었습니다.

```java
class Solution {
    public int solution(int[] dot) {
        int answer = 0;
        int x = dot[0];
        int y = dot[1];
        
        if (x > 0) {
            answer = (y > 0) ? 1 : 4;
        } 
        else {
            answer = (y > 0) ? 2 : 3;
        }

        return answer;
    }
}
```