---
title: Programmers Java Lv.0 (15) - 문자 반복 출력하기
author: jay
date: 2024-03-30
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
---
## **문자 반복 출력하기**

<br />

---

<br/>
###### **문제 설명**

문자열 `my_string`과 정수 `n`이 매개변수로 주어질 때, `my_string`에 들어있는 각 문자를 `n`만큼 반복한 문자열을 return 하도록 solution 함수를 완성해보세요.

---

##### **제한사항**

- 2 ≤ `my_string` 길이 ≤ 5
- 2 ≤ `n` ≤ 10
- "my_string"은 영어 대소문자로 이루어져 있습니다.

---

##### **입출력 예**

|my_string|n|result|
|---|---|---|
|"hello"|3|"hhheeellllllooo"|

---

##### **입출력 예 설명**

입출력 예 #1

- "hello"의 각 문자를 세 번씩 반복한 "hhheeellllllooo"를 return 합니다.

<br />

---

<br/>

## Solution

> `StringBuffer, 이중 반복문`을 이용해 문자를 `append`하는 방법으로 문제를 풀었습니다.

```java
class Solution {
    public String solution(String my_string, int n) {
        StringBuffer answer = new StringBuffer();
        
        for (int i = 0; i < my_string.length(); i++){
            for (int j = 0; j<n; j++){
                answer.append(my_string.charAt(i));    
            }
        }
        
        return answer.toString();
    }
}
```

> 이전 문제에서 배운 `StringBuilder, repeat`를 사용해서 문제를 다시 풀어봤습니다. `charAt()`은 char 타입으로 반환되기 때문에 `+ ""`를 해줌으로써 `String으로 타입 캐스팅` 할 수 있었습니다.

```java
class Solution {
    public String solution(String my_string, int n) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < my_string.length(); i++){
            String temp = my_string.charAt(i) + "";
            stringBuilder.append(temp.repeat(n));
        }
        return stringBuilder.toString();
    }
}
```