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

- 💡 리스트 vs 배열

  ![리스트와 배열의 차이](/assets/images/java/list_vs_array.png)

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
        System.out.print(arrList.get(i) + " "); // 40 20 30 10
      }
      
      // remove() 메소드를 이용한 요소의 제거
      arrList.remove(1);
      
      // Enhanced for, get() 메소드를 이용한 요소의 출력
      for(int e : arrList) {
        System.out.print(e + " "); // 40 30 10
      }
      
		  // Collections.sort() 메소드를 이용한 요소의 정렬
		  Collections.sort(arrList);
      
      // iterator(), get() 메소드를 이용한 요소의 출력
      Iterator<Integer> iter = arrList.iterator();
      while(iter.hasNext()) {
        System.out.print(iter.next() + " "); // 10 30 40 
      }
      
      // set() 메소드를 이용한 요소의 변경
      arrList.set(0, 20);
      
      for(int e : arrList) {
        System.out.print(e + " "); // 20 30 40
      }
      
      // size() 메소드를 이용한 요소의 총 개수
      System.out.println("리스트의 크기 : " + arrList.size()); // 3
    }
  }
  ```
  - 자바의 **Collections 클래스**는 JDK 1.2부터 제공되는 **컬렉션에서 동작하거나 컬렉션을 반환하는 클래스 메소드(static method)만으로 구성된 클래스**
  - 자바의 **Collection**은 인터페이스이며, **Collections**는 클래스임을 주의!
  
## LinkedList\<E> 클래스
- ArrayList 클래스가 배열을 이용하여 요소를 저장함으로써 발생하는 단점을 극복하기 위해 고안되었다.
- JDK 1.2부터 제공된 LinkedList 클래스는 **내부적으로 연결 리스트(linked list)를 이용하여 요소를 저장**한다.

- 배열은 저장된 요소가 순차적으로 저장되나, 연결 리스트는 저장된 요소가 **비순차적으로 분포**되며 이러한 **요소들 사이를 링크(link)로 연결**하여 구성한다.
  - **다음 요소를 가리키는 참조만을 가지는 연결 리스트**를 **단일 연결 리스트(singly linked list)**라고 한다.

    ![단일 연결 리스트](/assets/images/java/singly_linked_list.png)
  
  - 단일 연결 리스트는 요소의 저장과 삭제 작업이 **다음 요소를 가리키는 참조만 변경**하면 되므로, 아주 빠르게 처리될 수 있다.
  - 하지만, 단일 연결 리스트는 현재 요소에서 이전 요소로 접근하기가 어렵다. 따라서, **이전 요소를 가리키는 참조**도 가지는 **이중 연결 리스트(doubly linked list)**가 좀 더 많이 사용된다.
  
    ![이중 연결 리스트](/assets/images/java/doubly_linked_list.png)
    
    
  - **LinkedList 클래스**도 위와 같은 **이중 연결 리스트**를 내부적으로 구현한 것.
  - 또한, LinkedList 클래스 역시 List 인터페이스를 구현하므로 ArrayList 클래스와 사용할 수 있는 메소드가 거의 같다.<br/>
  
- ex) 여러 LinkedList 메소드를 이용하여 리스트를 생성하고 조작

  ```java
  import java.util.*;
  
  public class ListExam02 {
    public static void main(String[] args) {
      LinkedList<String> lnkList = new LinkedList<String>();
      
      // add() 메소드를 이용한 요소의 저장
      lnkList.add("넷");
      lnkList.add("둘");
      lnkList.add("셋");
      lnkList.add("하나");
      
      // for문, get() 메소드를 이용한 요소의 출력
      for(int i = 0; i < lnkList.size(); i++) {
        System.out.print(lnkList.get(i) + " "); // 넷 둘 셋 하나
      }
      
      // remove() 메소드를 이용한 요소의 제거
      lnkList.remove(1);
      
      // Enhanced for문, get() 메소드를 이용한 요소의 출력
      for(String e : lnkList) {
        System.out.print(e + " "); // 넷 셋 하나
      }
      
      // set() 메소드를 이용한 요소의 변경
      lnkList.set(2, "둘");
      
      for(String e : lnkList) {
        System.out.print(e + " "); // 넷 셋 둘
      }
      
      // size() 메소드를 이용한 요소의 총 개수
      System.out.println("리스트의 크기 : " + lnkList.size()); // 3
    }
  }
  ```
  - ArrayList와 LinkedList의 사용 방법은 동일하다. 내부적으로 요소를 저장하는 방법에 차이가 있다.
  
## Vector\<E> 클래스
- JDK 1.0부터 사용해 온 **ArrayList 클래스와 같은 동작을 수행**하는 클래스.
- 현재의 Vector 클래스는 ArrayList 클래스와 마찬가지로 **List 인터페이스를 상속받는다**.
- 따라서, Vector 클래스에서 사용할 수 있는 메소드는 ArrayList 클래스에서 사용할 수 있는 메소드와 거의 같다.
- 하지만, 현재에는 기존 코드와의 호환성을 위해서만 남아있으므로, Vector 클래스보다는 **ArrayList 클래스를 사용하는 것이 좋다**.

## List 인터페이스 메소드
- List 인터페이스는 Collection 인터페이스를 상속받으므로, Collection 인터페이스에서 정의한 메소드도 모두 사용할 수 있다.
- List 인터페이스에서 제공하는 주요 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | boolean add(E e) | 리스트(list)에 전달된 요소를 추가(선택적 기능) |
  | void add(int index, E e) | 리스트의 특정 위치에 전달된 요소를 추가(선택적 기능) |
  | void clear() | 리스트의 모든 요소를 제거(선택적 기능) |
  | boolean contains(Object o) | 리스트가 전달된 객체를 포함하고 있는지 확인 |
  | boolean equals(Object o) | 리스트와 전달된 객체가 같은지 확인 |
  | E get(int index) | 리스트의 특정 위치에 존재하는 요소 반환 |
  | boolean isEmpty() | 리스트가 비어있는지 확인 |
  | Iterator\<E> iterator() | 리스트의 반복자(iterator)를 반환 |
  | boolean remove(Object o) | 리스트에서 전달된 객체를 제거(선택적 기능) |
  | boolean remove(int index) | 리스트에서 특정 위치에 존재하는 요소를 제거(선택적 기능) |
  | E set(int index, E e) | 리스트의 특정 위치에 존재하는 요소를 전달받은 객체로 대체(선택적 기능) |
  | int size() | 리스트 요소의 총 개수 반환 |
  | Object\[\] toArray() | 리스트의 모든 요소를 Object 타입의 배열로 반환 |

## 관련 포스트 - 컬렉션 프레임워크
- [컬렉션 프레임워크(Collection Framework)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework/)
- [컬렉션 프레임워크 : Set](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework-set/)
- [컬렉션 프레임워크 : Stack과 Queue](https://seo2021.github.io/java/java-collection-framework-stack-and-queue/)
- [컬렉션 프레임워크 : Map](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework-map/)
- [컬렉션 프레임워크 : Iterator](https://seo2021.github.io/java/001-java-collection-framework-iterator/)
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| List](https://programmers.co.kr/learn/courses/9/lessons/259)
- [코딩의 시작, TCP School \| JAVA \| List 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_list)
