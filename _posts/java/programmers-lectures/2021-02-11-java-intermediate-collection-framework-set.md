---
title: "[프로그래머스 자바 중급] 컬렉션 프레임워크 : Set"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - collection-framework
  - set
  - 자바중급
---

## Set 컬렉션 클래스
- Set 인터페이스를 구현한 모든 Set 컬렉션 클래스는 다음과 같은 특징을 가진다.
  1. 요소의 저장 순서를 유지하지 않는다. 👉 순서 X
  2. 같은 요소의 중복 저장을 허용하지 않는다. 👉 중복 X
  
- 대표적인 Set 컬렉션 클래스에 속하는 클래스는 다음과 같다.
  1. HashSet<E>
  2. TreeSet<E>
  
## HashSet<E> 클래스
- Set 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나.
- JDK 1.2부터 제공된 HashSet 클래스는 **해시 알고리즘을 사용하여 검색 속도가 매우 빠르다**.
- 내부적으로 **HashMap 인스턴스**를 이용하여 요소를 저장한다.
- **Set 인터페이스를 구현**하므로, 요소를 **순서에 상관없이 저장**하고 **중복된 값은 저장하지 않는다**.
  - 만약 요소의 저장 순서를 유지해야 한다면, JDK 1.4부터 제공하는 **LinkedHashSet 클래스**를 사용하면 된다.
  
- ex) HashSet 메소드를 이용하여 집합을 생성하고 조작
  
  ```java
  import java.util.HashSet;
  import java.util.Iterator;
  
  public class SetExam {
    public static void main(String[] args) {
      HashSet<String> hs01 = new HashSet<String>();
      HashSet<String> hs02 = new HashSet<String>();

      // add() 메소드를 이용한 요소의 저장
      hs01.add("홍길동");
      hs01.add("이순신");
      System.out.println(hs01.add("임꺽정")); // true
      System.out.println(hs01.add("임꺽정")); // false, 중복된 요소의 저장

      // Enhanced for문, get() 메소드를 이용한 요소의 출력
      for(String e : hs01) {
        System.out.print(e + " "); // 홍길동 이순신 임꺽정
      }

      // add() 메소드를 이용한 요소의 저장
      hs02.add("임꺽정");
      hs02.add("홍길동");
      hs02.add("이순신");

      // iterator() 메소드를 이용한 요소의 출력
      Iterator<String> iter02 = hs02.iterator();
      while(iter02.hasNext()) {
        System.out.print(iter02.next() + " "); // 홍길동 이순신 임꺽정
      }

      // size() 메소드를 이용한 요소의 총 개수
      System.out.println("집합의 크기: " + hs02.size()); // 집합의 크기: 3
    }
  }
  ```
  - 요소의 저장 순서를 바꿔도 실제 **저장되는 순서에는 영향이 없는 것**을 확인할 수 있다.
  - 또한, HashSet에 이미 존재하는 요소를 추가하려고 하면 해당 요소를 저장하지 않고 false가 반환된다.


  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Set](https://programmers.co.kr/learn/courses/9/lessons/258)
- [코딩의 시작, TCP School \| JAVA \| Set 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_set)