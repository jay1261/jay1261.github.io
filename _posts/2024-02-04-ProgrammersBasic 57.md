---
title: Basic57 첫 번째로 나오는 음수
author: jay
date: 2024-02-04
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 첫 번째로 나오는 음수

###### 문제 설명

정수 리스트 `num_list`가 주어질 때, 첫 번째로 나오는 음수의 인덱스를 return하도록 solution 함수를 완성해주세요. 음수가 없다면 -1을 return합니다.

---

##### 제한사항

- 5 ≤ `num_list`의 길이 ≤ 100
- -10 ≤ `num_list`의 원소 ≤ 100

---

##### 입출력 예

|num_list|result|
|---|---|
|[12, 4, 15, 46, 38, -2, 15]|5|
|[13, 22, 53, 24, 15, 6]|-1|

---

##### 입출력 예 설명

입출력 예 #1

- 5번 인덱스에서 음수가 처음 등장하므로 5를 return합니다.

입출력 예 #2

- 음수가 없으므로 -1을 return합니다.

---

## Solution

> `index`를 리턴해야하기 때문에 `enumerated`를 사용했고, 값이 음수인 경우의 첫번째 인덱스를 리턴, 없다면 -1을 리턴하게 코드를 작성했습니다.

```swift
import Foundation

func solution(_ num_list:[Int]) -> Int {
    return num_list.enumerated().filter{index, value in value < 0}.map{$0.offset}.first ?? -1
}
```