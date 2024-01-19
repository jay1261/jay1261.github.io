---
title: Basic31 수열과 구간 쿼리 4
author: jay
date: 2024-01-19
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 수열과 구간 쿼리 4

###### 문제 설명

정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[s, e, k]` 꼴입니다.

각 `query`마다 순서대로 `s` ≤ `i` ≤ `e`인 모든 `i`에 대해 `i`가 `k`의 배수이면 `arr[i]`에 1을 더합니다.

위 규칙에 따라 `queries`를 처리한 이후의 `arr`를 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `arr`의 길이 ≤ 1,000
    - 0 ≤ `arr`의 원소 ≤ 1,000,000
- 1 ≤ `queries`의 길이 ≤ 1,000
    - 0 ≤ `s` ≤ `e` < `arr`의 길이
    - 0 ≤ `k` ≤ 5

---

##### 입출력 예

|arr|queries|result|
|---|---|---|
|[0, 1, 2, 4, 3]|[[0, 4, 1],[0, 3, 2],[0, 3, 3]]|[3, 2, 4, 6, 4]|

---

##### 입출력 예 설명

입출력 예 #1

- 각 쿼리에 따라 `arr`가 다음과 같이 변합니다.

|arr|
|---|
|[0, 1, 2, 4, 3]|
|[1, 2, 3, 5, 4]|
|[2, 2, 4, 5, 4]|
|[3, 2, 4, 6, 4]|

- 따라서 [3, 2, 4, 6, 4]를 return 합니다.

---

## Solution

> 지난번에 공부했던 `reduec(into)`와 `map`을 사용해서 문제를 풀어봤습니다. 

```swift
import Foundation

func solution(_ arr:[Int], _ queries:[[Int]]) -> [Int] {
    return queries.reduce(into: arr) { result, q in
        result = result.enumerated().map{index, value in  
            index >= q[0] && index<=q[1] && index % q[2] == 0 ? value+1 : value
        }
    }
}
```