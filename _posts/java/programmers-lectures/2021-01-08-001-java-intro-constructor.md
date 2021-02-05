---
title: "[프로그래머스 자바 입문] 생성자(Constructor)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - 생성자
  - 자바입문
---

## 💡 모든 클래스는 인스턴스화될 때 생성자를 사용한다.
- ex) `Car()` 부분이 생성자

  ```java
  public static void main(String[] args) {
    Car c1 = new Car();
  }
  ```

## 생성자의 특징
- 생성자는 리턴타입이 없다.
- 생성자를 프로그래머가 만들지 않으면, 매개변수가 없는 생성자가 컴파일할 때 자동으로 만들어진다.
- 매개변수가 없는 생성자를 **기본 생성자**라고 한다.
- <u>생성자를 하나라도 프로그래머가 만들었다면, 기본 생성자는 자동으로 만들어지지 않는다.</u>

## 생성자의 역할
- 생성자가 하는 일은 객체가 생성될 때 필드를 초기화하는 역할을 수행한다.
- ex) 자동차가 객체가 생성될 때 반드시 name을 가지도록 하려면, Car 클래스를 다음과 같이 만들어야 한다.

  ```java
  public class Car {
  
    String name;
    int number;
    
    // 생성자
    public Car(String n) {
      name = n; // 매개변수를 n을 받아서 name 속성에 대입
    }
  }
  ```
  
  - 위의 Car 클래스를 이용하여 Car 인스턴스를 생성하는 방법
  
    ```java
    public class CarExam2 {
    
      public static void main(String[] args) {
      
        // Car 객체를 생성할 때, name 필드를 초기화
        Car c1 = new Car("소방차");
        Car c2 = new Car("구급차");
        // Car c3 = new car(); // 컴파일 오류 발생(기본 생성자가 없으므로)
        
        System.out.println(c1.name); // 소방차
        System.out.println(c2.name); // 구급차
      }
    }
    ```
    
    - Car 클래스는 기본 생성자를 가지지 않으므로, 기본 생성자로 Car 객체를 생성할 수 없다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 생성자](https://programmers.co.kr/learn/courses/5/lessons/168)
