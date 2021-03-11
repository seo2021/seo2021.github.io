---
title: "[프로그래머스 자바 중급] 날짜와 시간 : Date"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - date
  - 자바중급
---

## Date 클래스
- **날짜**와 **시간**을 구하기 위한 클래스
- **java.util 패키지**에 속한다.
- `Date` 클래스는 JDK 1.0에 만들어졌고, `Calendar` 클래스는 JDK 1.1에 만들어졌다.
- **지역화에 대한 부분이 고려되지 않았다**.
  - 지역에 따라서 시간, 통화(원, 달러 등), 언어 등에 대하여 고려하는 프로그래밍을 지역화에 맞춘 프로그래밍이라고 한다.
  - 이러한 `Date` 클래스의 단점을 보완하기 위해 등장한 것이 **`Calendar` 클래스**이다.
- 대부분의 생성자와 메소드가 **Deprecated**되어 있다.
  - Deprecated된 것은 더 이상 지원하지 않는 기능이므로, 문제가 있을 수 있으니 사용을 자제하라는 의미.

<br/>

- **기본 생성자**를 이용한 `Date` 클래스 생성.
  - 기본 생성자로 `Date` 인스턴스를 만들게 되면, 현재 시간과 날짜 정보를 `Date` 인스턴스가 가지게 된다.
  
  ```java
  Date date = new Date();
  ```
  <br/>
  
- `toString()` 메소드를 이용하여 현재 시간을 문자열로 구할 수 있다.

  ```java
  // Wed Jan 06 18:36:56 KST 2016
  System.out.println(date.toString());
  ```
  <br/>
  
- `java.util.SimpleDateFormat` 클래스를 이용하여 원하는 형태로 출력할 수 있다.
  - **yyyy**는 년, **MM**은 월, **dd**는 일을 표현.
  - **hh**는 시간, **mm**은 분, **ss**는 초를 표현하며, **a**는 오전/오후를 표현.
  - **zzz**는 TimeZone을 나타낸다. 한국의 경우 한국 표준시 KST가 TimeZone에 해당하는 값이다.  

  ```java
  SimpleDateFormat ft = new SimpleDateFormat("yyyy.MM.dd 'at' hh:mm:ss a zzz");
  // 2016.01.10 at 10:34:52 오전 KST
  System.out.println(ft.format(date));
  ```
  - `SimpleDateFormat` 생성자의 인자에 원하는 포맷을 전달하면 된다.
  - 홑따옴표(single quote) 안의 문자열은 문자열 그대로 출력된다.

<br/>
  
- 현재 시간을 long 값으로 구하기

  ```java
  System.out.println(date.getTime()); // 1452389759575
  
  // System이 가지고 있는 currentTimeMillis() 메소드를 사용해도 된다.
  long today = System.currentTimeMillis();
  System.out.println(today);
  ```
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Date](https://programmers.co.kr/learn/courses/9/lessons/263)
