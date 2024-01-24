---
title: Basic41 배열만들기 5
author: jay
date: 2024-01-24
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 배열만들기 5

###### 문제 설명

문자열 배열 `intStrs`와 정수 `k`, `s`, `l`가 주어집니다. `intStrs`의 원소는 숫자로 이루어져 있습니다. 

배열 `intStrs`의 각 원소마다 `s`번 인덱스에서 시작하는 길이 `l`짜리 부분 문자열을 잘라내 정수로 변환합니다. 이때 변환한 정수값이 `k`보다 큰 값들을 담은 배열을 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 0 ≤ `s` < 100
- 1 ≤ `l` ≤ 8
- 10l - 1 ≤ `k` < 10l
- 1 ≤ `intStrs`의 길이 ≤ 10,000
    - `s` + `l` ≤ `intStrs`의 원소의 길이 ≤ 120

---

##### 입출력 예

|intStrs|k|s|l|result|
|---|---|---|---|---|
|["0123456789","9876543210","9999999999999"]|50000|5|5|[56789, 99999]|

---

##### 입출력 예 설명

입출력 예 #1

- idx에 따라 잘라낸 문자열과 그에 따른 `ret`의 변화를 표시하면 다음 표와 같습니다.

|idx|잘라낸 문자열|ret|
|---|---|---|
|0|"56789"|[56789]|
|1|"43210"|[56789]|
|2|"99999"|[56789, 99999]|

- 따라서 [56789, 99999]를 return 합니다.

---

## Solution

> 처음에 `map, filter`를 사용해서 풀려고 노력해봤는데, 풀기는 했지만 코드를 알아보기 어렵고 굉장히 비효율적인 코드가 되었습니다.

```swift
import Foundation

func solution(_ intStrs:[String], _ k:Int, _ s:Int, _ l:Int) -> [Int] {
    let arr = intStrs.map{ $0.enumerated().filter{$0.offset >= s && $0.offset < s+l}.map{String($0.element)}.joined()}
    
    return arr.map{Int($0)!}.filter{$0 > k}
}
```

> 이후 `String.prefix(), String.suffix()`를 사용해서 문제를 푸는 방법을 알았습니다. 
> `prefix(5)`는 앞에서 5번째까지의 string값을 가져오는 것이고,
> `suffix(5)`는 뒤에서 5번째까지의 string값을 가져오는 함수입니다.

```swift
import Foundation

func solution(_ intStrs:[String], _ k:Int, _ s:Int, _ l:Int) -> [Int] {
    let result = intStrs.map {Int($0.prefix(s+l).suffix(s))!}.filter{$0 > k}
    return result
}
```