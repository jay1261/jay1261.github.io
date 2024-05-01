---
title: Programmers Java Lv.0 (27) - 구슬을 나누는 경우의 수
author: jay
date: 2024-04-15
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **구슬을 나누는 경우의 수**

<br />

---

<br/>

###### 문제 설명

머쓱이는 구슬을 친구들에게 나누어주려고 합니다. 구슬은 모두 다르게 생겼습니다. 머쓱이가 갖고 있는 구슬의 개수 `balls`와 친구들에게 나누어 줄 구슬 개수 `share`이 매개변수로 주어질 때, `balls`개의 구슬 중 `share`개의 구슬을 고르는 가능한 모든 경우의 수를 return 하는 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `balls` ≤ 30
- 1 ≤ `share` ≤ 30
- 구슬을 고르는 순서는 고려하지 않습니다.
- `share` ≤ `balls`

---

##### 입출력 예

|balls|share|result|
|---|---|---|
|3|2|3|
|5|3|10|

---

##### 입출력 예 설명

입출력 예 #1

- 서로 다른 구슬 3개 중 2개를 고르는 경우의 수는 3입니다. ![스크린샷 2022-08-01 오후 4.15.55.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/668adf7a-38b1-4112-bbc5-4fab429168c9/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-08-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.15.55.png)

입출력 예 #2

- 서로 다른 구슬 5개 중 3개를 고르는 경우의 수는 10입니다.

---

##### Hint

- 서로 다른 n개 중 m개를 뽑는 경우의 수 공식은 다음과 같습니다. ![스크린샷 2022-08-01 오후 4.37.53.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/54c8b2b9-f88c-4a09-8956-7560ff7ea918/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-08-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.37.53.png)


<br />

---

<br/>

## **Solution**

> 처음엔 factorial 함수를 만들어서 접근했지만, 숫자가 너무 크게 나와서 일부 케이스에서는 오버플로우가 발생했습니다. 

```java
class Solution {
    public int solution(int balls, int share) {
		 double result = factorial(balls) / (factorial(balls-share) * factorial(share));
        return (int) result;
    }
    
    private static double factorial(int n){
        if (n == 0) {
            return 1;
        }
        
        double result = 1;
        for(int i = 1; i <= n; i++){
            result *= i;
        }
        return result;
    }
}
```

> for문을 사용해 각 반복 단계에서 `answer`에 `(balls - i) / (i+1)`을 곱하는 방법으로 문제를 풀었습니다.

```java
class Solution {
    public int solution(int balls, int share) {
         double answer = 1;

        for(int i = 0; i < share; i++){
            answer = answer * (balls - i) / (i+1);
        }
        return (int)answer;
    }
}
```