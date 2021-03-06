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
- 기존부터 Java에서 제공하는 Date API, Time API는 부족한 기능 지원을 포함한 여러가지 문제점을 가지고 있었다.
- JDK 코어에서 이런 문제점들을 해결하고, 직관적인 API들을 제공하기 위해 **Java SE 8부터 새로운 날짜와 시간 API인 java.time 패키지를 제공**.
- `java.time` 패키지에는 자바에서 **날짜와 시간을 다루는 데 사용되는 필수 클래스들이 포함**되어 있다.
- 또한, 오브젝트를 생성하기 위해 다양한 **factory 메소드**를 사용한다(어떤 클래스의 인스턴스를 생성할지에 대한 결정을 factory 클래스에 위임).

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

## LocalDate 클래스와 LocalTime 클래스
- `LocalDate` 클래스는 **날짜**를 표현하는 데 사용되며, `LocalTime` 클래스는 **시간**을 표현하는 데 사용.
- `java.time` 패키지에 포함된 대부분의 클래스들은 이 두 클래스를 확장한 것이 많으므로, 이 두 클래스를 잘 이해하는 것이 중요하다.

## 날짜와 시간 객체의 생성
- `LocalDate`와 `LocalTime` 클래스는 **객체를 생성**하기 위해서 `now()`와 `of()` 클래스 메소드를 제공.
- `now()` 메소드는 **현재의 날짜와 시간**을 이용하여 **새로운 객체를 생성하여 반환**.
- `of()` 메소드는 **전달된 인수**를 가지고 **특정 날짜와 시간**을 표현하는 **새로운 객체를 생성하여 반환**.
- `parse()` 메소드는 **인수로 전달된 문자열**에 대한 **LocalTime 객체를 생성**한다.

  ```java
  import java.time.*;
  
  public class TimeEx01 {
    public static void main(String[] args) {
      // 현재 날짜와 시간
      LocalDate today = LocalDate.now();
      LocalTime present = LocalTime.now();
      System.out.println(today + " " + present); // 2017-02-16 09:21:50.634

      // static LocalDate of(int year, int month, int dayOfMonth)
      LocalDate birthDay = LocalDate.of(1982, 02, 19);

      // static LocalTime of(int hour, int minute, int second, int nanoOfSecond)
      LocalTime birthTime = LocalTime.of(02, 02, 00, 100000000);
      // birthTime = LocalTime.parse("02:02:00:00.100"); 
      System.out.println(birthDay + " " + birthTime); // 1982-02-19 02:02:00.100
    }
  }
  ```
  - `of()` 메소드는 위의 예제에서 사용된 메소드 시그니처 이외에도 **다양한 형태가 오버로딩**되어 제공된다.

## 날짜와 시간 객체에 접근하기
- `LocalDate'와 LocalTime` 클래스는 특정 필드의 값을 가져오기 위해 다양한 **getter 메소드를 제공**한다.

- `LocalDate` 클래스에서 제공하는 대표적인 getter 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | int **get**(TemporalField field)<br/>long **getLong**(TemporalField field) | 날짜 객체의 명시된 **필드의 값**을 int형이나 long형으로 **반환** |
  | int **getYear**() | 날짜 객체의 **연도(YEAR) 필드 값 반환** |
  | Month **getMonth**() | 날짜 객체의 **월(MONTH_OF_YEAR) 필드 값**을 **Month 열거체**를 이용하여 **반환** |
  | int **getMonthValue**() | 날짜 객체의 **월(MONTH_OF_YEAR) 필드 값 반환**(1~12) |
  | int **getDayOfMonth**() | 날짜 객체의 **일(DAY_OF_MONTH) 필드 값 반환**(1~31) |
  | int **getDayofYear**() | 날짜 객체의 **일(DAY_OF_YEAR) 필드 값 반환**(1~365, 윤년이면 366) |
  | DayOfWeek **getDayOfWeek**() | 날짜 객체의 **요일(DAY_OF_WEEK) 필드 값**을 **DayOfWeek 열거체**를 이용하여 **반환** |
  
  
- **기존**의 `Calendar` 클래스에서는 1월을 0으로 표현하여 **월의 범위가 0~11**이었으며, **요일은 일요일부터 1**로 표현.
- 하지만, `java.time` 패키지에서는 1월을 1로 표현하여 **월의 범위가 1~12**가 되었으며, **요일은 월요일부터 1**로 표현하도록 변경.
- 💡 `Calendar` 클래스와 `java.time` 패키지의 클래스를 **같이 사용**할 때에는 특히 위와 같은 차이점에 **주의**해야 한다.

