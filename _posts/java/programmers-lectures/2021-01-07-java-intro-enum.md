---
title: \[프로그래머스 \| 자바 입문\] 열거형(Enum)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 열거형
  - Enum
  - 상수
---

## 자바는 변수를 선언할 때, 열거 타입을 변수 타입으로 사용할 수 있다
- 열거형은 JDK5에서 추가되었다.
- JDK5 이전에는 상수를 열거형 대신 사용

## 열거형 대신 상수를 사용하는 방법
  ```java
  public class EnumExam {
    
    // 상수 선언
    public static final String MALE = "MALE";
    public static final String FEMALE = "FEMALE";
    
    public static void main(String[] args) {
      
      String gender1;
      
      gender1 = EnumExam.MALE;
      gender1 = EnumExam.FEMALE;
    }
  }
  ```
- 상수를 사용했을 때 문제점
  - String으로 선언된 gender1이 MALE, FEMALE 둘 중 한 가지 값만 갖게 하고 싶을 때, gender1의 type이 String이기 때문에 'gender1 = "BOY";' 이렇게 수행되어도 전혀 문제가 되지 않는다.
  - 따라서 실행할 때, 원했던 값인 MALE, FEMALE이 아닌 다른 값이 들어오게 되므로 문제를 발생시킬 수 있다.

## 열거형의 사용
- 위와 같은 문제를 발생시키지 않기 위해 열거형을 사용
- 열거형의 정의 방법

  ```java
  enum Gender {
    MALE, FEMALE; // 넣고 싶은 값만 열거
  }
  ```

- 열거형 사용 방법

  ```java
  Gender gender2;

  // Gender 타입의 변수에는 MALE이나 FEMALE만 대입 가능. 다른 값은 저장할 수 없다.
  gender2 = Gender.MALE;
  gender2 = Gender.FEMALE;
  ```

## 💡 특정 값만 가져야 한다면 열거형을 사용하는 것이 좋다
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 열거형(enum)](https://programmers.co.kr/learn/courses/5/lessons/423)
