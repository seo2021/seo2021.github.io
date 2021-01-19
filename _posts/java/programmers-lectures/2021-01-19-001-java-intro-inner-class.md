---
title: \[프로그래머스 \| 자바 입문\] 내부 클래스(Inner Class)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 내부클래스
---

## 내부 클래스(inner class)란?
- 클래스 안에 선언된 클래스.

## 내부 클래스의 장점
- 내부 클래스에서 외부 클래스의 멤버에 손쉽게 접근 가능.
- 서로 관련 있는 클래스를 논리적으로 묶어서 표현함으로써, 코드의 캡슐화를 증가.
- 외부에서는 내부 클래스에 접근할 수 없으므로, 코드의 복잡성을 줄일 수 있다.

## 내부 클래스의 종류
- 어느 위치에 선언하느냐에 따라 4가지 형태가 있다.
  - 인스턴스 클래스(instance class, 중첩 클래스)
    - 클래스 안에 인스턴스 변수, 즉 필드를 선언하는 위치에 선언
    - 주로 외부 클래스의 인스턴스 변수나 인스턴스 메소드에 사용될 목적으로 선언된다.
    - ex) 내부에 있는 Cal 클래스의 객체를 생성하기 위해서는 외부 클래스인 InnerExam1의 객체를 만든 후에 `InnerExam.Cal cal = t.new Cal();`과 같은 방법으로 Cal 객체를 생성한 후 사용한다.
    
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
        InnerExam1.Cal cal = t.new Cal(); // 내부 클래스 객체 생성

        // 내부 클래스의 메소드 사용
        cal.plus();
        System.out.println(cal.value);
      }
    }
    ```
    
  - static 클래스(static class, 정적 중첩 클래스)
    - 내부 클래스가 static으로 정의
    - 주로 외부 클래스의 클래스 메소드에 사용될 목적으로 선언된다.
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
        InnerExam2.Cal cal = new InnerExam2.Cal(); // 내부 클래스 객체 생성
        
        // 내부 클래스의 메소드 사용
        cal.plus();
        System.out.println(cal.value);
      }
    }
    ```
    
  - 지역 클래스(local class, 지역 중첩 클래스)
    - 외부 클래스의 메소드 안에 클래스를 선언
    - 메소드 안에서 해당 클래스를 이용할 수 있다.
    
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
        
        Cal cal = new Cal();
        cal.plus();
        System.out.println(cal.value);
      }
      
      public static void main(String[] args) {
        InnerExam3 t = enw InnerExam3();
        t.exec(); // 외부 클래스의 메소드 호출
      }
    }
    ```
  
  - 익명 클래스

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 내부클래스](https://programmers.co.kr/learn/courses/5/lessons/242)
- [코딩의 시작, TCP School \| JAVA \| 내부 클래스](https://www.tcpschool.com/java/java_usingClass_innerClass)
