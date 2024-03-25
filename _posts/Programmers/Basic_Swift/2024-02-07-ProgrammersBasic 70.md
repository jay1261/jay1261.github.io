---
title: Basic70 수열과 구간 쿼리 1
author: jay
date: 2024-02-07
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 수열과 구간 쿼리 1
## 문제: 수열과 구간 쿼리 1

###### 문제 설명

정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[s, e]` 꼴입니다.

각 `query`마다 순서대로 `s` ≤ `i` ≤ `e`인 모든 `i`에 대해 `arr[i]`에 1을 더합니다.

위 규칙에 따라 `queries`를 처리한 이후의 `arr`를 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `arr`의 길이 ≤ 1,000
    - 0 ≤ `arr`의 원소 ≤ 1,000,000
- 1 ≤ `queries`의 길이 ≤ 1,000
    - 0 ≤ `s` ≤ `e` < `arr`의 길이

---

##### 입출력 예

|arr|queries|result|
|---|---|---|
|[0, 1, 2, 3, 4]|[[0, 1],[1, 2],[2, 3]]|[1, 3, 4, 4, 4]|

---

##### 입출력 예 설명

입출력 예 #1

- 각 쿼리에 따라 `arr`가 다음과 같이 변합니다.

|i|queries[i]|arr|
|---|---|---|
|-|-|[0, 1, 2, 3, 4]|
|0|[0,1]|[1, 2, 2, 3, 4]|
|1|[1,2]|[1, 3, 3, 3, 4]|
|2|[2,3]|[1, 3, 4, 4, 4]|

- 따라서 [1, 3, 4, 4, 4]를 return 합니다.

---

## Solution

> 먼저 `queries.reduce(into: arr)`을 사용해서 `arr`을 `reduce`의 `초기값`으로 넣어주었습니다.

```swift
queries.reduce(into: arr){ result, q in }
```

> 그런 다음 `arr.indices.filter`를 사용해서 `index`의 값이 `queries의 범위`에 있는 `index들`을 뽑아낸 다음 그에 해당하는 `요소에 += 1`를 해주는 방법으로 문제를 풀었습니다.

```swift
import Foundation

func solution(_ arr:[Int], _ queries:[[Int]]) -> [Int] {
    return queries.reduce(into: arr){ result, q in
        arr.indices.filter{$0 >= q[0] && $0 <= q[1]}.map{result[$0] += 1}
    }
}
```