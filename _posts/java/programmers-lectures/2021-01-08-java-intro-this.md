---
title: \[프로그래머스 \| 자바 입문\] this
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - this
---

## this는 현재 객체, 자기 자신을 나타낸다.
- this는 객체 자신을 참조하는 키워드이다.

## this의 사용
- Car 클래스의 생성자 매개변수의 이름이 n이다.

  ```java
  public class Car {

    String name;
    int number;

    public Car(String n) {

      name = n;
    }
  }
  ```

- n이라는 변수명은 무엇을 의미하는지 쉽게 알 수 없으므로, n보다는 name으로 사용하는 것이 좋다.
  - 변수명은 알아보기 쉽게 직관적으로 선언하는 것이 좋다.

  ```java
    public Car(String name) {
      name = name;
    }
  ```

- 위와 같이 `name = name`으로 코드를 바꾸면, **가깝게 선언된 변수를 우선 사용**하기 때문에 이는 **매개변수 name의 값을 매개변수 name에 대입**하라는 의미가 된다.
- 즉, 필드의 값이 초기화되지 않는다.
- 이런 경우 필드라는 것을 컴파일러와 JVM에게 알려주기 위해서 this 키워드를 사용해야 한다.

  ```java
  public Car(String name) {
    this.name = name;
  }
  ```
  
  - 앞의 `this.name`은 필드 name을 의미하고, 그 뒤의 `name`은 매개변수를 의미한다.
  - 즉, 매개변수의 값을 필드에 대입하라는 의미가 된다.

## 💡 클래스 안에서 자기 자신이 가지고 있는 메소드를 사용할 때도 `this.메소드명()`으로 호출할 수 있다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| this](https://programmers.co.kr/learn/courses/5/lessons/169)
