---
title: "[자바] Arrays 클래스"
layout: single
related: true
categories:
  - JAVA
tags:
  - java.util패키지
  - arrays
---

## java.util 패키지
- 프로그램을 개발하는 데 사용할 수 있는 유용한 유틸리티 클래스가 다수 포함되어 있다.
- java.lang 패키지 다음으로 가장 많이 사용되는 패키지.
- import 문을 사용하지 않아도 바로 사용할 수 있는 java.lang 패키지와는 달리, **import 문으로 패키지를 불러오고 나서야 사용할 수 있다**.

## Arrays 클래스
- 배열을 다루기 위한 다양한 메소드가 포함되어 있다.
- Arrays 클래스의 모든 메소드는 **클래스 메소드(static method)**이므로, **객체를 생성하지 않아도 바로 사용**할 수 있다.
- java.util 패키지에 포함되므로, 반드시 **import 문으로 java.util 패키지를 불러오고 나서 사용**해야 한다.

## binarySearch() 메소드
- 전달받은 배열에서 **특정 객체의 위치**를 이진 검색 알고리즘을 사용하여 검색한 후, 해당 위치를 반환.
- **이진 검색 알고리즘**을 사용하므로, **매개변수로 전달되는 배열**이 sort() 메소드 등을 사용하여 **미리 정렬**되어 있어야만 제대로 동작.

  ```java
  import java.util.*;
  
  public class prog {
    public static void main(String[] args) {
      int[] arr = new int[1000];
      for(int i = 0; i < arr.length; i++) {
        arr[i] = i;
      }

      System.out.println(Arrays.binarySearch(arr, 437)); // 437
    }
  }
  ```
  
## copyOf() 메소드
- 전달받은 배열의 특정 길이만큼을 **새로운 배열로 복사**하여 반환.
  - **첫 번째 매개변수**로 **원본 배열**을 전달받고, **두 번째 매개변수**로 **새로운 배열로 복사할 요소의 개수**를 전달받는다.
  - 원본 배열과 같은 타입의 복사된 새로운 배열을 반환.
  
- 새로운 배열의 길이가 원본 배열보다 길면, 나머지 요소는 배열 요소의 타입에 맞게 다음과 같은 기본값으로 채워진다.

  | 배열 요소의 타입 | 기본값 |
  |:----------------|:------|
  | char | '\u0000' |
  | byte, short, int | 0 |
  | long | 0L |
  | float | 0.0F |
  | double | 0.0 또는 0.0D |
  | boolean | false |
  | 배열, 인스턴스 등 | null |
  
  ```java
  import java.util.*;
  
  public class prog {
	  public static void main(String[] args) {
      int[] arr1 = {1, 2, 3, 4, 5};
      int[] arr2 = Arrays.copyOf(arr1, 3); // 첫 번째 배열 요소부터 3개의 요소 복사

      for(int i = 0; i < arr2.lenght; i++) {
        System.out.print(arr2[i] + " "); // 1 2 3 
      }
      System.out.println();

      // 첫 번째 배열 요소부터 10개의 요소 복사 -> 원본 배열의 개수를 초과하여 복사
      int[] arr3 = Arrays.copyOf(arr1, 10);
      for(int i = 0; i < arr3.lenght; i++) {
        System.out.print(arr3[i] + " "); // 1 2 3 4 5 0 0 0 0 0 -> int 타입이므로 0으로 채워짐
      }
    }
  }
  ```
  - 배열 arr2에는 배열 arr1의 첫 번째 요소부터 3개의 요소를 복사하여 대입.
  - 배열 arr3에는 배열 arr1에서 10개의 요소를 복사하여 대입.
    - 하지만, 배열 arr1의 길이가 5밖에 안되므로, 배열 arr3의 나머지 요소에는 **int형의 기본값인 0이 채워진다**.
    
## copyOfRange() 메소드
- 전달받은 배열의 **특정 범위에 해당하는 요소**만을 새로운 **배열로 복사**하여 반환.
  - 첫 번째 매개변수로 복사의 대상이 될 **원본 배열**을 전달받는다.
  - 두 번째 매개변수로 **원본 배열에서 복사할 시작 인덱스**를 전달받는다.
  - 세 번째 매개변수로 **마지막으로 복사될 배열 요소의 바로 다음 인덱스**를 전달받는다.
    - 즉, 세 번째 매개변수로 전달된 인덱스 바로 전까지의 배열 요소까지만 복사된다.
  - 원본 배열과 같은 타입의 복사된 새로운 배열을 반환.
  
  ```java
  import java.util.*;

  public class prog {
    public static void main(String[] args) {
      int[] arr1 = {1, 2, 3, 4, 5};

      int[] arr2 = Arrays.copyOfRange(arr1, 2, 4);
      for (int i = 0; i < arr2.length; i++) {
        System.out.print(arr2[i] + " "); // 3 4 
      }
    }
  }
  ```
  
## fill() 메소드
- 전달받은 배열의 **모든 요소를 특정 값으로 초기화**해준다.
  - 첫 번째 매개변수로 **초기화할 배열**을 전달받고, 두 번째 매개변수로 **초기값**을 전달받는다.
- 전달받은 **원본 배열의 값을 변경**한다.

  ```java
  import java.util.*;

  public class prog {
    public static void main(String[] args) {
      int[] arr = new int[10];

      Arrays.fill(arr, 7);
      for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " "); // 7 7 7 7 7 7 7 7 7 7 
      }
    }
  }
  ```
  
## sort() 메소드
- 전달받은 배열의 모든 요소를 **오름차순으로 정렬**.
- 매개변수로 정렬할 배열을 전달받으며, 전달받은 **원본 배열의 순서를 변경**한다.

  ```java
  import java.util.*;

  public class prog {
    public static void main(String[] args) {
      int[] arr = {5, 3, 4, 1, 2};

      Arrays.sort(arr);
      for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " "); // 1 2 3 4 5 
      }
    }
  }
  ```
  
## 그 외 대표적인 Arrays 클래스 메소드

  | 메소드 | 설명 |
  |:------|:------|
  | List<T> asList(T... a) | 전달받은 배열을 고정 크기의 리스트(ArrayList, java.util.ArrayList 클래스와는 다른 클래스)로 변환하여 반환 |
  | boolean equals(Object[] a, Object[] a2) | 전달받은 두 배열이 같은지 확인 |
  
  - 💡 **java.util.Arrays.ArrayList 클래스**는 set(), get(), contains() 메소드를 가지고 있지만, **원소를 추가하는 메소드는 가지고 있지 않기 때문에 사이즈를 바꿀 수 없다**.

## 출처
- [코딩의 시작, TCP School \| JAVA \| Arrays 클래스](https://www.tcpschool.com/java/java_api_arrays)
- [minjara 님의 블로그 \| [JAVA] Arrays.asList()](https://blog.naver.com/roropoly1/221140156345)
