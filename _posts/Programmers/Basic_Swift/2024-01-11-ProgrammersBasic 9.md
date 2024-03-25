---
title: Basic9 홀짝 구분하기
author: jay
date: 2024-01-12
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 9. 홀짝 구분하기

### 문제 설명

자연수 `n`이 입력으로 주어졌을 때 만약 `n`이 짝수이면 "`n` is even"을, 홀수이면 "`n` is odd"를 출력하는 코드를 작성해 보세요.

---

### 제한사항

- 1 ≤ `n` ≤ 1,000

---

### 입출력 예

입력 #1

```
100
```

출력 #1

```
100 is even
```

입력 #2

```
1
```

출력 #2

```
1 is odd
```

---

### Solution

```swift
import Foundation

let a = Int(readLine()!)!

if a % 2 == 0 {
    print("\(a) is even")
} else {
    print("\(a) is odd")
}
```



