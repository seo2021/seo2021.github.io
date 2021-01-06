---
title: \[프로그래머스 \| 자바 입문\] 변수의 Scope와 Static
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 변수
  - scope
  - static
---

## 변수의 Scope
- 변수가 선언된 블럭이 그 변수의 사용범위이다.

```java
public class VariableScopeExam {

  int globalScope = 10; // 인스턴스 변수
  
  public void scopeTest(int value) {
    int localScope = 10;
    System.out.println(globalScope);
    System.out.println(localScope);
    System.out.println(value);
  }
}
```
- 클래스의 속성으로 선언된 변수 globalScope의 사용 범위는 클래스 전체이다.
- 매개변수로 선언된 int value는 블럭 바깥에 존재하기는 하지만, 메소드 선언부에 존재하므로 사용범위는 해당 메소드 블럭 내이다.
- 메소드 블럭 내에서 선언된 localScope 변수의 사용범위는 메소드 블럭 내이다.

## main 메소드에서 변수 사용하기

```java
public class VariableScopeExam {

  int globalScope = 10; // 인스턴스 변수
  
  public void scopeTest(int value) {
    int localScope = 10;
    System.out.println(globalScope);
    System.out.println(localScope);
    System.out.println(value);
  }
  
  public static void main(String[] args) {
    System.out.println(globalScope); //오류
    System.out.println(localScope); //오류
    System.out.println(value); //오류
  }
}
```
- 같은 클래스 안에 있음에도 globalScope 변수를 사용할 수 없다.
- main은 static한 메소드이다. static한 메소드에서는 static하지 않은 필드를 사용할 수 없다.

## static
- 

## 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [Kephi Javatory \| 4. Java 자바 - 연산자 종류, 연산자 우선순위](https://kephilab.tistory.com/28)
