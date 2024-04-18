---
title: Programmers Java Lv.0 (16) - 특정 문자 제거하기
author: jay
date: 2024-03-30
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **특정 문자 제거하기**

<br />

---

<br/>
###### **문제 설명**

문자열 `my_string`과 문자 `letter`이 매개변수로 주어집니다. `my_string`에서 `letter`를 제거한 문자열을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 1 ≤ `my_string`의 길이 ≤ 100
- `letter`은 길이가 1인 영문자입니다.
- `my_string`과 `letter`은 알파벳 대소문자로 이루어져 있습니다.
- 대문자와 소문자를 구분합니다.

---

##### **입출력 예**

|my_string|letter|result|
|---|---|---|
|"abcdef"|"f"|"abcde"|
|"BCBdbe"|"B"|"Cdbe"|

---

##### **입출력 예 설명**

입출력 예 #1

- "abcdef" 에서 "f"를 제거한 "abcde"를 return합니다.

입출력 예 #2

- "BCBdbe" 에서 "B"를 모두 제거한 "Cdbe"를 return합니다.

<br />

---

<br/>


## **Solution**

> 반복문을 사용해서 `my_string의 요소`가 `letter`와 같으면 넘어가고, 아니면 `answer`에 더하는 방식으로 문제를 풀었습니다.

```java
class Solution {
    public String solution(String my_string, String letter) {
        String answer = "";
        for(int i = 0; i < my_string.length(); i++){
            if (letter.equals(my_string.charAt(i)+"")){
                continue;
            }
            answer += (my_string.charAt(i) + "");
        }
        
        return answer;
    }
}
```

<br/>

> String에 `replace`라는 함수를 이용하면 코드를 더 간결하게 만들 수 있습니다.

```java
class Solution {
    public String solution(String my_string, String letter) {
        return my_string.replace(letter, "");
    }
}
```