---
title: Basic18 홀짝에 따라 다른 값 반환하기
author: jay
date: 2024-01-14
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 홀짝에 따라 다른 값 반환하기
###### 문제 설명

양의 정수 `n`이 매개변수로 주어질 때, `n`이 홀수라면 `n` 이하의 홀수인 모든 양의 정수의 합을 return 하고 `n`이 짝수라면 `n` 이하의 짝수인 모든 양의 정수의 제곱의 합을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 100

---

##### 입출력 예

|n|result|
|---|---|
|7|16|
|10|220|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `n`은 7로 홀수입니다. 7 이하의 모든 양의 홀수는 1, 3, 5, 7이고 이들의 합인 1 + 3 + 5 + 7 = 16을 return 합니다.

입출력 예 #2

- 예제 2번의 `n`은 10으로 짝수입니다. 10 이하의 모든 양의 짝수는 2, 4, 6, 8, 10이고 이들의 제곱의 합인 22 + 42 + 62 + 82 + 102 = 4 + 16 + 36 + 64 + 100 = 220을 return 합니다.

---

## Solution

> 처음에 적당한 문법이 떠오르지 않아서 `for`문, `%`연산자를 통해 문제를 해결했습니다. 

```swift
import Foundation

func solution(_ n:Int) -> Int {
    var result = 0
    
    if n % 2 == 0 {
        for i in 0...n {
            if i % 2 == 0 {
                result += (i*i)
            }
        }
    } else {
        for i in 0...n {
            if i % 2 != 0 {
                result += i
            }
        }
    }
    return result
}
```

> 이후 stride라는 함수를 알게되어서 적용시켜 보았습니다. stride(from: x, through: y, by: z)는 x부터 y까지(through는 y포함 to는 y포함하지 않음) z의 보폭으로 나아간다고 생각하면 이해하기 좋습니다.

```swift
func solution(_ n:Int) -> Int {
    if n % 2 != 0 {
        return stride(from: 1, through: n, by: 2).reduce(0){$0 + $1}
    } else {
        return stride(from: 2, through: n, by: 2).reduce(0){$0 + $1 * $1}
    }
}
```