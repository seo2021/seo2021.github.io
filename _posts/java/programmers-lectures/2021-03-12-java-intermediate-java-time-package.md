---
title: "[프로그래머스 자바 중급] 날짜와 시간 : java.time 패키지"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - java.time
  - 자바중급
---

## java.time 패키지
- Java SE 8부터 제공되는 `java.time` 패키지에는 자바에서 **날짜와 시간을 다루는 데 사용되는 필수 클래스들이 포함**되어 있다.

- 또한, 다음과 같은 기능을 하는 하위 패키지를 포함하고 있다.
  1. `java.time.chrono`: ISO-8601에 정의된 **표준 달력 이외의 달력 시스템**을 사용할 때 필요한 클래스들
  2. `java.time.format`: 날짜와 시간에 대한 데이터를 **구문분석하고 형식화**하는 데 사용되는 클래스들
  3. `java.time.temporal`: 날짜와 시간에 대한 데이터를 **연산**하는 데 사용되는 보조 클래스들
  4. `java.time.zone`: **타임 존(time-zone)**과 관련된 클래스들

- 기존에 사용되던 `Calendar` 클래스의 단점을 보완.
  - 따라서, `java.time` 패키지에 속하는 모든 클래스의 인스턴스는 **불변 객체(immutable object)**로 생성
  - 즉, `java.time` 패키지에 속하는 클래스의 메소드들은 모두 **새로운 객체를 생성하여 반환**

## java.time 패키지의 구성 클래스
- 기존의 `Calendar` 클래스는 **날짜와 시간**을 한 번에 표현했지만, `java.time` 패키지에서는 **별도로 구분**하여 처리.
- `LocalDate` 클래스는 **날짜**를 표현할 때 사용하며, `LocalTime` 클래스는 **시간**을 표현할 때 사용.
- `Calendar` 클래스처럼 **날짜와 시간**을 한 번에 표현하고 싶을 때는 `LocalDateTime` 클래스를 사용.

- `ZonedDateTime` 클래스는 **특정 타임 존(time-zone)**에 해당하는 날짜와 시간을 다루는 데 사용.
- 기존의 `Date`클래스와 비슷한 용도로 사용되는 `Instant` 클래스도 있다.
  - `Instant` 클래스는 특정 시점의 날짜와 시간을 **나노초(nanosecond) 단위**로 표현하는 **타임스탬프(time-stamp)**를 다루는 데 사용.
- `Period` 클래스는 **두 날짜 사이의 차이**를 표현하는 데 사용되며, `Duration` 클래스는 **두 시각 사이의 차이**를 표현하는 데 사용된다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| java.time 패키지](https://programmers.co.kr/learn/courses/9/lessons/265)
- [코딩의 시작, TCP School \| JAVA \| java.time 패키지](https://www.tcpschool.com/java/java_time_javaTime)
