---
title: Basic27 수 조작하기 1
author: jay
date: 2024-01-16
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 수 조작하기 1

###### 문제 설명

정수 `n`과 문자열 `control`이 주어집니다. `control`은 "w", "a", "s", "d"의 4개의 문자로 이루어져 있으며, `control`의 앞에서부터 순서대로 문자에 따라 `n`의 값을 바꿉니다.

- "w" : `n`이 1 커집니다.
- "s" : `n`이 1 작아집니다.
- "d" : `n`이 10 커집니다.
- "a" : `n`이 10 작아집니다.

위 규칙에 따라 `n`을 바꿨을 때 가장 마지막에 나오는 `n`의 값을 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- -100,000 ≤ `n` ≤ 100,000
- 1 ≤ `control`의 길이 ≤ 100,000
    - `control`은 알파벳 소문자 "w", "a", "s", "d"로 이루어진 문자열입니다.

---

##### 입출력 예

|n|control|result|
|---|---|---|
|0|"wsdawsdassw"|-1|

---

##### 입출력 예 설명

입출력 예 #1

- 수 `n`은 `control`에 따라 다음과 같은 순서로 변하게 됩니다.
- 0 → 1 → 0 → 10 → 0 → 1 → 0 → 10 → 0 → -1 → -2 → -1
- 따라서 -1을 return 합니다.

---

## Solution

>switch case를 사용해서 문제를 풀었습니다.

```swift
import Foundation

func solution(_ n:Int, _ control:String) -> Int {
    var result = n
    let controllArray = Array(control)
    
    for sign in controllArray {
        switch sign {
            case "w": 
                result += 1
                break
            case "s": 
                result -= 1
                break
            case "d": 
                result += 10
                break
            case "a": 
                result -= 10
                break
            default: 
                break
        }
    }
    
    return result
}
```