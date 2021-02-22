---
title: "[프로그래머스 자바 중급] java.lang 패키지 : 래퍼 클래스(Wrapper Class)와 Boxing"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - java.lang패키지
  - wrapper
  - boxing
  - 자바중급
---

## 래퍼 클래스(wrapper class)
- 기본 타입 데이터를 객체로 포장해주는 클래스
- 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어준다.
- 이러한 래퍼 클래스는 모두 java.lang 패키지에 포함되어 제공된다.

- 자바의 기본 타입과 대응되는 래퍼 클래스들

  | 기본 타입 | 래퍼 클래스 |
  |:----------|:----------|
  | byte | Byte |
  | short | Short |
  | int | **Integer** |
  | long | Long |
  | float | float |
  | double | Double |
  | char | **Character** |
  | boolean | Boolean |
  
## 박싱(boxing)과 언박싱(unboxing)
- 래퍼 클래스는 산술 연산을 위해 정의된 클래스가 아니므로, **인스턴스에 저장된 값을 변경할 수 없다**.
- 단지, 값을 참조하기 위해 새로운 인스턴스를 생성하고, 생성된 인스턴스의 값만을 참조할 수 있다.
- 기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하는 과정을 **박싱(boxing)**이라고 한다.
  - 기본 타입 데이터를 객체 타입 데이터로 자동 형 변환.
- 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 **언박싱(unboxing)**이라고 한다.
  - 객체 타입 데이터를 기본형 타입 데이터로 자동 형 변환.

  ![박싱과 언박싱](/assets/images/java/boxing_unboxing.png)
  
## 오토 박싱(autoboxing)과 오토 언박싱(autounboxing)
- **JDK 1.5**부터는 박싱과 언박싱이 필요한 상황에서 **자바 컴파일러가 이를 자동으로 처리**해준다.
- 이렇게 **자동화된 박싱과 언박싱**을 오토 박싱과 오토 언박싱이라고 한다.

- ex) 박싱과 언박싱, 오토 박싱과 오토 언박싱의 차이

  ```java
  Integer num = new Integer(17); // 박싱
  int n = num.intValue(); // 언박싱
  System.out.println(n); // 17
  
  Character ch = 'X'; // Character ch = new Character('X'); - 오토박싱
  char c = ch; // char c = ch.charValue(); - 오토언박싱
  System.out.println(c); // X
  ```
  - 래퍼 클래스에는 **intValue(), charValue()와 같은 언박싱을 위한 메소드가 포함**되어 있다.
  - **오토 박싱**을 이용하면 new 키워드를 사용하지 않고도 자동으로 Character 인스턴스를 생성할 수 있다.
  - 반대로, **오토 언박싱**을 이용하여 인스턴스에 저장된 값을 바로 참조할 수 있다.
  
- ex) 오토 박싱과 오토 언박싱을 통한 기본 타입과 래퍼 클래스 간의 연산

  ```java
  public class Wrapper02 {
    public static void main(String[] args) {
      Integer num1 = new Integer(7); // 박싱
      Integer num2 = new Integer(3); // 박싱
      
      int int1 = num1.intValue(); // 언박싱
      int int2 = num2.intValue(); // 언박싱
      
      // 래퍼 클래스를 오토 언박싱하여 기본 타입으로 연산하고, 기본 타입 연산 결과를 오토 박싱
      Integer result1 = num1 + num2; // 10
      // 기본 타입 연산 결과를 오토박싱
      Integer result2 = int1 - int2; // 4
      // 래퍼 클래스를 오토 언박싱하여 기본 타입으로 연산
      int result3 = num1 * int2; // 21
    }
  }
  ```
  - 내부적으로 래퍼 클래스인 피연산자를 오토언박싱하여 기본 타입끼리의 연산을 수행한다.
  
- ex) 래퍼 클래스의 객체 비교

  ```java
  public class Wrapper03 {
    public static void main(String[] args) {
      // 박싱
      Integer num1 = new Integer(10);
      Integer num2 = new Integer(20);
      Integer num3 = new Integer(10);
      
      System.out.println(num1 < num2); // true, 비교 연산도 오토언박싱을 통해 가능
      System.out.println(num1 == num3); // false, 동등 연산자로 동등 여부 판단 X
      System.out.println(num1.equals(num3)); // true, equals()로 동등 여부 판단
    }
  }
  ```
  - **래퍼 클래스도 객체**이므로 **동등 연산자(==)**를 사용하게 되면, **두 인스턴스의 주소값을 비교**한다.
  - 인스턴스에 저장된 **값의 동등 여부**를 정확히 판단하려면 **equals() 메소드**를 사용해야 한다.
  
- 💡 래퍼 클래스도 '클래스'이기 때문에 속성과 메소드를 가진다.
  - ex) Integer 클래스의 필드와 메소드 사용
    ```java
    Integer i1 = 5;
    int max_int = i1.MAX_VALUE; // 2147483647
    long i1_long = i1.longValue(); // 5
    ```
    - [참고: Integer 클래스의 필드와 메소드](https://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html)

## 관련 포스트 - java.lang 패키지
- [Object 클래스와 오버라이딩(Overriding)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-object-class/)
- [스트링 클래스(String Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-string-class/)
- [스트링버퍼 클래스(StringBuffer Class)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-stringbuffer-class/)
- [Math 클래스](https://seo2021.github.io/java/programmers-lectures/java-intermediate-math-class/)
- [Enum 클래스](https://seo2021.github.io/java/001-java-intermediate-enum-class/)

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| java.lang 패키지/오토박싱](https://programmers.co.kr/learn/courses/9/lessons/251)
- [코딩의 시작, TCP School \| JAVA \| Wrapper 클래스](https://www.tcpschool.com/java/java_api_wrapper)
