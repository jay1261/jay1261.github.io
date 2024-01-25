---
title: Basic40 문자열 여러 번 뒤집기
author: jay
date: 2024-01-23
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
	## 문제: 문자열 여러 번 뒤집기
###### 문제 설명

문자열 `my_string`과 이차원 정수 배열 `queries`가 매개변수로 주어집니다. `queries`의 원소는 [s, e] 형태로, `my_string`의 인덱스 s부터 인덱스 e까지를 뒤집으라는 의미입니다. `my_string`에 `queries`의 명령을 순서대로 처리한 후의 문자열을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- `my_string`은 영소문자로만 이루어져 있습니다.
- 1 ≤ `my_string`의 길이 ≤ 1,000
- `queries`의 원소는 [s, e]의 형태로 0 ≤ s ≤ e < `my_string`의 길이를 만족합니다.
- 1 ≤ `queries`의 길이 ≤ 1,000

---

##### 입출력 예

|my_string|queries|result|
|---|---|---|
|"rermgorpsam"|[[2, 3], [0, 7], [5, 9], [6, 10]]|"programmers"|

---

##### 입출력 예 설명

- 예제 1번의 `my_string`은 "rermgorpsam"이고 주어진 `queries`를 순서대로 처리하면 다음과 같습니다.
    
    |queries|my_string|
    |---|---|
    ||"rermgorpsam"|
    |[2, 3]|"remrgorpsam"|
    |[0, 7]|"progrmersam"|
    |[5, 9]|"prograsremm"|
    |[6, 10]|"programmers"|
    
    따라서 "programmers"를 return 합니다.

---

## Solution

> 처음 풀이는 조금 복잡했습니다. 먼저 `my_string`을 배열로 만들고, `queries`에 `reduce(into: array)`를 사용해서 `arr.reversed()`를 써서 `arr`안의 요소들을 뒤집어 주는 방식을 사용했습니다.

```swift
import Foundation

func solution(_ my_string:String, _ queries:[[Int]]) -> String {
    var array = Array(my_string)
    let result = queries.reduce(into: array) { arr, q in
        let (s, e) = (q[0], q[1])
        let reversedArray = Array(arr[s...e].reversed())
        for i in s...e{
            arr[i] = reversedArray[i-s]
        }
        
    }
    return String(result)
}
```

> 원리는 동일하지만 .reverse() 함수를 알게되어 아래와 같이 코드를 조금 다듬었습니다.

```swift
func solution(_ my_string:String, _ queries:[[Int]]) -> String {
	var array = Array(my_string)
    let result = queries.reduce(into: array) { arr, q in
        arr[q[0]...q[1]].reverse()
    }
    return String(result)
}
```