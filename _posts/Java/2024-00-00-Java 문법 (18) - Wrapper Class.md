---
title: Java 문법 (18) - Wrapper Class
author: jay
date: 2024-04-29
categories:
  - Java
  - Java_Mid1
tags:
  - Java
source: https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-1
---
## **객체가 아닌 기본형**

int, char, double 등의 기본형 타입은 객체가 아니다. 따라서 다음과 같은 객체지향의 장점을 적용시킬 수 없다. 

#### **객체 메서드 사용 불가능**
객체는 유용한 메서드를 제공할 수 있는데, 기본형은 객체가 아니라서 메서드를 제공할 수 없다.
```java
String str = "hello java";
str.split(" "); // 공백을 기준으로 나눠주는 메서드

int num = 0;
num.~~ // 기본형은 메서드 사용 불가능
```

#### **null 값을 담을 수 없음**

값이 없음을 나타내는 null을 사용해야할 때가 있는데, 기본형은 불가능하다.

```java
String str = null; // 객체는 가능
int num = null; // 기본형은 컴파일 오류 발생
```

#### **컬렉션 사용 불가능**

메서드에서 매개변수로 객체를 요구한다거나, 컬렉션에서 요구하는 객체타입에 넣을 수 없어서 사용할 수 없다.

```java
ArrayList<String> list = new ArrayList<>(); // 객체 가능
ArrayList<int> list = new ArrayList<>(); // 기본형은 불가능 컴파일 오류 발생
```
 
<br/>

---
<br/>

## **자바 래퍼 클래스**

자바는 이런 기본형을 객체로 사용할 수 있게 해주는 Wrapper 클래스를 제공한다. 자바의 모든 기본타입에 해당되는 Wrapper 클래스가 있고, 이를 사용해 만든 객체를 포장 객체라고도 한다. 기본 타입의 값을 내부에 두고 포장하는 것처럼 보이기 때문이다. 포장된 물건을 바꿀 수 없듯이, 내부 값은 변경할 수 없는 불변으로 만들어진다. 

#### 래퍼 클래스 종류

| 기본 타입   | Wrapper 클래스 |
| ------- | ----------- |
| byte    | Byte        |
| short   | Short       |
| int     | Integer     |
| long    | Long        |
| float   | Float       |
| double  | Double      |
| char    | Character   |
| boolean | Boolean     |

### **박싱 언박싱**

기본형을 Wrapper 클래스로 변경하는 것을 마치 박스에 물건을 담는 것 같다고 해서 박싱(Boxing)이라고 하고, 반대로 Wrappe 클래스에 들어있는 값을 다시 꺼내는 것을 박스에서 물건을 꺼내는 것 같다고 해서 언박싱(Unboxing)이라고 한다.

- Boxing: 기본형 -> Wrapper 클래스
- Unboxing: Wrapper 클래스 -> 기본형

```java
// 박싱
int n1 = 10
Integer num = Integer.valueOf(n1); // Integer에 기본형을 박싱
// 언박싱 (intValue)
int n = num.intValue(); // Integer의 값을 꺼내 가져온다.
```

### **자동 박싱, 언박싱**

기본형과 Wrapper 클래스 간에 변환할 일이 자주 발생하다보니, 자바 1.5부터는 자동 박싱(Auto-boxing), 자동 언박싱(Auto-unboxing)을 지원한다. 기본타입 값을 직접 박싱, 언박싱하지 않아도 래퍼 클래스 변수에 대입만 하면 자동으로 박싱과 언박싱이 되도록 컴파일러가 자동으로 처리해준다.

```java
int value = 7;  
Integer boxedValue = value; // 오토 박싱  

int unboxedValue = boxedValue; // 오토 언박싱
```

### **Wrapper 클래스 성능**

아래 예시는 10억번 더하는 단순 반복 예시이다. 기본형만 사용하면 349ms만에 끝나지만 Wrapper 클래스를 사용하게 되면 1550ms가 걸리게 된다. 약 5배정도 차이가 나는 것을 알 수 있는데, 기본형은 메모리에서 단순히 그 크기만큼의 공간을 차지하지만, Wrapper 클래스의 객체는 값 뿐만 아니라 객체를 다루는데 필요한 객체 메타데이터를 포함하기 때문에 더 많은 메모리를 사용하기 때문이다. 