- ex) `LocalDate` 클래스를 이용해 날짜와 시간 객체에 접근

  ```java
  import java.time.*;
  import java.time.temporal.*;
  
  public class TimeEx02 {
    public static void main(String[] args) {
      LocalDate today = LocalDate.now();

      // 올해는 2017년입니다.
      System.out.println("올해는 " + today.getYear() + "년입니다."); 
      // 이번달은 2월입니다.
      System.out.println("이번달은 " + today.getMonthValue() + "월입니다.");
      // 오늘은 THURSDAY입니다.
      System.out.println("오늘은 " + today.getDayOfWeek() + "입니다."); 
      // 오늘은 1년 중 47일째 날입니다.
      System.out.println("오늘은 1년 중 " + today.get(ChronoField.DAY_OF_YEAR) + "일째 날입니다.");
    }
  }
  ```
  
- `LocalTime` 클래스에서 제공하는 대표적인 getter 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | int **get**(TemporalField field)<br/>long **getLong**(TemporalField field) | 시간 객체의 명시된 **필드의 값**을 int형이나 long형으로 **반환** |
  | int getHour() | 시간 객체의 **시(HOUR_OF_DAY) 필드의 값**을 **반환** |
  | int getMinute() | 시간 객체의 **분(MINUTE_OF_HOUR) 필드의 값**을 **반환** |
  | int getSecond() | 시간 객체의 **초(SECOND_OF_MINUTE) 필드의 값**을 반환** ** |
  | int getNano() | 시간 객체의 **나노초(NANO_OF_SECOND) 필드의 값**을 **반환** |
  
  
- ex)  `LocalTime` 클래스를 이용해 날짜와 시간 객체에 접근
  
  ```java
  import java.time.*;
  
  public class TimeEx03 {
    public static void main(String[] args) {
      LocalTime present = LocalTime.now();
      // 현재 시간은 9시 22분입니다.
      System.out.println("현재 시각은 " + present.getHour() + "시 " + present.getMinute() + "분입니다."); 
    }
  }
  ```
  
## TemporalField 인터페이스
- 월(month-of-year)과 시(hour-of-day)와 같이 **날짜와 시간과 관련된 필드를 정의**해놓은 인터페이스.
- 해당 인터페이스를 구현하여 **날짜와 시간을 나타낼 때 사용하는 열거체**가 바로 `ChronoField`이다.
- `java.time` 패키지를 구성하는 클래스의 메소드에서는 이 열거체를 사용하여 날짜와 시간을 처리하고 있다.

- `ChronoField` 열거체에 정의된 **대표적인 열거체 상수**는 다음과 같다.

  | 열거체 상수 | 설명 |
  |:----------|:------|
  | ERA | 시대 |
  | YEAR | 연도 |
  | MONTH_OF_YEAR | 월 |
  | DAY_OF_MONTH | 일 |
  | DAY_OF_WEEK | 요일 (월요일:1, 화요일:2, ..., 일요일:7) |
  | AMPM_OF_DAY | 오전/오후 |
  | HOUR_OF_DAY | 시(0~23) |
  | CLOCK_HOUR_OF_DAY | 시(1~24) |
  | HOUR_OF_AMPM | 시(0~11) |
  | CLOCK_HOUR_OF_AMPM | 시(1~12) |
  | MINUTE_OF_HOUR | 분 |
  | SECOND_OF_MINUTE | 초 |
  | DAY_OF_YEAR | 해당 연도의 몇 번째 날 (1~365, 윤년이면 366) |
  | EPOCH_DAY | EPOCH(1970년 1월 1일)을 기준으로 몇 번째 날 |
  
  
- ex) `ChronoField` 열거체 상수 사용

  ```java
  import java.time.*;
  import java.time.temporal.ChronoField;
  
  public class TimeEx04 {
	  public static void main(String[] args){
      LocalTime present = LocalTime.now();
      String ampm;

      if(present.get(ChronoField.AMPM_OF_DAY) == 0 {
        ampm = "오전";
      }
      else {
        ampm = "오후";
      }
      // 지금은 오전 9시입니다.
      System.out.println("지금은 " + ampm + " " + present.get(ChronoField.HOUR_OF_AMPM) + "시입니다.");
    }
  }
  ```
  
## 날짜와 시간 객체의 필드값 변경
- `LocalDate`와 `LocalTime` 클래스는 날짜와 시간 객체에 접근하여 특정 필드의 값을 변경하기 위해서 **with() 메소드**를 사용.
- `with()` 메소드를 사용하면 **값이 변경될 필드**를 사용자가 **직접 명시**할 수 있다.
- 또한, 특정 필드의 값을 변경하기 위해 **미리 정의되어 제공되는 다양한 with() 메소드**를 사용할 수도 있다.

- `LocalDate` 클래스에서 제공하는 `with()` 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | LocalDate **with**(TemporalField field, long newValue) | 날짜 객체에서 **특정 필드**를 전달된 **새로운 값으로 설정**한 **새로운 날짜 객체를 반환** |
  | LocalDate **withYear**(int year) | 날짜 객체에서 **연도(YEAR) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 날짜 객체를 반환** |
  | LocalDate **withMonth**(int month) | 날짜 객체에서 **월(MONTH_OF_YEAR) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 날짜 객체를 반환** |
  | LocalDate **withDayOfMonth**(int dayOfMonth) | 날짜 객체에서 **일(DAY_OF_MONTH) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 날짜 객체를 반환** |
  | LocalDate **withDayOfYear**(int dayOfYear) | 날짜 객체에서 **DAY_OF_YEAR 필드**를 전달된 **새로운 값으로 설정**한 새**로운 날짜 객체를 반환** |
  
    
