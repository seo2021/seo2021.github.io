---
title: "[프로그래머스 자바 중급] 컬렉션 프레임워크 : List"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - collection-framework
  - list
  - 자바중급
---

## List 컬렉션 클래스
- List 인터페이스를 구현한 모든 List 컬렉션 클래스는 다음과 같은 특징을 가진다.
  1. 요소의 저장 순서가 유지된다. 👉 **순서 O**
  2. 같은 요소의 중복 저장을 허용한다. 👉 **중복 O**
  
- List 컬렉션 클래스에 속하는 대표적인 클래스는 다음과 같다.
  1. **ArrayList\<E>**
  2. **LinkedList\<E>**
  3. **Vector\<E>**
  4. **Stack\<E>**
  
## ArrayList\<E> 클래스
- 가장 많이 사용되는 컬렉션 클래스 중 하나.
- JDK 1.2부터 제공된 ArrayList 클래스는 **내부적으로 배열을 이용하여 요소를 저장**한다.

- ArrayList 클래스는 배열을 이용하기 때문에 **인덱스를 이용해 배열 요소에 빠르게 접근**할 수 있다.
- 하지만 배열은 크기를 변경할 수 없는 인스턴스이므로, 크기를 늘리기 위해서는 새로운 배열을 생성하고 기존의 요소들을 옮겨야 하는 복잡한 과정을 거쳐야 한다.
  - 물론 이 과정은 자동으로 수행되지만, **요소의 추가 및 삭제 작업에 걸리는 시간이 매우 길어지는 단점**이 있다.

- ex) 여러 ArrayList 메소드를 이용하여 리스트를 생성하고 조작

  ```java
  import java.util.*;
  
  public class ListExam01 {
    public static void main(String[] args) { 
      ArrayList<Integer> arrList = new ArrayList<Integer>();
      
      // add() 메소드를 이용한 요소의 저장
      arrList.add(40);
      arrList.add(20);
      arrList.add(30);
      arrList.add(10);
      
      // for문, get() 메소드를 이용한 요소의 출력
      for(int i = 0; i < arrList.size(); i++) {
        System.out.print(arrList.get(i) + " ");
      }
      
      // remove() 메소드를 이용한 요소의 제거
      
      
    }
  }
  
  ```


  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| List](https://programmers.co.kr/learn/courses/9/lessons/259)
- [코딩의 시작, TCP School \| JAVA \| List 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_list)
