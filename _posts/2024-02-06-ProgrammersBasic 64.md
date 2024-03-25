---
title: Basic64 n 번째 원소까지
author: jay
date: 2024-02-06
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: n 번째 원소까지

###### 문제 설명

정수 리스트 `num_list`와 정수 `n`이 주어질 때, `num_list`의 첫 번째 원소부터 `n` 번째 원소까지의 모든 원소를 담은 리스트를 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `num_list`의 길이 ≤ 30
- 1 ≤ `num_list`의 원소 ≤ 9
- 1 ≤ `n` ≤ `num_list`의 길이 ___

##### 입출력 예

|num_list|n|result|
|---|---|---|
|[2, 1, 6]|1|[2]|
|[5, 2, 1, 7, 5]|3|[5, 2, 1]|

---

##### 입출력 예 설명

입출력 예 #1

- [2, 1, 6]의 첫 번째 원소부터 첫 번째 원소까지의 모든 원소는 [2]입니다.

입출력 예 #2

- [5, 2, 1, 7, 5]의 첫 번째 원소부터 세 번째 원소까지의 모든 원소는 [5, 2, 1]입니다.

--- 

## Solution

>`[0..<n]`을 사용해서 배열의 구간을 나누어 문제를 풀었습니다.
> `참고: num_list[0..<n]의 반환타입은 'ArraySlice<Int>'이므로 map을 사용해 [Int] 타입으로 변환해주어야 합니다. 

```swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    return num_list[0..<n].map{$0}
}
```