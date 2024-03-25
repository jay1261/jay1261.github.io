---
title: Basic60 배열 조각하기
author: jay
date: 2024-02-05
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 배열 조각하기

###### 문제 설명

정수 배열 `arr`와 `query`가 주어집니다.

`query`를 순회하면서 다음 작업을 반복합니다.

- 짝수 인덱스에서는 `arr`에서 `query[i]`번 인덱스를 제외하고 배열의 `query[i]`번 인덱스 뒷부분을 잘라서 버립니다.
- 홀수 인덱스에서는 `arr`에서 `query[i]`번 인덱스는 제외하고 배열의 `query[i]`번 인덱스 앞부분을 잘라서 버립니다.

위 작업을 마친 후 남은 `arr`의 부분 배열을 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 5 ≤ `arr`의 길이 ≤ 100,000
    - 0 ≤ `arr`의 원소 ≤ 100
- 1 ≤ `query`의 길이 < min(50, `arr`의 길이 / 2)
    - `query`의 각 원소는 0보다 크거나 같고 남아있는 `arr`의 길이 보다 작습니다.

---

##### 입출력 예

|arr|query|result|
|---|---|---|
|[0, 1, 2, 3, 4, 5]|[4, 1, 2]|[1, 2, 3]|

---

##### 입출력 예 설명

입출력 예 #1

- 이번에 매번 처리할 `query`의 값과 처리 전후의 `arr`의 상태를 표로 나타내면 다음과 같습니다.

|query의 값|query 처리 전|query 처리 후|비고|
|---|---|---|---|
|4|[0, 1, 2, 3, 4, 5]|[0, 1, 2, 3, 4]|0번 인덱스의 쿼리이므로 뒷부분을 자른다.|
|1|[0, 1, 2, 3, 4]|[1, 2, 3, 4]|1번 인덱스의 쿼리이므로 앞부분을 자른다.|
|2|[1, 2, 3, 4]|[1, 2, 3]|2번 인덱스의 쿼리이므로 뒷부분을 자른다.|

- 따라서 [1, 2, 3]을 return 합니다.

---

## Solution

> `reduce(into:)`를 이용해서 먼저 `arr`을 초기값으로 넣어주었고, `query`의 요소가 짝수라면 `[0...q]`로 slice를 해주고 홀수라면 `[q...]`를 적용시켜주었습니다. 

```swift
import Foundation

func solution(_ arr:[Int], _ query:[Int]) -> [Int] {
    var index = 0
    return query.reduce(into: arr) { result, q in
        index % 2 == 0 ? result = result[0...q].map{$0} : result = result[q...].map{$0}
        index += 1
    }
}
```