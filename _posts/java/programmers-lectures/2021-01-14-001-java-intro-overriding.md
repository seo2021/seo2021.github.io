---
title: "[프로그래머스 자바 입문] 오버라이딩(Overriding)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 오버라이딩
  - 자바입문
---

## 메소드 오버라이딩(method overriding) 
- 상속받은 부모 클래스의 메소드를 재정의하여 사용하는 것.
  - 자바에서 자식 클래스는 부모 클래스의 private 멤버를 제외한 모든 메소드를 상속받는다.
- ex) 상속받은 메소드를 그대로 사용해도 된다.

  ```java
  // 부모 클래스
  public class Car {
    public void run() {
      System.out.println("Car의 run 메소드");
    }
  }
  
  // Car를 상속받는 자식 클래스
  public class Bus extends Car {}
  
  public class BusExam {
    public static void main(String[] args) {
      Bus bus = new Bus();
      bus.run(); // 상속받은 Car 클래스의 메소드 실행
    }
  }
  ```
  
- ex) 오버라이딩: 상속받은 메소드를 재정의

  ```java
  // Car를 상속받는 자식 클래스
  public class Bus extends Car {
    // 메소드 오버라이딩
    public void run() {
      System.out.println("Bus의 run 메소드");
    }
  }
  
  public class BusExam {
    public static void main(String[] args) {
      Bus bus = new Bus();
      bus.run(); // Bus 클래스에서 재정의한 메소드 실행
    }
  }
  ```
  
  - 메소드를 오버라이딩하면, 항상 자식 클래스에서 정의된 메소드가 호출된다.
  
- 오버라이딩한다고 해서 부모 클래스의 메소드가 사라지는 것은 아니다.
  - **super 키워드로 부모의 메소드를 호출**할 수 있다.
  
  ```java
  // Car를 상속받는 자식 클래스
  public class Bus extends Car {
    // 메소드 오버라이딩
    public void run() {
      super.run(); // **부모의 run() 메소드 호출
      System.out.println("Bus의 run 메소드");
    }
  }
  ```
  
## 오버라이딩의 조건
- 오버라이딩은 메소드의 동작만을 재정의하는 것이므로, 메소드의 **선언부는 기존 메소드와 완전히 같아야** 한다.
- 메소드의 반환 타입은 부모 클래스의 반환 타입으로 변경 가능하다.
- 부모 클래스의 메소드보다 접근 제어자를 더 좁은 범위로 변경할 수 없다.
- 부모 클래스의 메소드보다 더 큰 범위의 예외를 선언할 수 없다.

## 오버로딩(overloading) 🆚 오버라이딩(overriding)
- 오버로딩은 **새로운 메소드**를 정의하는 것.
  - 서로 다른 시그니처, 동일한 이름
- 오버라이딩은 상속받은 **기존의 메소드를 재정의**하는 것.
  - 동일한 시그니처와 이름
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 오버라이딩](https://programmers.co.kr/learn/courses/5/lessons/189)
- [코딩의 시작, TCP School \| JAVA \| 메소드 오버라이딩](https://www.tcpschool.com/java/java_inheritance_overriding)
