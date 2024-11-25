---
title: "[자료구조] - ArrayList 직접 만들어보기"
author: jay
date: 2024-11-19
categories:
  - Projcet
tags:
  - Java
  - 자료구조
  - ArrayList
source: 
pin: false
---
## **1. Array vs ArrayList**
---

#### Array

- 배열은 크기가 고정되어있어, 선언 시 크기를 지정해야 하며, 이후 변경할 수 없습니다.
- 기본 자료형과 객체형 데이터 모두 저장할 수 있습니다.
- 데이터 추가, 삭제시 인덱스로를 통해 직접 접근하여 조작해야 합니다.

#### ArrayList

- 내부적으로 크기가 동적으로 증가합니다.
- 객체 데이터 타입을 저장할 수 있습니다.
- add(), remove() 등의 메서드를 사용해 데이터를 추가, 삭제합니다.


## **2. ArrayList 동적 크기 조절**
---

ArrayList는 데이터를 저장하기 위해 내부적으로 배열을 사용합니다. 배열은 생성시 크기가 고정되므로 처음부터 너무 큰 배열을 생성하면 메모리 낭비가 발생합니다. 반대로, 너무 작은 배열을 생성하면 데이터가 추가될 때마다 크기를 변경해야 합니다. 
ArrayList는 기존 배열의 크기에서 확장이 필요할 때 1.5배씩 크기를 늘리는 방식으로 두가지 문제를 해결합니다.

생성시에 기본 사이즈는 10이며, 개발자가 예상 크기를 알고 있다면 생성자를 통해 크기를 설정할 수 있습니다.


## **3. 직접 구현해보기**
---

```java
  
public class MyArrayList<T> {  
  
    private int size;  
    private T[] array;  
  
    public MyArrayList() {  
        size = 0;  
        this.array = (T[]) new Object[10];  
    }  
  
    public MyArrayList(int size) {  
        this.size = 0;  
        this.array = (T[]) new Object[size];  
    }  
  
    public void add(T element){  
        if(size+1 > array.length){  
            resize();  
        }  
        array[size] = element;  
        size++;  
    }  
  
    public void remove(int index){  
        if (index < 0 || index >= size) {  
            throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);  
        }  
  
        for(int i = index; i < this.size - 1; i++){  
            array[i] = array[i+1];  
        }  
  
        array[size--] = null;  
    }  
  
    public void removeLast(){  
        if (size == 0) {  
            throw new IllegalStateException("ArrayList is empty.");  
        }  
        array[size-1] = null;  
        size--;  
    }  
  
    private void resize(){  
        int newCapacity = array.length + (array.length >> 1); // 기존 크기의 1.5배  
        T[] newArray = (T[]) new Object[newCapacity];  
        System.arraycopy(array, 0, newArray, 0, size);  
        this.array = newArray;  
    }  
  
    public T get(int index) {  
        if (index < 0 || index >= size) {  
            throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);  
        }  
        return array[index];  
    }  
  
    public boolean contains(T element) {  
        for (int i = 0; i < size; i++) {  
            if (array[i].equals(element)) return true;  
        }  
        return false;  
    }  
  
    public void clear() {  
        for (int i = 0; i < size; i++) {  
            array[i] = null;  
        }  
        size = 0;  
    }  
  
    @Override  
    public String toString() {  
        if (size == 0) return "[]";  
  
        StringBuilder sb = new StringBuilder();  
        sb.append("[");  
        for (int i = 0; i < size - 1; i++) {  
            sb.append(array[i] + ", ");  
        }  
        sb.append(array[size-1]);  
        sb.append("]");  
        return sb.toString();  
    }  
}
```
