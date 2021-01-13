---
title: \[프로그래머스 \| 자바 입문\] 추상 클래스(Abstract Class)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - abstract
---

## 추상 메소드(abstract method)
- 자식 클래스에서 반드시 **오버라이딩(overriding)**해야만 사용할 수 있는 메소드.
- 자바에서 추상 메소드를 선언하여 사용하는 **목적**은 추상 메소드가 포함된 클래스를 상속받는 **자식 클래스가 반드시 추상 메소드를 구현**하도록
하기 위함.
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
  💡 추상 클래스는 추상 메소드를 포함하고 있다는 점을 제외하면, 일반 클래스와 모든 점이 같다.  
  즉, 생성자와 필드, 일반 메소드도 포함할 수 있다.

## 💡 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [코딩의 시작, TCP School \| JAVA \| 추상 클래스](https://www.tcpschool.com/java/java_polymorphism_abstract)
- [코딩의 시작, TCP School \| JAVA \| 메소드 오버라이딩](https://www.tcpschool.com/java/java_inheritance_overriding)
