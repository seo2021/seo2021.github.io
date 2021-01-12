---
title: \[프로그래머스 \| 자바 입문\] 생성자 오버로딩과 this(Constructor Overloading and \"this\")
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 오버로딩
  - overloading
  - 생성자
  - constructor
  - this
---

## 생성자 오버로딩
- 생성자의 매개변수 유형과 개수를 다르게 하여 같은 이름의 생성자를 여러 개 가질 수 있다.

  ```java
  public class Car {
    String name;
    int number;
    
    // 기본 생성자
    public Car() {}
    
    // String 매개변수 1개
    public Car(String name) {
      this.name = name;
    }
    
    // String, int 매개변수 2개
    public Car(String name, int number) {
      this.name = name;
      this.number = number;
    }
  }
  ```
  
- 오버로딩된 생성자 이용하기

  ```java
  public class CarExam4 {
  
    public static void main(String args[]) {
      Car c1 = new Car();
      Car c2 = new Car("소방차");
      Car c3 = new Car("구급차", 1234);
    }
  }
  ```
  
## this()
- 기본 생성자를 호출했을 때, name을 "이름없음", number를 0으로 초기화하기

  ```java
  public Car() {
    this.name = "이름없음";
    this.number = 0;
  }
  ```
  
- 위처럼 작성할 경우 코드의 중복이 일어난다.
- 자신이 가지고 있는 다른 생성자를 이용할 수 있다.

  ```java
  public Car() {
    this("이름없음", 0);
  }
  ```
  
  - 자기 자신의 생성자를 호출함으로써 비슷한 코드가 중복되어 나오는 것을 방지할 수 있다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 생성자 오버로딩과 this](https://programmers.co.kr/learn/courses/5/lessons/171)