- ex) `LocalDate` 클래스의 `with()` 메소드 사용

  ```java
  import java.time.*;

  public class TimeEx05 {
    public static void main(String[] args) {
      LocalDate today = LocalDate.now();
      // 올해는 2017년입니다.
      System.out.println("올해는 " + today.getYear() + "년입니다.");
      
      LocalDate otherDay = today.withYear(1982);
      // 올해는 1982년입니다.
      System.out.println("올해는 " + otherDay.getYear() + "년입니다.");
    }
  }
  ```
    
- `LocalTime` 클래스에서 제공하는 `with()` 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | LocalTime **with**(TemporalField field, long newValue) | 시간 객체에서 **특정 필드**를 전달된 **새로운 값으로 설정**한 **새로운 시간 객체를 반환** |
  | LocalTime **withHour**(int hour) | 시간 객체에서 **시(HOUR_OF_DAY) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 시간 객체를 반환** |
  | LocalTime **withMinute**(int minute) | 시간 객체에서 **분(MINUTE_OF_HOUR) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 시간 객체를 반환** |
  | LocalTime **withSecond**(int second) | 시간 객체에서 **초(SECOND_OF_MINUTE) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 시간 객체를 반환** |
  | LocalTime **withNano**(int nanoOfSecond) | 시간 객체에서 **나노초(NANO_OF_SECOND) 필드**를 전달된 **새로운 값으로 설정**한 **새로운 시간 객체를 반환** |
  
  
- ex) `LocalTime` 클래스의 `with()` 메소드 사용

  ```java
  import java.time.*;

  public class TimeEx06 {
    public static void main(String[] args) {
      LocalTime present = LocalTime.now();
      // 현재 시간은 9시입니다.
      System.out.println("현재 시각은 " + present.getHour() + "시입니다.");
      
      LocalTime otherTime = present.withHour(8);
      // 현재 시간은 8시입니다.
      System.out.println("현재 시각은 " + otherTime.getHour() + "시입니다.");
    }
  }
  ```
  
- `with()` 메소드 이외에도 특정 필드의 값을 더하거나 뺄 수 있는 `plus()`, `minus()` 메소드도 제공된다.

## 날짜와 시간 객체의 비교
- `LocalDate`와 `LocalTime` 클래스에도 객체를 비교할 수 있는 **compareTo() 메소드**가 오버라이딩되어 있다.
  - `compareTo()` > 0 : 현재 객체가 더 미래
  - `compareTo()` < 0 : 현재 객체가 더 과거
  - `compareTo()` == 0 : 현재 객체와 인자와 같은 시간
  
- 하지만, 더욱 편리하게 날짜와 시간 객체를 서로 비교할 수 있도록 다음과 같은 메소드를 제공한다.
  1. `isEqual()` 메소드 : `equals()` 메소드와는 달리 오직 **날짜만을 비교**(LocalDate 클래스에서만 제공).
  2. `isBefore()` 메소드 : **두 개의 날짜와 시간 객체**를 비교하여, **현재 객체**가 명시된 객체보다 **앞선 시간인지를 비교**.
  3. `isAfter()` 메소드 : **두 개의 날짜와 시간 객체**를 비교하여, **현재 객체**가 명시된 객체보다 **늦은 시간인지를 비교**.

  ```java
  import java.time.*;

  public class TimeEx07 {
    public static void main(String[] args) {
      LocalDate today = LocalDate.now();
      LocalDate otherDay = LocalDate.of(1982, 02, 19);
  
      System.out.println(today.compareTo(otherDay)); // 35
      System.out.println(today.isBefore(otherDay)); // false
      System.out.println(today.isEqual(otherDay)); // false
    }
  }
  ```
  
## 관련 포스트 - 날짜와 시간
- [날짜와 시간 : Date](https://seo2021.github.io/java/programmers-lectures/java-intermediate-date/)
- [날짜와 시간 : Calendar](https://seo2021.github.io/java/programmers-lectures/java-intermediate-calendar/)
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| java.time 패키지](https://programmers.co.kr/learn/courses/9/lessons/265)
- [코딩의 시작, TCP School \| JAVA \| java.time 패키지](https://www.tcpschool.com/java/java_time_javaTime)
- [chacha \| Java - 시간(Time), 날짜(Date) 비교하는 방법](https://codechacha.com/ko/java-compare-date-and-time/)
- [sonnie \| Factory Method란?](https://modunaeggu.medium.com/factory-method%EB%9E%80-9bf9b1024711)
