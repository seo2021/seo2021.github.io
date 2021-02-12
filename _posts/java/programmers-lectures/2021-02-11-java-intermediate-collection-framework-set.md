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
  1. 요소의 저장 순서를 유지하지 않는다. 👉 **순서 X**
  2. 같은 요소의 중복 저장을 허용하지 않는다. 👉 **중복 X**
  
- 대표적인 Set 컬렉션 클래스에 속하는 클래스는 다음과 같다.
  1. **HashSet\<E>**
  2. **TreeSet\<E>**
  
## HashSet\<E> 클래스
- Set 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나.
- JDK 1.2부터 제공된 HashSet 클래스는 **해시 알고리즘을 사용하여 검색 속도가 매우 빠르다**.
- 내부적으로 **HashMap 인스턴스**를 이용하여 요소를 저장한다.
- **Set 인터페이스를 구현**하므로, 요소를 **순서에 상관없이 저장**하고 **중복된 값은 저장하지 않는다**.
  - 만약 요소의 저장 순서를 유지해야 한다면, JDK 1.4부터 제공하는 **LinkedHashSet 클래스**를 사용하면 된다.
  
- ex) HashSet 메소드를 이용하여 집합을 생성하고 조작
  
  ```java
  import java.util.HashSet;
  import java.util.Iterator;
  
  public class SetExam01 {
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
    - HashSet에 이미 존재하는 요소인지 파악하기 위해 내부에서 일어나는 과정
      1. 해당 요소에 hashCode() 메소드를 호출하여 반환된 해시값으로 검색할 범위를 결정.
      2. 해당 범위 내 요소들을 equals() 메소드로 비교
    - 💡 따라서, HashSet에서 add() 메소드를 사용하여 **중복없이 새로운 요소를 추가**하기 위해서는 **hashCode()와 equals() 메소드를 상황에 맞게 오버라이딩**해야 한다.

- ex) 사용자가 정의한 Animal 클래스의 인스턴스를 HashSet에 저장하기 위해 **hashCode()와 equals() 메소드를 오버라이딩**

  ```java
  import java.util.*;
  
  class Animal {
    // String 변수
    String species;
    String habitat;
    
    Animal(String species, String habitat) {
      this.species = species;
      this.habitat = habitat;
    }
    
    // hashCode() 재정의: species + habitat를 해시코드로 반환
    public int hashCode() { 
      return (species + habitat).hashCode(); 
    }
    
    // equals() 재정의
    public boolean equals(Object obj) {
      // Animal 클래스의 인스턴스면
      if(obj instanceof Animal) {
        Animal temp = (Animal)obj;
        // species와 habitat의 문자열이 전부 동일한지 확인
        return species.equals(temp.species) && habitat.equals(temp.habitat);
      } 
      else {
        return false;
      }
    }
  } //--end of Animal
  
  public class SetExam02 {
    public static void main(String[] args) {
      HashSet<Animal> hs = new HashSet<Animal>();
      
      hs.add(new Animal("고양이", "육지"));
      hs.add(new Animal("고양이", "육지"));
      hs.add(new Animal("고양이", "육지"));
      
      System.out.println(hs.size()); // 1
    }
  }
  ```
  - Animal 인스턴스들을 **오버라이딩한 equals()로 비교**한 결과, 각 인스턴스의 **species와 habitat 문자열이 모두 동일하므로 동일한 인스턴스라고 판단**된다. 따라서, 처음의 인스턴스 1개만 HashSet에 저장되었다.
  
## 해시 알고리즘(hash algorithm)
- **해시 함수(hash function)**을 사용하여 **데이터를 해시 테이블(hash table)에 저장**하고, 다시 그것을 **검색**하는 알고리즘.
- 자바에서 해시 알고리즘을 이용한 자료 구조는 아래의의 그림과 같이 **배열**과 **연결 리스트**로 구현된다.

  ![해시 알고리즘을 이용한 자료구조](/assets/images/java/hash_algorithm.png)
  
  1. 저장할 데이터의 키값을 해시 함수에 넣어 반환되는 값으로 배열의 인덱스를 구한다.
  2. 해당 인덱스에 저장된 연결 리스트에 데이터를 저장한다.
  
  - ex) 정수형 데이터를 길이가 10인 배열에 저장한다고 하면 '1,000,002'를 검색하는 방법
    - 1,000,002를 10으로 나눈 나머지가 2이므로, **배열의 세 번째 요소**에 연결된 **연결 리스트**에서 검색
    
## TreeSet\<E> 클래스
-


  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Set](https://programmers.co.kr/learn/courses/9/lessons/258)
- [코딩의 시작, TCP School \| JAVA \| Set 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_set)
