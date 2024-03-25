---
title: Basic6 덧셈식 출력하기
author: jay
date: 2024-01-10
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제 설명

두 정수 `a`, `b`가 주어질 때 다음과 같은 형태의 계산식을 출력하는 코드를 작성해 보세요.

```
a + b = c
```

---

### 제한사항

- 1 ≤ `a`, `b` ≤ 100

---

### 입출력 예

입력 

```
4 5
```

출력

```
4 + 5 = 9
```

---

### Solution

```swift
import Foundation

let n = readLine()!.components(separatedBy: [" "]).map { Int($0)! }
let (a, b) = (n[0], n[1])

print("\(a) + \(b) = \(a+b)")

```