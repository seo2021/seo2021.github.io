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
  
## 바이트(Byte) 단위 입출력 예제 1
- **파일**로부터 **1 바이트씩 읽어 들여** 파일에 **1 바이트씩 저장**하는 프로그램 작성.
  - 파일로부터 읽어 오기 위한 객체 : `FileInputStream`
  - 파일에 쓰기 위한 객체 : `FileOutputStream`

- `read()` 메소드는 
  - **1 byte**씩 읽어 들인다. 
  - 읽어 들일 바이트가 있다면 **양수를 반환**(읽은 1 바이트의  int 형으로 반환)하며, 더 이상 읽어들일 바이트가 없을 때 **-1을 반환**한다.
  - 반환 타입은 **int(4 바이트)**이며, 4 바이트 중 **마지막 바이트**에 **읽어 들인 1 바이트를 저장**한다.

<br/>

  ```java
  package javaIO.exam;

  import java.io.FileInputStream;
  import java.io.FileOutputStream;

  public class ByteExam1 {
    public static void main(String[] args) {
      FileInputStream fis = null; // 파일로부터 읽어오기 위한 객체
      FileOutputStream fos = null; // 파일에 쓰기 위한 객체
      
      try {
        // FileInputStream 객체 생성. 읽어 들이기 위한 파일의 경로 설정
        fis = new FileInputStream("src/javaIO/exam/ByteExam1.java");
        // FileOutputStream 객체 생성. 프로젝트 아래에 txt 파일을 생성하고 쓰기.
        fos = new FileOutputStream("byte.txt");

        // 파일로부터 1 바이트씩 읽어 들인 값을 담기 위한 변수
        int readData = -1;

        // 파일에 읽어올 값이 남아있다면
        while((readData = fis.read()) != -1) {
	  // 읽어 온 1 바이트의 값을 int 형으로 반환
	  // System.out.println(readData); 
	  
          // 1 바이트씩 쓰기
          fos.write(readData);
        }
	
      } catch (Exception e) {
        // 에러의 발생근원지를 찾아서 단계별로 에러를 출력
        e.printStackTrace();

      } finally {
        // io의 객체는 인스턴스화하면 마지막에 닫아주기
        try {
          fos.close();
        } catch (Exception e) {
          e.printStackTrace();
        }
        try {
          fis.close();
        } catch (Exception e) {
          e.printStackTrace();
        }
      }
	  }//--main()
  }//--class
  ```

- 실행 결과 `ByteExam1`으로부터 다.를 1 바이트씩 읽어 들여, 1 바이트씩 써진 파일 `byte.txt`가 프로젝트 아래에 생성되었다.

  ![byte.txt가 생성된 모습](/assets/images/java/byteexam1_result.png)
  
## 바이트(Byte) 단위 입출력 예제 2
- **파일**로부터 **512 바이트씩 읽어 들여** 파일에 **512 바이트씩 저장**하는 프로그램 작성.
- 512 바이트만큼 읽어 들이기 위해 **byte 배열**을 사용.
  - `byte[] buffer = new byte[512];`

- `read(byte[] b)` 메소드는
  - 입력 스트림으로부터 **배열 크기 바이트만큼을 읽어들인 후, 배열 b에 저장**.
  - **읽은 바이트 수를 int 형으로 반환** 

<br/>

  ```java
  package javaIO.exam;

  import java.io.FileInputStream;
  import java.io.FileOutputStream;

  public class ByteExam2 {
    public static void main(String[] args) {
      // *currentTimeMillis(): 현재 시간을 long 타입으로 반환
      long startTime = System.currentTimeMillis(); // 메소드 시작 시간을 구하기 위해

      FileInputStream fis = null; // 파일로부터 읽어오기 위한 객체
      FileOutputStream fos = null; // 파일에 쓰기 위한 객체
      
      try {
	// FileInputStream 객체 생성. 읽어 들이기 위한 파일의 경로 설정
	fis = new FileInputStream("src/javaIO/exam/ByteExam1.java");
	// FileOutputStream 객체 생성. 프로젝트 아래에 txt 파일을 생성하고 쓰기.
	fos = new FileOutputStream("byte2.txt");

	int readCount = -1; // 파일로부터 읽어 들인 바이트 수를 담기 위한 변수
	byte[] buffer = new byte[512]; // 512 바이트만큼 읽어 들이기 위한 배열

	// 스트림으로부터 최대 512 바이트를 읽어 들인 후, 바이트 배열 buffer에 저장
	// 파일에 읽어올 값이 남아있다면 반복
	while((readCount = fis.read(buffer)) != -1) {
		// 읽은 바이트 수를 반환 -> 512 512 338
		System.out.print(readCount + " ");

		// buffer[0]부터 readCount 바이트만큼을 출력 스트림에 저장
		fos.write(buffer, 0, readCount);
	}
	
      } catch (Exception e) {
        // 에러의 발생근원지를 찾아서 단계별로 에러를 출력
	e.printStackTrace();

      } finally {
	// io의 객체는 인스턴스화하면 마지막에 닫아주기
	try {
	  fos.close();
	} catch (Exception e) {
	  e.printStackTrace();
	}
	try {
	  fis.close();
	} catch (Exception e) {
	  e.printStackTrace();
        }
      }

      // 메소드가 끝난 시간 구하기 위해
      long endTime = System.currentTimeMillis();
      // 메소드 수행 시간 계산
      System.out.println(endTime - startTime);
      
    }//--main()
  }//--class
  ```
  - 1 바이트씩 읽어 들이는 것보다 수행시간이 짧아진다.
    - 💡 `read()` 메소드는 1 바이트씩 **바이트 수만큼 반복**해서 읽지만, `read(byte[] b)`는 **주어진 바이트 배열의 길이만큼** 읽기 때문에 반복 횟수가 현저히 적다.
    - 💡 운영체제는 **파일**을 읽어 들일 때 **512 바이트**씩 읽어 오기 때문에, **512 바이트의 배수**로 **배열의 크기**를 잡아주는 것이 성능상 좋다.
  
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Byte 단위 입출력](https://programmers.co.kr/learn/courses/9/lessons/267)
- [코딩의 시작, TCP School \| JAVA \| 스트림](https://www.tcpschool.com/java/java_io_stream)
- [알통몬의 인생 \| [ JAVA ] - 입력 스트림과 출력 스트림(1)...](https://blog.naver.com/PostView.nhn?blogId=rain483&logNo=220625042360&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [알통몬의 인생 \| [ JAVA ] - 입력 스트림과 출력 스트림(3)...](https://blog.naver.com/rain483/220625901561)
