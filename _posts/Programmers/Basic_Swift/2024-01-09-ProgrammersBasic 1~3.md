---
title: Basic1~3
author: jay
date: 2024-01-09
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 1. 문자열 출력하기

### 문제설명

	문자열 `str`이 주어질 때, `str`을 출력하는 코드를 작성해 보세요.
### 제한사항

- 1 ≤ `str`의 길이 ≤ 1,000,000
- `str`에는 공백이 없으며, 첫째 줄에 한 줄로만 주어집니다.

### 입출력 예시

입력

```
HelloWorld!
```

출력

```
HelloWorld!
```

**Solution**

```swift
import Foundation

let s1 = readLine()!

print(s1)
```

---

## 2. a와 b 출력하기

### 문제 설명

정수 `a`와 `b`가 주어집니다. 각 수를 입력받아 입출력 예와 같은 형식으로 출력하는 코드를 작성해 보세요.

### 제한사항

- -100,000 ≤ `a`, `b` ≤ 100,000

### 입출력 예

입력

```
4 5
```

출력

```
a = 4
b = 5
```

**Solution**

```swift
import Foundation

let n = readLine()!.components(separatedBy: [" "]).map { Int($0)! }
let (a, b) = (n[0], n[1])

print("a = \(a) \nb = \(b)")
```

---

## 3. 문자열 반복해서 출력하기

### 문제 설명

문자열 `str`과 정수 `n`이 주어집니다.  
`str`이 `n`번 반복된 문자열을 만들어 출력하는 코드를 작성해 보세요.

### 제한사항

- 1 ≤ `str`의 길이 ≤ 10
- 1 ≤ `n` ≤ 5

### 입출력 예

입력

```
string 5
```

출력

```
stringstringstringstringstring
```

**Solution**

일반적으로 반복문을 사용해서 해결하는 방법과, swift의 String에서 지원하는 repeating을 사용하는 방법 두가지가 있습니다.
- 반복문

```swift
import Foundation

let inp = readLine()!.components(separatedBy: [" "]).map { $0 }
let (s1, a) = (inp[0], Int(inp[1])!)

var result = ""
for _ in 0..<a {
    result += s1
}
print(result)
```
- repeating

```swift
import Foundation

let inp = readLine()!.components(separatedBy: [" "]).map { $0 }
let (s1, a) = (inp[0], Int(inp[1])!)

print(String(repeating: s1, count: a))
```