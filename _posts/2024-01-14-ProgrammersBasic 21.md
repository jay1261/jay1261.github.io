---
title: Basic21 코드 처리하기
author: jay
date: 2024-01-14
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 코드 처리하기
###### 문제 설명

문자열 `code`가 주어집니다.  
`code`를 앞에서부터 읽으면서 만약 문자가 "1"이면 `mode`를 바꿉니다. `mode`에 따라 `code`를 읽어가면서 문자열 `ret`을 만들어냅니다.

`mode`는 0과 1이 있으며, `idx`를 0 부터 `code의 길이 - 1` 까지 1씩 키워나가면서 `code[idx]`의 값에 따라 다음과 같이 행동합니다.

- `mode`가 0일 때 
    - `code[idx]`가 "1"이 아니면 `idx`가 짝수일 때만 `ret`의 맨 뒤에 `code[idx]`를 추가합니다.
    - `code[idx]`가 "1"이면 `mode`를 0에서 1로 바꿉니다.
- `mode`가 1일 때
    - `code[idx]`가 "1"이 아니면 `idx`가 홀수일 때만 `ret`의 맨 뒤에 `code[idx]`를 추가합니다.
    - `code[idx]`가 "1"이면 `mode`를 1에서 0으로 바꿉니다.

문자열 `code`를 통해 만들어진 문자열 `ret`를 return 하는 solution 함수를 완성해 주세요.

단, 시작할 때 `mode`는 0이며, return 하려는 `ret`가 만약 빈 문자열이라면 대신 "EMPTY"를 return 합니다.

---

##### 제한사항

- 1 ≤ `code`의 길이 ≤ 100,000
    - `code`는 알파벳 소문자 또는 "1"로 이루어진 문자열입니다.

---

##### 입출력 예

|code|result|
|---|---|
|"abc1abc1abc"|"acbac"|

---

##### 입출력 예 설명

입출력 예 #1

- `code`의 각 인덱스 `i`에 따라 다음과 같이 `mode`와 `ret`가 변합니다.

|i|code[i]|mode|ret|
|---|---|---|---|
|0|"a"|0|"a"|
|1|"b"|0|"a"|
|2|"c"|0|"ac"|
|3|"1"|1|"ac"|
|4|"a"|1|"ac"|
|5|"b"|1|"acb"|
|6|"c"|1|"acb"|
|7|"1"|0|"acb"|
|8|"a"|0|"acba"|
|9|"b"|0|"acba"|
|10|"c"|0|"acbac"|

따라서 "acbac"를 return 합니다.

---

## Solution

> 문제의 조건에 따라 `for`문과 `if`문을 이용해 풀은 코드는 아래와 같습니다.

```swift
import Foundation

func solution(_ code:String) -> String {
    var mode = 0
    var codeArray = Array(code)
    var ret = [Character]()
    for i in 0..<code.count {
        if mode == 0 {
            if codeArray[i] == "1" {
                mode = 1
                continue;
            }
            if i % 2 == 0 {
                ret.append(codeArray[i])
            }
        } 
        else {
            if codeArray[i] == "1" {
                mode = 0
                continue;
            }
            
            if i % 2 != 0 {
                ret.append(codeArray[i])
            }
        }
    
    }
    return String(ret) == "" ? "EMPTY" : String(ret)
}
```

> 이후 다른 풀이법으로, enumerated()함수를 사용해 코드를 줄일 수 있었습니다.

```swift
func solution(_ code:String) -> String {
	var mode = false
	var ret = ""
	code.enumerated().forEach{ index, char in
		if char == "1"{mode.toggle()}
		else {
			if !mode && index % 2 == 0 {
				ret += String(char)
			}
			else if mode && index % 2 != 0 {
				ret += String(char)
			}
		}
    }    
    return ret.isEmpty ? "EMPTY" : ret
}
```