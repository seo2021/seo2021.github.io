---
title: "[프로그래머스 자바 중급] java.lang 패키지 : Math 클래스"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - java.lang패키지
  - math
  - 자바중급
---

## Math 클래스
- 수학에서 자주 사용하는 **상수들과 함수들을 미리 구현**해놓은 클래스.
- Math 클래스의 모든 메소드는 **클래스 메소드(static method)**이므로, **객체를 생성하지 않고도 바로 사용**할 수 있다.
  - **Math 클래스는 생성자가 private**로 되어 있기 때문에 **new 연산자를 이용하여 객체를 생성할 수 없다**.
- java.lang 패키지에 포함되어 제공된다.

- Math 클래스에 정의되어 있는 **클래스 필드**는 다음과 같다.
  1. **Math.E**: 오일러의 수라 불리며, 자연로그(natural logarithms)의 밑(base) 값으로 약 2.718을 의미.
  2. **Math.PI**: 원의 원주를 지금으로 나눈 비율(원주율) 값으로 약 3.14159를 의미.
  
# random() 메소드
- **0.0 이상 1.0 미만**의 범위에서 **임의의 double형 값**을 하나 생성하여 반환.
- 내부적으로 java.util 패키지의 Random 클래스
를 사용한 의사 난수 발생기(pseudorandom-number generator)를 사용하여 임의의 수를 생성한다.

- ex) 0부터 99까지의 난수를 생성

  ```java
  // Math 클래스의 random() 메소드
  System.out.println(int)(Math.random() * 100)); // 0 ~ 99
  
  // Random 클래스의 nextInt() 메소드
  Random ran = new Random();
  System.out.println(ran.nextInt(100)); // 0 ~ 99
  ```
  - **Math 클래스의 random() 메소드**뿐만 아니라, **java util 패키지에 포함된 Random 클래스의 nextInt() 메소드**를 사용해도 난수를 생성할 수 있다.

- ex) 특정 범위에 속하는 난수 생성

  ```java
  (int)(Math.random() * 6); // 0 ~ 5
  ((int)(Math.random() * 6) + 1); // 1 ~ 6
  ((int)(Math.random() * 6) + 3); // 3 ~ 8
  ```
  - 위와 같은 방법으로 난수 생성 범위를 조절할 수 있다.
  
## abs() 메소드
- 전달된 값이 **음수**이면 그 값의 **절댓값을 반환**하며, 전달된 값이 **양수**이면 **전달된 값을 그대로 반환**.

  ```java
  System.out.println(Math.abs(10)); // 10
  System.out.println(Math.abs(-10)); // 10
  System.out.println(Math.abs(-3.14)); // 3.14
  ```
  
## floor() 메소드와 ceil() 메소드, round() 메소드
- floor() 메소드는 인수로 전달받은 값과 **같거나 작은 수** 중에서 **가장 큰 정수**를 반환.
  - 각 실수 이하의 최대 정수를 구하는 함수.
- ceil() 메소드는 인수로 전달받은 값과 **같거나 큰 수** 중에서 **가장 작은 정수**를 반환.
  - 각 실수 이상의 최소 정수를 구하는 함수.
- round() 메소드는 전달받은 실수를 **소수점 첫째 자리에서 반올림한 정수**를 반환.

  ```java
  System.out.println(Math.floor(10.0)); // 10.0
  System.out.println(Math.floor(10.9)); // 10.0 -> 10.9 이하의 최대 정수
  
  System.out.println(Math.ceil(10.0)); // 10.0
  System.out.println(Math.ceil(10.1)); // 11.0 -> 10.1 이상의 최소 정수
  System.out.println(Math.ceil(10.000001)); // 11.0
  
  System.out.println(Math.round(10.0)); // 10
  System.out.println(Math.round(10.4)); // 10
  System.out.println(Math.round(10.5)); // 11
  ```
  
  - 💡 round() 함수를 활용하여 **소수 n번째 자리까지 나타내는 반올림**도 가능하다.
    - ex) 소수점 둘째 자리까지 나타내기
    
      ```java
      double pie = 3.14159265358979;
      System.out.println(Math.round(pie*100)/100.0); // 3.14
      ```
      - 3.14159265358979 * 100 = 314.159265358979
      - round(314.159265358979) = 314
      - 314 / 100 = 3.14
      
## pow() 메소드와 sqrt() 메소드
- **pow() 메소드**는 전달된 두 개의 double형 값을 가지고 **제곱 연산**을 수행한다.
  - 예를 들어 pow(a, b)는 a^b를 반환한다.
- 반대로, **sqrt() 메소드**는 전달된 double형 값의 **제곱근 값**을 반환한다.
  - 예를 들어, sqrt(a)는 √a를 반환한다.
  
  ```java
  System.out.println((int)Math.pow(5, 2)); // 25
  System.out.println((int)Math.sqrt(25)); // 5
  ```
  
## 그 외 대표적인 Math() 메소드

  | 메소드 | 설명 |
  |:------|:------|
  | static double rint(double a) | 전달된 double형 값과 가장 가까운 정수값을 double형으로 반환 |
  | max(), min() | 전달된 두 값을 비교하여 큰 값, 작은 값을 반환 |
  | static double sin(double a)<br/>static double cos(double a)<br/>static double tan(double a) | 전달된 double형 값에 해당하는 각각의 삼각 함숫값을 반환 |
  
## 관련 포스트 - java.lang 패키지
- [Object 클래스와 오버라이딩(Overriding)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-object-class/)
- [래퍼 클래스(Wrapper Class)와 Boxing](https://seo2021.github.io/java/programmers-lectures/java-intermediate-wrapper-class-and-boxing/)
- [스트링 클래스(String Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-string-class/)
- [스트링버퍼 클래스(StringBuffer Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-stringbuffer-class/)
- [Enum 클래스](https://seo2021.github.io/java/001-java-intermediate-enum-class/)
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Math](https://programmers.co.kr/learn/courses/9/lessons/261)
- [코딩의 시작, TCP School \| JAVA \| Math 클래스](https://www.tcpschool.com/java/java_api_math)
- [위키백과 \| 바닥 함수와 천장 함수](https://ko.wikipedia.org/wiki/바닥_함수와_천장_함수)
- [코딩팩토리 \| [Java] 자바 소수점 n번째 자리까지 반올림하기](https://coding-factory.tistory.com/250)
