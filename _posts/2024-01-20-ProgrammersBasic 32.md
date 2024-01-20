---
title: Basic32 배열 만들기 2
author: jay
date: 2024-01-20
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 배열 만들기 2

###### 문제 설명

정수 `l`과 `r`이 주어졌을 때, `l` 이상 `r`이하의 정수 중에서 숫자 "0"과 "5"로만 이루어진 모든 정수를 오름차순으로 저장한 배열을 return 하는 solution 함수를 완성해 주세요.

만약 그러한 정수가 없다면, -1이 담긴 배열을 return 합니다.

---

##### 제한사항

- 1 ≤ `l` ≤ `r` ≤ 1,000,000

---

##### 입출력 예

|l|r|result|
|---|---|---|
|5|555|[5, 50, 55, 500, 505, 550, 555]|
|10|20|[-1]|

---

##### 입출력 예 설명

입출력 예 #1

- 5 이상 555 이하의 0과 5로만 이루어진 정수는 작은 수부터 5, 50, 55, 500, 505, 550, 555가 있습니다. 따라서 [5, 50, 55, 500, 505, 550, 555]를 return 합니다.

입출력 예 #2

- 10 이상 20 이하이면서 0과 5로만 이루어진 정수는 없습니다. 따라서 [-1]을 return 합니다.

---

## Solution

> String으로 변환한 l부터 r까지 숫자를 하나씩 돌면서 `"0","5"`를 제외한 숫자가 포함되어 있지 않을 경우에만 `result`배열에 추가하는 방식으로 문제를 풀었습니다. 그러나 처음에 테스트케이스 하나에서 시간초과라는 결과가 나왔습니다.

```swift
import Foundation

func solution(_ l:Int, _ r:Int) -> [Int] {
    let arr = ["1","2","3","4","6","7","8","9"]
    var result = [Int]()
    
    for i in l...r {
        let iString = String(i)
		if arr.filter{iString.contains($0)}.count == 0 {
			result.append(i)
		}
    }
    
    return result.isEmpty ? [-1] : result
}
```

> 그래서 `if i%5 == 0 `를 추가해 줌으로써 i가 5의 배수일 때만 filter를 실행시키도록 하여, 검사 수를 줄여서 시간초과를 해결했습니다.

```swift
import Foundation

func solution(_ l:Int, _ r:Int) -> [Int] {
    let arr = ["1","2","3","4","6","7","8","9"]
    var result = [Int]()
    
    for i in l...r {
        let iString = String(i)
        if i%5 == 0 {
            if arr.filter{iString.contains($0)}.count == 0 {
                result.append(i)
            }
        }
    }
    
    return result.isEmpty ? [-1] : result
}
```

---

> 아래 코드는 다른사람이 작성한 효율적인 코드입니다. 먼저, 처음 문제를 풀 때 `for`문이 아니라 `l...r`을 이용해 문제를 풀려고 접근했었는데, `[l...r]`이 코드를 작성하는 실수를 했습니다. `[l...r]`은 `(l...r)`과 다르게 ClosedRange로 map을 사용했을때 오류가 발생했습니다. 
> 
> 또한 Set을 사용할 생각은 하지 못했고, isSubset도 알지 못했는데, 이부분을 예시를 들어 해석하자면 `"505"`를 Set으로 변형시켜서 `["5","0"]`으로 변형하고, `isSubset(of:["5","0"])`는 앞의 `"505"`의 Set이 `(of: )`의 Set을 Subset으로 갖는지를 판별해주는 함수입니다.

```swift

func solution(_ l:Int, _ r:Int) -> [Int] {
    let result = (l...r).map{$0}.filter{Set(String($0)).isSubset(of:["5","0"])}
    return result.isEmpty ? [-1] : result
}
```
