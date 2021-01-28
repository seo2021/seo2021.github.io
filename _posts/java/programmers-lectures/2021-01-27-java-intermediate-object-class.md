---
title: "[프로그래머스 자바 중급] Object 클래스와 오버라이딩(Overriding)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - object
  - 오버라이딩
  - 자바중급
---

## java.lang 패키지
- 자바에서 가장 **기본적인 동작을 수행**하는 **클래스들의 집합**.
- java.lang 패키지의 클래스들은 import 문을 사용하지 않아도 **클래스 이름만으로 바로 사용**할 수 있음.

## Object 클래스
- java.lang 패키지 중에서 가장 많이 사용되는 클래스.
- 모든 자바 클래스의 **최상위 클래스**.
- 아무것도 상속받지 않으면 자동으로 Object를 상속.
- Object 클래스의 메소드는 **모든 자바 클래스에서 사용**할 수 있다.
- 총 11개의 메소드만으로 구성되어 있다.

## Object 클래스의 메소드
- 사용할 때 반드시 오버라이딩해서 사용한다.

  | 메소드 | 설명 |
  |:------|:------|
  | protected Object **clone()** | 해당 객체의 복제본을 생성하여 반환 |
  | boolean **equals(Object obj)** | 해당 객체와 전달받은 객체가 같은지 여부를 확인 |
  | protected void **finalize()** | 해당 객체를 더는 아무도 참조하지 않아 가비지 컬렉터가 객체의 리소스를 정리하기 위해 호출함 |
  | Class<T> **getClass()** | 해당 객체의 클래스 타입을 반환 |
  | int **hashCode()** | 해당 객체의 해시 코드값을 반환 |
  | void **nofity()** | 해당 객체의 대기(wait)하고 있는 하나의 스레드를 다시 실행할 때 호출 |
  | void **notifyAll()** | 해당 객체의 대기(wait)하고 있는 모든 스레드를 다시 실행할 때 호출 |
  | String **toString()** | 해당 객체의 정보를 문자열로 반환 |
  | void **wait()** | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  | void **wait(long timeout)** | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나, 전달받은 시간이 지날 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  | void wait(long timeout, int nanos) | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나, 전달받은 시간이 지나거나, 다른 스레드가 현재 스레드를 인터럽트(interrupt)할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  
## 가장 많이 사용되는 Object 클래스의 메소드 3가지
- toString()
  - 해당 인스턴스에 대한 정보를 문자열로 반환
  - 이때, 반환되는 문자열은 **클래스 이름**과 함께 구분자로 '**@**'가 사용되며, 그 뒤로 **16진수 해시 코드(hash code)**가 추가된다.
  - 16진수 해시 코드 값은 **인스턴스의 주소**를 가리키는 값으로, 인스턴스마다 모두 **다르게** 반환된다.
  
  - ex) toString() 메소드를 이용하여 인스턴스의 정보를 출력
  
    ```java
    Car car01 = new Car();
    Car car02 = new Car();

    System.out.println(car01.toString()); // Car@15db9742
    System.out.println(car02.toString()); // Car@6d06d69c
    ```
  
  - 💡 자바에서 toString() 메소드는 기본적으로 각 API 클래스마다 자체적으로 오버라이딩을 통해 재정의되어 있다.
  
  - ex) String 클래스에 재정의되어 있는 toString() 메소드 사용
    - 객체가 가진 속성값을 출력하도록 재정의되어 있다.
    
    ```java
    @Override
    public String toString() {
      return "Car [modelName=" + modelName + ", modelYear=" + modelYear + ", color=" + color + "]";
    }

    public static void main(String[] args) {
      ...
      // Car [modelName=아반떼, modelYear=2016, color=흰색]
      System.out.println(car01.toString()); 
      System.out.println(car01); 
    }
    ```
    - `s1`과 `s1.toString()`의 출력 결과는 동일.
      - 객체를 출력하면 내부적으로 toString() 메소드를 호출하여 출력.
      
