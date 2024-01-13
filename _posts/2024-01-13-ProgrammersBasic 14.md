---
title: Basic14 더 크게 합치기
author: jay
date: 2024-01-13
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 14. 더 크게 합치기

###### 문제 설명

연산 ⊕는 두 정수에 대한 연산으로 두 정수를 붙여서 쓴 값을 반환합니다. 예를 들면 다음과 같습니다.

- 12 ⊕ 3 = 123
- 3 ⊕ 12 = 312

양의 정수 `a`와 `b`가 주어졌을 때, `a` ⊕ `b`와 `b` ⊕ `a` 중 더 큰 값을 return 하는 solution 함수를 완성해 주세요.

단, `a` ⊕ `b`와 `b` ⊕ `a`가 같다면 `a` ⊕ `b`를 return 합니다.

---

##### 제한사항

- 1 ≤ `a`, `b` < 10,000

---

##### 입출력 예

|a|b|result|
|---|---|---|
|9|91|991|
|89|8|898|

---

##### 입출력 예 설명

입출력 예 #1

- `a` ⊕ `b` = 991 이고, `b` ⊕ `a` = 919 입니다. 둘 중 더 큰 값은 991 이므로 991을 return 합니다.

입출력 예 #2

- `a` ⊕ `b` = 898 이고, `b` ⊕ `a` = 889 입니다. 둘 중 더 큰 값은 898 이므로 898을 return 합니다.

--- 

### Solution

> String으로 형변환을 통해서 a와b를 붙이고, 다시 Int로 형변환을 통해 두개의 결과 값을 비교하여 더 큰 값을 return 했습니다.

```swift
import Foundation

func solution(_ a:Int, _ b:Int) -> Int {
    let str1 = String(a) + String(b)
    let str2 = String(b) + String(a)
    let result1 = Int(str1) ?? 0
    let result2 = Int(str2) ?? 0
    
    return (result1 > result2 ? result1 : result2)
}
```