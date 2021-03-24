---
title: "[프로그래머스 자바 중급] 입력과 출력 : 파일(File) 입출력"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - io
  - 자바중급
---

## RandomAccessFile 클래스
- 앞서 살펴본 다양한 **입출력 스트림**을 이용하면 **파일에 순차적으로 입출력 작업**을 수행할 수 있다.

- 하지만, 순차적 접근이 아닌 **임의의 지점**에 접근하여 작업을 수행하고 싶다면, **`RandomAccessFile` 클래스**를 사용하면 된다.
  - `RandomAccessFile` 클래스는 **파일**만을 대상으로 하며, **임의의 지점에서 입출력을 동시에 수행**할 수 있다.
  - **생성자**에는 **인수**로 **파일의 이름**뿐만 아니라 **파일 모드**까지 함께 전달해야 한다.
    - 💡 **파일 모드**란 **파일의 사용 용도를 나타내는 문자열**로, 자바에서 사용할 수 있는 대표적인 파일 모드는 다음과 같다.

      | 파일 모드 | 설명 |
      |:--------:|:-----|
      | "r" | 파일을 오로지 **읽는 것만 가능**한 모드로 개방 |
      | "rw" | 파일을 **읽고 쓰는 것이 모두 가능**한 모드로 개방. 만약 파일이 없으면 새로운 파일을 생성 |
      
  - `getFilePointer()` 메소드를 사용하면 **파일 포인터의 현재 위치**를 확인할 수 있다.
  - 또한, `seek()` 메소드를 사용하면 **파일 포인터의 위치를 변경**할 수도 있다.
  
  ```java
  public static void main(String[] args) {
		try {
			// "rw" 모드로 "data.txt" 파일을 개방
			RandomAccessFile file = new RandomAccessFile("data.txt", "rw");
			
			System.out.println(file.getFilePointer()); // 0: 파일 포인터의 현재 위치를 반환
			file.writeInt(10); // 정수 10을 저장(4 Byte)
			System.out.println(file.getFilePointer()); // 4
			
			file.seek(20); // 파일 포인터의 위치를 20으로 이동
			System.out.println(file.getFilePointer()); // 20
			
		} catch (IOException e) {
			e.printStackTrace();
		}

	}//--main()
  ```

## File 클래스
- **입출력 스트림**을 사용하면 **파일을 통한 입출력 작업**을 수행할 수 있다.
- 하지ak


  

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| Char 단위 입출력(File)](https://programmers.co.kr/learn/courses/9/lessons/320)
- [코딩의 시작, TCP School \| JAVA \| 파일 입출력](https://www.tcpschool.com/java/java_io_file)