- equals()
  - 해당 인스턴스를 매개변수로 전달받는 참조 변수와 비교하여, 그 결과를 반환.
  - 참조 변수가 가리키는 값(주소)을 비교하므로, 서로 다른 두 객체는 언제나 false를 반환
  
  - ex) equals() 메소드를 이용하여 두 인스턴스를 서로 비교
  
    ```java
    Car car01 = new Car();
    Car car02 = new Car();
    
    System.out.println(car01.equals(car02)); // false
    car 01 = car02; // 두 참조 변수가 같은 주소를 가리킴
    System.out.println(car01.equals(car02)); // true
    ```
    
  - 💡 자바에서 equals() 메소드는 기본적으로 각 API 클래스마다 자체적으로 오버라이딩을 통해 재정의되어 있다.
  
  **🐥🐥🐥🐥🐥🐥여기서부터 작성🐥🐥🐥🐥🐥🐥🐥**
  

- hashCode()
  - 객체의 해시코드 값 반환.
  - 해시코드는 되도록 서로 다른 값을 가지는 것이 좋다.
  
- ex) Object 클래스로부터 상속받은 equals(), hashCode() 사용

  ```java
  public class Student {
    String name;
    String number;
    int birthYear;
    
    public static void main(String[] args) {
      // Student 객체 생성
      Student s1 = new Student();
      s1.name = "홍길동";
      s1.number = "1234";
      s1.birthYear = 1995;
      
      Student s2 = new Student();
      s2.name = "홍길동";
      s2.number = "1234";
      s2.birthYear = 1995;

      // 서로 다른 두 객체 비교(각 참조 변수가 다른 주소를 가리킴)
      if(s1.equals(s2))
        System.out.println("s1 == s2");
      else
        System.out.println("s1 != s2"); // "s1 != s2" 출력
      
      // 각 객체의 hashcode 출력
      System.out.println(s1.hashCode()); // 705927765
      System.out.println(s2.hashCode()); // 366172642
    }
  }
  ```
  - Object 클래스의 hashcode() 메소드를 통해서는 두 객체가 서로 다른 hashcode를 가진다.
  - Object 클래스의 equals() 메소드는 hashcode로 객체를 비교하므로, 두 객체의 필드가 동일한 값을 가짐에도 서로 다른 객체라고 판단한다.
  
- ex) equals(), hashCode() 오버라이딩

  ```java
  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    // number 속성을 사용하여 hashcode 구하기
    result = prime * result + ((number == null) ? 0 : number.hashCode());
    return result;
  }
  
  @Override
  public boolean equals(Object obj) {
    if(this == obj) // 참조가 같다면
      return true;
    if(obj == null) // 비교하는 객체가 null이면
      return false;
    if(getClass() != obj.getClass()) // 서로 다른 클래스이면
      return false;
      
    Student other = (Student) obj;
    if(number == null) {
      if(other.number != null)
        return false;
    }
    // number로 객체를 비교
    else if(!number.equals(other.number))
      return false;
      
    return true;
  }
  ```
  - number 속성으로 hashcode를 구하도록 hashCode() 메소드를 오버라이딩
    - number가 동일하면 동일한 hashcode를 가지게 된다.
  - hashcode가 아닌 number 필드로 두 객체가 동일한지 판단하도록 eqauls() 메소드를 오버라이딩
  
  - 다시 두 객체를 비교하면 number로 비교하므로 동일한 객체라고 판단된다.
  - 또한, 동일한 number를 가지므로 동일한 hashcode를 가진다.
  
    ```java
    public static void main(String[] args) {
      ...
      // "s1 == s2" 출력
      if(s1.equals(s2))
        System.out.println("s1 == s2");
      else
        System.out.println("s1 != s2"); 

      // 동일한 hashcode를 가진다
      System.out.println(s1.hashCode()); // 1509473
      System.out.println(s2.hashCode()); // 1509473
    }
    ```



## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Object와 오버라이딩](https://programmers.co.kr/learn/courses/9/lessons/249#)
- [코딩의 시작, TCP School \| JAVA \| Object 클래스](https://www.tcpschool.com/java/java_api_object)
