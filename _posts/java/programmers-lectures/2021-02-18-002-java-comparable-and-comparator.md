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
- **객체를 정렬**하는 데 사용되는 메소드인 **compareTo() 메소드**를 정의하고 있다.
- 자바에서 같은 타입의 인스턴스를 서로 비교해야만 하는 클래스들은 모두 Comparable 인터페이스를 구현하고 있다.
  - 따라서, **Boolean을 제외한 래퍼 클래스**나 **String, Time, Date**와 같은 클래스의 인스턴스는 모두 정렬 가능.
- **기본 정렬 순서**는 작은 값에서 큰 값으로 정렬되는 **오름차순**.

- Comparable 인터페이스는 다음과 같은 메소드를 사용하여 객체를 정렬한다.

  | 메소드 | 설명 |
  |:------|:------|
  | int compareTo(T o) | 해당 객체와 전달된 객체의 순서를 비교 |

- ex) 인스턴스의 비교를 위해 사용자 정의 클래스인 Car 클래스가 Comparable 인터페이스를 구현

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
    
    // 객체를 정렬하기 위해 비교
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
  
## Comparator\<T> 인터페이스
- Comparable 인터페이스와 같이 **객체를 정렬**하는 데 사용되는 인터페이스.
- Comparable 인터페이스를 구현한 클래스는 기본적으로 오름차순으로 정렬된다. 반면에 **Comparator 인터페이스는 내림차순이나 아니면 다른 기준으로 정렬**하고 싶을 때 사용할 수 있다.
  - 즉, Comparator 인터페이스를 구현하면 **오름차순 이외의 기준으로도 정렬**할 수 있게 된다. 
- Comparator 인터페이스를 구현한 클래스에서는 **compare() 메소드를 재정의**하여 사용하게 된다.

- Comparator 인터페이스는 다음과 같은 메소드를 사용하여 객체를 정렬

  | 메소드 | 설명 |
  |:------|:------|
  | int compare(T o1, T o2) | 전달된 두 객체의 순서를 비교 |
  | boolean equals(Object obj) | 해당 comparator와 전달된 객체가 같은지 확인 |
  | default Comparator\<T> reversed() | 해당 comparator의 역순인 comparator를 반환 |

- ex) 요소를 내림차순으로 정렬하여 저장하는 TreeSet 인스턴스를 생성하기 위해 Comparator 인터페이스를 구현

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

## 출처
- [코딩의 시작, TCP School \| JAVA \| Comparable과 Comparator](https://www.tcpschool.com/java/java_collectionFramework_comparable)
