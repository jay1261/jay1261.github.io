---
title: Programmers Java Lv.0 (33) - 합성수 찾기
author: jay
date: 2024-04-18
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **합성수 찾기**

<br />

---

<br/>

###### 문제 설명

약수의 개수가 세 개 이상인 수를 합성수라고 합니다. 자연수 `n`이 매개변수로 주어질 때 `n`이하의 합성수의 개수를 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 100

---

##### 입출력 예

|n|result|
|---|---|
|10|5|
|15|8|

---

##### 입출력 예 설명

입출력 예 #1

- 10 이하 합성수는 4, 6, 8, 9, 10 로 5개입니다. 따라서 5를 return합니다.

입출력 예 #1

- 15 이하 합성수는 4, 6, 8, 9, 10, 12, 14, 15 로 8개입니다. 따라서 8을 return합니다.


<br />

---

<br/>

## **Solution**

> 이중 for문을 사용해서, 2부터 n까지의 수들을 하나씩 보면서 합성수인지 아닌지 판별했습니다.

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = 2; i <= n; i++){
            int temp = 0;
            for(int j = 1; j <= i; j++){
                if (i % j == 0){
                    temp++;
                }
            }
            if (temp >= 3){
                answer++;
            }
        }
        
        return answer;
    }
}
```