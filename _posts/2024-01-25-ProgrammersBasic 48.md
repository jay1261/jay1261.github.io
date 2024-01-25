---
title: Basic48 문자열 뒤집기
author: jay
date: 2024-01-25
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 문자열 뒤집기

###### 문제 설명

문자열 `my_string`과 정수 `s`, `e`가 매개변수로 주어질 때, `my_string`에서 인덱스 `s`부터 인덱스 `e`까지를 뒤집은 문자열을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- `my_string`은 숫자와 알파벳으로만 이루어져 있습니다.
- 1 ≤ `my_string`의 길이 ≤ 1,000
- 0 ≤ `s` ≤ `e` < `my_string`의 길이

---

##### 입출력 예

|my_string|s|e|result|
|---|---|---|---|
|"Progra21Sremm3"|6|12|"ProgrammerS123"|
|"Stanley1yelnatS"|4|10|"Stanley1yelnatS"|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`에서 인덱스 6부터 인덱스 12까지를 뒤집은 문자열은 "ProgrammerS123"이므로 "ProgrammerS123"를 return 합니다.

입출력 예 #2

- 예제 2번의 `my_string`에서 인덱스 4부터 인덱스 10까지를 뒤집으면 원래 문자열과 같은 "Stanley1yelnatS"이므로 "Stanley1yelnatS"를 return 합니다.

---

## Solution

>`my_string`을 Array로 변환해주고, Array에 s부터 e까지를 reverse한 후에 다시 String으로 변환해주었습니다.

```swift
import Foundation

func solution(_ my_string:String, _ s:Int, _ e:Int) -> String {
    var strArray = Array(my_string)
    strArray[s...e].reverse()
    
    return String(strArray)
}
```