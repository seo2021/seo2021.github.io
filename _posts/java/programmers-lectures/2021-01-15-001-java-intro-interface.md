---
title: \[프로그래머스 \| 자바 입문\] 인터페이스(Interface)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 인터페이스
---

## 인터페이스(interface)
- 서로 관계가 없는 물체들이 상호작용하기 위해 사용하는 장치나 시스템
- 인터페이스는 다른 클래스를 작성할 때 **기본이 되는 틀**을 제공하면서, 다른 클래스 사이의 **중간 매개 역할**까지 담당하는 
**일종의 추상 클래스**이다.
- 생성자, 필드, 일반 메소드도 포함할 수 있는 추상 클래스와 다르게 인터페이스는 **추상메소드와 상수만을 포함**할 수 있다.

## 인터페이스의 정의
- **추상 메소드**와 **상수**를 정의할 수 있다.

   ```java
   public interface TV {
     public int MAX_VOLUME = 100;
     public int MIN_VOLUME = 0;
     
     public void turnOn();
     public void turnOff();
     public void changeVolume(int volume);
     public void changeChannel(int channel);
   }
   ```
   
- 인터페이스에서 변수를 선언하면 **컴파일 시 자동으로** 아래와 같이 변경된다.

  ```java
  public static final int MAX_VOLUME = 100;
  public static final int MIN_VOLUME = 0;
  ```

- 인터페이스에서 정의된 메소드는 모두 추상 메소드이다. 선언된 메소드는 **컴파일 시 자동으로** 다음과 같이 변경된다.

  ```java
   public abstract void turnOn();
   public abstract void turnOff();
   public abstract void changeVolume(int volume);
   public abstract void changeChannel(int channel);
  ```

- 인터페이스의 모든 필드는 **public static final**이어야 하며, 모든 메소드는 **public abstract**이어야 한다.
  - 이 제어자는 모든 인터페이스 공통으로 적용되는 부분이므로 **생략 가능**.
  - 이렇게 생략된 제어자는 컴파일 시 자바 **컴파일러가 자동으로 추가**.
  
## 인터페이스의 구현
- 인터페이스를 추상 클래스와 마찬가지로 직접 인스턴스를 생성할 수는 없다.
- 따라서, 인터페이스의 **추상 메소드를 구현할 클래스를 작성**해야 한다.
- **implements** 키워드를 이용하여 구현한다.

  ```java
  public class LedTV implements TV {
  
    // 인터페이스의 메소드 오버라이딩
    public void turnOn() {
      System.out.println("켜다");
    }
    public void turnOff() {
      System.out.println("끄다");
    }
    public void changeVolume(int volume) {
      System.out.println(volume + "(으)로 볼륨조정하다.");
    }
    public void changeChannel(int channel) {
      System.out.println(channel + "(으)로 채널조정하다.");
    } 
  }
  ```

- **참조 변수의 타입으로 인터페이스**를 사용할 수 있다. 이 경우 **인터페이스가 가지고 있는 메소드만 사용**할 수 있다.

  ```java
  public class LedTvExam {
    public static void main(String[] args) {
      TV tv = new LedTV();
      
      tv.turnOn();
      tv.changeVolume(50);
      tv.changeChannel(6);
      tv.turnOff();
    }
  }
  ```
  
- 상속과 구현을 동시에 할 수도 있다.

  ```java
  public class 클래스명 extends 상위클래스명 implements 인터페이스명 { ... }
  ```

- 동일한 인터페이스를 구현한다는 것은 클래스 사용법이 같다는 것을 의미한다.
  - TV 인터페이스를 구현하는 LcdTV, OledTV 등을 생성했을 때, LedTV와 동일한 기능을 가진다.
  
- 💡 인터페이스가 가지고 있는 메소드를 하나라도 구현하지 않는다면, 해당 클래스는 **추상 클래스**가 된다.
  - abstract 키워드를 사용하여 추상 클래스로 선언해야 한다.
  
## 인터페이스를 이용한 다중 상속
- 클래스는 **인터페이스를 여러 개 구현**할 수 있다.

  ```java
  interface Animal { ... }
  interface Pet { ... }
  
  // 2개의 인터페이스를 동시에 구현
  class Cat implements Animal, Pet { ... }
  ```

- 자식 클래스가 여러 부모 클래스를 상속받는 다중 상속을 할 경우 메소드 출처의 모호성 등 여러가지 문제 발생 가능성 때문에
**자바에서는 클래스를 통한 다중 상속을 지원하지 않는다.**

  ```java
  class Animal { public void cry() {...} }
  
  // 상속받은 메소드 오버라이딩
  class Cat extends Animal { public void cry() {...} } 
  class Dog extends Animal { public void cry() {...} }
  
  class MyPet extends Cat, Dog {}
  ```
  - Cat 클래스와 Dog 클래스는 Animal 클래스를 상속받아 cry() 메소드를 오버라이딩하고 있다. 
  - MyPet 클래스가 Cat과 Dog 클래스를 다중 상속받게 되면서, MyPet 인스턴스가 cry() 메소드를 호출할 경우 **어느 클래스에서 상속받은 메소드인지 구분할 수 없는 모호성**을 지니게 된다.

- 하지만, **인터페이스를 다중 상속**을 하게 되면 메소드 호출의 모호성을 방지할 수 있다.

  ```java
  interface Animal { public abstract void cry(); }
  
  // 인터페이스를 상속받는 인터페이스
  interface Cat extends Animal { public abstract void cry(); } 
  interface Dog extends Animal { public abstract void cry(); }
  
  // 
  class MyPet implement Cat, Dog { public void cry() {...} }
  ```
  - 인터페이스에서는 메소드 구현부를 작성하지 않고, Cat, Dog 인터페이스를 구현한 MyPet 클래스에서만 cry() 메소드를 정의하므로
  앞에서 발생한 메소드 호출의 모호성이 없다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 인터페이스 만들기](https://programmers.co.kr/learn/courses/5/lessons/239)
- [코딩의 시작, TCP School \| JAVA \| 인터페이스](https://www.tcpschool.com/java/java_polymorphism_interface)
