---
title: "[프로그래머스 자바 중급] java.lang 패키지 : 스트링 클래스(String Class)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java.lang패키지
  - String
  - 자바중급
---

## String 클래스
- 자바에서는 문자열을 위한 String 클래스를 제공하고 있다.
- 문자열과 관련된 작업을 할 때, 유용하게 사용할 수 있는 다양한 메소드가 포함되어 있다.
- String 클래스는 java.lang 패키지에 포함되어 제공된다.

- String 인스턴스는 한번 생성되면 **그 값을 읽기만 할 수 있고, 변경할 수는 없다**.
  - 이러한 객체를 자바에서는 **불변 객체(immutable object)**라고 한다.
  - 즉, 자바에서 덧셈(+) 연산자를 이용하여 **문자열 결합**을 수행하면, **기존 문자열의 내용이 변경되는 것이 아니라 내용이 합쳐진 새로운 String 인스턴스가 생성**된다.
    - 💡 덧셈(+) 연산자를 통한 문자열 결합 시, 내부적으로 아래와 같은 코드가 실행된다.
    
      ```java
      String str1 = "hello";
      String str2 = "world";

      // 덧셈 연산자를 통한 문자열 결합
      String str3 = str1 + str2;

      // 내부적으로 실행되는 코드
      String str4 = new StringBuffer().append(str1).append(str2).toString();
      ```
      - 문자열을 더하게 되면 **내부적으로 StringBuffer 인스턴스가 만들어지고**, 이를 반복문 안에서 수행하면 StringBuffer 인스턴스를 계속 생성해야 하므로 성능상 좋지 않다.
      - 따라서, **반복적으로 문자열 결합**을 수행할 경우 **StringBuffer 인스턴스를 처음부터 만들고 append() 메소드로 수행**하는 것이 좋다.

## charAt() 메소드
- 문자열의 **특정 인덱스에 해당하는 문자를 반환**.
- 만약, 해당 문자열의 길이보다 큰 인덱스나 음수를 전달하면 IndexOutOfBoundsException 오류가 발생.

- ex) 문자열의 각 문자를 chatAt() 메소드를 이용하여 하나씩 출력
  
  ```java
  String str = new String("Java");
  System.out.println("원본 문자열: " + str); // 원본 문자열 : Java
  
  for(int i = 0; i < str.length(); i++) {
     System.out.print(str.chatAt(i) + " "); // J a v a 
  }
  ```
  
## compareTo() 메소드
- 문자열을 **인수로 전달된 문자열과 사전 순으로 비교**.
- 대소문자 구분하여 비교.
  - 대소문자 구분없이 비교하려면 compareToIgnoreCase() 메소드 사용.
- 두 문자열이 **같다면 0을 반환**하며, 문자열이 인수로 전달된 문자열보다 **작으면 음수**를, **크면 양수**를 반환.

- ex) compareTo() 메소드와 compareToIgnoreCase() 메소드를 이용하여 두 문자열을 비교

  ```java
  String str = new String("abcd");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : abcd
  
  System.out.println(str.compareTo("bcef")); // -1, 작음
  System.out.println(str.compareTo("abcd")); // 0, 같음
  
  // 대소문자 미구분과 구분
  System.out.println(str.compareTo("Abcd")); // 32, 큼
  System.out.println(str.compareToIgnoreCase("Abcd"); // 0, 같음
  ```
  
## concat() 메소드
- **문자열의 뒤에 인수로 전달된 문자열을 추가**한 **새로운 문자열**을 반환.
- 인수로 전달된 문자열의 길이가 0이면, 문자열을 그대로 반환.

- ex) concat() 메소드를 이용하여 두 문자열을 연결

  ```java
  String str = new String("Java");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : Java
  
  System.out.println(str.concat("수업")); // Java수업
  // 기존 문자열에는 영향 없음
  System.out.println("메소드 호출 후 원본 문자열 : " + str); // 메소드 호출 후 원본 문자열 : Java
  ```

