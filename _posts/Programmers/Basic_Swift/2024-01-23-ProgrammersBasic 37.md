---
title: Basic37 주사위 게임 3
author: jay
date: 2024-01-23
categories:
  - Programmers
  - Basic_Swift
tags:
  - Algorithm
  - SwiftAlgorithm
---
## 문제: 주사위 게임 3

###### 문제 설명

1부터 6까지 숫자가 적힌 주사위가 네 개 있습니다. 네 주사위를 굴렸을 때 나온 숫자에 따라 다음과 같은 점수를 얻습니다.

- 네 주사위에서 나온 숫자가 모두 p로 같다면 1111 × p점을 얻습니다.
- 세 주사위에서 나온 숫자가 p로 같고 나머지 다른 주사위에서 나온 숫자가 q(p ≠ q)라면 (10 × p + q)2 점을 얻습니다.
- 주사위가 두 개씩 같은 값이 나오고, 나온 숫자를 각각 p, q(p ≠ q)라고 한다면 (p + q) × |p - q|점을 얻습니다.
- 어느 두 주사위에서 나온 숫자가 p로 같고 나머지 두 주사위에서 나온 숫자가 각각 p와 다른 q, r(q ≠ r)이라면 q × r점을 얻습니다.
- 네 주사위에 적힌 숫자가 모두 다르다면 나온 숫자 중 가장 작은 숫자 만큼의 점수를 얻습니다.

네 주사위를 굴렸을 때 나온 숫자가 정수 매개변수 `a`, `b`, `c`, `d`로 주어질 때, 얻는 점수를 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- `a`, `b`, `c`, `d`는 1 이상 6 이하의 정수입니다.

---

##### 입출력 예

|a|b|c|d|result|
|---|---|---|---|---|
|2|2|2|2|2222|
|4|1|4|4|1681|
|6|3|3|6|27|
|2|5|2|6|30|
|6|4|2|5|2|

---

##### 입출력 예 설명

입출력 예 #1

- 예제 1번에서 네 주사위 숫자가 모두 2로 같으므로 1111 × 2 = 2222점을 얻습니다. 따라서 2222를 return 합니다.

입출력 예 #2

- 예제 2번에서 세 주사위에서 나온 숫자가 4로 같고 나머지 다른 주사위에서 나온 숫자가 1이므로 (10 × 4 + 1)2 = 412 = 1681점을 얻습니다. 따라서 1681을 return 합니다.

입출력 예 #3

- 예제 3번에서 `a`, `d`는 6으로, `b`, `c`는 3으로 각각 같으므로 (6 + 3) × |6 - 3| = 9 × 3 = 27점을 얻습니다. 따라서 27을 return 합니다.

입출력 예 #4

- 예제 4번에서 두 주사위에서 2가 나오고 나머지 다른 두 주사위에서 각각 5, 6이 나왔으므로 5 × 6 = 30점을 얻습니다. 따라서 30을 return 합니다.

입출력 예 #5

- 예제 5번에서 네 주사위 숫자가 모두 다르고 나온 숫자 중 가장 작은 숫자가 2이므로 2점을 얻습니다. 따라서 2를 return 합니다.

---

## Solution

> `Array`를 만들어 정렬시키고, `Set`을 만들어줍니다. `Set.count`를 통해서 중복된 숫자의 경우의 수를 나눌 수 있습니다. 
> `case 2`의 경우 `a,b,c,d`중 세개의 숫자가 같은 경우와, 두개씩 같은 경우 두가지가 있습니다. 여기서 세개의 숫자가 같은 경우는 배열을 정렬시켰기 때문에 `[2,2,2,5] or [4,6,6,6,]`처럼 배열의 0번째와 1번째 값이 다른경우 or 2번째와 3번째가 다른경우로 나뉘어집니다. 이를 제외한 나머지의 경우는 숫자가 두개씩 같은경우가 됩니다.
> `case 3`은 두개의 숫자가 같고 나머지는 전부 다른 경우입니다. `filter`를 사용해서 두개의 값이 같은 원소를 찾아내고(p), 한번 더 필터를 사용해서 `p`를 제외한 나머지 두개의 요소를 찾아낸 후에, 조건대로 곱해서 return합니다.

```swift
import Foundation

func solution(_ a:Int, _ b:Int, _ c:Int, _ d:Int) -> Int {
    let array = [a,b,c,d].sorted()
    let s = Set(array)
    switch s.count {
        case 1 :
            return 1111 * a
        case 2 :
            if array[0] != array[1] {
                return (10*array[1]+array[0]) * (10*array[1]+array[0])
            }
            else if array[2] != array[3] {
                return (10*array[2]+array[3]) * (10*array[2]+array[3])
            }
            else {
                return (array[1] + array[2]) * abs(array[1] - array[2])
            }
        case 3 :
            let tmp = array.enumerated().filter{index, value in
                let nextIndex = index + 1
                return nextIndex < array.count && array[nextIndex] == value
            }
            let p = tmp.map{$0.element}[0]
            let last = s.filter{ $0 != p}
            
            return last.reduce(1){$0*$1}
        case 4 :
            return s.min() ?? 0
        default :
            return -1
    }
}


```