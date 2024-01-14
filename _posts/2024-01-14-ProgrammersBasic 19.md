---
title: Basic19 조건 문자열
author: jay
date: 2024-01-14
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 조건 문자열

###### 문제 설명

문자열에 따라 다음과 같이 두 수의 크기를 비교하려고 합니다. 

- 두 수가 `n`과 `m`이라면
    - ">", "=" : `n` >= `m`
    - "<", "=" : `n` <= `m`
    - ">", "!" : `n` > `m`
    - "<", "!" : `n` < `m`

두 문자열 `ineq`와 `eq`가 주어집니다. `ineq`는 "<"와 ">"중 하나고, `eq`는 "="와 "!"중 하나입니다. 그리고 두 정수 `n`과 `m`이 주어질 때, `n`과 `m`이 `ineq`와 `eq`의 조건에 맞으면 1을 아니면 0을 return하도록 solution 함수를 완성해주세요.

---

##### 제한 사항

- 1 ≤ `n`, `m` ≤ 100

---

##### 입출력 예

|ineq|eq|n|m|result|
|---|---|---|---|---|
|"<"|"="|20|50|1|
|">"|"!"|41|78|0|

---

##### 입출력 예 설명

입출력 예 #1

- 20 <= 50은 참이기 때문에 1을 return합니다.

입출력 예 #2

- 41 > 78은 거짓이기 때문에 0을 return합니다.

---

## Solution 

> `switch case`문을 사용하여 문제를 해결했습니다.

```swift
import Foundation

func solution(_ ineq:String, _ eq:String, _ n:Int, _ m:Int) -> Int {
    switch (ineq, eq){
        case (">", "=") :
            return n >= m ? 1 : 0
        case ("<", "=") :
            return n <= m ? 1 : 0
        case (">", "!") :
            return n > m ? 1 : 0
        case ("<", "!") :
            return n < m ? 1 : 0
        default :
            return n == m ? 1 : 0
    }
}
```