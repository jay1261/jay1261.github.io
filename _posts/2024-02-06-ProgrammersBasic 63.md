---
title: Basic63 왼쪽 오른쪽
author: jay
date: 2024-02-06
categories:
  - Algorithm
  - Programmers
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 왼쪽 오른쪽
###### 문제 설명

문자열 리스트 `str_list`에는 "u", "d", "l", "r" 네 개의 문자열이 여러 개 저장되어 있습니다. `str_list`에서 "l"과 "r" 중 먼저 나오는 문자열이 "l"이라면 해당 문자열을 기준으로 왼쪽에 있는 문자열들을 순서대로 담은 리스트를, 먼저 나오는 문자열이 "r"이라면 해당 문자열을 기준으로 오른쪽에 있는 문자열들을 순서대로 담은 리스트를 return하도록 solution 함수를 완성해주세요. "l"이나 "r"이 없다면 빈 리스트를 return합니다.

---

##### 제한사항

- 1 ≤ `str_list`의 길이 ≤ 20
- `str_list`는 "u", "d", "l", "r" 네 개의 문자열로 이루어져 있습니다.

---

##### 입출력 예

|str_list|result|
|---|---|
|["u", "u", "l", "r"]|["u", "u"]|
|["l"]|[]|

---

##### 입출력 예 설명

입출력 예 #1

- "r"보다 "l"이 먼저 나왔기 때문에 "l"의 왼쪽에 있는 문자열들을 담은 리스트인 ["u", "u"]를 return합니다.

입출력 예 #2

- "l"의 왼쪽에 문자열이 없기 때문에 빈 리스트를 return합니다.

---

## Solution

> `왼쪽, 오른쪽`의 기준이 될 값을 찾기 위해서 `filter`를 사용해 값이 `r, l` 인 요소들을 걸러낸 후 그 중 `첫 번째` 값을 `piviot` 변수에 저장했습니다. `if let`을 이용해서 만약 값이 없을 경우는 `빈 리스트를 리턴`하도록 했습니다.
 
```swift
if let pivot = str_list.enumerated().filter{$0.element == "r" || $0.element == "l"}.first{

}
else {
	  return []
}
```

> 이후에는 `pivot`의 값이 `l` 인지 `r` 인지에 따라서 문제의 요구사항 대로 리스트를 만들어 return해주는 코드를 작성했습니다.

```swift
import Foundation

func solution(_ str_list:[String]) -> [String] {
    if let pivot = str_list.enumerated().filter{$0.element == "r" || $0.element == "l"}.first {
        return pivot.element == "l" ? str_list[0..<pivot.offset].map{$0} : str_list[(pivot.offset+1)...].map{$0}
    }
    else {
        return []
    }
}
```