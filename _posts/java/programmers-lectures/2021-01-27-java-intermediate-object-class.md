---
title: "[프로그래머스 자바 중급] Object 클래스와 오버라이딩(Overriding)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java.lang패키지
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

  | 메소드 | 설명 |
  |:------|:------|
  | protected Object **clone()** | 해당 객체의 복제본을 생성하여 반환 |
  | boolean **equals(Object obj)** | 해당 객체와 전달받은 객체가 같은지 여부를 확인 |
  | protected void **finalize()** | 해당 객체를 더는 아무도 참조하지 않아 가비지 컬렉터가 객체의 리소스를 정리하기 위해 호출함 |
  | Class\<T\> **getClass()** | 해당 객체의 클래스 타입을 반환 |
  | int **hashCode()** | 해당 객체의 해시 코드값을 반환 |
  | void **nofity()** | 해당 객체의 대기(wait)하고 있는 하나의 스레드를 다시 실행할 때 호출 |
  | void **notifyAll()** | 해당 객체의 대기(wait)하고 있는 모든 스레드를 다시 실행할 때 호출 |
  | String **toString()** | 해당 객체의 정보를 문자열로 반환 |
  | void **wait()** | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  | void **wait(long timeout)** | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나, 전달받은 시간이 지날 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  | void **wait(long timeout, int nanos)** | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나, 전달받은 시간이 지나거나, 다른 스레드가 현재 스레드를 인터럽트(interrupt)할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출 |
  
## 가장 많이 사용되는 Object 클래스의 메소드 3가지
- **toString()**
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
  
  - ex) **String 클래스에 재정의**되어 있는 toString() 메소드
    - 인스턴스가 가진 **속성값을 출력**하도록 재정의되어 있다.
    - 어떠한 속성값을 출력할지 지정할 수 있다.
    
    ```java
    // 모든 속성값을 출력하도록 재정의
    @Override
    public String toString() {
      return "Car [modelName=" + modelName + ", modelYear=" + modelYear + ", color=" + color + "]";
    }

    public static void main(String[] args) {
      Car car01 = new Car("아반떼", 2016, "흰색");
      
      // Car [modelName=아반떼, modelYear=2016, color=흰색]
      System.out.println(car01.toString()); 
      System.out.println(car01); 
    }
    ```
    - `car01`과 `car01.toString()`의 출력 결과는 동일.
      - 인스턴스를 출력하면 내부적으로 toString() 메소드를 호출하여 출력.  
      
- **equals()**
  - 해당 **인스턴스**를 매개변수로 전달받는 **참조 변수와 비교**하여, 그 결과를 반환.
  - 참조 변수가 가리키는 **값(주소)을 비교**하므로, 서로 다른 두 인스턴스는 언제나 false를 반환.
  - **하위 클래스에서 재정의**하여 **원하는 기준으로 비교 가능**하다.
  
  - ex) equals() 메소드를 이용하여 두 인스턴스를 서로 비교
  
    ```java
    Car car01 = new Car();
    Car car02 = new Car();
    
    System.out.println(car01.equals(car02)); // false
    car01 = car02; // 두 참조 변수가 같은 주소를 가리킴
    System.out.println(car01.equals(car02)); // true
    ```
    
    ![Car 객체의 참조변수가 가지는 값(가리키는 주소)](/assets/images/java/address_of_car_reference_variable.png)
    
  - 💡 자바에서 equals() 메소드는 기본적으로 각 API 클래스마다 자체적으로 오버라이딩을 통해 재정의되어 있다.
  
  - ex) **String 클래스에 재정의**되어 있는 equals() 메소드
    - **문자열 내용이 같으면 true를 반환**하도록 재정의되어 있다(내용이 같은지 비교).
    - 문자열을 char 단위로 한 글자씩 모두 비교하여 동일하면 true를 반환.
    - 따라서, **서로 다른 인스턴스라도 같은 문자열을 가지고 있으면 동일하다고 판단**.
    
    ```java
    String s1 = new String("abc");
    String s2 = new String("abc");
    
    System.out.println(s1 == s2); // false, 서로 다른 주소값
    System.out.println(s1.equals(s2)); // true, 동일한 문자열
    ```
    - 동일한 문자열을 가진 String 인스턴스이기 때문에 재정의된 equals()의 결과로 true가 반환.
    
    
  - ex) Car 클래스의 equals() 메소드 재정의
    
    ```java
    public class Car {
      String modelName;
      int modelYear;
      String color;
      
      Car(String modelName, int modelYear, String color) {
        this.modelName = modelName;
        this.modelYear = modelYear;
        this.color = color;
      }
      
      @Override
      public boolean equals(Object obj) {
        Car other = (Car) obj;
        return (this.modelName.equals(other.modelName));
      }
    }
    ```
    - 멤버 변수인 modelName의 문자열로 두 인스턴스를 비교하도록 재정의.
    - equals()는 **사용자가 어떻게 재정의하느냐에 따라 원하는 기준으로 비교 가능**하다.
    
