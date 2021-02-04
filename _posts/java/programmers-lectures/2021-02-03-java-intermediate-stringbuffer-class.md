---
title: "[프로그래머스 자바 중급] java.lang 패키지 : 스트링버퍼 클래스(StringBuffer Class)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java.lang패키지
  - stringbuffer
  - 자바중급
---

## StringBuffer 클래스
- String 클래스와 달리 StringBuffer 클래스의 인스턴스는 **값을 변경하고 추가할 수 있다**.
- 내부적으로 **버퍼(buffer)**라고 하는 **독립적인 공간**을 가진다.
  - 버퍼 크기의 기본값은 **16개의 문자**를 저장할 수 있는 크기이며, 생성자를 통해 그 크기를 별도로 설정할 수 있다.
  - 인스턴스 생성 시 사용자가 설정한 크기보다 16개의 문자를 더 저장할 수 있도록 여유 있는 크기로 생성된다.
- java.lang 패키지에 포함되어 제공된다.

## 불변 클래스(immutable class)와 가변 클래스(mutable class)
- String 클래스와 같이 인스턴스가 한 번 생성되면 그 값을 변경할 수 없는 클래스를 **불변 클래스(immutable class)**라고 한다.
- 반대로, StringBuffer 클래스와 같이 자유롭게 인스턴스의 값을 변경할 수 있는 클래스를 **가변 클래스(mutable class)**라고 한다.

- 멀티 스레드 환경에서 객체가 변화되는 상황이라면 불변 인스턴스를 사용하는 것이 좀 더 신뢰할 수 있는 코드를 작성할 수 있다. 
  - 즉, **각각의 객체가 서로 영향을 주어서는 안 되는 경우**에 불변 인스턴스를 사용하면 값이 변하지 않는다는 점이 보장된다.
  
## append() 메소드
- 인수로 전달된 값을 문자열로 변환 후, 문자열의 마지막에 추가.
- String 클래스의 concat() 메소드와 같은 결과를 반환하지만, 내부적인 처리 속도가 훨씬 빠르다.

- ex) 한 문자열에 다른 문자열을 추가

  ```java
  StringBuffer str = new StringBuffer("Java");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : Java
  
  System.out.println(str.append("수업")); // Java수업
  // 원본 인스턴스의 값이 변경
  System.out.println("메소드 호출 후 원본 문자열 : " + str); // Java수업
  ```
  
## capacity() 메소드
- StringBuffer 인스턴스의 현재 버퍼 크기를 반환.

- ex) StringBuffer 인스턴스의 현재 버퍼 크기를 알아보기

  ```java
  StringBuffer str01 = new StringBuffer();
  StirngBuffer str02 = new StringBuffer("Java");
  
  System.out.println(str01.capacity()); // 16
  System.out.println(str02.capacity()); // 20
  ```
  - 길이가 4인 문자열로 StringBuffer 인스턴스를 생성하면, 기본적으로 생성되는 여유 버퍼 크기인 16에 문자의 길이를 더한 총 20개의 문자를 저장할 수 있는 버퍼가 생성되는 것을 확인할 수 있다.

## delete() 메소드
- 인수로 전달된 인덱스에 해당하는 부분 문자열을 문자열에서 제거
  - delete(int start, int end)
  - 첫 번째 매개변수로 전달된 인덱스부터 **두 번째 매개변수로 전달된 인덱스 바로 앞의 문자**까지를 삭제.
- 또한, **deleteCharAt(int index)** 메소드를 사용하면 특정 위치의 문자 한 개만을 제거할 수도 있다.

- ex) 문자열의 특정 부분을 제거

  ```java
  StringBuffer str = new StringBuffer("Java Oracle");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : Java Oracle
  
  // 인덱스가 4인 위치의 문자부터 7인 문자까지 삭제
  System.out.println(str.delete(4, 8)); // Javacle
  // 인덱스가 1인 위치의 문자 한 개 삭제
  System.out.println(str.deleteCharAt(1)); // Jvacle
  System.out.println("메소드 호출 후 원본 문자열 : " + str); // Jvacle
  ```

## insert() 메소드
- 인수로 전달된 값을 문자열로 변환한 후, 문자열의 지정된 인덱스 위치에 추가.
- 전달된 인덱스가 문자열의 길이와 같으면, append() 메소드와 같은 결과를 반환.

- 문자열 중간에 다른 문자열을 삽입

  ```java
  StringBuffer str = new StringBuffer("Java 만세");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : Java 만세
  
  // 인덱스가 4인 위치부터 두 번째 매개변수로 전달된 문자열을 추가
  System.out.println(str.insert(4, "Script")); // JavaScript 만세
  System.out.println("메소드 호출 후 원본 문자열 : " + str); // JavaScript 만세
  ```
  
## 메소드 체이닝(method chaining)
- 자기 자신의 메소드를 호출하여 자기 자신의 값을 바꿔나가는 것을 메소드 체이닝이라고 한다.
- StringBuffer 클래스는 메소드 체인 방식으로 사용할 수 있도록 만들어져 있다.

  ```java
  String str2 = new StringBuffer().append("hello").append(" ").append("world").toString();
  ```
  - StringBuffer 클래스가 가진 toString() 메소드를 이용하여 String 객체로 반환했다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 스트링버퍼](https://programmers.co.kr/learn/courses/9/lessons/253)
- [코딩의 시작, TCP School \| JAVA \| StringBuffer 클래스](https://www.tcpschool.com/java/java_api_stringBuffer)
