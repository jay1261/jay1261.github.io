---
title: Basic69 n 보다 커질 때까지 더하기
author: jay
date: 2024-02-07
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: n 보다 커질 때까지 더하기

###### 문제 설명

정수 배열 `numbers`와 정수 `n`이 매개변수로 주어집니다. `numbers`의 원소를 앞에서부터 하나씩 더하다가 그 합이 `n`보다 커지는 순간 이때까지 더했던 원소들의 합을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `numbers`의 길이 ≤ 100
- 1 ≤ `numbers`의 원소 ≤ 100
- 0 ≤ n < `numbers`의 모든 원소의 합

---

##### 입출력 예

|numbers|n|result|
|---|---|---|
|[34, 5, 71, 29, 100, 34]|123|139|
|[58, 44, 27, 10, 100]|139|239|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `numbers`를 문제 설명대로 더해가는 과정을 나타내면 다음의 표와 같습니다.
    
    |i|numbers[i]|sum|
    |---|---|---|
    |||0|
    |0|34|34|
    |1|5|39|
    |2|71|110|
    |3|29|139|
    
    29를 더한 뒤에 sum 값은 139이고 `n` 값인 123보다 크므로 139를 return 합니다.
    
- 예제 2번의 `numbers`의 마지막 원소 전까지의 원소를 sum에 더하면 139입니다. 139는 `n` 값인 139보다 크지 않고 마지막 원소인 100을 더하면 139보다 커지므로 239를 return 합니다.

---

## Solution

> 주어진 조건에 맞춰서 while문을 통해 numbers의 값들을 더하다가 reuslt가 n보다 커지는 순간 break를 통해서 result를 반환하는 방식으로 문제를 풀었습니다.

```swift
import Foundation

func solution(_ numbers:[Int], _ n:Int) -> Int {
    var result = 0
    var index = 0
    while true {
	    if result > n {
            break
        }
        result += numbers[index]
        index += 1
    }
    return result
}
```

> 이를 짧게 reduce를 활용해서, 처음 주어진 $0의 값이 n보다 작으면 $0 + $1을 해줌으로써 값을 더해주고, $0 > n이 되면 $0을 더이상 더해주지 않는 방법으로도 문제를 풀어봤습니다.

```swift
    return numbers.reduce(0){$0 > n ? $0 : $0 + $1}
```