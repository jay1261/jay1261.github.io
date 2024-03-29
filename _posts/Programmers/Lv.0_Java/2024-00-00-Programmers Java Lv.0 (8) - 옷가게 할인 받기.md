---
title: Programmers Java Lv.0 (8) - 옷가게 할인 받기
author: jay
date: 2024-03-29
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **옷가게 할인 받기**

<br />

---

<br/>

###### **문제 설명**

머쓱이네 옷가게는 10만 원 이상 사면 5%, 30만 원 이상 사면 10%, 50만 원 이상 사면 20%를 할인해줍니다.  
구매한 옷의 가격 `price`가 주어질 때, 지불해야 할 금액을 return 하도록 solution 함수를 완성해보세요.

---

##### **제한사항**

- 10 ≤ `price` ≤ 1,000,000
    - `price`는 10원 단위로(1의 자리가 0) 주어집니다.
- 소수점 이하를 버린 정수를 return합니다.

---

##### **입출력 예**

|price|result|
|---|---|
|150,000|142,500|
|580,000|464,000|

---

##### **입출력 예 설명**

입출력 예 #1

- 150,000원에서 5%를 할인한 142,500원을 return 합니다.

입출력 예 #2

- 580,000원에서 20%를 할인한 464,000원을 return 합니다.



<br />

---

<br/>


## **Solution** 

> 단순하게 if문을 사용해서 50만원 부터 차례로 검사하는 코드로 문제를 풀었습니다.

```java
class Solution {
    public int solution(int price) {
        double answer = 0;
        if (price >= 500000) {
            answer = price - (price * 0.2);
        } else if (price >= 300000) {
            answer = price - (price * 0.1);
        } else if (price >= 100000) {
            answer = price - (price * 0.05);
        } else {
            return price;
        }        
        
        return (int)answer;
    }
}
```