---
title: "[자바] 컬렉션 프레임워크 : Stack과 Queue"
layout: single
related: true
categories:
  - JAVA
tags:
  - collection-framework
  - stack
  - queue
---

## Stack\<E> 클래스
- **List 컬렉션 클래스의 Vector 클래스를 상속받아**, 전형적인 스택 메모리 구조의 클래스를 제공.
- 스택 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 **후입선출(LIFO)**의 시멘틱을 따르는 자료 구조.
  - 즉, 가장 나중에 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조.
  
  ![스택의 구조](/assets/images/java/stack.png)
  
- Stack 클래스는 스택 메모리 구조를 표현하기 위해, **Vector 클래스의 메소드를 5개만 상속받아** 사용.

  | 메소드 | 설명 |
  |:------|:------|
  | boolean empty() | 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환 |
  | E peek() | 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소를 반환 |
  | E pop() | 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소를 반환하고, 해당 요소를 스택에 제거 |
  | E push(E item) | 스택의 제일 상단에 전달된 요소를 삽입 |
  | int search(Object o) | 스택에서 전달된 객체가 존재하는 위치의 인덱스를 반환<br/>이때, 인덱스는 제일 상단에 있는(제일 마지막으로 저장된) 요소의 위치부터 0이 아닌 1부터 시작 |
  
- 💡 더욱 복잡하고 빠른 스택을 구현하고 싶다면, Deque 인터페이스를 구현한 ArrayDeque 클래스를 사용.

  ```java
  Deque<Integer> st = new ArrayDeque<Integer>();
  ```
  - 단, ArrayDeque 클래스는 Stack 클래스와 달리 search() 메소드는 지원하지 않는다.
  
- ex) 여러 Stack 메소드를 이용하여 스택 메모리 구조를 구현

  ```java
  import java.util.*;
  
  public class StackExam {
    public static void main(String[] args) {
      Stack<Integer> st = new Stack<Integer>(); // 스택의 생성
      // Deque<Integer> st = new ArrayDeque<Integer>();
      
      // push() 메소드를 이용한 요소의 저장
      st.push(4);
      st.push(2);
      st.push(3);
      st.push(1);
      
      // peek() 메소드를 이용한 요소의 반환
      System.out.println(st.peek()); // 1
      System.out.println(st); // [4, 2, 3, 1]
      
      // pop() 메소드를 이용한 요소의 반환 및 제거
      System.out.println(st.pop()); // 1
      System.out.println(st); // [4, 2, 3]
      
      // search() 메소드를 이용한 요소의 위치 탐색(인덱스 반환)
      System.out.println(st.search(4)); // 3
      System.out.println(st.search(3)); // 1
    }
  }
  ```
  
## Queue\<E> 인터페이스
- 클래스로 구현된 스택과 달리 자바에서 **큐 메모리 구조는 별도의 인터페이스 형태**로 제공된다.
- 이러한 Queue 인터페이스를 상속받는 하위 인터페이스는 다음과 같다.
  1.
  


  
## 출처
- [코딩의 시작, TCP School \| JAVA \| Stack과 Queue](https://www.tcpschool.com/java/java_collectionFramework_stackQueue)
