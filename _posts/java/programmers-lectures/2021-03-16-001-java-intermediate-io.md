---
title: "[프로그래머스 자바 중급] 입력과 출력 : Java I/O"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - io
  - 자바중급
---

## 입출력을 위한 인터페이스와 클래스
- **자바 I/O**는 크게 **Byte 단위 입출력 클래스**와 **Char 단위 입출력 클래스**로 나뉜다.
  - **Byte 단위 입출력 클래스**는 **InputStream**과 **OutputStream**이라는 **추상 클래스**를 **상속**받아 만들어진다. 
  - **Char 단위 입출력 클래스**는 **Reader**와 **Writer**라는 **추상 클래스**를 **상속**받아 만들어진다.

  ![java i/o 클래스](/assets/images/java/io_class.png)


- **파일**로부터 **입력**받고 **쓰기** 위한 클래스: `FileInputStream`, `FileOutputStream`, `FileReader`, `FileWriter`
- **배열**로부터 **입력**받고 **쓰기** 위한 클래스: `ByteArrayInputStream`, `ByteArrayOutputStream`, `CharReader`, `CharWriter`
  - 해당 클래스들은 **어디로부터 입력받고, 어디에 쓸지 대상을 지정할 수 있는 I/O 클래스**이다. 이런 클래스를 **장식 대상 클래스**라고 한다.

## 데코레이터 패턴(Decorator Pattern)
- 자바 I/O는 데코레이터 패턴으로 만들어져 있다.
- 객체를 장식하는 디자인 패턴으로 실행 중에 클래스를 덧붙이는 패턴.
  - 데코레이터 패턴은 하나의 클래스를 장식하는 것처럼 **생성자에서 감싸서, 새로운 기능을 계속 추가**할 수 있도록 **클래스를 만드는 방식**.
- 데코레이터 패턴을 사용하면 부모 클래스를 건드리지 않으면서 **실행 중에 원하는 기능을 추가**할 수 있다.

  ```java
  Parent = new Child(new child());
  ```
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| 자바IO](https://programmers.co.kr/learn/courses/9/lessons/266#note)
- [victolee - 티스토리 \| [Java] 핵심정리 (2) - File I/O ( Stream )](https://victorydntmd.tistory.com/134)
