---
title: "[프로그래머스 자바 중급] 입력과 출력 : 보조 스트림"
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

## 보조 스트림
- 자바에서 제공하는 보조 스트림은 실제로 **데이터를 주고받을 수는 없지만**, 다른 스트림의 **기능을 향상**시키거나 **새로운 기능을 추가**해주는 스트림이다.

- 자바에서는 다음과 같은 보조 스트림을 제공하고 있다.

  | 입력 스트림 | 출력 스트림 | 설명 |
  |:----------:|:----------:|:-----|
  | FilterInputStream | FilterOutputStream | **필터**를 이용한 입출력 |
  | BufferedInputStream | BufferedOutputStream | **버퍼**를 이용한 입출력 |
  | DataInputStream | DataOutputStream | 입출력 스트림으로부터 자바의 **기본 타입**으로 데이터를 읽어올 수 있게 함 |
  | ObjectInputStream | ObjectOutputStream | 스트림으로부터 객체를 입력(**역직렬화**)하거나, 객체를 스트림에 출력(**직렬화**) |
  | SequenceInputStream | X | **두 개의 입력 스트림**을 논리적으로 **연결** |
  | PushbackInputStream | X | 다른 **입력 스트림**에 **버퍼를 이용**하여 push back이나 unread와 같은 **기능을 추가** |
  | X | PrintStream | 다른 **출력 스트림**에 **버퍼를 이용**하여 다양한 데이터를 출력하기 위한 **기능을 추가** |
  
    >- 직렬화(Serialization)
    >    - **객체를 데이터 스트림으로** 바꾸는 것. 
    >    - 즉, **객체**에 저장된 데이터를 **스트림에 쓰기(write)** 위해 **연속적인(serial) 데이터로 변환**하는 것.
    >    - 객체를 상태 그대로 저장하거나 메모리, 데이터베이스 혹은 파일로 옮기기 위해 사용.
    >- 역직렬화(Deserialization)3
    >    - 네트워크나 영구저장소에서 **스트림을 다시 객체로 변환**하는 것.
    >  ![자바에서의 직렬화 & 역직렬화](/assets/images/java/serialize_deserialize_java.png)

## 다양한 타입의 출력
- 다양한 타입으로 저장할 수 있는 `DataOutputStream`
  - `writeInt()` : int 값으로 저장
  - `writeBoolean()` : boolean 값으로 저장
  - `writeDouble()` : double 값으로 저장

  <br/>  

  ```java
  import java.io.FileOutputStream;
  import java.io.DataOutputStream;

  public class ByteExam3 {

    public static void main(String[] args) {
      // try-with-resources
      try (DataOutputStream out = new DataOutputStream(new FileOutputStream("data.txt"));) { // io 객체 선언
        // io 객체 사용 후, 자동으로 자원 종료
        out.writeInt(100);
        out.writeBoolean(true);
        out.writeDouble(50.5);

      } catch (Exception e) {

        e.printStackTrace();
      }

    }//--main()

  }//--class
  ```
  - 💡 `try-with-resources`를 이용한 자원 종료
    - **자바 I/O 객체**는 인스턴스를 만들고 모두 사용하면 **close() 메소드**를 호출하여 **사용한 자원을 종료**해야 한다.
    - `try-with-resources`를 사용하면 `close()` 메소드를 사용자가 호출하지 않더라도, `try(...)`에 선언된 객체들에 대해서 **try 블럭이 종료될 때 자동으로 사용한 자원을 종료**해준다.

      ```java
      try ( // io 객체 선언) {
        // io 객체 사용
      } catch (Exception ex) {
        ex.printStackTrace();
      }
      ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| ]()
- [코딩의 시작, TCP School \| JAVA \| 스트림](https://www.tcpschool.com/java/java_io_stream)
- [LUNA Y0UNG – Medium \| Basics: 직렬화(Serialization)란? (feat. Java)](https://medium.com/@lunay0ung/basics-%EC%A7%81%EB%A0%AC%ED%99%94-serialization-%EB%9E%80-feat-java-2f3eb11e9a8)
- [Integerous DevLog \| 자바의 정석 - 직렬화(Serialization)](https://ryan-han.com/post/java/java-serialization/)
