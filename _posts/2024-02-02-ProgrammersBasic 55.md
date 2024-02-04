---
title: Basic55 가까운 1 찾기
author: jay
date: 2024-02-02
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 가까운 1 찾기

###### 문제 설명

정수 배열 `arr`가 주어집니다. 이때 `arr`의 원소는 1 또는 0입니다. 정수 `idx`가 주어졌을 때, `idx`보다 크면서 배열의 값이 1인 가장 작은 인덱스를 찾아서 반환하는 solution 함수를 완성해 주세요.

단, 만약 그러한 인덱스가 없다면 -1을 반환합니다.

---

##### 제한사항

- 3 ≤ `arr`의 길이 ≤ 100'000
    - `arr`의 원소는 전부 1 또는 0입니다. 

---

##### 입출력 예

|arr|idx|result|
|---|---|---|
|[0, 0, 0, 1]|1|3|
|[1, 0, 0, 1, 0, 0]|4|-1|
|[1, 1, 1, 1, 0]|3|3|

---

##### 입출력 예 설명

입출력 예 #1

- 1보다 크면서 원소가 1인 가장 작은 인덱스는 3입니다. 따라서 3을 return 합니다.

입출력 예 #2

- 4번 인덱스 이후에 1은 등장하지 않습니다. 따라서 -1을 return 합니다.

입출력 예 #3

- 3번 인덱스의 값이 1입니다. 따라서 3을 return 합니다.

---

## Solution
``
> `arr`를 `idx` 부터 끝까지의 배열을 추출해 냅니다. `enumerated`를 사용해서 `index`와 `element`를 받아오고 그중 `element`가 1인 요소들을 `filter`를 사용해 걸러냅니다. 그 중의 최초 값을 반환하는데 만약 없다면 `-1`을 반환합니다. 현재 이 배열의 `index`는 `idx`앞의 값들을 제외하고 `0`부터 시작했기 때문에 `idx`를 마지막에 더해줍니다.

```swift
import Foundation

func solution(_ arr:[Int], _ idx:Int) -> Int {
    return (arr[idx...].enumerated().filter{$0.element == 1}.map{$0.offset}.first ?? -1-idx) + idx
}
```