## indexOf() 메소드
- 문자열에서 **특정 문자나 문자열이 처음으로 등장하는 위치의 인덱스**를 반환.
- 문자열에 인수로 전달된 문자나 문자열이 포함되어 있지 않으면 -1을 반환.
- 대소문자 구분.

- ex) indexOf() 메소드를 이용하여 특정 문자나 문자열이 처음 등장하는 위치의 인덱스 찾기

  ```java
  Stirng str = new String("Oracle Java");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 : Oracle Java
  
  System.out.println(str.indexOf('o')); // -1, 없음
  System.out.println(str.indexOf('a'); // 2
  System.out.println(str.indexOf("Java")); // 7
  ```
  
## trim() 메소드
- 문자열의 맨 앞과 맨 뒤에 포함된 모든 공백 문자를 제거

- ex) trim() 메소드를 이용하여 문자열에 포함된 띄어쓰기와 탭 문자 제거

  ```java
  Stirng str = new String(" Java     ");
  System.out.println("원본 문자열 : " + str); // 원본 문자열 :  Java     
  
  System.out.println(str + '|'); //  Java     |
  System.out.println(str.trim() + '|'); // Java|
  // 기존 문자열에는 영향 없음
  System.out.println("메소드 호출 후 원본 문자열 : " + str); // 메소드 호출 후 원본 문자열 :  Java       
  ```

## 대표적인 String 클래스 메소드
- 많이 사용되는 메소드는 다음과 같다.

  | 메소드 | 설명 |
  |:------|:------|
  | char charAt(int index) | 문자열의 특정 인덱스에 해당하는 문자를 반환 |
  | int compareTo(String str) | 문자열을 인수로 전달된 문자열과 사전순으로 비교 | 
  | int compareToIgnoreCase(String str) | 문자열을 인수로 전달된 문자열과 대소문자를 구분하지 않고 사전순으로 비교 |
  | String concat(String str) | 문자열의 뒤에 인수로 전달된 문자열을 추가한 새로운 문자열을 반환 |
  | int indexOf(int ch)<br/>int indexOf(String str) | 문자열에서 특정 문자나 문자열이 처음으로 등장하는 위치의 인덱스를 반환 |
  | int indexOf(int ch, int fromIndex)<br/>int indexOf(String str, int fromIndex) | 문자열에서 특정 문자나 문자열이 **인수로 전달된 인덱스 이후에** 처음으로 등장하는 위치의 인덱스를 반환 |
  | int lastIndexOf(int ch) | 문자열에서 특정 문자가 마지막으로 등장하는 위치의 인덱스를 반환 |
  | int lastIndexOf(int ch, int fromIndex) | 문자열에서 특정 문자가 **인수로 전달된 인덱스 이후에** 마지막으로 등장하는 위치의 인덱스를 반환 |
  | String[] split(String regex) | 문자열을 인수로 전달된 정규 표현식(regular expression)에 따라 나눠서 반환 |
  | String substring(int beginIndex) | 인수로 전달된 인덱스부터 끝까지 문자열을 잘라 새로운 문자열로 반환 |
  | String substring(int begin, int end) | 인수로 전달된 시작 인덱스부터 마지막 인덱스까지 문자열을 잘라 새로운 문자열로 반환 |
  | String toLowerCase() | 문자열의 모든 문자를 소문자로 변환 |
  | String toUpperCase() | 문자열의 모든 문자를 대문자로 변환 |
  | String trim() | 문자열의 맨 앞과 맨 뒤에 포함된 모든 공백 문자를 제거 |
  | length() | 문자열의 길이를 반환 |
  | isEmpty() | 문자열의 길이가 0이면 true를 반환하고, 아니면 false를 반환 |
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 스트링 클래스의 문제점](https://programmers.co.kr/learn/courses/9/lessons/254)
- [코딩의 시작, TCP School \| JAVA \| String 클래스](https://www.tcpschool.com/java/java_api_string)
