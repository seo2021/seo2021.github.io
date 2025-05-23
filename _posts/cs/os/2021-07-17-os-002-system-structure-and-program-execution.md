---
title: "[KOCW 운영체제] 2강 컴퓨터 시스템 구조와 프로그램 실행(System Structure & Program Execution)"
layout: single
related: true
categories:
- CS
- OS
tags:
  - 운영체제
  - KOCW
---
 
> KOCW 이화여대 반효경 교수님의 운영체제(2014-1) 강의 정리입니다.


### 2강
- 컴퓨터 시스템에서 하드웨어의 동작
- 하드웨어 위에서의 프로그램의 실행


## 컴퓨터 시스템 구조

![컴퓨터 시스템 구조](https://user-images.githubusercontent.com/76505625/126018047-e36a1cef-d538-4c11-a2ee-3bd2ef2cdc5b.png)

- CPU와 메모리로 구성된 것을 보통 컴퓨터라고 한다.
- I/O device의 데이터가 컴퓨터로 들어가는 것을 Input이라고 하며, I/O device의 결과를 컴퓨터로 내보내는 것은 output이라고 한다. 

- 메모리는 CPU의 작업 공간이다.
- CPU는 메모리에서 기계어를 읽어서 실행한다.
- 디스크는 Input, Output device의 역할을 모두 수행한다.

![컴퓨터 시스템 구조 상세](https://user-images.githubusercontent.com/76505625/126018780-d4fa7308-7870-4986-8508-1e72e51e851b.png)

- I/O device를 전담하는 작은 CPU 같은 Device Controller가 있다.
- Device Controller를 위한 작업 공간을 Local Buffer라고 한다.


## CPU

![CPU](https://user-images.githubusercontent.com/76505625/126019043-f5260e5a-67f3-438f-a22b-49f7c44e4a6f.png)

- Register
  - 정보를 저장하는 공간이다.
- Mode Bit
  - CPU안에서 실행되는 프로그램이 운영체제인지 사용자 프로그램인지를 구분해준다.

  - **사용자 프로그램의 잘못된 수행**으로 다른 프로그램 및 운영체제에 피해가 가지 않도록 하기 위한 **보호** 장치 필요.
    - Mode Bit을 통해 하드웨어적으로 두 가지 모드의 Operation 지원.
      - **1** 사용자 모드: 사용자 프로그램 수행.
      - **0** 모니터 모드: OS 코드 수행.

      - 보안을 해칠 수 있는 중요한 명령어는 **모니터 모드**에서만 수행 가능한 **특권명령**으로 규정.
      - Interrupt나 Exception 발생 시 하드웨어가 Mode Bit을 0으로 바꾼다.
      - 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 셋팅.

        > 모니터 모드(= 커널 모드, 시스템 모드)

          ![모니터 모드와 유저 모드](https://user-images.githubusercontent.com/76505625/126019920-77fb8c2e-b74d-448b-87d2-178abaf85e37.png)

- Interrupt Line
  - 메모리 접근을 하면서 명령어를 실행하는 동안 I/O Device, Timer에서 들어온다.
  - Interrupt가 들어오면 프로그램의 CPU 사용 제어권이 OS로 넘어간다.

  - 인터럽트(Interrupt)
    - 일반적으로 하드웨어 인터럽트를 말한다. 
    - 인터럽트 당한 시점의 레지스터와 Program Counter(메모리 주소를 가리키고 있는 레지스터)를 저장한 후, CPU의 제어를 인터럽트 처리 루틴에 넘긴다.

    - 하드웨어 인터럽트(Interrupt)
      - 하드웨어가 발생시킨 인터럽트
    - 소프트웨어 인터럽트(Trap)
      - Exception: 프로그램이 오류를 범한 경우
      - System Call: 프로그램이 커널 함수를 호출하는 경우  

    - 💡 인터럽트 관련 용어
      - 인터럽트 벡터
        - 해당 인터럽트의 처리 루틴 주소를 가지고 있다(각 인터럽트 마다 어디에 있는 함수를 실행해야 하는지 알 수 있다).
      - 인터럽트 처리 루틴(=Interrupt Service Routine, 인터럽트 핸들러)
        - 해당 인터럽트를 처리하는 커널 함수.


## Timer

![Timer의 인터럽트](https://user-images.githubusercontent.com/76505625/126021519-7a5b7d14-5810-4dcd-a1b0-7caeed532c85.png)

- CPU를 특정 프로그램이 독점하는 것으로부터 보호한다.
  - 정해진 시간이 흐른 뒤 운영체제에게 제어권이 넘어가도록 인터럽트를 발생시킨다.
    - 타이머는 매 클럭 틱 때마다 1씩 감소.
    - 타이머 값이 0이 되면 타이머 인터럽트 발생.

- Time Sharing을 구현하기 위해 널리 이용된다.
- 현재 시간을 계산하기 위해서도 사용한다.


## Device Controller

![Device Controller의 인터럽트](https://user-images.githubusercontent.com/76505625/126021549-f7c12b7e-571a-481c-a2c8-b53cfabff360.png)

- 해당 I/O 장치유형을 관리하는 일종의 작은 CPU
  - (CPU가 지시한)제어 정보를 위해 Control Register, Status Register를 가진다.
  - Local Buffer(일종의 Data Register)를 가진다.

- I/O는 실제 Device와 Local Buffer 사이에서 일어난다.
- Device Controller는 I/O가 끝났을 경우 Interrupt로 CPU에 그 사실을 알린다.

    > Device Driver(장치 구동기)
    >   - OS 코드 중 각 장치별 처리 루틴 👉 Software
    >   - 각 하드웨어에 접근하기 위한 매개체(?)

    > Device Controller(장치 제어기)
    >   - 각 장치를 통제하는 일종의 작은 CPU 👉 Hardware


## DMA(Direct Memory Access) Controller
- CPU와 같이 메모리에 직접 접근할 수 있는 Controller.
  - CPU의 중재없이 Device Controller가 Device의 Buffer Storage의 내용을 메모리에 Block 단위로 직접 전송.
- I/O Device로부터 CPU에 들어오는 인터럽트를 대신 처리해준다.
  - 바이트 단위가 아니라 Block 단위로 인터럽트를 발생시킨다. 

- 💡 CPU와 CMA Controller가 동시에 접근 시 이를 제어할 수 있도록 Memory Controller가 있다.


## 입출력(I/O)의 수행
- 운영체제를 통해서만 I/O 장치에 접근할 수 있다. 
- 모든 입출력 명령은 특권 명령이다.

- 사용자 프로그램이 I/O를 하는 과정 

  ![시스템 콜](https://user-images.githubusercontent.com/76505625/126021624-779b01aa-2ae3-45fd-89ea-9763fa3725ce.png)

  1. 시스템 콜(System Call)
    - 사용자 프로그램이 운영체제의 서비스를 받기 위해 (운영체제) 커널 함수를 호출하는 것.
      - 프로그램은 운영체제에게 요청을 하기 위해서 CPU에 인터럽트를 걸 수 있다. 👉 소프트웨어 인터럽트
      - 따라서, Mode Bit이 0으로 바뀌고, CPU 제어권이 운영체제로 넘어가고 운영체제는 해당 I/O 장치에 요청할 수 있게 된다.
  2. Trap을 사용하여 인터럽트 벡터의 특정 위치로 이동.
  3. 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동.
  4. 올바른 I/O 요청인지 확인 후 I/O 수행.
  5. I/O 완료 시 제어권을 시스템콜 다음 명령으로 옮긴다.
    - I/O가 끝나면 이를 CPU에게 알린다. 👉 하드웨어 인터럽트

## 동기식 입출력과 비동기식 입출력

![동기식 입출력과 비동기식 입출력](https://user-images.githubusercontent.com/76505625/126022284-f76f16cf-eb37-46a0-b70c-5c3684f1506c.png)

- 동기식 입출력(Synchronous I/O)
  - I/O 요청 후 입출력 **작업이 완료된 후에** 제어가 사용자 프로그램에 넘어간다.
  - 일반적으로 read 수행 시.

  - 구현 방법 1
    - I/O가 끝날 때까지 CPU를 낭비시킨다.
    - 매 시점 하나의 I/O만 일어날 수 있다
  - 구현 방법 2
    - I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗는다.
    - I/O 처리를 기다리는 줄에 그 프로그램을 줄 세운다.
    - **다른 프로그램에게 CPU를 준다**.

- 비동기식 입출력(asynchronous I/O)
  - I/O가 시작된 후 입출력 **작업이 끝나기를 기다리지 않고**, 제어가 사용자 프로그램에 즉시 넘어간다.
    - I/O 요청 후, **I/O와 무관한 일을 계속 진행**.
  - 일반적으로 write 수행 시.

- 두 경우 모두 I/O의 완료는 인터럽트로 알려준다.


## 서로 다른 입출력 명령어

![서로 다른 입출력 명령 방식](https://user-images.githubusercontent.com/76505625/126025490-4cccc268-f0f3-4f10-bd89-d5899a70f153.png)

1. I/O를 수행하는 **Special Instruction**에 의해 수행(좌측 그림)
  - 메모리를 수행하는 명령어가 따로 있고, I/O를 수행하려면 Special Instruction에 의해 수행하는 방식.
2. **Memory Mapped** I/O에 의해 수행(우측 그림)
  - I/O Device에도 메모리 주소의 연장 주소를 붙이고, 주소에 의해 접근하는 방식.


## 저장장치 계층 구조

![저장장치 계층 구조](https://user-images.githubusercontent.com/76505625/126025588-feb7f214-7d80-4742-82d0-e99ba2f7227d.png)

- 위로 갈수록 속도가 빠른 매체를 사용하고, 단위 공간당 가격이 비싸기 때문에 용량이 적다.

- Primary
  - 휘발성 매체로 구성.
  - CPU에서 직접 접근할 수 있는 메모리 매체.
    - CPU가 직접 접근하기 위해서는 바이트 단위로 접근 가능한 매체여야 한다.  
- Secondary
  - 비휘발성 매체로 구성.
  - 하드디스크는 섹터 단위로 접근이 가능하기 때문에 CPU에서 직접 접근하기 못한다. 


    > Caching
    >   - 다른 매체로부터 정보를 읽어들여서 쓰는 것.
    >   - 재사용을 목적으로 한다.


## 프로그램의 실행(메모리 load)
- 프로그램은 실행파일 형태로 파일 시스템(비휘발성)에 저장되어 있고, 실행시키면 메모리에 올라가서 프로세스가 된다.

![프로그램의 실행](https://user-images.githubusercontent.com/76505625/126025930-57c9a9f2-6780-4632-ba2d-bec43266a1b4.png)


- 정확하게는 물리적 메모리에 올라가기 전에 가상 메모리라는 한 단계를 더 거치게 된다.

![가상 메모리](https://user-images.githubusercontent.com/76505625/126025947-33b70e5d-124c-430f-a4bf-c11767f293d9.png)

- 각 프로그램의 독자적인 메모리 공간을 가상 메모리라고 한다.
- 프로그램을 실행시키면, 해당 프로그램만의 메모리 주소 공간이 형성된다. 이를 물리적 메모리에 올려서 실행한다.
  - 사용자 프로그램의 필요한 부분만 올리고, 그렇지 않은 부분은 디스크의 Swap Area에 올려둔다.
  - Swap Area는 메모리의 연장 공간으로 사용한다.
- 물리적 메모리에서 커널은 메모리에 항상 올라가 있지만, 사용자 프로그램은 종료 시 사라진다.

    > Kernel Address Space
    >   - Code: CPU에서 실행할 기계어 코드
    >   - Data: 변수 등 프로그램이 사용하는 자료구조
    >   - Stack: 함수를 호출하거나 실행할 때 사용

- Address Transition
  - 가상 메모리의 주소는 물리적 메모리의 주소로 변환. 


## 운영체제 커널 주소 공간의 내용

![운영체제 커널 주소 공간](https://user-images.githubusercontent.com/76505625/126026512-8b535ccc-f08d-4d12-8794-43a3a5d2aaeb.png)

- Data
  - 운영체제에서 사용하는 자료구조가 정의되어 있다.
  - CPU, 메모리, 디스크와 같은 하드웨어를 관리하기 위한 자료구조를 만들어서 정의하고 있다.
  - 프로세스를 관리하기 위한 자료구조(PCB, Process Control Block)를 만들어서 정의하고 있다.

- Stack
  - 어떤 사용자 프로그램들이 운영체제 커널의 코드를 실행 중인가를 저장.


## 사용자 프로그램이 사용하는 함수
- 함수(function)

  ![프로그램에서 사용하는 함수](https://user-images.githubusercontent.com/76505625/126026811-b7d1a075-960a-40ed-8b0b-3f63a7c8105f.png)

  - 사용자 정의 함수
    - 자신의 프로그램에서 정의한 함수. 
  - 라이브러리 함수   
    - 자신의 프로그램에서 정의하지 않고 갖다 쓴 함수.
    - 자신의 프로그램의 실행 파일에 포함되어 있다.

  - 사용자 정의 함수와 라이브러리 함수는 프로그램끼리 점프를 하여 함수에 접근할 수 있다.


  ![커널 함수](https://user-images.githubusercontent.com/76505625/126026828-056134e3-f15a-478a-89fe-666a2bad9beb.png)

  - 커널 함수
    - 운영체제 안에서 정의된 함수.
    - 커널 함수의 호출 = 시스템 콜. 
      - 시스템 콜을 통해서만 접근 가능하다. 


## 프로그램의 실행

![프로그램의 실행](https://user-images.githubusercontent.com/76505625/126026945-459c1df4-8631-4b86-970b-9c1ab43aa9e6.png)
 
 
## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
