---
title: "[자바] Comparable과 Comparator"
layout: single
related: true
categories:
  - JAVA
tags:
  - comparable
  - comparator
---

## Comparable\<T> 인터페이스
- 정렬 수행 시, **기본 정렬 기준**이 되는 메소드를 정의하는 인터페이스.
  - **객체를 정렬**하는 데 사용되는 메소드인 `compareTo()` 메소드를 정의하고 있다.
- 자바에서 같은 타입의 객체를 서로 비교해야만 하는 클래스들은 모두 `Comparable` 인터페이스를 구현하고 있다.
  - 따라서, **Boolean을 제외한 래퍼 클래스**나 `String, Time, Date`와 같은 클래스의 객체는 모두 정렬 가능.
- **기본 정렬 순서**는 작은 값에서 큰 값으로 정렬되는 **오름차순**.
- `java.lang` 패키지에 속한다.

- 사용 목적
  - 해당 **인터페이스를 구현한 객체** 스스로에게 부여하는 **한 가지 기본 정렬 기준**을 설정하는 목적으로 사용한다.
  - 배열의 정렬에는 보통 `Arrays` 클래스의 `sort()` 메소드를 사용한다. 아래와 같이 배열 하나만을 매개변수로 받는 `sort()` 메소드는 배열을 natural ordering 방식으로 정렬한다.

    ```java
    int[] numbers = {-3, -5, 1, 7, 4, -2};
    String[] strings = {"a", "b", "c", "A", "B", "C"};

    Arrays.sort(numbers); // {-5, -3, -2, 1, 4, 7}
    Arrays.sort(strings); // {"A", "B", "C", "a", "b", "c"}
    ```
    - 기본형(primitive type)인 `int` 배열은 바로 정렬이 가능하고, `String` 클래스는 기본적으로 `Comparable` 인터페이스를 구현하고 있기 때문에 `sort()` 메소드로 정렬이 가능하다.
    
  - 하지만, 아래와 같이 커스텀 객체 배열을 `Arrays.sort()`로 정렬하려고 하면 문제가 발생한다.
    
    ```java
    java.util.*;
    
    class Friend {
      private String name;
      private int age;
      
      public Friend(String name, int age) {
        super();
        this.name = name;
        this.age = age;
      }
    }
    
    public class SortExam {
      public static void main(String[] args) {
        Friend kim = new Friend("Kim", 36);
        Friend park = new Friend("Park", 20);
        Friend lee = new Friend("Lee", 28);
        Friend yong = new Friend("Yong", 18);
        
        Friend[] friends = {kim, park, lee, yong};
        
        // 오류 발생 -> java.lang.ClassCastException: Friend cannot be cast to java.lang.Comparable
        Arrays.sort(friends);
      }
    }
    ```
    - `Friend` 객체에 대한 **정렬 기준이 없기 때문에 오류가 발생**한다.
    - 바로 그 정렬 기준을 정하는 방법이 **`Comparable` 인터페이스를 구현**하는 것이며, `sort()` 메소드에서는 `Comparable` 인터페이스를 구현한 객체의 배열만 보낼 수 있다.
    - `Comparable` 인터페이스를 구현하면 **`compareTo()` 메서드를 오버라이딩**해야 하는데, 이 메소드가 정렬 기준을 정하는 메소드이다.
    
- 즉, `Comparable` 인터페이스는 다음과 같은 메소드를 사용하여 객체를 정렬한다.

  | 메소드 | 설명 |
  |:------|:------|
  | int compareTo(T o) | 해당 객체와 전달된 객체의 순서를 비교 |
  
  - 매개변수로 비교 대상이 되는 객체가 들어온다.
  
  
- 구현 방법 
  - 정렬할 객체에 `Comparable` 인터페이스를 `implements` 후, `compareTo()` 메소드를 재정의하여 구현.
  - `compareTo()` 메소드 작성법
    - 현재 객체 < 매개변수로 넘어온 객체 👉 음수 반환
    - 현재 객체 == 매개변수로 넘어온 객체 👉 0 반환
    - 현재 객체 > 매개변수로 넘어온 객체 👉 양수 반환
  - **음수**는 앞으로 가고, **0**은 제자리에 머물고 **양수**는 뒤로 간다.
  

- 사용 방법
  - `Arrays.sort(array)`: 배열 정렬의 경우
  - `Collections.sort(list)`: List Collection 정렬의 경우

