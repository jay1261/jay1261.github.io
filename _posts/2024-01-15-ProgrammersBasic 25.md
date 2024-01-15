---
title: "Basic25 이어 붙인 수\x1c"
author: jay
date: 2024-01-15
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 이어 붙인 수

###### 문제 설명

정수가 담긴 리스트 `num_list`가 주어집니다. `num_list`의 홀수만 순서대로 이어 붙인 수와 짝수만 순서대로 이어 붙인 수의 합을 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `num_list`의 길이 ≤ 10
- 1 ≤ `num_list`의 원소 ≤ 9
- `num_list`에는 적어도 한 개씩의 짝수와 홀수가 있습니다.

---

##### 입출력 예

|num_list|result|
|---|---|
|[3, 4, 5, 2, 1]|393|
|[5, 7, 8, 3]|581|

---

##### 입출력 예 설명

입출력 예 #1

- 홀수만 이어 붙인 수는 351이고 짝수만 이어 붙인 수는 42입니다. 두 수의 합은 393입니다.

입출력 예 #2

- 홀수만 이어 붙인 수는 573이고 짝수만 이어 붙인 수는 8입니다. 두 수의 합은 581입니다.

---

## Solution

> `filter`와 `reduce` 함수를 이용해서 문제를 풀었습니다.

```swift
import Foundation

func solution(_ num_list:[Int]) -> Int {
    let odd = Int(num_list.filter{$0 % 2 != 0}.reduce(""){String($0) + String($1)}) ?? 0
    let even = Int(num_list.filter{$0 % 2 == 0}.reduce(""){String($0) + String($1)}) ?? 0
    
    return odd + even
}
```

> 아래는 같은 방법이지만 조금 더 깔끔한 코드입니다. `filter, map, joined`을 사용했습니다.

```swift
func solution(_ num_list:[Int]) -> Int {
    let odd = Int(num_list.filter{$0 % 2 != 0}.map{String($0)}.joined()) ?? 0
    let even = Int(num_list.filter{$0 % 2 == 0}.map{String($0)}.joined()) ?? 0
    
    return odd + even
}
```