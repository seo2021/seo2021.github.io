---
title: "[프로그래머스 자바 중급] java.lang 패키지 : 래퍼 클래스(Wrapper Class)와 Boxing"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java.lang패키지
  - wrapper
  - boxing
  - 자바중급
---

## 래퍼 클래스(wrapper class)
- 기본 타입 데이터를 객체로 포장해주는 클래스
- 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어준다.
- 이러한 래퍼 클래스는 모두 java.lang 패키지에 포함되어 제공된다.

- 자바의 기본 타입과 대응되는 래퍼 클래스

  | 기본 타입 | 래퍼 클래스 |
  |:----------|:----------|
  | byte | Byte |
  | short | Short |
  | int | **Integer** |
  | long | Long |
  | float | float |
  | double | Double |
  | char | **Character** |
  | boolean | Boolean |
  
## 박싱(boxing)과 언박싱(unboxing)
- 래퍼 클래스는 산술 연산을 위해 정의된 클래스가 아니므로, **인스턴스에 저장된 값을 변경할 수 없다**.
- 단지, 값을 참조하기 위해 새로운 인스턴스를 생성하고, 생성된 인스턴스의 값만을 참조할 수 있다.
- 기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하는 과정을 **박싱(boxing)**이라고 하고, 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 **언박싱(unboxing)**이라고 한다.

  ![박싱과 언박싱](/assets/images/java/boxing_unboxing.png)
  
## 오토 박싱(autoboxing)과 오토 언박싱(autounboxing)
- JDK 1.5부터는 박싱과 언박싱이 필요한 상황에서 **자바 컴파일러가 이를 자동으로 처리**해준다.
- 이렇게 **자동화된 박싱과 언박싱**을 오토 박싱과 오토 언박싱이라고 한다.

- ex) 박싱과 언박싱, 오토 박싱과 오토 언박싱의 차이

  ```java
  Integer num = new Integer(17); // 박싱
  int n = num.intValue(); // 언박싱
  System.out.println(n); // 17
  
  Character ch = 'X'; // Character ch = new Character('X'); - 오토박싱
  char c = ch; // char c = ch.charValue(); - 오토언박싱
  System.out.println(c); // X
  ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| java.lang 패키지/오토박싱](https://programmers.co.kr/learn/courses/9/lessons/251)
- [코딩의 시작, TCP School \| JAVA \| Wrapper 클래스](https://www.tcpschool.com/java/java_api_wrapper)
