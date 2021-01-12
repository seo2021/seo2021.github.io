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
    
    public Car(String name) {
    
    }
    
  }
  ```


## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 메소드 오버로딩](https://programmers.co.kr/learn/courses/5/lessons/170)
