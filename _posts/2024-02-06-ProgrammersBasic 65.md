---
title: Basic65 n개 간격의 원소들
author: jay
date: 2024-02-06
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: n개 간격의 원소들

###### 문제 설명

정수 리스트 `num_list`와 정수 `n`이 주어질 때, `num_list`의 첫 번째 원소부터 마지막 원소까지 `n`개 간격으로 저장되어있는 원소들을 차례로 담은 리스트를 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 5 ≤ `num_list`의 길이 ≤ 20
- 1 ≤ `num_list`의 원소 ≤ 9
- 1 ≤ `n` ≤ 4

---

##### 입출력 예

|num_list|n|result|
|---|---|---|
|[4, 2, 6, 1, 7, 6]|2|[4, 6, 7]|
|[4, 2, 6, 1, 7, 6]|4|[4, 7]|

---

##### 입출력 예 설명

입출력 예 #1

- [4, 2, 6, 1, 7, 6]에서 2개 간격으로 저장되어 있는 원소들은 [4, 6, 7]입니다.

입출력 예 #2

- [4, 2, 6, 1, 7, 6]에서 4개 간격으로 저장되어 있는 원소들은 [4, 7]입니다.

---

## Solution

> `filter`와 `% 연산자`를 사용해서 `n`개의 간격으로 원소를 걸러내는 코드를 구현했습니다.

```swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    return num_list.enumerated().filter{$0.offset % n == 0}.map{$0.element}
}
```

> 다른 방법으로는 `stride`를 이용해서 n개의 간격으로 원소를 담는 코드를 구현할 수 있습니다.

```swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    return stride(from:0 , to: num_list.count, by: n).map{num_list[$0]}
}
```