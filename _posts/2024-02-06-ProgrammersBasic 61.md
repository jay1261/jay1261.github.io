---
title: Basic61 n 번째 원소부터
author: jay
date: 2024-02-06
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: n 번째 원소부터

###### 문제 설명

정수 리스트 `num_list`와 정수 `n`이 주어질 때, `n` 번째 원소부터 마지막 원소까지의 모든 원소를 담은 리스트를 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `num_list`의 길이 ≤ 30
- 1 ≤ `num_list`의 원소 ≤ 9
- 1 ≤ `n` ≤ `num_list`의 길이

---

##### 입출력 예

|num_list|n|result|
|---|---|---|
|[2, 1, 6]|3|[6]|
|[5, 2, 1, 7, 5]|2|[2, 1, 7, 5]|

---

##### 입출력 예 설명

입출력 예 #1

- [2, 1, 6]의 세 번째 원소부터 마지막 원소까지의 모든 원소는 [6]입니다.

입출력 예 #2

- [5, 2, 1, 7, 5]의 두 번째 원소부터 마지막 원소까지의 모든 원소는 [2, 1, 7, 5]입니다.

---

## Solution

>`[n-1...]` 을 사용해서 배열의 구간을 나누어 return 했습니다.

```swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    let num = n - 1
    return num_list[num...].map{$0}
}
```