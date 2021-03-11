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
- **JDK 1.0**에서는 **Date 클래스**를 사용하여 **날짜**에 관한 간단한 처리를 수행할 수 있었으나, 현재 Date 클래스 대부분의 메소드는 **사용을 권장하지 않고(deprecated) 있다**.
- **JDK 1.1부터**는 새롭게 제공되는 **Calendar 클래스**를 이용하여 **날짜와 시간**에 관한 처리를 수행.
  - 하지만, Calendar 클래스는 다음과 같은 **문제점**이 있다.
    1. Calendar 인스턴스는 불변 객체(immutable object)가 아니라서 **값이 수정될 수 있다**.
    2. 윤초(leap second)와 같은 **특별한 상황을 고려하지 않는다**.
    3. 월(month)을 나타낼 때, 1월부터 12월을 **0부터 11까지로 표현**해야 하는 불편함이 있다. 

  - 따라서, 더 나은 성능의 **Joda-Time**이라는 라이브러리를 함께 사용.
  - **Java SE 8** 버전에서는 **Joda-Time 라이브러리를 발전**시킨 새로운 날짜와 시간 API인 **java.time 패키지**를 제공.
    - java.time 패키지는 위와 같은 문제점을 모두 해결했으며, 다양한 기능을 지원하는 다수의 하위 패키지를 포함하고 있다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Calendar](https://programmers.co.kr/learn/courses/9/lessons/264)
- [코딩의 시작, TCP School \| JAVA \| Calendar 클래스](https://www.tcpschool.com/java/java_api_calendar)
