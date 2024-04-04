---
title: Java 문법 (8) - 자바 메모리 구조와 static
author: jay
date: 2024-04-03
categories:
  - Java
  - Java_Basic
tags:
  - Java
---
## **Java 문법 (8) - 자바 메모리 구조와 static**


<br />

---

<br/>


### **자바 메모리 구조** 
<br/>

자바의 메모리 구조는 크게 `메서드 영역`, `스택 영역`, `힙 영역` 3개로 나눌 수 있습니다.

#### **메서드 영역**

메서드 영역은 프로그램을 실행하는데 필요한 공통 데이터를 관리하는 영역입니다. 프로그램의 모든 영역에서 공유합니다.

- 클래스 정보(클래스의 실행코드, 필드, 매서드, 생성자 등)를 보관
- static 변수들을 보관
- 런타임 상수 풀: 공통 리터럴 상수들을 보관 (ex "hello")

#### **스택 영역**

스택 영역은 자바 실행시 쓰레드 별로 하나씩 스택이 생성됩니다. 각 스택 프레임은 지역변수, 중간 연산 결과, 메서드 호출 정보 등을 포함합니다.

- 매서드를 호출할 때마다 하나의 스택 프레임이 쌓이고, 메서드가 종료되면 해당 스택 프레임이 제거
- 자바는 스택 영역을 사용해서 메서드 호출과 지역변수, 매개변수를 관리
- 메서드를 계속 호출하면 스택 프레임이 계속 쌓임
- 스택 프레임이 종료되면 지역변수도 함게 제거, 스택 프레임이 모두 종료되면 프로그램도 종료

#### **힙 영역**

객체(인스턴스)와 배열이 생성되는 영역입니다. GC(가비지 컬렉션)이 이루어지는 주요 영역이고, 더 이상 참조되지 않는 객체는 GC에 의해서 제거됩니다.


<br />

---

<br/>

### **스택 영역 예시**
<br/>

`main`에서 `method1`을 호출하고, `method1`에서 `method2`를 호출한 예시입니다. 각각 함수마다 `start`와 `end`를 시작과 끝에 넣어주면 스택이 어떻게 실행되는지 눈으로 확인할 수 있습니다.
<br/>
`main 시작 -> method1 시작 -> method2 시작 -> method2 종료 -> method1 종료 -> main 종료` 순으로 실행됩니다.

```java
package memory;  
  
public class JavaMemoryMain1 {  
    public static void main(String[] args) {  
        System.out.println("main start");  
        method1(10);  
        System.out.println("main end");  
    }  
    static void method1(int m1){  
        System.out.println("method1 start");  
        int cal = m1 * 2;  
        method2(cal);  
        System.out.println("method1 end");  
    }  
    static void method2(int m2){  
        System.out.println("method2 start");  
        System.out.println("method2 end");  
    }  
}

// 실행결과
// main start
// method1 start
// method2 start
// method2 end
// method1 end
// main end

```


<br />

---

<br/>

### **스택 영역과 힙 영역**
<br/>

아래 예시코드는 스택과 힙 영역이 함께 사용되는 경우를 보기 위한 코드입니다.
`method1`에서 `Data`의 객체 `data1`이 생성되고, 이 객체의 참조값을 `method2`의 매개변수로 전달합니다. 실행 순서를 보면 아래와 같습니다.

- `main()`스택 프레임 생성, (main start 출력)
- `method1()` 스택 프레임 생성, (method1 start 출력)
- `Data`의 객체 힙 영역에 생성, `data1` 이라는 참조값을 담는 지역변수 스택 프레임에 보관
- `method2()` 스택 프레임 생성, `data1`을 매개변수 `data2`로 받음, (method2 start 출력)
- `method2` 종료, `method2()` 스택 프레임 및 `data2` 제거, (method2 end 출력)
- `method1` 종료, `method1()` 스텍 프레임 및 `data1` 제거, (method1 end 출력)
- `Data`의 객체를 참조하는 곳이 없음, GC가 제거
- `main` 종료, `main()` 스택 프레임 제거, (main end 출력)
- 프로그램 종료

