---
title: "[프로그래머스 자바 입문] 내부 클래스(Inner Class)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - 내부클래스
  - 익명클래스 
  - 자바입문
---

## 내부 클래스(inner class)란?
- 클래스 안에 선언된 클래스.

## 내부 클래스의 장점
- 내부 클래스에서 외부 클래스의 멤버에 손쉽게 접근 가능.
- 서로 관련 있는 클래스를 논리적으로 묶어서 표현함으로써, 코드의 캡슐화를 증가.
- 외부에서는 내부 클래스에 접근할 수 없으므로, 코드의 복잡성을 줄일 수 있다.

## 내부 클래스의 종류
- 어느 위치에 선언하느냐에 따라 4가지 형태가 있다.
  - **인스턴스 클래스(instance class, 중첩 클래스)**
    - 클래스 안에 인스턴스 변수, 즉 필드를 선언하는 위치에 선언
    - 주로 **외부 클래스의 인스턴스 변수나 인스턴스 메소드에 사용될 목적**으로 선언된다.
    - ex) 내부에 있는 Cal 클래스의 객체를 생성하기 위해서는 외부 클래스인 InnerExam1의 객체를 만든 후에 `t.new Cal();`과 같은 방법으로 Cal 객체를 생성한 후 사용한다.
    - 타입 선언은 `외부클래스.내부클래스`와 같이 한다.
    
    ```java
    public class InnerExam1 { // 외부 클래스
    
      class Cal { // 내부 클래스
        int value = 0;
        
        public void plus() {
          value++;
        }
      }
      
      public static void main(String[] args) {
        InnerExam1 t = new InnerExam1(); // 외부 클래스 객체 생성
        InnerExam1.Cal cal = t.new Cal(); // 외부 클래스 객체를 이용해 내부 클래스 객체 생성

        // 내부 클래스의 메소드와 필드 사용
        cal.plus();
        System.out.println(cal.value);
      }
    }
    ```
    
  - **정적 클래스(static class, 정적 중첩 클래스)**
    - 내부 클래스가 static으로 정의
    - 주로 **외부 클래스의 클래스 메소드에 사용될 목적**으로 선언된다.
    - ex) InnerExam2 객체를 생성할 필요 없이 `new InnerExam2.Cal()`로 객체를 생성할 수 있다.
    
    ```java
    public class InnerExam2 {
      
      static class Cal { // static 클래스
        int value = 0;
        
        public void plus() {
          value++;
        }
      }
      
      public static void main(String[] args) {
        // static 클래스이기 때문에 바로 접근해서 객체 생성
        InnerExam2.Cal cal = new InnerExam2.Cal();
        
        // 내부 클래스의 메소드 사용
        cal.plus();
        System.out.println(cal.value);
      }
    }
    ```
    
  - **지역 클래스(local class, 지역 중첩 클래스)**
    - 외부 클래스의 메소드 안에 클래스를 선언
    - 선언된 메소드 안에서만 해당 클래스를 이용할 수 있다.
    
    ```java
    public class InnerExam3 {

      public void exec() {
        // 지역 클래스
        class Cal {
          int value = 0;
          public void plus() {
            value++;
          }
        }
        // 메소드 내에서 클래스 사용
        Cal cal = new Cal();
        cal.plus();
        System.out.println(cal.value);
      }
      
      public static void main(String[] args) {
        InnerExam3 t = enw InnerExam3();
        t.exec(); // 외부 클래스의 메소드 호출함으로써, 메소드 내에 생성되어 있는 클래스 이용
      }
    }
    ```
  
  - **익명 클래스(anonymous class, 익명 중첩 클래스)**
    - 다른 내부 클래스와는 달리 **이름을 가지지 않는 클래스**.
    - 익명 클래스는 **클래스의 선언과 동시에 객체를 생성**하므로, **단 하나의 객체만을 생성**하는 일회용 클래스.
    - 따라서 생성자를 선언할 수도 없으며, 오로지 **단 하나의 클래스나 단 하나의 인터페이스를 상속받거나 구현**할 수 있다.
    - 매우 제한적인 용도에 사용되며, **구현해야 하는 메소드가 매우 적은 클래스를 구현할 때** 사용.
      - 상속받는 클래스를 만들 필요가 없을 경우.
      - 상속받는 클래스가 해당 클래스에서만 사용되고 다른 클래스에서는 사용되지 않는 경우.
    
    ```java
    // 익명 클래스는 선언과 동시에 생성하여 참조변수에 대입
    클래스이름 참조변수이름 = new 클래스이름() {
      // 메소드의 선언
    };
    ```
    
    ```java
    // 추상 클래스 Action
    public abstract class Action {
      public abstract void exec();
    }
    
    // 추상 클래스 Action을 상속받는 자식 클래스 MyAction
    public class MyAction extends Action {
      // 메소드 오버라이딩
      public void exec() {
        System.out.println("exec");
      }
    }
    
    // MyAction을 사용하는 클래스
    public class ActionExam {
      public static void main(String[] args) {
        Action action = new MyAction();
        action.exec(); // 오버라이딩한 메소드 사용
      }
    }
    
    // 자식 클래스인 MyAction을 만들지 않고, Action 클래스를 바로 상속받는 익명 클래스를 만들어서 사용
    public class ActionExam {
      public static void main(Strin[] args) {
        // 익명 클래스. Action 클래스를 상속받는 이름없는 객체를 만든다.
        Action action = new Action() {
          // 상속받은 메소드 구현
          public void exec() {
            System.out.println("exec");
          }
        };
        // 이름 없는 객체를 action이라는 참조변수가 참조
        action.exec();
      }
    }
    ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 내부클래스](https://programmers.co.kr/learn/courses/5/lessons/242)
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 익명클래스](https://programmers.co.kr/learn/courses/5/lessons/243)
- [코딩의 시작, TCP School \| JAVA \| 내부 클래스](https://www.tcpschool.com/java/java_usingClass_innerClass)
