---
title: Basic49 세로 읽기
author: jay
date: 2024-01-25
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 세로 읽기

###### 문제 설명

문자열 `my_string`과 두 정수 `m`, `c`가 주어집니다. `my_string`을 한 줄에 `m` 글자씩 가로로 적었을 때 왼쪽부터 세로로 `c`번째 열에 적힌 글자들을 문자열로 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- `my_string`은 영소문자로 이루어져 있습니다.
- 1 ≤ `m` ≤ `my_string`의 길이 ≤ 1,000
- `m`은 `my_string` 길이의 약수로만 주어집니다.
- 1 ≤ `c` ≤ `m`

---

##### 입출력 예

|my_string|m|c|result|
|---|---|---|---|
|"ihrhbakrfpndopljhygc"|4|2|"happy"|
|"programmers"|1|1|"programmers"|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`을 한 줄에 4 글자씩 쓰면 다음의 표와 같습니다.
    
    |1열|2열|3열|4열|
    |---|---|---|---|
    |i|h|r|h|
    |b|a|k|r|
    |f|p|n|d|
    |o|p|l|j|
    |h|y|g|c|
    
    2열에 적힌 글자를 세로로 읽으면 happy이므로 "happy"를 return 합니다.
    

입출력 예 #2

- 예제 2번의 `my_string`은 `m`이 1이므로 세로로 "programmers"를 적는 것과 같고 따라서 1열에 적힌 글자를 세로로 읽으면 programmers입니다. 따라서 "programmers"를 return 합니다.

--- 

## Solution

> `my_string`의 각각 `index`의 값을 `m`으로 나누었을 때의 나머지 값은 `2차원 배열로 봤을 때 열의 값`과 같습니다. 이를 이용해서 문제를 풀었습니다.

```swift
import Foundation

func solution(_ my_string:String, _ m:Int, _ c:Int) -> String {
    var strArray = Array(my_string)
    return String(strArray.indices.filter{$0 % m == c-1}.map{strArray[$0]})
}
```