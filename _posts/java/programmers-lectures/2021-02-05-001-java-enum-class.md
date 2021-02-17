---
title: "[자바] java.lang 패키지 : Enum 클래스"
layout: single
related: true
categories:
  - JAVA
tags:
  - java.lang패키지
  - enum
---

## Enum 클래스
- JDK 1.5부터는 열거체를 정의한 Enum 클래스를 사용할 수 있다.
- **모든 자바 열거체의 공통된 조상 클래스**.
- 열거체를 조작하기 위한 다양한 메소드가 포함되어 있다.

## values() 메소드
- 해당 **열거체의 모든 상수를 저장한 배열**을 생성하여 반환.
- 자바의 모든 열거체에 컴파일러가 자동으로 추가해주는 메소드.

  ```java
  enum Rainbow { RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET }
  
  public class Enum01 {
    public static void main(String[] args) {
      Rainbow[] arr = Rainbow.values();
      
      for(Rainbow rb : arr) {
        // RED ORANGE YELLOW GREEN BLUE INDIGO VIOLET 
        System.out.print(rb + " ");
      }
    }
  }
  ```
  
## valueOf() 메소드
- 전달된 **문자열과 일치하는 해당 열거체 상수를 반환**.

  ```java
  enum Rainbow { RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET }
  
  public class Enum02 {
    public static void main(String[] args) {
      Rainbow rb = Rainbow.valueOf("GREEN");
      System.out.println(rb); // GREEN
    }
  }
  ```
  
## ordinal() 메소드
- 해당 열거체 상수가 열거체 정의에서 **정의된 순서(0부터 시작)를 반환**.
- 이때 반환되는 값은 열거체 정의에서 해당 열거체 상수가 정의된 **순서**이며, **상숫값 자체가 아님을 주의**.

  ```java
  enum Rainbow { RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET }
  
  public class Enum02 {
    public static void main(String[] args) {
      int idx = Rainbow.YELLOW.ordinal();
      System.out.println(idx); // 2
    }
  }
  ```
  
## 그 외 대표적인 Enum 클래스 메소드

  | 메소드 | 설명 |
  |:------|:------|
  | protected void finalize() | 해당 Enum 클래스가 final 메소드를 가질 수 없게 됨 |
  | String name() | 해당 열거체 상수의 이름을 반환 |
  
## 관련 포스트 - java.lang 패키지
- [Object 클래스와 오버라이딩(Overriding)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-object-class/)
- [래퍼 클래스(Wrapper Class)와 Boxing](https://seo2021.github.io/java/programmers-lectures/java-intermediate-wrapper-class-and-boxing/)
- [스트링 클래스(String Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-string-class/)
- [스트링버퍼 클래스(StringBuffer Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-stringbuffer-class/)
- [Math 클래스](https://seo2021.github.io/java/programmers-lectures/java-intermediate-math-class/)

## 출처
- [코딩의 시작, TCP School \| JAVA \| Enum 클래스](https://www.tcpschool.com/java/java_api_enum)
