---
title: Basic4~5
author: jay
date: 2024-01-10
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 4. 대소문자 바꿔서 출력하기

### 문제 설명

영어 알파벳으로 이루어진 문자열 `str`이 주어집니다. 각 알파벳을 대문자는 소문자로 소문자는 대문자로 변환해서 출력하는 코드를 작성해 보세요.

### 제한사항

- 1 ≤ `str`의 길이 ≤ 20
    - `str`은 알파벳으로 이루어진 문자열입니다.

### 입출력 예

입력

```
aBcDeFg
```

출력

```
AbCdEfG
```

### Solution
```swift
import Foundation

let s1 = readLine()!

let result = s1.map {$0.isLowercase ? $0.uppercased() : $0.lowercased()}.joined()

print(result)
```


---

## 5. 특수문자 출력하기
### 문제 설명

다음과 같이 출력하도록 코드를 작성해 주세요.

출력 예시

```
!@#$%^&*(\'"<>?:;
```
### 설명
- 양 끝에 #을 붙여주어야 합니다.

### Solution

```swift
import Foundation

print(#"!@#$%^&*(\'"<>?:;"#)
```
