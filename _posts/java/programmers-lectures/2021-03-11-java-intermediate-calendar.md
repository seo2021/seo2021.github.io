---
title: "[프로그래머스 자바 중급] 날짜와 시간 : Calendar"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - calendar
  - 자바중급
---

## 자바에서의 날짜 및 시간 처리
- **JDK 1.0**에서는 **`Date` 클래스**를 사용하여 **날짜**에 관한 간단한 처리를 수행할 수 있었으나, 현재 `Date` 클래스 대부분의 메소드는 **사용을 권장하지 않고(deprecated) 있다**.
- **JDK 1.1부터**는 새롭게 제공되는 **`Calendar` 클래스**를 이용하여 **날짜와 시간**에 관한 처리를 수행.
  - 하지만, `Calendar` 클래스는 다음과 같은 **문제점**이 있다.
    1. `Calendar` 인스턴스는 불변 객체(immutable object)가 아니라서 **값이 수정될 수 있다**.
    2. 윤초(leap second)와 같은 **특별한 상황을 고려하지 않는다**.
    3. 월(month)을 나타낼 때, 1월부터 12월을 **0부터 11까지로 표현**해야 하는 불편함이 있다. 

  - 따라서, 더 나은 성능의 **Joda-Time**이라는 라이브러리를 함께 사용.
    - **Java SE 8** 버전에서는 **Joda-Time 라이브러리를 발전**시킨 새로운 날짜와 시간 API인 **`java.time` 패키지**를 제공.
    - `java.time` 패키지는 위와 같은 문제점을 모두 해결했으며, 다양한 기능을 지원하는 다수의 하위 패키지를 포함하고 있다.

## java.util.Calendar 클래스
- 자바에서 **날짜와 시간**에 관한 데이터를 손쉽게 처리할 수 있도록 제공하는 **추상 클래스**.
  - 추상 클래스로 선언된 이유는 나라마다 사용하는 달력 체계가 조금씩 다를 수 있기 때문이다.
- 날짜와 시간을 처리하기 위한 다양한 필드와 메소드가 포함되어 있다.
- **현재 날짜와 시간**에 대한 정보를 가진다.
- `Date`의 단점을 보완하기 위해 등장
- 모든 필드는 **클래스 변수(static variable)**이므로, **인스턴스를 생성하지 않고도 바로 사용**할 수 있다. 
 
## Calendar 클래스의 인스턴스 생성
- `Calendar` 클래스는 추상 클래스이므로, **직접 인스턴스를 생성할 수 없다**.
- `Calendar` 클래스가 가지고 있는 클래스 메소드 `getInstance()`를 사용해 **`GregorianCalendar` 클래스의 인스턴스를 생성하여 사용**한다.
  - `getInstance()` 메소드를 호출하면 내부적으로 `java.util.GregorianCalendar` 인스턴스를 만들어 반환한다.
  
  ```java
  Calendar cal = Calendar.getInstance();
  ```

  >- GregorianCalendar 클래스
  >    - 현재 전 세계적으로 많이 사용되는 달력으로, 1582년 교황 그레고리오 13세가 개혁한 그레고리오 달력.
  >    - 추상 클래스인 Calendar 클래스를 상속받아, 그레고리오 달력을 완전히 구현한 하위 클래스.

## add() 메소드
- 전달된 `Calendar` 필드에서 **일정 시간 만큼을 더하거나 빼준다**.
- 즉, 특정 시간을 기준으로 **일정 시간 전후의 날짜와 시간**을 알 수 있다.

- ex) 현재 시각에 120초를 더하기

  ```java
  Calendar time = Calendar.getInstance();
  System.out.println(time.getTime()); // Thu Feb 16 08:57:29 KST 2017
  
  time.add(Calendar.SECOND, 120);
  System.out.println(time.getTime()); // Thu Feb 16 08:59:29 KST 2017
  ```
  
## before()와 after() 메소드
- 두 시간 사이의 **전후 관계**를 알고 싶을 때 사용.
- **`before()`** 메소드는 **현재 `Calendar` 인스턴스**가 전달된 객체가 나타내는 시간보다 **앞서는지** 판단.
- **`after()`** 메소드는 **현재 `Calendar` 인스턴스**가 전달된 객체가 나타내는 시간보다 **나중인지**를 판단.

  ```java
  Calendar time1 = Calendar.getInstance(); // 현재
  Calendar time2 = Calendar.getInstance();
  Calendar time3 = Calendar.getInstance();
  
  time2.set(1982, 2, 19);
  time3.set(2022, 2, 19);
  
  System.out.println(time1.before(time2)); // false, time1이 time2보다 앞서지 않는다.
  System.out.println(time1.before(time3)); // true, time1이 time3보다 앞선다.
  ```
  
## get() 메소드
- 전달된 `Calendar` 필드에 저장된 값을 반환.

  ```java
  Calendar time = Calendar.getInstance();
  
  System.out.println(time.getTime()); // Thu Feb 16 08:57:44 KST 2017 -> 현재 날짜와 시간
  System.out.println(time.get(Calendar.DAY_OF_WEEK)); // 5 -> 목요일(1~7, 일~토)
  System.out.println(time.get(Calendar.MONTH) + 1); // 2 -> 2월(0부터 시작)
  System.out.println(time.get(Calendar.DAY_OF_MONTH)); // 16 -> 16일
  System.out.println(time.get(Calendar.HOUR_OF_DAY)); // 8 -> 8시(24시간제)
  System.out.println(time.get(Calendar.MINUTE)); // 57 -> 57분
  System.out.println(time.get(Calendar.SECOND)); // 44 -> 44초
  System.out.println(time.get(Calendar.YEAR)); // 2017 -> 2017년
  ```
  
## roll() 메소드

  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Calendar](https://programmers.co.kr/learn/courses/9/lessons/264)
- [코딩의 시작, TCP School \| JAVA \| Calendar 클래스](https://www.tcpschool.com/java/java_api_calendar)
