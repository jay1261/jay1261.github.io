---
title: Programmers Java Lv.0 (13) - 직각삼각형 출력하기
author: jay
date: 2024-03-30
categories:
  - Programmers
  - Lv.0_Java
tags:
  - Java
  - Java문법
source: https://programmers.co.kr/
---
## **직각삼각형 출력하기**

<br />

---

<br/>

###### **문제 설명**

"*"의 높이와 너비를 1이라고 했을 때, "*"을 이용해 직각 이등변 삼각형을 그리려고합니다. 정수 n 이 주어지면 높이와 너비가 n 인 직각 이등변 삼각형을 출력하도록 코드를 작성해보세요.

---

##### **제한사항**

- 1 ≤ `n` ≤ 10

---

##### **입출력 예**

입력 #1

```
3
```

출력 #1

```
*
**
***
```

##### **입출력 예 설명**

입출력 예 #1

- n이 3이므로 첫째 줄에 * 1개, 둘째 줄에 * 2개, 셋째 줄에 * 3개를 출력합니다.


<br />

---

<br/>

## Solution

> 이중 반복문을 통해서 `i는 1~n까지`, `j는 1~i까지` 반복하도록 코드를 작성했습니다.

```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        for (int i = 1 ; i <= n; i++){
            for (int j = 1; j<=i; j++){
                System.out.print("*");
            }
            System.out.println();
        }
        
    }
}
```

<br/>


> 다른 사람의 풀이 방식을 보다가, String에 `repeat()`함수를 알게되어서 유용하게 사용할 수 있을 것 같습니다.

```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        for (int i = 1 ; i <= n; i++){
			System.out.println("*".repeat(i)); //repeat()
        }
    }
}
```