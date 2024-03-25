---
title: Basic13 문자열 곱하기
author: jay
date: 2024-01-13
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 13. 문자열 곱하기

###### 문제 설명

문자열 `my_string`과 정수 `k`가 주어질 때, `my_string`을 `k`번 반복한 문자열을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `my_string`의 길이 ≤ 100
- `my_string`은 영소문자로만 이루어져 있습니다.
- 1 ≤ `k` ≤ 100

---

##### 입출력 예

|my_string|k|result|
|---|---|---|
|"string"|3|"stringstringstring"|
|"love"|10|"lovelovelovelovelovelovelovelovelovelove"|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`은 "string"이고 이를 3번 반복한 문자열은 "stringstringstring"이므로 이를 return 합니다.

입출력 예 #2

- 예제 2번의 `my_string`은 "love"이고 이를 10번 반복한 문자열은 "lovelovelovelovelovelovelovelovelovelove"이므로 이를 return 합니다.

---

### Solution 

>간단하게 반복문으로도 구현할 수 있겠지만 String의 init 중 (repeating:count:)를 사용해서 구현할 수 있습니다.

```swift 
import Foundation

func solution(_ my_string:String, _ k:Int) -> String {
    return String(repeating: my_string, count: k)
}
```
