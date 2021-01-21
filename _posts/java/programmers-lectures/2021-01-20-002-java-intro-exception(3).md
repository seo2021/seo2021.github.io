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

## 예외 회피하기(throws)
- **throws**는 예외가 발생했을 때, 예외를 **호출한 쪽에서 처리하도록 던져준다**.
- **메소드 선언부에 throws 키워드**를 사용하여 해당 메소드를 사용할 때 발생할 수 있는 **예외를 미리 명시**할 수 있다.

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
      int k = i / j; // ArithmeticException 발생
      return k;
    }
  }
  ```

- 위의 divide 메소드를 수정하여, divide 메소드에서 발생하는 **ArithmeticException을 호출하는 쪽에서 처리**하도록 한다.
- divide 메소드를 호하는 main 메소드에서 예외를 처리하도록 코드를 수정한다.

  ```java
  public class ExceptionExam2 [
    
    public static voiid main(String[] args) {
      int i = 10;
      int j = 0;
     
      try {
        // 예외 발생 메소드 호출
        int k = divide(i, j);
        System.out.println(k);
       
      } catch(ArithmeticException e) {
        // 호출하는 쪽에서 예외 처리
        System.out.println("0으로 나눌 수 없습니다.");
      }
    }
    
    // ArithmeticException 발생 메소드. 예외를 호출한 쪽으로 넘긴다.
    public static int divide(int i, int j) throws ArithmeticException {
      int k = i / j;
      return k;
    }
  }
  ```
  - 💡 Exception 클래스는 모든 예외의 조상이므로 `throws Exception`을 하면, 해당 메소드 내에서 발생하는 **모든 예외를 모두 넘길 수 있다**.
  
## 예외 발생시키기(throw)
- **throw** 키워드를 사용하여 **강제로 예외를 발생**시킬 수 있다.
- 오류를 떠넘기는 **throws와 주로 같이 사용**된다.

  ```java
  public class ExceptionExam3 {
  
    public static void main(String[] args) {
      int i = 10;
      int j = 0;
      
      try {
        // 예외 발생 메소드 호출
        int k = divide(i, j);
        System.out.println(k);
       
      } catch(ArithmeticException e) {
        // 호출하는 쪽에서 예외 처리
        System.out.println("0으로 나눌 수 없습니다.");
      }
    }
    
    // 예외를 호출한 쪽으로 넘긴다.
    public static int divide(int i, int j) throws IllegalArgumentException {
      // **2번째 매개변수가 0으로 전달될 경우 강제로 예외를 발생시킨다.
      if(j == 0) { 
        throw new IllegalArgumentException("0으로 나눌 수 없어요.");
      }
      int k = i / j;
      return k;
    }
  }
  ```
  - 0으로 잘못된 나누기를 하여 ArithmeticException을 발생시키기 전에, **두 번째 매개변수가 0이 아닌지 먼저 확인해 예외 처리**하려 한다.
  - j가 0일 경우 **new 연산자**를 통하여 **IllegalArgumentException 객체**를 만들고, **throw** 키워드로 **강제로 예외를 발생**시킨다.
  - 예외가 발생하면, **throws 키워드로 해당 예외를 호출한 쪽으로 넘긴다**.
    
## 사용자 정의 예외 클래스
- **Exception이나 Exception의 후손 클래스를 상속받아** 자신만의 새로운 예외 클래스를 정의하여 사용할 수 있다.
- 클래스의 이름만으로 어떤 오류가 발생했는지 알려주어 **코드의 직관성**을 높일 수 있다.
- 사용자 정의 예외 클래스에는 **생성자**뿐만 아니라 **필드 및 메소드**도 원하는 만큼 추가할 수 있다.

- 사용자 정의 예외 클래스는 다음과 같이 2가지로 나눌 수 있다.
  1. **Exception 클래스**를 상속받아 정의한 **checked Exception**
    - 반드시 오류를 처리해야만 하는 Exception
  2. **RuntimeException 클래스**를 상속받아 정의한 **unChecked Exception**
    - 예외 처리를 하지 않아도 컴파일 시 오류를 발생시키지 않는다.
<br/>    
- ex) RuntimeException을 상속받은 사용자 정의 예외 클래스 RuntimeException
  - 부모 클래스인 RuntimeException에 이미 같은 기능을 가지는 생성자가 있기 때문에, **매개변수로 받아들인 값을 부모 생성자에게 전달**해주기만 하면 된다.
  - 비즈니스 로직이 수행될 때 발생하는 예외
  
  ```java
  public class BizException extends RuntimeException {
  
    // 문자열 오류메시지를 받는 생성자 (4)
    public BizException(String msg) {
      super(msg);
    }
    
    // 실제 발생한 예외를 받는 생성자
    public BizException(Exception ex) {
      super(ex);
    }
  }
  ```

- ex) 업무 처리 메소드를 가진 BizService 클래스.
  - 사용자 정의 예외를 발생시키는 BizException를 사용.
  - 업무와 관련하여 예외가 발생했음을 호출한 곳에 알린다.
  
  ```java
  public class BizService {
    // BizExcepton 예외를 호출한 곳으로 넘긴다. (5)
    public void bizMethod(int i) throws BizExcepton {
    
      System.out.println("비지니스 로직이 시작합니다."); // (2)
      
      if(i < 0) { 
        // 예외를 발생시킨다 (3)
        throw new BizException("매개변수 i는 0이상이어야 합니다.");
      }
      
      System.out.println("비지니스 로직이 종료됩니다.");
    }
  }
  ```
  
- ex) 앞에서 만든 BizService를 이용하는 BizExam 클래스

  ```java
  public class BizExam {
    public staic void main(String[] args) {
      BizService biz = new BizService();
      biz.bizMethod(5);
      
      try {
        // 메소드 호출. 예외를 발생시키는 인자 전달 (1)
        biz.bizMethod(-3);
        // 메소드를 호출한 곳에서 예외 처리 (6)
      } catch(Exception ex) {
      
        ex.printStackStrace(); 
      }
    }
  }
  ```

- 실행 결과

  ```java
  비지니스 로직이 시작합니다.
  비지니스 로직이 종료됩니다.
  비지니스 로직이 시작합니다.
  javaStudy.BizException: 매개변수 i는 0이상이어야 합니다.
          at javaStudy.BizService.bizMethod(BizService.java:7)
          at javaStudy.BizExam.main(BizExam.java:9)
  ```
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Throws](https://programmers.co.kr/learn/courses/5/lessons/245)
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Exception 발생시키기](https://programmers.co.kr/learn/courses/5/lessons/315)
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 사용자 정의 Exception](https://programmers.co.kr/learn/courses/5/lessons/316)
- [코딩의 시작, TCP School \| JAVA \| 예외 발생 및 회피](https://www.tcpschool.com/java/java_exception_throw)
