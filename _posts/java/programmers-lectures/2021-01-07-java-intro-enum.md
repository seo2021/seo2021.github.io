---
title: \[프로그래머스 \| 자바 입문\] 열거형(Enum)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 열거형
  - Enum
---

## 자바는 열거 타입을 이용하여 변수를 선언할 때 변수타입으로 사용할 수 있다.
- 열거형은 JDK5에서 추가되었다.
- JDK5 이전에는 상수를 열거형 대신 사용
  - 상수를 이용하는 방법
  ```java
  public class EnumExam {
    
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
    - String으로 선언된



## 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [Kephi Javatory \| 4. Java 자바 - 연산자 종류, 연산자 우선순위](https://kephilab.tistory.com/28)