```java
// memory.java
package memory;  
  
public class Data {  
    private int value;  
  
    public Data(int value) {  
        this.value = value;  
    }  
  
    public int getValue(){  
        return value;  
    }  
}

// JavaMemoryMain2.java
package memory;  
  
public class JavaMemoryMain2 {  
    public static void main(String[] args) {  
        System.out.println("main start");  
        method1();  
        System.out.println("main end");  
    }  
    static void method1(){  
        System.out.println("method1 start");  
        Data data1 = new Data(10);  
        method2(data1);  
        System.out.println("method1 end");  
    }  
    static void method2(Data data2){  
        System.out.println("method2 start");  
        System.out.println("data.value = " + data2.getValue());  
        System.out.println("method2 end");  
    }  
}

/* 실행결과
	main start
	method1 start
	method2 start
	data.value = 10
	method2 end
	method1 end
	main end
*/
```



<br />

---

<br/>

### **Static 변수**
<br/> 

static은 주로 멤버변수와 메서드에 사용됩니다. 

클래스의 멤버변수는 두가지 종류로 나뉩니다.
- **인스턴스 변수** : static이 붙지 않은 멤버변수 `ex) private String name;`
	- 인스턴스 변수는 인스턴스를 생성해야 사용할 수 있고, 인스턴스에 소속되어 있어서 인스턴스 변수
	- 인스턴스를 만들 때 마다 새로 만들어짐
- **클래스 변수** : static이 붙은 멤버 변수 `ex) public static int count;`
	- `클래스 변수`, `정적 변수`, `static 변수` 등으로 불림
	- static 변수는 클래스 자체에 소속되어 있어서 클래스명으로 바로 접근이 가능하며, 메모리의 메서드 영역에 만들어잠
	- 자바 프로그램을 시작할 때 딱 1개가 만들어지며 보통 여러곳에서 공유하는 목적으로 사용됩니다.

```java
// Data3.java
package static1;  
  
public class Data3 {  
    public String name;  
    public static int count;  
  
    public Data3 (String name){  
        this.name = name;  
        count++;  
    }  
}

// DataCountMain3.java
package static1;  
  
public class DataCountMain3 {  
    public static void main(String[] args) {  
        // static으로 count를 공유하기 때문에 공용으로 사용 가능한 특별하게 관리되는 변수  
        // static 변수는 메서드 영역에서 관리함  
        Data3 data1 = new Data3("A");  
        System.out.println("A Count: " + Data3.count); // static 변수는 클래스명으로 접근 가능하다.  
        Data3 data2 = new Data3("B");  
        System.out.println("B Count: " + Data3.count);  
        Data3 data3 = new Data3("C");  
        System.out.println("C Count: " + Data3.count);  
  
        // 추가 인스턴스를 통한 접근도 가능  
        // 권장하지 않음. count가 인스턴스변수인지 static 변수인지 코드만 보고 알 수 없다.  
        Data3 data4 = new Data3("D");  
        System.out.println(data4.count);  
  
        // 클래스를 통한 접근  
        System.out.println(Data3.count);  
    }  
}
```

<br />

---

<br/>

### **Static 메서드**
<br/>

매서드 앞에 static이 붙는 것을 `정적 메서드` 또는 `클래스 메서드`라고 합니다. 클래스 자체에 소속되어 있어서 객체 생성없이 클래스명으로 메서드를 바로 호출할 수 있습니다. 

static 메서드는 `같은 static만 호출할 수 있습니다. ``정적 변수나 정적 메서드`만 호출이 가능합니다. 인스턴스 변수나 인스턴스 메서드는 사용할 수 없습니다. 반대로 인스턴스 변수나 메서드는 static 메서드를 호출할 수 있습니다.

```java
package static2;  
  
public class DecoData {  
    private int instanceValue;  
    private static int staticValue;  
  
    // static은 static만 접근 가능  
    public static void staticCall(){  
        staticValue++; // 정적 변수 접근  
        staticMethod(); // 정적 메서드 접근 가능  
        // instanceValue++; // static method는 인스턴스 변수 접근 불가능  
        // instanceMethod(); // 인스턴스 메서드 접근 불가능  
    }  
  
    // instance는 static, instance 전부 접근 가능  
    public void instanceCall(){  
        instanceValue++; // 인스턴스 변수 접근 가능  
        instanceMethod(); // 인스턴스 메서드 접근 가능  
  
        staticValue++; // 스태틱 변수 접근 가능  
        staticMethod(); // 스태틱 메서드 접근 가능  
    }  
  
    private void instanceMethod(){  
        System.out.println("instanceValue= " + instanceValue);  
    }  
    private static void staticMethod(){  
        System.out.println("static methpd= " + staticValue);  
    }  
}
```
