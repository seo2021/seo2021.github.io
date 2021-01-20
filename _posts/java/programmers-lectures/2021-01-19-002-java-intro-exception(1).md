---
title: \[프로그래머스 \| 자바 입문\] 예외(Exception)-1
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 예외
---

## 오류(error)와 예외(exception)
- 컴퓨터 시스템이 동작하는 도중에 **예상하지 못한 사태**가 발생하여 실행 중인 프로그램이 영향을 받는 것을 **오류**와 **예외** 두 가지로 구분할 수 있다.
- **오류**는 **시스템 레벨에서 프로그램에 심각한 문제를 야기**하여 **실행 중인 프로그램을 종료**시킨다. 이러한 오류는 개발자가 **미리 예측하여 처리할 수 없는 것이 대부분**이므로, 오류에 대한 처리는 할 수 없다.
- **예외**는 오류와 마찬가지로 실행 중인 프로그램을 **비정상적으로 종료**시키지만, 발생할 수 있는 상황을 **미리 예측하여 처리**할 수 있다.
- 따라서, 개발자는 **예외 처리(exception handling)**를 통해 예외 상황을 처리할 수 있도록 코드의 흐름을 바꿀 필요가 있다.

## 예외 처리(exception handling)
- 자바에서는 프로그램이 실행되는 도중 발생하는 예외를 처리하기 위해 `try-catch-finally` 구문을 사용할 수 있다.
- **발생한 예외**와 **catch 블록에 선언해놓은 예외**가 맞아야 해당 catch 블록을 실행시킨다.
- 발생한 예외를 처리할 수 있는 catch 블록이 없으면, 예외는 처리되지 못한 채 프로그램은 강제종료된다.

  ```java
  try {
  
    // 수행할 코드, 예외 발생 가능성이 있는 블록
    
  } catch(예외클래스 변수명)
  
    // 예외 처리 블록
  
  } finally {
  
    // 예외 발생 여부에 상관없이 반드시 실행되는 블록 
    // 생략 가능
    
  }
  ```

- ex) 아래 코드에서 j를 0으로 바꾸면 예외 발생
  - 정수를 0으로 나누면 ArithmeticException이 발생하면서 프로그램이 종료

  ```java
  public class ExceptionExam {
    public static void main(String[] args) {
      int i = 10;
      int j = 5;
      int k = i / j;
      
      System.out.println(k); // 예외가 발생한 시점부터 프로그램 종료
      System.out.println("main 종료!!"); // 미실행
    }
  }
  ```
  
- 변수 j에 0이 들어오는 상황을 미리 예측하고 처리할 수 있다.
  - 오류 발생 예상 부분을 try 블록으로 감싼 후, 발생한 오류와 관련된 예외를 catch 블록에서 처리.
  - finally 블록은 오류 발생 여부와 상관없이 무조건 실행되며, 생략 가능.
  

  ```java
  public class ExceptionExam {
    public static void main(String[] args) {
      int i = 10;
      int j = 0;
      
      // 예외 처리
      try {
      
        int k = i / j;
        System.out.println(k);
        
      } catch(ArithmeticException e) {
      
        // 예외클래스변수명.toString(): 예외 정보를 알려주는 메소드
        System.out.println("0으로 나눌 수 없습니다. : " + e.toString());
        
      } finally {
      
        System.out.println("오류 여부와 상관없이 실행");
        
      }
    }
  }
  ```
  - 실행결과
  
    ```java
    0으로 나눌 수 없습니다. : java.lang.ArithmeticException: / by zero
    오류 여부와 상관없이 실행
    ```
    - 예외 처리를 하지 않았을 때는 프로그램이 강제 종료되었으나, 예외 처리를 한 후에는 강제 종료되지 않고 잘 실행된다.
    
- try 블록에서 여러 종류의 예외가 발생한다면 **catch 블록을 여러 개** 둘 수 있다.
- 💡 모든 예외 클래스들은 **Exception 클래스를 상속**받으므로, 예외 클래스로 Exception을 두게 되면 어떤 오류가 발생하든지 간에 하나의 catch 블록에서 모든 오류를 처리할 수 있다.
   
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Exception](https://programmers.co.kr/learn/courses/5/lessons/244)
- [코딩의 시작, TCP School \| JAVA \| 예외 처리](https://www.tcpschool.com/java/java_exception_intro)
