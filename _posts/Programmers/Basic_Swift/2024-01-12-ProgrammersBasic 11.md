---
title: Basic11 문자열 섞기
author: jay
date: 2024-01-12
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 11. 문자열 섞기

###### 문제 설명

길이가 같은 두 문자열 `str1`과 `str2`가 주어집니다.

두 문자열의 각 문자가 앞에서부터 서로 번갈아가면서 한 번씩 등장하는 문자열을 만들어 return 하는 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `str1`의 길이 = `str2`의 길이 ≤ 10
    - `str1`과 `str2`는 알파벳 소문자로 이루어진 문자열입니다.

---

##### 입출력 예

|str1|str2|result|
|---|---|---|
|"aaaaa"|"bbbbb"|"ababababab"|

---

### Solution

> 이전 문제와 마찬가지로 Array로 변환한 후에 처리한 코드는 아래와 같습니다.

```swift
import Foundation

func solution(_ str1:String, _ str2:String) -> String {
    var result = [Character]()
    var str1Array = Array(str1)
    var str2Array = Array(str2)
    
    for i in 0..<str1.count {
        result.append(str1Array[i])
        result.append(str2Array[i])
    }
    
    return String(result)
}
```

> 다른 방법으로는, 두 개의 시퀀스를 이용해서 시퀀스 쌍을 만들 수 있는 zip을 이용해서 문제를 풀 수 있습니다.

```swift
func solution(_ str1:String, _ str2:String) -> String {
    var result = ""
    for (a,b) in zip(str1, str2){
        result.append(a)
        result.append(b)
    }
    return result
}
```