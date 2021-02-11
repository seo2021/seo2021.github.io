---
title: "[프로그래머스 자바 중급] 제네릭(Generic)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - generic
  - 자바중급
---

## 제네릭(generic)이란?
- 자바에서 제네릭이란 **데이터의 타입을 일반화(generalize)**하는 것을 의미.
- **클래스**나 **메소드**에서 사용할 **내부 데이터 타입**을 컴파일 시 **미리 지정**하는 방법.

- 컴파일 시 미리 타입 검사를 수행하면 다음과 같은 장점을 가진다.
  1. 클래스나 메소드 내부에서 사용되는 **객체의 타입 안정성**을 높일 수 있다.
  2. 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있다.
  
## 제네릭의 선언 및 생성
- 제네릭은 클래스와 메소드에만 다음과 같은 방법으로 선언할 수 있다.

  ```java
  class MyArray<T> {
    T element;
    void setElement(T element) { this.element = element; }
    T getElement() { return element; }
  }
  ```
  - 위의 예제에서 사용된 `T`를 **타입 변수(type variable)**라고 하며, **임의의 참조형 타입**을 의미.
  - 꼭 `T`뿐만 아니라 어떠한 문자를 사용해도 상관없으며, 여러 개의 타입 변수는 쉼표(,)로 구분하여 명시할 수 있다.
  - 타입 변수는 **클래스**에서 뿐만 아니라 **메소드의 매개변수나 반환값**으로 사용할 수 있다.<br/>  
  
- 위와 같이 선언된 **제네릭 클래스(generic class)**를 생성할 때는 타입 변수 자리에 **사용할 실제 타입을 명시**해야 한다.
  - ex) MyArray 클래스에 사용될 타입 변수로 Integer 타입을 사용
  
    ```java
    MyArray<Integer> myArr = new MyArray<Integer>();
    ```
    - 내부적으로 **정의된 타입 변수가 명시된 실제 타입으로 변환**되어 처리된다.
    - 💡 타입 변수 자리에는 기본 타입을 사용할 수 없다. **래퍼(wrapper) 클래스**를 사용해야 한다.
    
- Java SE 7부터 인스턴스 생성 시, 타입을 추정할 수 있는 경우에는 타입을 생략할 수 있다.

  ```java
  MyArray<Integer> myArr = new MyArray<>();
  ```
  
- ex) 제네릭 클래스를 사용하는 MyArrayExam 클래스

  ```java
  public class MyArrayExam {
    public static void main(String[] args) {
      // 타입을 Object로 한 인스턴스 생성
      MyArray<Object> myArr1 = new MyArray<>();
      myArr1.setElement(new Object());
      Object obj = myArr1.getElement();
      
      // 타입을 String으로 한 인스턴스 생성
      MyArray<String> myArr2 = new MyArray<>();
      myArr2.setElement("hello");
      String str = myArr2.getElement();
      
      // 타입을 Integer로 한 인스턴스 생성
      MyArray<Integer> myArr3 = new MyArray<>();
      myArr3.setElement(1);
      int num = (int)myArr3.getElement();
    }
  }
  ```
  - 참조 타입으로 `<Object>`, `<String>`, `<Integer>`를 사용했다.
  - 제네릭 클래스를 선언할 때는 **가상의 타입으로 선언**하고, **사용 시에는 구체적인 타입을 설정**함으로써 다양한 타입으로 인스턴스를 만들 수 있다.
  - 제네릭을 사용하는 대표적인 클래스는 컬렉션 프레임워크와 관련된 클래스.
  
- ex) 제네릭에서 적용되는 타입 변수의 다형성

```java
  import java.util.*;

  class LandAnimal { public void crying() { System.out.println("육지동물"); } }
  class Cat extends LandAnimal { public void crying() { System.out.println("냐옹냐옹"); } }
  class Dog extends LandAnimal { public void crying() { System.out.println("멍멍"); } }
  class Sparrow { public void crying() { System.out.println("짹짹"); } }

  // 제네릭 클래스 선언
  class AnimalList<T> {
    ArrayList<T> al = new ArrayList<T>();

    void add(T animal) { al.add(animal); }
    T get(int index) { return al.get(index); }
    boolean remove(T animal) { return al.remove(animal); }
    int size() { return al.size(); }
  }

  public class Generic01 {
    public static void main(String[] args) {
      // LandAnimal을 타입으로 제네릭 클래스 생성
      AnimalList<LandAnimal> landAnimal = new AnimalList<>();	// Java SE 7부터 생략가능

      landAnimal.add(new LandAnimal());
      landAnimal.add(new Cat());
      landAnimal.add(new Dog());
      // landAnimal.add(new Sparrow());	// 오류 발생

      for (int i = 0; i < landAnimal.size() ; i++) {
        // 육지동물
        // 냐옹냐옹
        // 멍멍
        landAnimal.get(i).crying();
      }
    }
  }
  ```
  - Cat과 Dog 클래스는 LandAnimal 클래스를 상속받는 자식 클래스이므로, AnimalList<LandAnimal>에 추가할 수 있다.
    
## 제네릭의 제거 시기
- 자바 코드에서 선언되고 사용된 제네릭 타입은 컴파일 시 컴파일러에 의해 자동으로 검사되어 타입 변환된다.
- 그리고 코드 내의 모든 제네릭 타입은 제거되어, **컴파일된 class 파일에는 어떠한 제네릭 타입도 포함되지 않게 된다**.
- 이런 식으로 동작하는 이유는 제네릭을 사용하지 않는 코드와의 **호환성 유지**를 위해서이다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Generic](https://programmers.co.kr/learn/courses/9/lessons/257)
- [코딩의 시작, TCP School \| JAVA \| 제네릭의 개념](https://www.tcpschool.com/java/java_generic_concept)
