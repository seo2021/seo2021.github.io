---
title: \[프로그래머스 \| 자바 입문\] 객체 형 변환(Object Type Casting)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 형변환
---

## 다형성(polymorphism)이란?
- 하나의 객체가 여러 가지 타입을 가질 수 있는 것.
- 상속, 추상화와 더불어 객체 지향 프로그래밍을 구성하는 중요한 특징 중 하나.

## 참조 변수의 다형성
- 자바에서는 다형성을 위해 **부모 클래스 타입의 참조 변수**로 **자식 클래스 타입의 인스턴스를 참조**할 수 있도록 하고 있다.
- 이때, **참조 변수가 사용할 수 있는 멤버의 개수**가 **참조하는 인스턴스의 멤버 개수**보다 **같거나 적어야** 참조할 수 있다. 

  ```java
  class Parent { ... }
  class Child extends Parent { ... }
  ...
  Parent pa = new Parent(); // 허용
  Child ch = new Child(); // 허용
  
  Parent pc = new Child(); // 허용
  
  Child cp = new Parent(); // 오류 발생
  ```
  - 당연히 **같은 타입**의 인스턴스는 참조할 수 있다.
    - 참조 변수가 사용할 수 있는 멤버의 개수가 실제 인스턴스의 **멤버 개수와 같기** 때문이다.
  - **부모 클래스 타입**의 참조 변수로도 **자식 클래스 타입의 인스턴스를 참조**할 수 있다.
    - 참조 변수가 사용할 수 있는 멤버의 개수가 실제 인스턴스의 **멤버 개수보다 적기** 때문이다.
  - 하지만, <u>자식 클래스 타입의 참조 변수로는 부모 클래스 타입의 인스턴스를 참조할 수 없다.</u>
    - 참조 변수가 사용할 수 있는 멤버의 개수가 실제 인스턴스 **멤버 개수보다 많기** 때문이다.
    
## 참조 변수의 형 변환 조건
- 서로 **상속 관계**에 있는 클래스 사이에만 형 변환을 할 수 있다.
- **자식 클래스 타입에서 부모 클래스 타입으로의 형 변환**은 **생략**할 수 있다.
  
  ```java
  class Parent { ... }
  class Child extends Parent { ... }
  ...
  Parent pa01 = null;
  Child ch = new Child();
  
  pa01 = ch; // pa01 = (Parent)ch;와 같으며, 타입 변환을 생략할 수 있음
  ```
  - 더 '큰 그릇'인 부모에 '작은 그릇'인 자식을 담을 수 있음.
  
- 하지만, **부모 클래스 타입에서 자식 클래스 타입으로의 형 변환**은 **반드시 명시**해야 한다.

  ```java
  ch = (Child)pa01; // 타입 변환을 생략할 수 없음
  ```
  - '작은 그릇'인 자식에 '큰 그릇'인 부모를 담을 수 없음.


## 참조 변수의 형 변환
- 부모 타입으로 자식 객체를 참조할 수 있다.
- 부모 타입으로 자식 객체를 참조하게 되면(가리키게 되면), **부모가 가지고 있는 메소드만 사용**할 수 있다.

  ```java
  // 부모 클래스
  public class Car {
    public void run() {
      System.out.println("Car의 run 메소드");
    }
  }
  
  // 자식 클래스
  public class Bus extends Car {
    public void ppangppang() {
      System.out.println("빵빵");
    }
  }
  
  public class BusExam {
    public static void main(String[] args) {
      // 부모 타입으로 자식 객체 참조
      Car car = new Bus(); 
      
      car.run(); // 부모의 메소드 참조 가능
      car.ppangppang(); // **자식 메소드 참조 시, 컴파일 오류 발생
    }
  }
  ```

- 자식 객체가 가지고 있는 메소드나 속성을 사용하고 싶다면 **형 변환**을 해야 한다.

  ```java
  // 부모 타입을 자식 타입으로 형 변환
  Bus bus = (Bus)car;
  bus.run();
  bus.ppangppang();
  ```
  - ppangppang() 메소드를 호출하고 싶다면, Bus 타입의 참조 변수로 참조해야 한다.
  
- Bus는 Car이기도 함. 따라서 Car로 Bus를 가리킬 수 있음.
- 하지만, Car는 Truck일 수도 있고, Sports Car일 수도 있다. 따라서 Bus로 Car를 가리킬 수 없다.
  - Truck을 Bus라고 가리킬 수 없다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 클래스 형변환](https://programmers.co.kr/learn/courses/5/lessons/193)
- [코딩의 시작, TCP School \| JAVA \| 다형성의 개념](https://www.tcpschool.com/java/java_polymorphism_concept)
