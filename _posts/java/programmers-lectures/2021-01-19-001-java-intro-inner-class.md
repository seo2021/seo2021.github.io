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
- 클래스 안에 선언된 클래스
- 어느 위치에 선언하느냐에 따라 4가지 형태가 있다.
  1. 인스턴스 클래스(중첩 클래스)
    - 클래스 안에 인스턴스 변수, 즉 필드를 선언하는 위치에 선언되는 경우
    - ex) 내부에 있는 Cal 클래스의 객체를 생성하기 위해서는 외부 클래스인 InnerExam1의 객체를 만든 후에 `InnerExam.Cal cal = t.new Cal();`과
    같은 방법으로 Cal 객체를 생성한 후 사용한다.
    
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



## 추상 메소드(abstract method)
- 자식 클래스에서 반드시 **오버라이딩(overriding)**해야만 사용할 수 있는 메소드.
- 자바에서 추상 메소드를 선언하여 사용하는 **목적**은 추상 메소드가 포함된 클래스를 상속받는 **자식 클래스가 반드시 추상 메소드를 구현**하도록 하기 위함.
  - 자식 클래스는 추상 메소드를 구현해야만 인스턴스를 생성할 수 있으므로.
- 선언부만 존재하며, 구현부는 작성되어 있지 않다.
  - 내용이 없는 메소드. 즉, 구현이 되지 않은 메소드이다.
- 이 작성되어 있지 않은 **구현부를 자식 클래스에서 오버라이딩**하여 사용한다.

  > 메소드 오버라이딩(method overriding)  
  > - 상속받은 부모 클래스의 메소드를 재정의하여 사용하는 것.

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
  

 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 추상클래스](https://programmers.co.kr/learn/courses/5/lessons/188)
- [코딩의 시작, TCP School \| JAVA \| 추상 클래스](https://www.tcpschool.com/java/java_polymorphism_abstract)
- [코딩의 시작, TCP School \| JAVA \| 메소드 오버라이딩](https://www.tcpschool.com/java/java_inheritance_overriding)