- `Friend` 클래스에 나이 오름차순 정렬 기준을 정하는 `Comparable` 인터페이스를 구현하면 다음과 같다.

  ```java
  @Override
  public int compareTo(Friend o) {
    // 현재 객체의 age가 크면 클수록 더 큰 양수가 반환되어, 뒤 순서에 위치하게 된다.
    return this.age - o.age;
  }
  ```
  - `Friend` 클래스 내부에 정해진 정렬 규칙(나이 오름차순)으로 배열이 정렬. 만약, 나이 내림차순으로 정렬하려면 다음과 같이 작성하면 된다.
  
    ```java
    @Override
    public int compareTo(Friend o) {
      // 현재 객체의 age 크면 클수록 더 큰 음수가 반환되어, 앞 순서에 위치하게 된다.
      return o.age - this.age;
    }
    ```
  
- `List`는 `Collections` 클래스의 `sort()` 메소드를 사용하여 정렬한다.

  ```java
  Friend kim = new Friend("Kim", 36);
  Friend park = new Friend("Park", 20);
  Friend lee = new Friend("Lee", 28);
  Friend yong = new Friend("Yong", 18);
  
  List<Friend> friends = new ArrayList<>();
  friends.add(kim);
  friends.add(park);
  friends.add(lee);
  friends.add(yong);
  
  Collections.sort(friends);
  ```

- ex) 인스턴스의 비교를 위해 사용자 정의 클래스인 `Car` 클래스가 `Comparable` 인터페이스를 구현

  ```java
  class Car implements Comparable<Car> {
    // 멤버변수
    private String modelName;
    private int modelYear;
    private String color;
    
    // 생성자
    Car(String mn, int my, String c) {
      this.modelName = mn;
      this.modelYear = my;
      this.color = c;
    }
    
    // getter
    public String getModel() {
      return this.modelYear + "식 " + this.modelName + " " + this.color;
    }
    
    // 인스턴스를 정렬하기 위해 비교
    public int compareTo(Car obj) {
      if(this.modelYear == obj.modeYear) { // 같으면
        return 0;
      } else if(this.modelYear < obj.modelYear) { // 작으면
        return -1;
      } else { // 크면
        return 1;
      }
    }
  }//--end of Car
  
  public class Comparable01 {
    public static void main(String[] args) {
      Car car01 = new Car("아반떼", 2016, "노란색");
      Car car02 = new Car("소나타", 2010, "흰색");
      
      System.out.println(car01.compareTo(car02)); // 1
    }
  }
  ```
  
- 이처럼, `Comparable` 인터페이스는 그것을 구현하는 객체의 정렬 규칙을 고정적으로 갖게 된다.
  
## Comparator\<T> 인터페이스
- `Comparable` 인터페이스와 같이 **객체를 정렬**하는 데 사용되는 인터페이스.
  - 정렬 가능한 클래스(Comparable 인터페이스를 구현한 클래스)들의 **기본 정렬 기준과 다르게 정렬**하고 싶을 때 사용.
    - `Comparable`로 구현한 정렬 기준 외에 특수한 기준을 줄 수 있다. 
  - `Comparable` 인터페이스를 구현한 클래스는 기본적으로 오름차순으로 정렬된다. 기본적인 정렬 방법인 오름차순 정렬을 **내림차순으로 정렬**할 때 많이 사용한다.
  - 이때 `Comparator` 인터페이스를 구현한 클래스에서는 **`compare()` 메소드를 재정의**하여 사용하게 된다.
- 해당 인터페이스를 구현한 클래스는 **정렬 규칙 그 자체**를 의미한다.
- 주로 익명 클래스로 사용된다.
  - 그때그때 필요한 특수한 정렬 기준을 만들어서 사용하기 때문이다.  
- `java.util` 패키지에 속한다.

- `Comparator` 인터페이스는 다음과 같은 메소드를 사용하여 객체를 정렬

  | 메소드 | 설명 |
  |:------|:------|
  | int compare(T o1, T o2) | 전달된 두 객체의 순서를 비교 |
  | boolean equals(Object obj) | 해당 comparator와 전달된 객체가 같은지 확인 |
  | default Comparator\<T> reversed() | 해당 comparator의 역순인 comparator를 반환 |
  
- 구현 방법
  - `Comparator` 인터페이스를 `implements` 후, `compare()` 메소드를 재정의하여 구현.
  - `compare()` 메소드 작성법
    - 첫 번째 매개변수로 넘어온 객체 < 두 번째 매개변수로 넘어온 객체 👉 음수 반환
    - 첫 번째 매개변수로 넘어온 객체 == 두 번째 매개변수로 넘어온 객체 👉 0 반환
    - 첫 번째 매개변수로 넘어온 객체 > 두 번째 매개변수로 넘어온 객체 👉 양수 반환
  - **음수**는 앞으로 가고, **0**은 제자리에 머물고 **양수**는 뒤로 간다.

