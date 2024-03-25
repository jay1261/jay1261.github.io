---
title: Basic51 문자 개수 세기
author: jay
date: 2024-01-26
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 문자 개수 세기

###### 문제 설명

알파벳 대소문자로만 이루어진 문자열 `my_string`이 주어질 때, `my_string`에서 'A'의 개수, `my_string`에서 'B'의 개수,..., `my_string`에서 'Z'의 개수, `my_string`에서 'a'의 개수, `my_string`에서 'b'의 개수,..., `my_string`에서 'z'의 개수를 순서대로 담은 길이 52의 정수 배열을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `my_string`의 길이 ≤ 1,000

---

##### 입출력 예

|my_string|result|
|---|---|
|"Programmers"|[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 2, 0, 1, 0, 0, 3, 1, 0, 0, 0, 0, 0, 0, 0]|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`에서 'P'가 1개, 'a'가 1개, 'e'가 1개, 'g'가 1개, 'm'이 2개, 'o'가 1개, 'r'가 3개, 's'가 1개 있으므로 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 2, 0, 1, 0, 0, 3, 1, 0, 0, 0, 0, 0, 0, 0]를 return 합니다.

---

## Solution

> `ascii코드`의 값을 이용해서 문제를 풀었습니다. 대문자 알파벳은 `65~90`까지이고, 소문자 알파벳은 `97~122`입니다.
> - 길이 52의 0이담긴 `result 배열`을 만듭니다. `0부터 25` 인덱스 까지는 대문자, `26부터 51`까지는 소문자의 인덱스입니다.
> - `my_string`의 각 문자들을 돌면서 ascii코드 값이 91 미만이라면 대문자, 이상이면 소문자라고 판멸합니다.
> - 대문자라면 65로 나눈 나머지를 구하고, 소문자라면 97로 나눈 나머지에 26을 더해서 각 알파벳의 인덱스를 찾습니다.
> - `result 배열`에 인덱스 자리에 1을 더해줍니다.

```swift
import Foundation

func solution(_ my_string:String) -> [Int] {
    var result = Array(repeating:0, count: 52)
    my_string.map{ Int($0.asciiValue!) < 91 ? Int($0.asciiValue!) % 65 : Int($0.asciiValue!) % 97 + 26}.map{result[$0] += 1}
    return result
}
```