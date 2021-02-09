---
title: "[프로그래머스 자바 중급] 컬렉션 프레임워크(Collection Framework)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - collection-framework
  - 자바중급
---

## 컬렉션 프레임워크(collection framework)란?
- 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합.
- 즉, 데이터를 저장하는 **자료 구조**와 데이터를 처리하는 **알고리즘**을 **구조화하여 클래스로 구현**해놓은 것.
- 인터페이스(interface)를 사용하여 구현된다.

## 컬렉션 프레임워크 주요 인터페이스
- 컬렉션 프레임워크에서는 데이터를 저장하는 자료 구조에 따라 다음과 같은 핵심이 되는 주요 인터페이스를 정의하고 있다.

  1. List 인터페이스
  2. Set 인터페이스
  3. Map 인터페이스
  
  
- 이 중에서 **List와 Set 인터페이스는 모두 Collection 인터페이스를 상속**받지만, 구조상의 차이로 인해 **Map 인터페이스는 별도로 정의**된다.
- 따라서, List 인터페이스와 Set 인터페이스의 공통된 부분을 Collection 인터페이스에서 정의하고 있다.

## 주요 인터페이스 간의 상속 관계
- 자바에서 컬렉션 프레임워크를 구성하고 있는 인터페이스 간의 상속 관계는 다음 그림과 같다.

  ![컬렉션 프레임워크 상속 관계](/assets/images/java/collection_interface_diagram.png)
  
  - 위의 그림에서 \<E>나 <K, V>라는 것은 **컬렉션 프레임워크를 구성하는 모든 클래스가 제네릭으로 표현되어 있음**을 알려준다.
  
## 주요 인터페이스의 간략한 특징

  | 인터페이스 | 설명 | 구현 클래스 |
  |:---------:|:-----|:-----------|
  | List<E> | 순서가 있는 데이터의 집합으로, 데이터의 중복을 허용. | Vector, ArrayList, LinkedList, Stack, Queue |
  | Set<E> | 순서가 없는 데이터의 집합으로, 데이터의 중복을 허용하지 않음. | HashSet, TreeSet |
  | Map<K, V> | 키와 값의 한 쌍으로 이루어지는 데이터의 집합으로, 순서가 없음.<br/>이때 키는 중복을 허용하지 않지만, 값은 중복될 수 있음 | HashMap, TreeMap, Hashtable, Properties |

## 컬렉션 클래스(collection class)
- **컬렉션 프레임워크에 속하는 인터페이스를 구현한 클래스**를 컬렉션 클래스(collection class)라고 한다.
- Vector나 Hashtable과 같은 컬렉션 클래스는 예전부터 사용해왔으므로, 기존 코드와의 호환을 위해 아직도 남아 있다.
  - 하지만, 기존 컬렉션 클래스 보다 새로 추가된 ArrayList나 HashMap 클래스를 사용하는 것이 성능 면에서 더 나은 결과를 얻을 수 있다.
  
- ex) ArrayList 클래스를 이용하여 리스트를 생성하고 조작하는 예제

  ```java
  import java.util.*;
  
  public class Collection01 {
    public static void main(String[] args) {
      // 리스트 생성
      ArrayList<String> arrList = new ArrayList<String>();
      
      // 리스트에 요소 저장
      arrList.add("넷");
      arrList.add("둘");
      arrList.add("셋");
      arrList.add("하나");
      
      // 리스트 요소 출력
      for(int i = 0; i < arrList.size(); i++) {
        // 넷
        // 둘
        // 셋
        // 하나
        System.out.println(arrList.get(i));
      }
    }
  }
  ```
  
## Collection 인터페이스
- List와 Set 인터페이스의 많은 공통된 부분을 Collection 인터페이스에서 정의하고, 두 인터페이스는 그것을 상속받는다.
- 따라서, Collection 인터페이스는 **컬렉션을 다루는데 가장 기본적인 동작들을 정의**하고, 그것을 **메소드로 제공**하고 있다.

- Collection 인터페이스에서 제공하는 주요 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | boolean add(E e) | 컬렉션에 전달된 요소를 추가(선택적 기능) |
  | void clear() | 컬렉션의 모든 요소를 제거(선택적 기능) |
  | boolean contains(Object o) | 컬렉션이 전달된 객체를 포함하고 있는지 확인 |
  | boolean equals(Object o) | 켈력션과 전달된 객체가 같은지 확인 |
  | boolean isEmpty() | 컬렉션이 비어있는지 확인 |
  | Iterator<E> iterator() | 컬렉션의 반복자(iterator) 반환 |
  | boolean remove(Object o) | 컬렉션에서 전달된 객체 제거(선택적 기능) |
  | int size() | 컬렉션 요소의 총 개수 반환 |
  | Object[] toArray() | 컬렉션의 모든 요소를 Object 타입의 배열로 반환 |
  
  - Iterator는 꺼낼 요소가 있는지 살펴보는 hasNext() 메소드와 요소를 하나씩 꺼낼 때 사용하는 next() 메소드 등을 가지고 있다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 컬렉션 프레임워크](https://programmers.co.kr/learn/courses/9/lessons/256)
- [코딩의 시작, TCP School \| JAVA \| 컬렉션 프레임워크의 개념](https://www.tcpschool.com/java/java_collectionFramework_concept)
