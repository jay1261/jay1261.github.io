---
title: Basic10 문자열 겹쳐쓰기
author: jay
date: 2024-01-12
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 10. 문자열 겹쳐쓰기

### 문제 설명

문자열 `my_string`, `overwrite_string`과 정수 `s`가 주어집니다. 문자열 `my_string`의 인덱스 `s`부터 `overwrite_string`의 길이만큼을 문자열 `overwrite_string`으로 바꾼 문자열을 return 하는 solution 함수를 작성해 주세요.

---

### 제한사항

- `my_string`와 `overwrite_string`은 숫자와 알파벳으로 이루어져 있습니다.
- 1 ≤ `overwrite_string`의 길이 ≤ `my_string`의 길이 ≤ 1,000
- 0 ≤ `s` ≤ `my_string`의 길이 - `overwrite_string`의 길이

---

### 입출력 예

|my_string|overwrite_string|s|result|
|---|---|---|---|
|"He11oWor1d"|"lloWorl"|2|"HelloWorld"|
|"Program29b8UYP"|"merS123"|7|"ProgrammerS123"|

---

### 입출력 예 설명

입출력 예 #1

- 예제 1번의 `my_string`에서 인덱스 2부터 `overwrite_string`의 길이만큼에 해당하는 부분은 "11oWor1"이고 이를 "lloWorl"로 바꾼 "HelloWorld"를 return 합니다.

입출력 예 #2

- 예제 2번의 `my_string`에서 인덱스 7부터 `overwrite_string`의 길이만큼에 해당하는 부분은 "29b8UYP"이고 이를 "merS123"로 바꾼 "ProgrammerS123"를 return 합니다.

---

### Solution

> swift에서는 인덱스를 사용해서 String의 각 요소에 접근하는 방법이 안됩니다. (my_string[i] - error) 그래서 String을 Array로 변환하고, 필요한 작업을 처리한 후에 다시 String으로 변환해서 반환해주는 코드를 작성했습니다.

```swift
import Foundation

func solution(_ my_string:String, _ overwrite_string:String, _ s:Int) -> String {
    var my_array = Array(my_string)
    var overwrite_array = Array(overwrite_string)

    for i in s..<overwrite_array.count + s {
        my_array[i] = overwrite_array[i-s]
    }

    return String(my_array)
}
```

> 또한 Array에는 replaceSubrange라는 내부함수가 있어서 이를 사용하는 방법도 있습니다.

```
my_array.replaceSubrange(s...(overwrite_array.count+s-1), with: overwrite_string)
```