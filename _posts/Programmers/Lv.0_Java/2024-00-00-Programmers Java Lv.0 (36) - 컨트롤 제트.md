---
title: Java Lv.0 (36) - 컨트롤 제트
author: jay
date: 2024-05-30
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Algorithm
  - Programmers
source: https://programmers.co.kr/
---
## **컨트롤 제트**

<br />

---

<br/>

###### **문제 설명**

숫자와 "Z"가 공백으로 구분되어 담긴 문자열이 주어집니다. 문자열에 있는 숫자를 차례대로 더하려고 합니다. 이 때 "Z"가 나오면 바로 전에 더했던 숫자를 뺀다는 뜻입니다. 숫자와 "Z"로 이루어진 문자열 `s`가 주어질 때, 머쓱이가 구한 값을 return 하도록 solution 함수를 완성해보세요.

---

##### **제한사항**

- 1 ≤ `s`의 길이 ≤ 200
- -1,000 < `s`의 원소 중 숫자 < 1,000
- `s`는 숫자, "Z", 공백으로 이루어져 있습니다.
- `s`에 있는 숫자와 "Z"는 서로 공백으로 구분됩니다.
- 연속된 공백은 주어지지 않습니다.
- 0을 제외하고는 0으로 시작하는 숫자는 없습니다.
- `s`는 "Z"로 시작하지 않습니다.
- `s`의 시작과 끝에는 공백이 없습니다.
- "Z"가 연속해서 나오는 경우는 없습니다.

---

##### **입출력 예**

|s|result|
|---|---|
|"1 2 Z 3"|4|
|"10 20 30 40"|100|
|"10 Z 20 Z 1"|1|
|"10 Z 20 Z"|0|
|"-1 -2 -3 Z"|-3|

---

##### **입출력 예 설명**

입출력 예 #1

- 본문과 동일합니다.

입출력 예 #2

- 10 + 20 + 30 + 40 = 100을 return 합니다.

입출력 예 #3

- "10 Z 20 Z 1"에서 10 다음 Z, 20 다음 Z로 10, 20이 지워지고 1만 더하여 1을 return 합니다.

입출력 예 #4, #5

설명 생략


<br />

---

<br/>


## Solution

> 먼저 공백을 기준으로 `split`해서 숫자들을 담고, `answer`에 더하면서 동시에 그 값을 `previous` 변수에 담아둡니다. 이후 `Z`가 나오게 되면 `answer`에 이전 값을 빼주는 형식으로 문제를 풀었습니다.

```java
class Solution {
    public int solution(String s) {
        int answer = 0;
        String[] splitted = s.split(" ");
        
        int previous = 0;
        for (String str: splitted){
            if (str.equals("Z")){
                answer -= previous;
            }
            else {
                answer += Integer.valueOf(str);
                previous = Integer.valueOf(str);
            }
            
        }
        
        return answer;
    }
}
```


> 이후 다른 답안을 찾아보니 이를 Stack을 이용해서 푼 방법이 있어서 다시 풀어봤습니다. 공백을 기준으로 split된 문자들을 하나씩 돌면서 Stack에 push하고, Z가 나온다면 pop을해서 기존에 있던 값을 삭제합니다. 이후 Stack에 남아있는 값들의 합을 구하는 방법입니다. 


```java
import java.util.*;
class Solution {
    public int solution(String s) {
        int answer = 0;
        Stack<Integer> stack = new Stack<>();
        
        for(String str: s.split(" ")){
            if (str.equals("Z")){
                stack.pop();
            } else {
                stack.push(Integer.valueOf(str));
            }
        }
        
        for(int i: stack) {
            answer += i;
        }
        
        return answer;
    }
}
```