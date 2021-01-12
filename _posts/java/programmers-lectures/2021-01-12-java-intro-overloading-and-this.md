---
title: \[프로그래머스 \| 자바 입문\] 생성자 오버로딩(Constructor Overloading)과 this()
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
    
    public Car() {}
    
    public Car(String name) {
      this.name = name;
    }
    
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
      Car c1 = new Car(); // 기본 생성자
      Car c2 = new Car("소방차"); // String 매개변수 1개
      Car c3 = new Car("구급차", 1234); // String, int 매개변수 2개
    }
  }
  ```
  
## 자기 자신의 생성자를 호출하는 this()
- 기본 생성자를 호출했을 때, name을 "이름없음", number를 "0"으로 초기화하기

  ```java
  public Car() {
    this.name = "이름없음";
    this.number = 0;
  }
  ```
  
- 위처럼 작성할 경우 코드의 중복이 일어난다.
  - String, int 인자 2개를 가지는 생성자가 이미 있다.
- 'this()'를 사용
  - 'this()'는 자기 자신의 생성자를 의미
  - 입력한 매개변수의 유형과 개수에 맞는 생성자가 알아서 호출
  - 비슷한 코드를 중복해서 작성하는 것을 방지할 수 있다.

  ```java
  public Car() {
    this("이름없음", 0);
  }
  ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 생성자 오버로딩과 this](https://programmers.co.kr/learn/courses/5/lessons/171)
