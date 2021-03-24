---
title: "[프로그래머스 자바 중급] 입력과 출력 : 표준 입출력"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - io
  - stream
  - 자바중급
---

## 표준 입출력
- 자바에서는 **콘솔**과 같은 표준 입출력 장치를 위해 `System`이라는 **표준 입출력 클래스**를 정의하고 있다.

- `java.lang` 패키지에 포함되어 있는 `System` 클래스는 표준 입출력을 위해 다음과 같은 **클래스 변수**를 제공한다.

  | 클래스 변수 | 입출력 스트림 | 설명 |
  |:----------:|:------------:|:----:|
  | System.in | InputStream | 콘솔로부터 데이터를 입력받음 |
  | System.out | PrintStream | 콘솔로 데이터를 출력 |
  | System.err | PrintStream | 콘솔로 데이터를 출력 |
  
- **표준 입출력 스트림**은 **자바가 자동으로 생성**하므로, 개발자가 별도로 스트림을 생성하지 않아도 사용할 수 있다.


## 표준 입출력의 대상 변경
- 앞서 살펴본 **표준 입출력 스트림**에 아래의 **`System` 메소드**를 사용하면 **스트림의 대상**을 콘솔이 아닌 **다른 입출력 장치로 변경**할 수 있다.

  | 메소드 | 설명 |
  |:------|:-----|
  | static void **setIn(InputStream in)** | 입력 스트림의 대상을 **전달된 입력 스트림**으로 변경 |
  | static void **setOut(PrintStream out)** | 출력 스트림의 대상을 **전달된 출력 스트림**으로 변경 |
  | static void **setErr(PrintStream err)** | 출력 스트림의 대상을 **전달된 출력 스트림**으로 변경 |
  
  
## 출처
- [코딩의 시작, TCP School \| JAVA \| 파일 입출력](https://www.tcpschool.com/java/java_io_file)
