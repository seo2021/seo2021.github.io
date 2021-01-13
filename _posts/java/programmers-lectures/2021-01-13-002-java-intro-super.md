---
title: \[프로그래머스 \| 자바 입문\] super와 부모 생성자
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - super
  - 부모생성자
  - constructor
---

## 부모 생성자
- 클래스가 인스턴스화될 때, 생성자가 실행되면서 객체의 초기화를 한다. 이 때, 자신의 생성자만 실행되는 것이 아니고 **부모의 생성자부터** 실행된다.

  ```java
  public class Car { // 부모 클래스
    public Car() {
      System.out.println("Car의 기본 생성자입니다.");
    }
  }
  
  public class Bus extends Car { // 자식 클래스
    public Bus() {
      System.out.println("Bus의 기본 생성자입니다.");
    }
  }
  
  public class BusExam {
    public static void main(String[] args) {
      Bus b = new Bus(); // 자식 클래스의 객체 생성
    }
  }
  ```
  
  - 실행 결과

    ```
    Car의 기본 생성자입니다.
    Bus의 기본 생성자입니다.
    ```
    - new 연산자로 Bus 객체를 생성하면, Bus 객체가 메모리에 올라갈 때 부모인 Car도 함께 메모리에 올라간다.
    - 생성자는 객체를 초기화하는 역할.
    - 생성자가 호출될 때 자동으로 **부모의 생성자도 호출**되면서 **부모 객체도 초기화**한다.
- 이러한 부모 클래스의 생성자 호출은 모든 클래스의 부모 클래스의 Object 클래스의 생성자까지 계속 거슬러 올라가며 수행된다.

## super 키워드
- 자신을 가리키는 키워드가 this라면, **부모를 가리키는 키워드**는 super.
- 부모 클래스로부터 상속받은 **필드**나 **메소드**를 자식 클래스에서 참조하는 데 사용하는 **참조 변수**.

## super()
- **부모의 생성자**를 의미.
- <u>부모의 생성자를 임의로 호출하지 않으면, **부모 클래스의 기본 생성자**가 자동으로 호출된다.</u>
  - 자바 컴파일러는 부모 클래스의 생성자를 명시적으로 호출하지 않는 모든 자식 클래스의 생성자 첫 줄에 자동으로 `super();`를 추가한다.
- 아래 예제는 super()를 호출할 때와 하지 않을 때 모두 부모 클래스의 기본 생성자를 호출하므로 결과가 같다.

  ```java
  // 자식 생성자
  public Bus() {
    // 부모 클래스 기본 생성자 자동 호출
    System.out.println("Bus의 기본 생성자입니다.");
  }
  
  public Bus() {
    // 부모 클래스 생성자 직접 호출
    super(); 
    System.out.println("Bus의 기본 생성자입니다.");
  }
  ```

## 부모의 기본 생성자가 아닌 다른 생성자를 호출하는 방법
- 클래스의 기본 생성자가 없는 경우도 존재

  ```java
  // 부모 클래스
  public class Car { 
    // 사용자 정의 생성자
    public Car(String name) {
      System.out.println(name + " 을 받아들이는 생성자입니다.");
    }
  }
  ```
  
- 부모 클래스의 기본 생성자가 없으므로, 자식 클래스에서 부모 클래스의 기본 생성자를 호출하면 오류가 발생한다.  
  💡 이와 같은 오류를 방지하기 위해, 매개변수를 가지는 생성자를 선언해야 할 경우에는 되도록이면 **기본 생성자까지 명시적으로 선언**하는 것이 좋다.
- 따라서, 자식 클래스의 생성자에서 직접 부모 클래스의 생성자를 호출해야 한다.

  ```java
  public Bus() {
    super("소방차"); // 문자열을 매개변수로 받는 부모 생성자 호출
    System.out.println("Bus의 기본생성자입니다.");
  }
  ```
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| super와 부모생성자](https://programmers.co.kr/learn/courses/5/lessons/192)
- [코딩의 시작, TCP School \| JAVA \| super와 super()](https://www.tcpschool.com/java/java_inheritance_super)
