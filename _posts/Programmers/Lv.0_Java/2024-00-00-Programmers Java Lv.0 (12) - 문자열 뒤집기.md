---
title: Programmers Java Lv.0 (12) - 문자열 뒤집기
author: jay
date: 2024-03-30
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **문자열 뒤집기**

<br />

---

<br/>
###### **문제 설명**

문자열 `my_string`이 매개변수로 주어집니다. `my_string`을 거꾸로 뒤집은 문자열을 return하도록 solution 함수를 완성해주세요.

---

##### **제한사항**

- 1 ≤ `my_string`의 길이 ≤ 1,000

---

##### **입출력 예**

|my_string|return|
|---|---|
|"jaron"|"noraj"|
|"bread"|"daerb"|

---

##### **입출력 예 설명**

입출력 예 #1

- `my_string`이 "jaron"이므로 거꾸로 뒤집은 "noraj"를 return합니다.

입출력 예 #2

- `my_string`이 "bread"이므로 거꾸로 뒤집은 "daerb"를 return합니다.


<br />

---

<br/>

## **Solution**

> 캐릭터 배열을 `my_string.length()`의 크기로 만들어 주고, `my_string`의 길이만큼 반복문을 돌면서 캐릭터 배열에 반대로 넣어주고, String으로 변환해 반환하는 방법으로 문제를 풀었습니다.

```java
class Solution {
    public String solution(String my_string) {
        char[] arr = new char[my_string.length()];
        for(int i = 0; i < my_string.length(); i++){
            arr[i] = my_string.charAt(my_string.length() - i - 1);
            
        }
        return String.valueOf(arr);
    }
}
```


> Java의 `StringBuilder`를 사용하면 해당 문제를 간결하게 풀 수 있습니다.

```java
class Solution {
    public String solution(String my_string) {
        StringBuilder stringBuilder = new StringBuilder(my_string);
        return stringBuilder.reverse().toString();
    }
}
```