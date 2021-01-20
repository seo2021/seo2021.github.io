---
title: \[프로그래머스 \| 자바 입문\] 예외(Exception)-3
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 예외
---

## 예외 발생시키기(throw)
- throw 키워드를 사용하여 강제로 예외를 발생시킬 수 있다.

## 예외 회피하기(throws)
- throws는 예외가 발생했을 때, 예외를 호출한 쪽에서 처리하도록 던져준다.
- ex) 정수 2개를 매개변수로 받아 나눗셈한 결과를 반환하는 divide 메소드. main 메소드에서는 divide 메소드를 호출한다.

  ```java
  public class ExceptionExam2 [
    public static voiid main(String[] args) {
      int i = 10;
      int j = 0;
      int k = divide(i, j);
      System.out.println(k);
    }
   
    public static int divide(int i, int j) {
      int k = i / j;
      return k;
    }
  }
  ```

- 위의 divide 메소드를 수정하여, divide 메소드에서 발생하는 ArithmeticException을 호출하는 쪽에서 처리하도록 한다.
- divide 메소드를 호츨하는 main 메소드에서 예외를 처리하도록 코드를 수정한다.
 
  ```java
  public class ExceptionExam2 [
 
    public static voiid main(String[] args) {
      int i = 10;
      int j = 0;
     
      try {
        // 예외 발생 블록
        int k = divide(i, j);
        System.out.println(k);
       
      } catch(ArithmeticException e) {
        // 예외 처리 블록
        System.out.println("0으로 나눌 수 없습니다.");
      }
    }
   
    public static int divide(int i, int j) throws ArithmeticException {
      int k = i / j;
      return k;
    }
  }
  ```
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Throws](https://programmers.co.kr/learn/courses/5/lessons/245)
- [코딩의 시작, TCP School \| JAVA \| 예외 발생 및 회피](https://www.tcpschool.com/java/java_exception_throw)
