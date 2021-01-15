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
- 자식 클래스가 여러 부모 클래스를 상속받는 다중 상속을 할 경우 메소드 출처의 모호성 등 여러가지 문제 발생 가능성 때문에
자바에서는 클래스를 통한 다중 상속을 지원하지 않는다.
- 하지만, **인터페이스를 통해 다중 상속**을 지원하고 있다.
- 인터페이스는 다른 클래스를 작성할 때 **기본이 되는 틀**을 제공하면서, 다른 클래스 사이의 **중간 매개 역할**까지 담당하는 
**일종의 추상 클래스**이다.
- 생성자, 필드, 일반 메소드도 포함할 수 있는 추상 클래스와 다르게 인터페이스는 **추상메소드와 상수만을 포함**할 수 있다.

## 인터페이스의 정의
- 추상 메소드와 상수를 정의할 수 있다.

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
   
- 인터페이스에서 변수를 선언하면 컴파일 시 자동으로 아래와 같이 변경된다.

  ```java
  public static final int MAX_VOLUME = 100;
  public static final int MIN_VOLUME = 0;
  ```

- 인터페이스에서 정의된 메소드는 모두 추상 메소드이다. 선언된 메소드는 컴파일 시 다음과 같이 자동으로 변경된다.

  ```java
   public abstract void turnOn();
   public abstract void turnOff();
   public abstract void changeVolume(int volume);
   public abstract void changeChannel(int channel);
  ```

- 인터페이스의 모든 필드는 **public static final**이어야 하며, 모든 메소드는 **public abstract**이어야 한다.
  - 이 제어자는 모든 인터페이스 공통으로 적용되는 부분이므로 생략 가능.
  - 이렇게 생략된 제어자는 컴파일 시 자바 컴파일러가 자동으로 추가.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 인터페이스 만들기](https://programmers.co.kr/learn/courses/5/lessons/239)
- [코딩의 시작, TCP School \| JAVA \| 인터페이스](https://www.tcpschool.com/java/java_polymorphism_interface)