```java
int iterations = 1_000_000_000; //  반복 횟수 설정, 10억;  
  
// 기본형 long 사용  
long sumPrimitive = 0;  
long startTime = System.currentTimeMillis();  
for (int i = 0; i < iterations; i++) {  
    sumPrimitive += i;  
}  
long endTime = System.currentTimeMillis();  
  
System.out.println("sumPrimitive = " + sumPrimitive);  
System.out.println("기본형 걸린 시간 = : " + (endTime - startTime) + "ms"); // 349ms , 0.35초 걸림  
  
  
  
// Wrapper class Long 사용  
  
Long sumWrapper = Long.valueOf(0);  
long startTime2 = System.currentTimeMillis();  
for (int i = 0; i < iterations; i++) {  
    sumWrapper += i;  
}  
long endTime2 = System.currentTimeMillis();  
System.out.println("sumWrapper = " + sumWrapper);  
System.out.println("Wrapper클래스 Long 걸린 시간 = : " + (endTime2 - startTime2) + "ms"); // 1550ms , 1.5초 걸림
```

또한 박싱, 언박싱을 반복하게되는 코드에서도 타입변환이 계속 일어나면서 성능에 영향을 줄 수 있다.

### **주요 메서드**

Wrapper 클래스가 제공하는 주요 메서드들이 있다.

- `valueOf()`: 래퍼 타입을 반환한다. 숫자, 문자열을 모두 지원
- `parseInt()`: 문자열을 기본형으로 반환한다.
- `compareTo()`: 내 값과 인수로 넘어온 값을 비교한다. 내 값이 크면 1, 같으면 0, 작으면 -1을 반환한다.
- `Integer.sum(),Integer.min(),Integer.max()`: static 메서드도 제공한다.

<br/>

---
<br/>

## **Class 클래스**

자바에서 Class 클래스는 클래스의 정보를 다루는데 사용한다. 이를 통해 실행중인 자바 앱 내에서 동적으로 필요한 클래스의 속성과 메서드에 대한 정보를 조회하고 조작할 수 있다.

#### **주요 기능**

- **타입 정보 조회**: 클래스의 이름, 부모 클래스, 인터페이스, 접근 제한자 등의 정보를 조회
	- **getDeclaredFields()**: 클래스의 모든 필드를 조회한다. 
	- **getDeclaredMethods()**: 클래스의 모든 메서드를 조회한다. 
	- **getSuperclass()**: 클래스의 부모 클래스를 조회한다. 
	- **getInterfaces()**: 클래스의 인터페이스들을 조회한다.
- **리플렉션**: 클래스에 정의된 메서드, 필드, 생성자를 조회하고, 이들을 통해 객체 인스턴스를 생성하거나 메서드를 호출하는 등의 작업을 할 수 있다.
- **동적 로딩 및 생성**: `Class.forName()` 메서드를 사용해서 클래스를 동적으로 로드하고, `newInstance()` 메서드를 통해 새로운 인스턴스를 생성할 수 있다.
- **애노테이션 처리**: 클래스에 적용된 애노테이션을 조회하고 처리하는 기능을 제공한다.


```java
// Class 조회 방법 3가지
Class clazz = String.class; // 1.클래스에서 조회  
Class clazz = new String().getClass();// 2.인스턴스에서 조회  
Class clazz = Class.forName("java.lang.String"); // 3.문자열로 조회
// 실행 도중 문자열을 입력으로 받아서 클래스를 만들 수 있음.
```

```java
// 모든 필드 출력
Field[] fields = clazz.getDeclaredFields(); 
for (Field field : fields) {
	 System.out.println("Field: " + field.getType() + " " + field.getName());
}
```

```java
// Hello라는 클래스가 있을 때
 Class helloClass = Class.forName("lang.clazz.Hello");
 // 생성자를 가져와서, 그 생성자를 기반으로 인스턴스를 생성할 수 있다.(리플렉션)
 Hello hello = (Hello) helloClass.getDeclaredConstructor().newInstance();
```


<br/>

---
<br/>

## **System 클래스**

시스템과 관련된 기본 기능들을 제공한다.

- **표준 입력, 출력, 오류 스트림**: `System.in` , `System.out` , `System.err` 은 각각 표준 입력, 표준 출력, 표준 오류 스트림
- **시간 측정**: `System.currentTimeMillis()` 와 `System.nanoTime()` 은 현재 시간을 밀리초 또는 나노초 단위로 제공
- **환경 변수**: `System.getenv()` 메서드를 사용하여 OS에서 설정한 환경 변수의 값 조회
- **시스템 속성**: `System.getProperties()` 를 사용해 현재 시스템 속성을 얻거나`System.getProperty(String key)` 로 특정 속성을 얻을 수 있다. 시스템 속성은 자바에서 사용하는 설정 값이다.  
- **시스템 종료**: `System.exit(int status)` 메서드는 프로그램을 종료하고, OS에 프로그램 종료의 상태 코 드를 전달한다.
- **배열 고속 복사**: `System.arraycopy` 는 시스템 레벨에서 최적화된 메모리 복사 연산을 사용한다. 직접 반복문 을 사용해서 배열을 복사할 때 보다 수 배 이상 빠른 성능을 제공
