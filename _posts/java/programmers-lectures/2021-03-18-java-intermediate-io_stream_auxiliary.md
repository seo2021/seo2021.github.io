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
  | DataInputStream | DataOutputStream | 자바의 **기본 자료형 데이터를 입출력**할 수 있도록 한다 |
  | ObjectInputStream | ObjectOutputStream | 스트림으로부터 객체를 입력(**역직렬화**)하거나, 객체를 스트림에 출력(**직렬화**) |
  | SequenceInputStream | X | **두 개의 입력 스트림**을 논리적으로 **연결** |
  | PushbackInputStream | X | 다른 **입력 스트림**에 **버퍼를 이용**하여 push back이나 unread와 같은 **기능을 추가** |
  | X | PrintStream | 다른 **출력 스트림**에 **버퍼를 이용**하여 다양한 데이터를 출력하기 위한 **기능을 추가** |
  
    >- 직렬화(Serialization)
    >    - **객체를 데이터 스트림으로** 바꾸는 것. 
    >    - 즉, **객체**에 저장된 데이터를 **스트림에 쓰기(write)** 위해 **연속적인(serial) 데이터로 변환**하는 것.
    >    - 객체를 상태 그대로 저장하거나 메모리, 데이터베이스 혹은 파일로 옮기기 위해 사용.
    >- 역직렬화(Deserialization)
    >    - 네트워크나 영구저장소에서 **스트림을 다시 객체로 변환**하는 것.
    >  ![자바에서의 직렬화 & 역직렬화](/assets/images/java/serialize_deserialize_java.png)

## 다양한 타입의 데이터 출력
- 다양한 자바 기본 자료형 데이터를 저장할 수 있는 `DataOutputStream`
  - `writeInt()` : int 값으로 저장
  - `writeBoolean()` : boolean 값으로 저장
  - `writeDouble()` : double 값으로 저장 

  ```java
  import java.io.FileOutputStream;
  import java.io.DataOutputStream;

  public class ByteExam3 {

    public static void main(String[] args) {
      // try-with-resources 사용
      // io 객체 선언.
      try (DataOutputStream out = new DataOutputStream(new FileOutputStream("data.txt"));) {
        // io 객체 사용 후, 자동으로 자원이 종료된다.
        out.writeInt(100); // int 형(4 바이트) 데이터를 쓰기
        out.writeBoolean(true); // boolean 형(1 바이트) 데이터를 쓰기
        out.writeDouble(50.5); // double 형(8 바이트) 데이터를 쓰기

      } catch (Exception e) {
        e.printStackTrace();
      }
    }//--main()
  }//--class
  ```
  - `DataOutputStream`은 **보조 스트림**이므로 기반 스트림이 필요하며, `FileOutputStream`을 **기반 스트림**으로 사용했다.
    -  `FileOutputStream`은 **바이트** 단위의 데이터만 출력할 수 있다.
      -  하지만, **보조 스트림**인 `DataOutputStream`을 사용하여 **자바 기본 자료형의 데이터를 출력**할 수 있다.
  - 아래와 같이 `DataOutputStream`은 **기본 자료형 데이터를 바이트 스트림으로 변환**하여 **출력**을 수행한다. 따라서 출력한 데이터(바이트 스트림 형태)를 다시 읽어올 때는 `DataInputStream`으로 읽어 와야 한다.

    ![DataOutputStream과 DataInputStream](/assets/images/java/datainputstream_dataoutputstream.png)

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
      
- 실행 결과

  ![ByteExam3 실행결과 : 13 바이트의 data.txt 파일 생성](/assets/images/java/byteexam3_result.png)
  
  - 13 바이트의 데이터가 써진 data.txt 파일이 생성되었다.

## 다양한 타입의 데이터 입력
- 다양한 자바 기본 자료형 데이터를 읽어낼 수 있는 `DataInputStream`
  - `readInt()` : 스트림으로부터 읽은 int 값을 반환
  - `readBoolean()` : 스트림으로부터 읽은 boolean 값 반환
  - `readDouble()` : 스트림으로부터 읽은 double 값 반환

- ex) data.txt로부터 값을 읽어 들여 콘솔에 출력

  ```java
  import java.io.DataInputStream;
  import java.io.FileInputStream;

  public class ByteExam4 {

    public static void main(String[] args) {
      // try-with-resources
      // io 객체 선언
      try ( DataInputStream in = new DataInputStream(new FileInputStream("data.txt")); ) {
        // io 객체 사용 후, 자동으로 자원 종료
        int i = in.readInt(); // int 형(4 바이트) 데이터 읽기
        boolean b = in.readBoolean(); // boolean 형(1 바이트) 데이터 읽기
        double d = in.readDouble(); // double 형(8 바이트) 데이터 읽기

        System.out.println(i);
        System.out.println(b);
        System.out.println(d);

      } catch(Exception ex) {
        ex.printStackTrace();
      }

    }//--main()

  }//--class
  ```
  - **파일**을 읽어 들이기 위해 **기반 스트림**으로 `FileInputStream`을 사용하고, 파일에서 읽어 들인 **바이트 스트림**을 **자바 기본 자료형**으로 읽어 들이기 위해 **보조 스트림**으로 `DataInputStream`을 사용했다.
  - 💡 각 자료형의 크기가 다르므로, 출력한 데이터를 다시 읽어 올 때는 **파일에 출력한 순서대로 읽어 들여야 한다**.
    - int, boolean, double 순서로 저장했기 때문에, 읽어 들일 때도 같은 순서로 읽어 들였다. 

- 실행 결과

  ```java
  100
  true
  50.5
  ```

- 이처럼 `DataInputStream`과 `DataOutputStream`을 사용하면 **특정 타입**으로 데이터를 저장하고 불러올 수 있다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| 다양한 타입의 출력](https://programmers.co.kr/learn/courses/9/lessons/317#)
- [코딩의 시작, TCP School \| JAVA \| 스트림](https://www.tcpschool.com/java/java_io_stream)
- [LUNA Y0UNG – Medium \| Basics: 직렬화(Serialization)란? (feat. Java)](https://medium.com/@lunay0ung/basics-%EC%A7%81%EB%A0%AC%ED%99%94-serialization-%EB%9E%80-feat-java-2f3eb11e9a8)
- [Integerous DevLog \| 자바의 정석 - 직렬화(Serialization)](https://ryan-han.com/post/java/java-serialization/)
- [개발이 하고 싶어요 \| [JAVA] ByteStream : DataInputStream / DataOutputStream](https://hyeonstorage.tistory.com/239)
- [techguruspeaks.com \| Low-level and High-level Byte Streams](https://www.techguruspeaks.com/low-level-and-high-level-byte-streams/)