- 사용 방법
  - `Arrays.sort(array, Comparator 인터페이스 구현 클래스의 객체)`
  - `Collections.sort(list, Comparator 인터페이스 구현 클래스의 객체)`

  - 💡 메소드의 두 번째 인자로 `Comparator` 인터페이스를 받을 수 있다.
    - **우선 순위 큐(PriorityQueue) 생성자**의 두 번째 인자로 `Comparator` 인터페이스를 받을 수 있다.
    - `PriorityQueue(int initialCapacity, Comparator<? super E> comparator)`
    - 지정된 `Comparator`의 정렬 방법에 따라 우선 순위를 할당.
    

- ex) Friend 목록을 기본 규칙인 age순 정렬이 아닌, name 오름차순으로 정렬
  - 별도의 정렬 규칙을 가진 클래스를 생성
    ```java
    class SortFriendByNameInAsc implements Comparator<Friend> {
      @Override
      public int compare(Friend o1, Friend o2) {
        return o1.name.compareTo(o2.name);
      }
    }
    ```
    - `Comparator`는 비교 객체 외부에서 구현되므로, `compare()` 메소드는 비교할 객체 두 개에 대힌 정보를 모두 인자로 받는다.
    

  - `sort()` 메소드에 **정렬 대상**과 **`Comparator`를 구현한 정렬 규칙 객체**를 인자로 보낸다.
    ```java
    Friend kim = new Friend("Kim", 36);
    Friend park = new Friend("Park", 20);
    Friend lee = new Friend("Lee", 28);
    Friend yong = new Friend("Yong", 18);
    
    List<Friend> friends = new ArrayList<>();
    friends.add(kim);
    friends.add(park);
    friends.add(lee);
    friends.add(yong);
    
    Collections.sort(friends, new SortFriendByNameInAsc()); // kim, lee, park, yong
    ```
    - 이처럼 `Comparator` 인터페이스는 그것을 구현하는 클래스 자체가 규칙이 된다.
    

  - Comparator 익명 클래스 이용
    ```java
    Comparator<Friend> sortFriendByNameInAsc = new Comparator<Friend>() {
      @Override
      public int compare(Friend o1, Friend o2) {
        return o1.name.compareTo(o2.name);
      }
    }
    
    public class ComparatorExam {
      public static void main(String[] args) {
      
        ...
        
        Collections.sort(friends, sortFriendByNameInAsc);
      }
    }
    ```
    - 클래스 선언과 동시에 객체 생성


- ex) 요소를 내림차순으로 정렬하여 저장하는 `TreeSet` 인스턴스를 생성하기 위해 `Comparator` 인터페이스를 구현
  ```java
  import java.util.*;
  
  class DescendingOrder implements Comparator<Integer> {
    public int compare(Integer o1, Integer o2) {
      if(o1 instanceof Comparable && o2 instanceof Comparable) {
        Integer c1 = (Integer)o1;
        Integer c2 = (Integer)o2;
        return c2.compareTo(c1);
      }
      return -1;
    }
  }//--end of DescendingOrder
  
  public class Comparable02 {
    public static void main(String[] args) {
      TreeSet<Integer> ts = new TreeSet<Integer>(new DescendingOrder());
      
      ts.add(30);
      ts.add(40);
      ts.add(20);
      ts.add(10);
      
      Iterator<Integer> iter = ts.iterator();
      while(iter.hasNext()) {
        // 40
        // 30
        // 20
        // 10
        System.out.println(iter.next());
      }
    }
  }
  ```
  
## 요약
> - Comparable 👉 해당 인터페이스를 구현한 **객체 스스로에게 부여**하는 **한 가지 기본 정렬 규칙**을 설정
> - Comparator 👉 해당 인터페이스를 구현한 클래스는 **정렬 규칙 그 자체**를 의미하며, **기본 정렬 규칙과 다르게 정렬**하고 싶을 때 사용

## 출처
- [코딩의 시작, TCP School \| JAVA \| Comparable과 Comparator](https://www.tcpschool.com/java/java_collectionFramework_comparable)
- [Heee's Development Blog \| [Java] Comparable와 Comparator의 차이와 사용법](https://gmlwjd9405.github.io/2018/09/06/java-comparable-and-comparator.html)
- [대한민국 개발자 아빠 \| Comparable / Comparator 인터페이스 차이점](https://dev-daddy.tistory.com/23)
- [StudyNote by sungjine \| Comparable와 Comparator비교](https://sung-studynote.tistory.com/41)
- [기본기를 쌓는 정아마추어 코딩블로그 \| 자바 Comparable, Comparator 하면 '정렬'을 떠올려라, 자바 객체 정렬의 '기준'을 정하는 방법!](https://jeong-pro.tistory.com/173)
