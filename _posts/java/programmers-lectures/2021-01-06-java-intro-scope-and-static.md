---
title: \[프로그래머스 \| 자바 입문\] 변수의 Scope와 Static
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - scope
  - static
  - 자바입문
---

## 변수의 Scope
- 변수가 선언된 블럭이 그 변수의 사용범위이다.

```java
public class VariableScopeExam {

  int globalScope = 10; // 인스턴스 변수
  
  public void scopeTest(int value) {
    int localScope = 10; // 지역 변수
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
    int localScope = 10; // 지역 변수
    System.out.println(globalScope);
    System.out.println(localScope);
    System.out.println(value);
  }
  
  public static void main(String[] args) {
    System.out.println(globalScope); // 오류
    System.out.println(localScope); // 오류
    System.out.println(value); // 오류
  }
}
```
- 같은 클래스 안에 있음에도 globalScope 변수를 사용할 수 없다.
- main은 static한 메소드이다. static한 메소드에서는 static하지 않은 필드를 사용할 수 없다.
  - static하지 않은 필드를 main 메소드에서 사용하려면 객체를 생성한 뒤 사용 가능하다.
    - ex) VariableScopeExam v1 = new VariableScopeExam();

## static
- static으로 선언된 변수는 (static한 메소드인) main 메소드에서 사용 가능

```java
public class VariableScopeExam {
  
  int globalScope = 10; // 인스턴스 변수
  static int staticVal = 7; // 클래스 변수
  
  public static void main(String[] args) {
    System.out.println(staticVal); // 사용가능
  }
}
```
- static으로 선언된 변수는 공유된다.
  - static으로 선언된 변수는 값을 저장할 수 있는 공간이 하나만 생성된다. 그러므로, 인스턴스가 여러 개 생성되어도 static 변수는 하나다.

```java
VariableScopeExam v1 = new VariableScopeExam();
VariableScopeExam v2 = new VariableScopeExam();
v1.globalScope = 20; // 인스턴스 변수
v2.globalScope = 30;

System.out.println(v1.globalScope); // 20 출력
System.out.println(v2.globalScope); // 30 출력

v1.staticVal = 10; // 클래스 변수
v2.staticVal = 20;

System.out.println(v1.staticVal); // 20 출력
System.out.println(v2.staticVal); // 20 출력
```
- globalScope같은 변수(필드)는 인스턴스가 생성될 때 생성되기 때문에, 인스턴스 변수라고 한다.
- staticVal같은 static한 필드를 클래스 변수라고 한다.
- 클래스 변수는 '레퍼런스.변수명'보다는 '클래스명.변수명'으로 사용하는 것이 바람직하다.
  - ex) VariableScopeExam.staticVal
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 변수의 scope와 static](https://programmers.co.kr/learn/courses/5/lessons/231)