- **hashCode()**
  - 인스턴스의 해시 코드 값 반환.
  - 해시 코드는 일반적으로 **각 인스턴스의 주소값을 변환하여 생성한 인스턴스의 고유한 정수값**이다.
  - 따라서, 두 인스턴스가 동일 인스턴스인지 비교할 때 사용할 수 있다.
  
  - ex) hashCode() 메소드를 이용하여 두 인스턴스의 해시 코드를 출력
  
    ```java
    Student s1 = new Student();
    Student s2 = new Student();

    System.out.println(s1.hashCode()); // 705927765
    System.out.println(s2.hashCode()); // 366172642
    ```
    - 서로 다른 인스턴스인 `s1`과 `s2`의 해시 코드는 당연히 다르다. 해시 코드는 주소값을 기반으로 생성된 정수값이기 때문이다.
    
  - **String 클래스**의 hashCode()
    - 문자열에서 한 글자씩 가져와 정수값으로 변경한다.
    - 결국 서로 다른 String 인스턴스도 **문자열이 같으면 해시 코드가 같다**.
    
    ```java
    String s1 = new String("abc");
    String s2 = new String("abc");
    
    System.out.println(s1.hashCode()); // 96354
    System.out.println(s2.hashCode()); // 96354
    ```
    - `s1`과 `s2`는 **주소값이 서로 다른 인스턴스**이지만, **동일한 문자열**을 가졌으므로 **해시 코드가 동일**하다.
    
  - ex) Car 클래스의 hashCode() 메소드 재정의
    - **equals()가 true**이면 **동일한 해시 코드를 가질 수 있도록** hashCode()를 재정의
    - equals() 기준에 맞추어 hashCode()도 재정의하는 것이 좋다.
    
    ```java
    public class Car {
      String modelName;
      int modelYear;
      String color;
      
      Car(String modelName, int modelYear, String color) {
        this.modelName = modelName;
        this.modelYear = modelYear;
        this.color = color;
      }
      
      @Override
      public boolean equals(Object obj) {
        Car other = (Car) obj;
        return (this.modelName.equals(other.modelName));
      }
      
      @Override
      public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((modelName == null) ? 0 : modelName.hashCode());
        return result;
      }
    }    
    ```
    - Car 인스턴스의 **modelName이 동일한 문자열이면 같은 해시 코드를 가지도록 재정의**.
    - 결국 String 클래스처럼 된 형태이다(문자열로 비교).
    - 서로 다른 인스턴스이지만 **equals()에서 어떤 기준(ex. 문자열)에 의한 결과가 동일하도록 재정의**하고, **hashCode()에서도 해당 기준을 기반으로 재정의**하면 된다.
    
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Object와 오버라이딩](https://programmers.co.kr/learn/courses/9/lessons/249#)
- [코딩의 시작, TCP School \| JAVA \| Object 클래스](https://www.tcpschool.com/java/java_api_object)
- [브런치 by 서준수 \| 자바의 == 연산자와 equals()](https://brunch.co.kr/@mystoryg/132#comment)
- [브런치 by 서준수 \| 자바의 hashCode()](https://brunch.co.kr/@mystoryg/133)
