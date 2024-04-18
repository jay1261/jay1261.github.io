---
title: Java 문법 (3) - 새로운 Switch문
author: jay
date: 2024-03-15
categories:
  - Java
  - Java_Start
tags:
  - Java
source: https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%9E%90%EB%B0%94-%EC%9E%85%EB%AC%B8
---
## **Java 문법 (2) - 새로운 Switch문**

<br />

---

<br/>

### **기존 Switch**
<br/>

자바의 switch 문은 아래와 같이 작성할 수 있습니다. 하지만 break도 꼭 써줘야하고, if 문보다 조금은 더 보기 편하지만 많이 차이나지는 않습니다. 따라서 Java14부터는 새로운 switch문을 사용할 수 있습니다.

```java
switch (조건){  
	case 1 :  
		// 조건의 결과값이 1일 때 실행할 코드  
		break;  
	case 2:  
		// 조건의 결과값이 2일 때 실행할 코드
		break;  
	case 3:  
		// 조건의 결과값이 3일 때 실행할 코드
		break;  
	default:  
		// 조건이 위의 어떤 값에도 해당하지 않을 때 실행할 코드
}
```

<br/>

---

<br />

### **새로운 Switch**
<br/>

기본적으로 아래와 같은 형식으로 switch 문을 작성할 수 있습니다. 훨씬 코드가 간결해진 모습입니다.


```java
switch(조건){
	case 1 -> //조건이 1일 떄 실행할 코드;
	case 2 -> //조건이 2일 떄 실행할 코드;
	default -> // 조건이 위의 어떤 값에도 해당하지 않을 때 실행할 코드 
}
```

<br/>

거기다 추가적으로 switch의 결과값을 return 받아서 변수에 할당해줄 수도 있습니다.

```java
int result = switch(조건){
	case 1 -> 10//조건이 1일 떄 실행할 코드;
	case 2 -> 20 //조건이 2일 떄 실행할 코드;
	default -> -1 // 조건이 위의 어떤 값에도 해당하지 않을 때 실행할 코드 
}
```