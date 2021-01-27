---
title: "[프로그래머스 자바 중급] Object 클래스와 오버라이딩(Overriding)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - object
  - 자바중급
---

## Object 클래스
- 모든 클래스의 최상위 클래스.
- 아무것도 상속받지 않으면 자동으로 Object를 상속.
- Object가 가지고 있는 메소드는 모든 클래스에서 다 사용할 수 있다.

## Object 클래스의 메소드
- 사용할 때 반드시 오버라이딩해서 사용한다.

- 가장 많이 사용되는 메소드 3가지
- equals()
  - 객체가 가진 값을 비교할 때 사용.
- toString()
  - 객체가 가진 값을 문자열로 반환.
- hashCode()
  - 객체의 해시코드 값 반환.
  - 해시코드는 되도록 서로 다른 값을 가지는 것이 좋다.
  
-  ex) Object 클래스로부터 상속받은 메소드 사용
  ```java
  public class Student {
    String name;
    String number;
    int birthYear;
    
    public static void main(String[] args) {
      // Student 객체 생성
      Student s1 = new Student();
      s1.name = "홍길동";
      s1.number = "1234";
      s1.birthYear = 1995;
      
      Student s2 = new Student();
      s2.name = "홍길동";
      s2.number = "1234";
      s2.birthYear = 1995;

      // s1 != s2 출력
      if(s1.equals(s2))
        System.out.println("s1 == s2");
      else
        System.out.println("s1 != s2"); 
        
      System.out.println(s1.hashCode); // 705927765
      System.out.println(s2.hashCode); // 366172642
    }
  }
  ```
  - Object로부터 상속받은 equals() 메소드를 그대로 사용하기 때문에, hashcode로 객체를 비교한다.

- ex) Object로부터 상속받은 메소드를 오버라이딩하여 사용
  ```java
  // hashcode 구하기
  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    // number 속성을 사용하여 hashcode 구하기
    result = prime * result + ((number == null) ? 0 : number.hashCode());
    return result;
  }
  
  @Override
  public boolean equals(Object obj) {
  
  }
  ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Object와 오버라이딩](https://programmers.co.kr/learn/courses/9/lessons/249#)
- [코딩의 시작, TCP School \| JAVA \| Object 클래스](https://www.tcpschool.com/java/java_api_object)
