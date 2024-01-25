---
title: Basic45 접미사인지 확인하기
author: jay
date: 2024-01-25
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 접미사인지 확인하기

###### 문제 설명

어떤 문자열에 대해서 접미사는 특정 인덱스부터 시작하는 문자열을 의미합니다. 예를 들어, "banana"의 모든 접미사는 "banana", "anana", "nana", "ana", "na", "a"입니다.  
문자열 `my_string`과 `is_suffix`가 주어질 때, `is_suffix`가 `my_string`의 접미사라면 1을, 아니면 0을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `my_string`의 길이 ≤ 100
- 1 ≤ `is_suffix`의 길이 ≤ 100
- `my_string`과 `is_suffix`는 영소문자로만 이루어져 있습니다.

---

##### 입출력 예

|my_string|is_suffix|result|
|---|---|---|
|"banana"|"ana"|1|
|"banana"|"nan"|0|
|"banana"|"wxyz"|0|
|"banana"|"abanana"|0|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번에서 `is_suffix`가 `my_string`의 접미사이기 때문에 1을 return 합니다.

입출력 예 #2

- 예제 2번에서 `is_suffix`가 `my_string`의 접미사가 아니기 때문에 0을 return 합니다.

입출력 예 #3

- 예제 3번에서 `is_suffix`가 `my_string`의 접미사가 아니기 때문에 0을 return 합니다.

입출력 예 #4

- 예제 4번에서 `is_suffix`가 `my_string`의 접미사가 아니기 때문에 0을 return 합니다.

---

## Solution

> `suffix` 함수를 사용해서 `my_string`에 `is_suffix.count` 숫자만큼 `suffix`를 실행시켜서, 그 값이 `is_suffix`와 같으면 1 아니면 0 을 반환합니다.

```swift
import Foundation

func solution(_ my_string:String, _ is_suffix:String) -> Int {
    return is_suffix == my_string.suffix(is_suffix.count) ? 1 : 0
}
```

> `hasSuffix`라는 함수를 찾아서 사용해봤습니다. 

```swift
import Foundation

func solution(_ my_string:String, _ is_suffix:String) -> Int {
    return my_string.hasSuffix(is_suffix) ? 1:0
}
```