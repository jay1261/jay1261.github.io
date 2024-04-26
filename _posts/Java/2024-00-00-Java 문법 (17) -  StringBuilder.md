---
title: Java 문법 (17) - StringBuilder
author: jay
date: 2024-04-26
categories:
  - Java
  - Java_Mid1
tags:
  - Java
source: https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-1
---

## **String의 단점**

지난 포스트 [String](https://jay1261.github.io/posts/Java-%EB%AC%B8%EB%B2%95-(16)-String/)에서 String은 불변이라고 배웠다. 불변인 String의 단점은 문자를 더하거나 변경할 때 마다 계속해서 새로운 객체를 생성해야한다는 점이다. 반복문 안에서 문자를 계속해서 더하거나 변경하는 상황이라면, 많은 String 객체가 생겼다가 GC에 의해 사라짐을 반복하게되고, 이는 cpu, 메모리 낭비로 직결된다.

아래 예제코드와 그림은 String 문자열을 서로 더할 때 일어나는 과정이다. "Hello Java World"를 만드는 과정에 객체가 계속 만들어지고, 쓰임도 없이 버려진다.

```java
String str = "Hello";
str = str + " Java";
str = str + " World";
```
<img align="center" src="https://ifh.cc/g/S3vD9b.png">
<br/>

---
<br/>

## **StringBuilder**

이 문제는 String이 가변이라면 간단하게 해결될 문제다. 자바는 이를 해결하기 위해 `StringBuilder`라는 `가변 String`을 제공한다. 가변은 내부의 값을 바로 변경하면 되기 때문에 새로운 객체를 생성할 필요가 없어서 성능과 메모리 사용면에서 효율적이다. 

`StringBuilder` 내부를 보면 `final`이 아닌 변경할 수 있는 `char[]`를 가지고 있다.

```java
public final class StringBuilder { 
	char[] value; // final이 아님
	...
}
```


<br/>

---
<br/>

## **StringBuilder 메서드**

- `append()` 메서드를 사용해 여러 문자열을 추가
- `insert()` 메서드로 특정 위치에 문자열을 삽입
- `delete` () 메서드로 특정 범위의 문자열을 삭제
- `reverse()` 메서드로 문자열 뒤집기

### StringBuilder 사용 예시

```java
// StringBuilder 사용 예시
StringBuilder sb = new StringBuilder();  
sb.append("A");  
sb.append("B");  
sb.append("C");  
sb.append("D");  
System.out.println("sb = " + sb);  
  
sb.insert(4, "Java");  
System.out.println("insert: " + sb);  
  
sb.delete(4, 8);  
System.out.println("delete: " + sb);  
  
sb.reverse();  
System.out.println("reverse: " + sb);  
  
String str = sb.toString();

/* 출력
sb = ABCD
insert: ABCDJava
delete: ABCD
reverse: DCBA
*/
```



<br/>

---
<br/>


## **StringBuilder를 사용하는 것이 더 좋은 경우**

- 반복문에서 반복해서 문자를 연결할 때 
- 조건문을 통해 동적으로 문자열을 조합할 때 
- 복잡한 문자열의 특정 부분을 변경해야 할 때 
- 매우 긴 대용량 문자열을 다룰 때

### String과 StringBuilder의 문자열 반복 변경 비교

문자열을 반복적으로 변경할 때 소요되는 시간을 비교해 보겠다. 먼저 아래와 같이 `String`은 수행시간이 2491ms, 2.5초 정도가 걸렸다. 

```java
// String
long startTime = System.currentTimeMillis();  
String result = "";  
for (int i = 0; i < 100000; i++) {  
    result += "Hello Java";  
}  
long endTime = System.currentTimeMillis();  
  
System.out.println("result = " + result);  
System.out.println("time = " + (endTime - startTime) + "ms");

/*
result = Hello JavaHello Java.....
time = 2491ms
*/
```

하지만 `StringBuilder`는 수행시간이 4ms가 걸렸다.

```java
long startTime = System.currentTimeMillis();  
StringBuilder sb = new StringBuilder();  
for (int i = 0; i < 100000; i++) {  
    sb.append("Hello Java");  
}  
long endTime = System.currentTimeMillis();  
  
System.out.println("result = " + sb.toString());  
System.out.println("time = " + (endTime - startTime) + "ms");

/*
result = Hello JavaHello Java.....
time = 4ms
*/
```

엄청난 차이를 볼 수 있는데, 이는 불변인 String은 반복횟수만큼(10만번) 객체를 생성하고 지웠기 때문이다.

<br/>

---
<br/>

## **메서드 체이닝**

메서드 체이닝은 메서드의 연산을 처리한 후, 자기 자신의 참조값을 반환하는 함수들을 연속으로 사용하는 것이다. 아래 예제를 보면, `Adder`라는 클래스의 `add` 함수는 매개변수 `value`를 증가시키고나서 `자기 자신(this)`를 반환한다. 이렇게 되면 자기 자신의 참조를 계속 반환값으로 받기 때문에 `.add()`를 계속 이어 붙여나갈 수 있다.

```java
public class Adder(){
	private int value;
	
	public Adder add(int addValue){
		value += addValue;
		return this;
	}
	public int getValue(){
		return value;
	}
}

public class Main(){
	public static void main(String[] args{
		Adder adder = new Adder();
		// adder = adder.add(10);
		// adder = adder.add(20);
		int result = adder.add(10).add(20).add(30).getValue(); // 메서드 체이닝
	}
}
```

### **StringBuilder 메서드 체이닝**

`StringBuilder`도 메서드 체이닝 기법을 제공한다. 아래 예제와 같이 편하게 사용할 수 있으며, 코드를 간결하고 읽기 쉽게 작성할 수 있다.

```java
sb.append("A").append("B").append("C").append("D");  
System.out.println("sb = " + sb.toString());  

// 출력
// sb = ABCD
```

