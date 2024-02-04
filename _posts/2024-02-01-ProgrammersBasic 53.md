---
title: Basic53 글자 지우기
author: jay
date: 2024-02-01
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 글자 지우기

###### 문제 설명

문자열 `my_string`과 정수 배열 `indices`가 주어질 때, `my_string`에서 `indices`의 원소에 해당하는 인덱스의 글자를 지우고 이어 붙인 문자열을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `indices`의 길이 < `my_string`의 길이 ≤ 100
- `my_string`은 영소문자로만 이루어져 있습니다
- 0 ≤ `indices`의 원소 < `my_string`의 길이
- `indices`의 원소는 모두 서로 다릅니다.

---

##### 입출력 예

|my_string|indices|result|
|---|---|---|
|"apporoograpemmemprs"|[1, 16, 6, 15, 0, 10, 11, 3]|"programmers"|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`의 인덱스가 잘 보이도록 표를 만들면 다음과 같습니다.
    
    |index|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|
    |---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
    |my_string|a|p|p|o|r|o|o|g|r|a|p|e|m|m|e|m|p|r|s|
    
    `indices`에 있는 인덱스의 글자들을 지우고 이어붙이면 "programmers"가 되므로 이를 return 합니다.

---

## Solution

> 처음에 아래 코드처럼 바로 remove(at:) 을 사용했는데, 이렇게 할 경우에는 중간에 있는 글자가 지워지면, 전체 길이가 짧아지고, 동시에 지워진 글자 뒤의 글자들의 index가 바뀌어서 제대로된 결과를 얻지 못했습니다.

```swift
func solution(_ my_string:String, _ indices:[Int]) -> String {
	var result = Array(my_string)
	result.map{result.remove(at: $0)}
}
```

> 따라서, 주어진 indices를 내림차순으로 정렬시켜서 글자를 맨 뒤에서부터 지워나가서 인덱스 변화에 영향을 받지 않도록 코드를 작성했습니다.

```swift
import Foundation

func solution(_ my_string:String, _ indices:[Int]) -> String {
    var result = Array(my_string)
    var sortedIndices = indices.sorted(by: >)
    
    sortedIndices.map{result.remove(at: $0)}
    
    return String(result)
} 
```