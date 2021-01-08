---
title: \[프로그래머스 \| 자바 입문\] 메소드 오버로딩(Method Overloading)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 오버로딩
  - overloading
---

## 메소드 오버로딩
- 매개변수의 유형과 개수를 다르게 하여, 같은 이름의 메소드를 여러 개 가질 수 있게 하는 기술
- 메소드 오버로딩은 매개변수 부분이 달라야 한다.

  ```java
  class MyClass2 {
  
    public int plus(int x, int y) {
      return x+y;
    }
    
    public int plus(int x, int y, int z) {
      return x + y + z;
    }
    
    public String plus(String x, String y) {
      return x + y;
    }
  }
  ```

- 매개변수명은 다르지만, **매개변수의 타입과 개수가 동일**한 메소드를 또 정의할 수는 없다.

  ```java
  public int plus(int i, int f) {
    return i + f;
  }
  ```

## 오버로딩된 메소드 이용하기
- 메소드의 인자에 어떤 값이 쓰이느냐에 따라서 각기 다른 메소드가 호출된다.
```java
public MethodOverloadExam {
  
  public static void main(String[] args) {
  
    MyClass2 m = new MyClass2();
    
    System.out.println(m.plus(5, 10));
    System.out.println(m.plus(5, 10, 15));
    System.out.println(m.plus("hello", " world"));
  }
}
```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 메소드 오버로딩](https://programmers.co.kr/learn/courses/5/lessons/170)
