---
title: Basic24 원소들의 곱과 합
author: jay
date: 2024-01-15
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 원소들의 곱과 합
###### 문제 설명

정수가 담긴 리스트 `num_list`가 주어질 때, 모든 원소들의 곱이 모든 원소들의 합의 제곱보다 작으면 1을 크면 0을 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `num_list`의 길이 ≤ 10
- 1 ≤ `num_list`의 원소 ≤ 9

---

##### 입출력 예

|num_list|result|
|---|---|
|[3, 4, 5, 2, 1]|1|
|[5, 7, 8, 3]|0|

---

##### 입출력 예 설명

입출력 예 #1

- 모든 원소의 곱은 120, 합의 제곱은 225이므로 1을 return합니다.

입출력 예 #2

- 모든 원소의 곱은 840, 합의 제곱은 529이므로 0을 return합니다.

---

## Solution

> `reduce`함수를 사용해 문제를 해결했습니다. 여기서 `reduce(0)`의 `()`안에 들어가는 매개변수는 `initialResult`로 초기누적값을 의미하는데, 이는 1부터 5를 더할때 `initialResult + 1`로 시작한다는 의미입니다. 그래서 처음에 `*`에도 reduce(0)을 사용했었는데, 이 때 초기값이 `0*1`이 되면서 모든 결과값이 0이 되는 상황을 겪었습니다.

```swift
import Foundation

func solution(_ num_list:[Int]) -> Int {
    let multiplication = num_list.reduce(1){$0 * $1}
    let sumSquar = pow(Float(num_list.reduce(0){$0 + $1}), 2)
    return multiplication < Int(sumSquar) ? 1 : 0
}
```

> 또한 reduce는 아래처럼 `reduce(0, +)`이렇게 사용할 수도 있습니다.

```swift
func solution(_ num_list:[Int]) -> Int {
    let multiplication = num_list.reduce(1, *)
    let sumSquar = pow(Float(num_list.reduce(0, +), 2)
    return multiplication < Int(sumSquar) ? 1 : 0
}
```