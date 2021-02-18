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
  2. 키는 중복을 허용하지 않지만, 값의 중복은 허용한다. 👉 **키 중복 X, 값 중복 O**

- 대표적인 Map 컬렉션 클래스에 속하는 클래스는 다음과 같다.
  1. **HashMap\<K, V>**
  2. **Hashtable\<K, V>**
  3. **TreeMap\<K, V>**

## HashMap\<K, V> 클래스
- Map 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나.
- JDK 1.2부터 제공된 HashMap 클래스는 **해시 알고리즘(hash algorithm)**을 사용하여 **검색 속도가 매우 빠르다**.
- Map 인터페이스를 구현하므로 요소를 **저장 순서에 상관없이 저장**하고 **중복된 키로는 값을 저장할 수 없으나**, 같은 값을 다른 키로 저장하는 것은 가능하다.

- ex) 여러 HashMap 메소드를 이용하여 맵을 생성하고 조작

  ```java
  import java.util.*;
  
  public class MapExam01 {
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
      // hm.put("이십", 200); -> 이와 같이 덮어씌워서 value를 변경할 수도 있다.
      
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
  - 저장 순서에 상관없이 내부 해시 알고리즘에 따라 저장되는 것을 볼 수 있다.
  - 💡 위의 예제에서 사용된 **keySet() 메소드**는 해당 맵에 포함된 **모든 키 값들을 하나의 집합(Set)으로 반환**해준다.

## Hashtable\<K, V> 클래스
- JDK 1.0부터 사용해왔으며, HashMap 클래스와 같은 동작을 하는 클래스.
- 현재의 Hashtable 클래스는 HashMap 클래스와 마찬가지로 **Map 인터페이스를 상속받는다**.
  - 따라서, Hashtable 클래스에서 사용할 수 있는 메소드는 HashMap 클래스에서 사용할 수 있는 메소드와 거의 같다.
- 하지만, 현재 기존 코드와의 호환성을 위해서만 남아있으므로, **Hashtable 클래스보다는 HashMap 클래스를 사용하는 것이 좋다**.

## TreeMap\<K, V> 클래스
- **키와 값을 한 쌍**으로 하는 데이터를 **이진 검색 트리(binary search tree)**의 형태로 저장.
  - 데이터를 **키를 기준으로 정렬된 상태**로 저장. 
  - **natural ordering**을 지원하며, 생성자의 매개변수를 **Comparator 객체로 하여 정렬 방법을 임의로 지정**해줄 수 있다.
  - 이진 검색 트리는 데이터를 추가하거나 제거하는 등의 기본 동작 시간이 매우 빠르다.
- JDK 1.2부터 제공된 TreeMap 클래스는 기존의 이진 검색 트리의 성능을 향상시킨 **레드-블랙 트리(Red-Black Tree)**로 구현된다.
- Map 인터페이스를 구현하므로 요소를 **저장 순서에 상관없이 저장**하고, **중복된 키로는 값을 저장할 수 없으나** 같은 값을 다른 키로 저장하는 것은 가능하다.
  - 저장 순서에 상관없이 키를 기준으로 정렬된 상태로 저장된다.

  >- 레드-블랙 트리(Red-Black Tree)
  >   - 트리에 값이 편향되게 입력될 때 한쪽으로 치우쳐진 트리가 되는 것을 보완하기 위해 등장했다.
  >   - 부모 노드보다 작은 값을 가지는 노드는 왼쪽 자식으로, 큰 값을 가지는 노드를 오른쪽 자식으로 배치하여 데이터의 추가나 삭제 시 트리가 한쪽으로 치우쳐지지 않도록 균형을 맞춰준다.

- ex) 여러 TreeMap 메소드를 이용하여 맵을 생성하고 조작

  ```java
  import java.util.*;
  
  public class MapExam02 {
	  public static void main(String[] args) {
      TreeMap<Integer, String> tm = new TreeMap<Integer, String>();
      
      // put() 메소드를 이용한 요소의 저장
      tm.put(30, "삼십");
      tm.put(10, "십");
      tm.put(40, "사십");
      tm.put(20, "이십");
      
      // Enhanced for문, get() 메소드를 이용한 요소의 출력
      System.out.println("맵에 저장된 키들의 집합 : " + tm.keySet()); // [10, 20, 30, 40]
      for(Integer key : tm.keySet()) {
        // 키 : 10, 값 : 십
        // 키 : 20, 값 : 이십
        // 키 : 30, 값 : 삼십
        // 키 : 40, 값 : 사십
        System.out.println(String.format("키 : %s, 값 : %s", key, tm.get(key)));
      }
      
      // remove() 메소드를 이용한 요소의 제거
      tm.remove(40);
      
      // iterator(), get() 메소드를 이용한 요소의 출력
      Iterator<Integer> keys = tm.keySet().iterator();
      while(keys.hasNext()) {
        Integer key = keys.next();
        // 키 : 10, 값 : 십
        // 키 : 20, 값 : 이십
        // 키 : 30, 값 : 삼십
        System.out.println(String.format("키 : %s, 값 : %s", key, tm.get(key)));
      }
      
      // replace() 메소드를 이용한 요소의 수정
      tm.replace(20, "twenty");
      
      for (Integer key : tm.keySet()) {
        // 키 : 10, 값 : 십
        // 키 : 20, 값 : twenty
        // 키 : 30, 값 : 삼십
        System.out.println(String.format("키 : %s, 값 : %s", key, tm.get(key)));
      }
      
      // size() 메소드를 이용한 요소의 총 개수
      System.out.println("맵의 크기 : " + tm.size()); // 3
    }
  }
  ```
  
## HashMap\<K, V> 주요 메소드

  | 메소드 | 설명 |
  |:------|:------|
  | void clear() | 맵의 모든 매핑을 제거 |
  | boolean containsKey(Object key) | 맵이 전달된 키를 포함하고 있는지 확인 |
  | boolean containsValue(Object value) | 맵이 전달된 값에 해당하는 하나 이상의 키를 포함하고 있는지 확인 |
  | V get(Object key) | 맵에서 전달된 키에 대응하는 값을 반환. 만약 해당 맵이 전달된 키를 포함한 매핑을 포함하고 있지 않으면, null을 반환 |
  | boolean isEmpty() | 맵이 비어있는지 확인 |
  | Set\<K> keySet() | 맵에 포함되어 있는 모든 키로 만들어진 Set 객체를 반환 |
  | V put(K key, V value) | 맵에 전달된 키에 대응하는 값으로 특정 값을 매핑 |
  | V remove(Object key) | 맵에 전달된 키에 대응하는 매핑을 제거 |
  | boolean remove(Object key, Object value) | 맵에서 특정 값에 대응하는 특정 키의 매핑을 제거 |
  | V replace(K key, V value) | 맵에서 전달된 키에 대응하는 값을 특정 값으로 대체 |
  | boolean replace(K key, V oldValue, V newValue) | 맵에서 특정 값에 대응하는 전달된 키의 값을 새로운 값으로 대체 |
  | int size() | 맵의 매핑 총 개수 반환 |
  
  - 💡 키와 값으로 구성되는 데이터를 **매핑(mapping)** 또는 **엔트리(entry)**라고 한다.

## TreeMap\<K, V> 주요 메소드

  | 메소드 | 설명 |
  |:------|:------|
  | Map.Entry\<K, V> ceilingEntry(K key) | 맵에서 전달된 키와 같거나, 전달된 키보다 큰 키 중에서 가장 작은 키와 그에 대응하는 엔트리를 반환. 만약 해당하는 키가 없으면 null 반환. |
  | K ceilingKey(K key) | 해당 맵에서 전달된 키와 같거나, 전달된 키보다 큰 키 중에서 가장 작은 키를 반환. 만약 해당하는 키가 없으면 null을 반환. |
  | void clear() | 해당 맵의 모든 매핑을 제거 |
  | boolean containsKey(Object key) | 맵이 전달된 키를 포함하고 있는지 확인 |
  | oolean containsValue(Object value) | 맵이 전달된 값에 해당하는 하나 이상의 키를 포함하고 있는지 확인 |
  | NavigableMap\<K, V> descendingMap() | 맵에 포함된 모든 매핑을 역순으로 반환 |
  | Set\<Map.Entry\<K, V>> entrySet | 맵에 포함된 모든 매핑을 Set 객체로 반환 |
  | Map.Entry\<K, V> firstEntry() | 맵에서 현재 가장 작은(첫 번째) 키와 그에 대응하는 값의 엔트리를 반환 |
  | K firstKey() | 맵에서 현재 가장 작은(첫 번째) 키를 반환 |
  | Map.Entry\<K, V> floorEntry(K key) | 맵에서 전달된 키와 같거나, 전달된 키보다 작은 키 중에서 가장 큰 키를 반환. 만약 해당하는 키가 없으면 null을 반환 |
  | K floorKey(K key) | 맵에서 전달된 키와 같거나, 전달된 키보다 작은 키 중에서 가장 큰 키를 반환. 해당하는 키가 없으면 null을 반환 |
  | V get(Object key) | 맵에서 전달된 키에 대응하는 값을 반환. 만약 해당 맵이 전달된 키를 포함한 매핑을 포함하고 있지 않으면 null을 반환. |
  | SortedMap\<K, V> headMap(K toKey) | 맵에서 전달된 키보다 작은 키로 구성된 부분만을 반환 |
  | Map.Entry\<K, V> higherEntry(K key) | 맵에서 전달된 키보다 작은 키 중에서 가장 큰 키와 그에 대응하는 값의 엔트리를 반환. 만약 해당하는 값의 엔트리를 반환. 만약 해당하는 키가 없으면 null을 반환. |
  | K higherKey(K key) | 맵에서 전달된 키보다 작은 키 중에서 가장 큰 키를 반환. 만약 해당하는 키가 없으면 null을 반환. |
  | Set\<K> keySet() | 맵에 포함되어 있는 모든 키로 만들어진 Set 객체를 반환 |
  | Map.Entry\<K, V> lastEntry() | 맵에서 현재 가장 큰(마지막) 키와 그에 대응하는 값의 엔트리를 반환 |
  | K lastKey() | 맵에서 현재 가장 큰(마지막) 키를 반환 |
  | Map.Entry\<K, V> lowerEntry(K key) | 맵에서 전달된 키보다 큰 키 중에서 가장 작은 키와 그에 대응하는 값의 엔트리를 반환. 만약 해당하는 키가 없으면 null을 반환. |
  | K lowerKey(K key) | 맵에서 전달된 키보다 큰 키 중에서 가장 작은 키를 반환. 만약 해당하는 키가 없으면 null을 반환 |
  | Map.Entry\<K, V> pollFirstEntry() | 맵에서 현재 가장 작은(첫 번째) 키와 그에 대응하는 값의 엔트리를 반환하고, 해당 엔트리를 맵에서 제거 |
  | Map.Entry\<K, V> pollLastEntry() | 맵에서 현재 가장 큰(마지막) 키와 그에 대응하는 값의 엔트리를 반환하고, 해당 엔트리를 맵에서 제거 |
  | V put(K key, V value) | 맵에 전달된 키에 대응하는 값으로 특정 값을 매핑 |
  | V remove(Object key) | 맵에서 전달된 키에 대응하는 매핑을 제거 |
  | boolean remove(K key, V value) | 맵에서 특정 값에 대응하는 특정 키의 매핑을 제거 |
  | V replace(K key, V value) | 맵에서 전달된 키에 대응하는 값을 특정 값으로 대체 |
  | boolean replace(K key, V oldValue, V newValue) | 맵에서 특정 값에 대응하는 전달된 키의 값을 새로운 값으로 대체 |
  | int size() | 맵의 매핑 총 개수 반환 |
  | SortedMap\<K, V> subMap(K fromKey, K toKey) | 맵에서 fromKey부터 toKey까지로 구성된 부분만을 반환. 이때 fromKey는 포함되나, toKey는 포함되지 않음. |
  | SortedMap\<K, V> tailMap(K fromKey) | 맵에서 fromKey와 같거나, fromKey보다 큰 키로 구성된 부분만을 반환 |
  
  - 💡 **Map.Entry 인터페이스**는 Map 인터페이스의 내부 인터페이스로, 맵에 저장되는 엔트리 조작을 위한 메소드가 정의되어 있다.
  - 💡 NavigableMap은 SortedMap을 확장한 인터페이스.

## 관련 포스트 - 컬렉션 프레임워크
- [컬렉션 프레임워크(Collection Framework)](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework/)
- [컬렉션 프레임워크 : Set](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework-set/)
- [컬렉션 프레임워크 : List](https://seo2021.github.io/java/programmers-lectures/java-intermediate-collection-framework-list/)
- [컬렉션 프레임워크 : Stack과 Queue](https://seo2021.github.io/java/java-collection-framework-stack-and-queue/)
- [컬렉션 프레임워크 : Iterator](https://seo2021.github.io/java/001-java-collection-framework-iterator/)
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| Map](https://programmers.co.kr/learn/courses/9/lessons/260)
- [코딩의 시작, TCP School \| JAVA \| Map 컬렉션 클래스](https://www.tcpschool.com/java/java_collectionFramework_map)
- [코딩팩토리 \| [Java] 자바 TreeSet 사용법 & 예제 총정리](https://coding-factory.tistory.com/555)
