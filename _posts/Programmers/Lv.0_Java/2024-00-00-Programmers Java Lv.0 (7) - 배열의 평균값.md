---
title: Programmers Java Lv.0 (7) - 배열의 평균값
author: jay
date: 2024-03-28
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **배열의 평균값**

<br />

---

<br/>

###### **문제 설명**

정수 배열 `numbers`가 매개변수로 주어집니다. `numbers`의 원소의 평균값을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 0 ≤ `numbers`의 원소 ≤ 1,000
- 1 ≤ `numbers`의 길이 ≤ 100
- 정답의 소수 부분이 .0 또는 .5인 경우만 입력으로 주어집니다.

---

##### 입출력 예

|numbers|result|
|---|---|
|[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]|5.5|
|[89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]|94.0|

---

##### **입출력 예 설명**

입출력 예 #1

- `numbers`의 원소들의 평균 값은 5.5입니다.

입출력 예 #2

- `numbers`의 원소들의 평균 값은 94.0입니다.



<br />

---

<br/>


## **Solution**
<br/>

> 배열의 모든 요소를 더해서 배열의 길이로 나누어서 평균을 구했습니다.

```java
class Solution {
    public double solution(int[] numbers) {
	    int sum = 0;
	    
		for(int number: numbers){
			sum += number;
        }
        
        return (double) sum / numbers.length;
    }
}
```

<br/>

> 다른 풀이들을 보니 Java의 Stream을 사용해서 더 간결한 코드를 작성할 수도 있었습니다.

```java
import java.util.*;

class Solution {
    public double solution(int[] numbers) {
        return Arrays.stream(numbers).average().orElse(0);
	}
}
```

