---
title: "[프로그래머스 자바 중급] 컬렉션 프레임워크 : Map"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - collection-framework
  - map
  - 자바중급
---

## Map 컬렉션 클래스
- Map 인터페이스는 Collection 인터페이스와는 다른 저장 방식을 가진다.
- Map 인터페이스를 구현한 Map 컬렉션 클래스들은 **키와 값을 하나의 쌍으로 저장하는 방식(key-value 방식)**을 사용.
  - 여기서 키(key)란 실질적인 값(value)을 찾기 위한 이름의 역할을 한다.

- Map 인터페이스를 구현한 모든 Map 컬렉션 클래스는 다음과 같은 특징을 가진다.
  1. 요소의 저장 순서를 유지하지 않는다. 👉 **순서 X**
  2. 키는 중복을 허용하지 않지만, 값의 중복은 허용한다. 👉 **값 중복 O**

- 대표적인 Map 컬렉션 클래스에 속하는 클래스는 다음과 같다.
  1. **HashMap\<K, V>**
  2. **Hashtable\<K, V>**
  3. **TreeMap\<K, V>**

## HashMap\<K, V> 클래스
- Map 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나.
- JDK 1.2부터 제공된 HashMap 클래스는 **해시 알고리즘(hash algorithm)**을 사용하여 **검색 속도가 매우 빠르다**.
- Map 인터페이스를 구현하므로 **중복된 키로는 값을 저장할 수 없으나**, 같은 값을 다른 키로 저장하는 것은 가능하다.

- ex) 여러 HashMap 메소드를 이용하여 맵을 생성하고 조작

  ```java
  import java.util.*;
  
  public class MapExam {
    public static void main(String[] args) {
      HashMap<String, Integer> hm = new HashMap(String, Integer>();
      
      // put() 메소드를 이용한 요소의 저장
      hm.put("삼십", 30);
      hm.put("십", 10);
      hm.put("사십", 40);
      hm.put("이십", 20);
      
      // Enhanced for문, get() 메소드를 이용한 요소의 출력
      System.out.println("맵에 저장된 키들의 집합 : " + hm.keySet()); // [이십, 삼십, 사십, 십]
      for(String key : hm.keySet()) {
        // 키 : 이십, 값 : 20
        // 키 : 삼십, 값 : 30
        // 키 : 사십, 값 : 40
        // 키 : 십, 값 : 10
        System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
      }
      
      // remove() 메소드를 이용한 요소의 제거
      hm.remove("사십");
      
      // iterator() 메소드와 get() 메소드를 이용한 요소의 출력
      Iterator<String> keys = hm.keySet().iterator();
      while(keys.hasNext()) {
        String key = keys.next();
        // 키 : 이십, 값 : 20
        // 키 : 삼십, 값 : 30
        // 키 : 십, 값 : 10
        System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
      }
      
      // replace() 메소드를 이용한 요소의 수정
      hm.replace("이십", 200);
      
      for (String key : hm.keySet()) {
        // 키 : 이십, 값 : 200
        // 키 : 삼십, 값 : 30
        // 키 : 십, 값 : 10
        System.out.println(String.format("키 : %s, 값 : %s", key, hm.get(key)));
      }

      // size() 메소드를 이용한 요소의 총 개수
      System.out.println("맵의 크기 : " + hm.size()); // 3
    }
  }
  ```
  - 위의 예제에서 사용된 **keySet() 메소드**는 해당 맵에 포함된 **모든 키 값들을 하나의 집합(Set)으로 반환**해준다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Map](https://programmers.co.kr/learn/courses/9/lessons/260)
- [코딩의 시작, TCP School \| JAVA \| Map 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_map)
