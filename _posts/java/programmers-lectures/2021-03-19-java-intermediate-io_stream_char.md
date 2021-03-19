---
title: "[프로그래머스 자바 중급] 입력과 출력 : 문자(Char) 단위 입출력"
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

## 문자(Char) 기반 스트림(Stream)
- 자바에서 **스트림**은 기본적으로 **바이트 단위**로 데이터를 전송한다.
- 하지만, 자바에서 가장 작은 타입인 **Char 형**이 **2 바이트**이므로, 1 바이트씩 전송되는 바이트 기반 스트림으로는 원활한 처리가 힘든 경우가 있다.
- 따라서, 자바에서는 바이트 기반 스트림뿐만 아니라 **문자 기반의 스트림도 별도로 제공**한다.
- 이러한 문자 기반 스트림은 기존의 바이트 기반 스트림에서 **InputStream을 Reader로, OutputStream을 Writer로 변경**하면 사용할 수 있다.

- 자바에서는 다음과 같은 **문자 기반 입출력 스트림**을 제공하고 있다.

  | 입력 스트림 | 출력 스트림 | 입출력 대상 |
  |:----------:|:----------:|:-----------:|
  | FileReader | FileWriter | 파일 |
  | CharArrayReader | CharArrayWriter | 메모리 |
  | PipedReader	| PipedWriter | 프로세스 |
  | StringReader | StringWriter | 문자열 |
  
  
- 지금까지 살펴본 **바이트 기반의 스트림**과 **문자 기반의 스트림**은 **활용 방법이 거의 같다**.
  - 따라서, **문자 기반의 보조 스트림**도 다음과 같이 제공된다.

  | 입력 스트림 | 출력 스트림 | 설명 |
  |:----------:|:----------:|:-----------:|
  | FilterReader | FilterWriter | **필터**를 이용한 입출력 |
  | BufferedReader | BufferedWriter | **버퍼**를 이용한 입출력 |
  | PushbackReader | X | 다른 **입력 스트림**에 **버퍼**를 이용하여 push back이나 unread와 같은 **기능을 추가** |
  | X | PrintWriter | 다른 **출력 스트림**에 **버퍼**를 이용하여 **다양한 데이터를 출력**하기 위한 **기능을 추가** |
  
## 문자(Char) 단위 입출력 예제
- **문자 단위 입출력 스트림**을 이용해서 **키보드로부터 한 줄씩 입력받아 콘솔에 출력**.
  - `System.in` : 키보드를 의미(InputStream)
  - 
  
  

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Char 단위 입출력(Console)](https://programmers.co.kr/learn/courses/9/lessons/319)
- [코딩의 시작, TCP School \| JAVA \| 스트림](https://www.tcpschool.com/java/java_io_stream)
