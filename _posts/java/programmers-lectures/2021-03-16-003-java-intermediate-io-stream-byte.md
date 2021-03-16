---
title: "[프로그래머스 자바 중급] 입력과 출력 : 바이트(Byte) 단위 입출력"
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

## 바이트(Byte) 기반 스트림(Stream)
- 자바에서 **스트림**은 기본적으로 **바이트 단위**로 데이터를 전송한다.

- 자바에서는 다음과 같은 **바이트 기반의 입출력 스트림**을 제공하고 있다.
  
  | 입력 스트림 | 출력 스트림 | 입출력 대상 |
  |:----------:|:-----------:|:----------:|
  | FileInputStream | FileOutputStream | 파일 |
  | ByteArrayInputStream | ByteArrayOutputStream | 메모리 |
  | PipedInputStream | PipedOutputStream | 프로세스 |
  | AudioInputStream | AudioOutputStream | 오디오 장치 |
  
## 바이트(Byte) 단위 입출력 예제
- **파일**로부터 **1 Byte씩 읽어 들여** 파일에 **1 Byte씩 저장**하는 프로그램 작성.
  - 파일로부터 읽어 오기 위한 객체 : `FileInputStream`
  - 파일에 쓰기 위한 객체 : `FileOutputStream`
  

  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Byte 단위 입출력](https://programmers.co.kr/learn/courses/9/lessons/267)
- [코딩의 시작, TCP School \| JAVA \| 스트림](https://www.tcpschool.com/java/java_io_stream)
