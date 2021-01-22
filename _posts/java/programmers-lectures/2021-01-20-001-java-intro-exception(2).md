---
title: \[프로그래머스 \| 자바 입문\] 예외(Exception)-2
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 예외
  - 자바입문
---

## 예외 클래스
- 자바에서 모든 예외의 조상 클래스가 되는 Exception 클래스는 크게 다음과 같이 구분할 수 있다.

  1. RuntimeException 클래스
  2. 그 외의 Exception 클래스의 자식 클래스
  
  ![자바 예외 클래스 계층도](/assets/images/java/exception_class_hierarchy.png)
  
  - **RuntimeException 클래스**를 상속받는 자식 클래스들은 주로 치명적인 예외 상황을 발생시키지 않는 예외들로 구성.
    - 따라서 `try-catch` 문을 사용하기보다는 프로그램을 **작성하면서 예외가 발생하지 않도록 주의**를 기울이는 편이 좋다.
  - **그 외의 Exception 클래스**에 속하는 자식 클래스들은 치명적인 예외 상황을 발생시키므로, 반드시 `try-catch`문을 사용하여 예외를 처리.
    - 예외 처리를 하지 않을 경우 **컴파일 오류** 발생.
  
## 예외 처리의 계층 관계
- 자바에서는 예외가 발생하면, try 블록과 가장 가까운 catch 블록부터 순서대로 검사.
- 여러 개의 catch 블록을 사용할 때는 **예외 클래스의 계층 관계에도 주의**를 기울여야 한다.

  ```java
  try {
    System.out.write(list);
  } catch (Exception e) {
    e.printStackTrace();
  } catch (IOException e) {
    e.printStackTrace();
  }
  ```
  - 위의 예제에서 IOException이 발생하면, **첫 번째 catch 블록부터** 순서대로 해당 예외를 처리할 수 있는지 검사한다.
  - 그런데, IOException은 Exception의 자식 클래스이므로 **첫 번째 catch 블록에서만 예외가 처리**되고 두 번째 catch 블록은 실행되지 못할 것이다.
  
- 따라서 IOException만을 따로 처리하고자 한다면, catch 블록의 순서를 변경해야 한다.

  ```java
  try {
    System.out.write(list);
  } catch (IOException e) {
    e.printStackTrace();
  } catch (Exception e) {
    e.printStackTrace();
  }
  ```
  
- 💡 범위가 더 **좁은** 예외를 처리하는 catch 블록을 **먼저 명시**해야만 정상적으로 해당 예외를 처리할 수 있다.

## 여러 예외 타입의 동시 처리
- 자바 SE 7부터는 `|`기호를 사용하여 하나의 cacth 블록에서 여러 타입의 예외를 동시에 처리할 수 있다.

  ```java
  try {
    this.db.commit();
  } catch (IOException | SQLException e) {
    e.printStackTrace();
  }
  ```

## 자주 사용되는 예외 클래스

| 클래스 | 설명 |
|:-----:|:-----:|
| ClassCastException | 수행할 수 없는 타입 변환이 진행될 경우 |
| ArrayIndexOutOfBoundsException | 배열에 잘못된 인덱스를 사용하여 접근할 경우 |
| NullPointerException | null 객체의 인스턴스 메소드를 호출하는 등의 경우 |
| ArithmeticException | 산술 연산에서 정수를 0으로 나누는 등 연산을 수행할 수 없는 경우 |

## 출처
- [코딩의 시작, TCP School \| JAVA \| 예외 클래스](https://www.tcpschool.com/java/java_exception_class)
