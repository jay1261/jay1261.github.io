---
title: Basic29 수열과 구간 쿼리 3
author: jay
date: 2024-01-17
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 수열과 구간 쿼리 3

###### 문제 설명

정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[i, j]` 꼴입니다.

각 `query`마다 순서대로 `arr[i]`의 값과 `arr[j]`의 값을 서로 바꿉니다.

위 규칙에 따라 `queries`를 처리한 이후의 `arr`를 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `arr`의 길이 ≤ 1,000
    - 0 ≤ `arr`의 원소 ≤ 1,000,000
- 1 ≤ `queries`의 길이 ≤ 1,000
    - 0 ≤ `i` < `j` < `arr`의 길이

---

##### 입출력 예

|arr|queries|result|
|---|---|---|
|[0, 1, 2, 3, 4]|[[0, 3],[1, 2],[1, 4]]|[3, 4, 1, 0, 2]|

---

##### 입출력 예 설명

입출력 예 #1

- 각 쿼리에 따라 `arr`가 다음과 같이 변합니다.

|arr|
|---|
|[0, 1, 2, 3, 4]|
|[3, 1, 2, 0, 4]|
|[3, 2, 1, 0, 4]|
|[3, 4, 1, 0, 2]|

- 따라서 [3, 4, 1, 0, 2]를 return 합니다.

---

## Solution

> 처음 `map`을 사용하고, swap로직을 직접 구현해서 문제를 풀었습니다.

```swift
import Foundation

func solution(_ arr:[Int], _ queries:[[Int]]) -> [Int] {
    var array = arr
    queries.map {
        let tmp = array[$0[0]]
        array[$0[0]] = array[$0[1]]
        array[$0[1]] = tmp
    }
    
    return array
}
```

> 이후 `swapAt` 이라는 함수가 있는 것을 알게 되었습니다. `swapAt`은 `swapAt(_ i, _j)`의 형태로 사용되고, `i, j`는 인덱스입니다. 배열안의 각 인덱스의 값을 서로 바꾸어주는 함수입니다.

```swift
func solution(_ arr:[Int], _ queries:[[Int]]) -> [Int] {
    var array = arr
    queries.map {
        array.swapAt($0[0], $0[1])
    }
    return array
}
```

> `reduce(into:_:)`를 이용한 풀이도 있습니다. 공식 문서를 보면 `reduce(into:_:)`는 `reduce(::)`와 다르게 inout 키워드가 붙은 Result를 받습니다. 따라서 초기값으로 넘기는 인자를 변형하여 결과를 얻고 싶다면, `reduce(into:_:)`를 사용할 수 있습니다.

```swift
func solution(_ arr:[Int], _ queries:[[Int]]) -> [Int] {
    return queries.reduce(into: arr) { result, q in
        print(result, q)
        result.swapAt(q[0], q[1])
    }
}
```
