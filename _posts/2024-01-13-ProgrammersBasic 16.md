---
title: Basic16 n의 배수
author: jay
date: 2024-01-13
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: n의 배수

###### 문제 설명

정수 `num`과 `n`이 매개 변수로 주어질 때, `num`이 `n`의 배수이면 1을 return `n`의 배수가 아니라면 0을 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `num` ≤ 100
- 2 ≤ `n` ≤ 9

---

##### 입출력 예

|num|n|result|
|---|---|---|
|98|2|1|
|34|3|0|

---

##### 입출력 예 설명

입출력 예 #1

- 98은 2의 배수이므로 1을 return합니다.

입출력 예 #2

- 32는 3의 배수가 아니므로 0을 return합니다.

---

## Solution

> `num`이 `n`의 배수라면 `num / 2`의 나머지는 0이 됩니다. 따라서 나머지 연산자 `%` 를 사용하여 문제를 풀었습니다.

```swift
import Foundation

func solution(_ num:Int, _ n:Int) -> Int {
    return num % n == 0 ? 1 : 0
}
```
