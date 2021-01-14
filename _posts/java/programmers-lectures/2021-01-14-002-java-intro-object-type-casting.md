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
- 이때, 참조 변수가 사용할 수 있는 멤버의 개수가 실제 인스턴스의 멤버 개수보다 같거나 적어야 참조할 수 있다. 

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

## 참조 변수의 형 변환
- 부모 타입으로 자식 객체를 참조할 수 있다.
- 부모 타입으로 자식 객체를 참조하게 되면, **부모가 가지고 있는 메소드만 사용**할 수 있다.

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
      car.run();
      car.ppangppang(); // 컴파일 오류 발생
    }
  }
  ```

- 자식 객체가 가지고 있는 메소드나 속성을 사용하고 싶다면 **형 변환**을 해야 한다.

  ```java
  public class BusExam {
    public static void main(String[] args) {
      // 부모 타입으로 자식 객체 참조
      Car car = new Bus(); 
      car.run();
      // car.ppangppang(); // 컴파일 오류 발생
      
      // 부모 타입을 자식 타입으로 형 변환
      Bus bus = (Bus)car;
      bus.run();
      bus.ppangppang();
    }
  }
  ```
  - ppangppang() 메소드를 호출하고 싶다면, Bus 타입의 참조 변수로 참조해야 한다.
- 객체들끼리도 형 변환이 가능하다. 단, 상속관계에 있을 때만 가능하다.
- 부모 타입으로 자식 타입의 객체를 참조할 때는 묵시적으로 형변환이 일어난다.
- 부모 타이



    
  




## 추상 메소드(abstract method)
- 자식 클래스에서 반드시 **오버라이딩(overriding)**해야만 사용할 수 있는 메소드.
- 자바에서 추상 메소드를 선언하여 사용하는 **목적**은 추상 메소드가 포함된 클래스를 상속받는 **자식 클래스가 반드시 추상 메소드를 구현**하도록 하기 위함.
  - 자식 클래스는 추상 메소드를 구현해야만 인스턴스를 생성할 수 있으므로.
- 선언부만 존재하며, 구현부는 작성되어 있지 않다.
  - 내용이 없는 메소드. 즉, 구현이 되지 않은 메소드이다.
- 이 작성되어 있지 않은 **구현부를 자식 클래스에서 오버라이딩**하여 사용한다.

  > 메소드 오버라이딩(method overriding)  
  > - 상속받은 부모 클래스의 메소드를 재정의하여 사용하는 것.

## 추상 클래스(abstract class)
- 하나 이상의 추상 메소드를 포함하는 클래스.
- 반드시 사용되어야 하는 메소드를 추상 클래스에서 추상 메소드로 선언해 놓으면, 이 클래스를 **상속받는 모든 클래스**에서는 이 **추상 메소드를 반드시 재정의**해야 한다.
- 추상 클래스는 동작이 정의되어 있지 않은 추상 메소드를 포함하고 있으므로, **인스턴스를 생성할 수 없다**.
  - 추상 클래스를 상속받은 자식 클래스에서 모든 추상 메소드를 오버라이딩하고 나서야 **자식 클래스의 인스턴스를 생성**할 수 있다.

## 추상 클래스 정의하기
- 클래스 앞에 abstract 키워드를 이용해서 정의한다.
- 추상 메소드는 리턴 타입 앞에 abstract 키워드를 붙인다.

  ```java
  public abstract class Bird { // 추상 클래스
    
    public abstract void sing(); // 추상 메소드
    
    public void fly() { // 일반 메소드
      System.out.println("날다.");
    }
  }
  ```
  💡 추상 클래스는 추상 메소드를 포함하고 있다는 점을 제외하면, 일반 클래스와 모든 점이 같다. 즉, 생성자와 필드, 일반 메소드도 포함할 수 있다.
  
## 추상 클래스를 상속받는 클래스 생성하기
- 추상 클래스를 상속받은 클래스는 추상 클래스가 갖고 있는 **추상 메소드를 반드시 구현**해야 한다.
- 추상 클래스를 상속받고, 추상 클래스가 갖고 있는 **추상 메소드를 구현하지 않으면 해당 클래스도 추상 클래스**가 된다.

  ```java
  public class Duck extends Bird { // 추상 클래스인 Bird 상속받음
  
    @Override
    public void sing() { // 상속받은 추상 메소드 오버라이딩
      System.out.println("꽥꽥");
    }
  }
  ```

## 사용하기
- 추상 클래스인 Bird는 객체를 생성할 수 없으므로, 이를 상속받은 자식 클래스인 Duck의 객체를 생성하여 사용한다.

  ```java
  public class DuckExam {
    public static void main(String[] args) {
    
      // Bird b = new Bird(); // 추상 클래스는 객체 생성 불가
    
      Duck duck = new Duck(); // 자식 클래스의 객체 생성
      duck.sing(); // 오버라이딩한 추상 메소드
      duck.fly(); // 상속받은 일반 메소드
    }
  }
  ```
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 추상클래스](https://programmers.co.kr/learn/courses/5/lessons/188)
- [코딩의 시작, TCP School \| JAVA \| 추상 클래스](https://www.tcpschool.com/java/java_polymorphism_abstract)
- [코딩의 시작, TCP School \| JAVA \| 메소드 오버라이딩](https://www.tcpschool.com/java/java_inheritance_overriding)
