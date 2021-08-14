---
title: "[KOCW 운영체제] 5강 CPU 스케줄링(CPU Scheduling)"
layout: single
related: true
categories:
- CS
tags:
  - 운영체제
  - KOCW
---
 
> KOCW 이화여대 반효경 교수님의 운영체제(2014-1) 강의 정리입니다.

## CPU and I/O Bursts in Program Execution

  ![프로그램 실행 Path](https://user-images.githubusercontent.com/76505625/129429671-0d399c31-b9e9-4842-bc53-2750ee220cf3.png)

- 프로그램은 **CPU Burst**와 **I/O Burst**를 반복하며 실행되며, 프로그램의 종류의 따라 빈도나 길이가 다르다.
- CPU만 연속적으로 쓰면서 명령어를 실행하는 단계를 **CPU Burst**라고 하고, I/O를 실행하는 단계를 **I/O Burst**라고 한다.

- **CPU-burst Time의 분포**

  ![CPU-burst Time의 분포](https://user-images.githubusercontent.com/76505625/129429941-7f4e7f44-25de-43cb-920b-ac48e58c131d.png)
  
  - CPU-burst Time이 짧을수록 중간에 I/O가 끼어드는 빈도가 많았고(**I/O Bound Job**), CPU-burst Time이 길수록 I/O가 끼어드는 빈도가 낮았다(**CPU Bound Job**).
  - <u>여러 종류의 Job(Process)이 섞여 있기 때문에 <strong>CPU 스케줄링</strong>이 필요하다</u>.
    - **I/O Bound Job**은 사람과 계속 Interation하는 Job이기 때문에 **적절한 Response 제공이 필요**하다. 
    - CPU와 I/O 장치 등 시스템 자원을 골고루 **효율적으로 사용**(공평성보다는 **사람이 너무 오래 기다리지 않도록** 하는 것이 필요하다).

## 프로세스의 특성 분류
- 프로세스는 그 특성에 따라 다음 두 가지로 나뉜다.
  - <u>I/O-bound Process</u>
    - CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 Job.
    - Many Short CPU Bursts.
      - CPU Burst가 빈번하고 짧다. 
  - <u>CPU-bound Process</u>
    - 계산 위주의 Job.
    - Few Very Long CPU Bursts.
      - CPU Burst가 길고, 빈번하지 않다.

## CPU Scheduler & Dispatcher
- <u>CPU Scheduler</u>
  - Ready 상태의 프로세스 중에서 이번에 **CPU를 줄 프로세스를 고른다**.
- <u>Dispatcher</u>
  - CPU의 제어권을 CPU Scheduler에 의해 **선택된 프로세스에게 넘긴다**.
  - 이 과정을 **Context Switch(문맥 교환)**라고 한다.

    > CPU Scheduler, Dispatcher는 운영체제 안에서 특정 기능을 하는 코드이다.

- CPU 스케줄링이 필요한 경우는 프로세스에게 다음과 같은 상태 변화가 있는 경우이다.
  1. Running ➡ Blocked (ex. I/O 요청하는 시스템 콜)
  2. Running ➡ Ready (ex. 할당시간만료로 Timer Interrupt) 
  3. Blocked ➡ Ready (ex. I/O 완료 후 인터럽트)
    - I/O가 끝난 후 바로 CPU를 주지 않지만, 해당 프로세스의 우선순위가 높을 경우 CPU를 바로 넘겨줘야 하는 경우도 있다.
  4. Terminate
    - 프로세스가 종료된 경우.

    - 1, 4에서의 스케줄링은 **nonpreemptive(=비선점형, 강제로 빼앗지 않고 자진 반납)**
    - All Other Schedulling Is **Preemptive(=선점형, 강제로 빼앗음)**

## Scheduling Criteria(Performance Index = Performance Measure = 성능 척도)
- 어떤 스케줄링 알고리즘이 좋은지 평가하기 위한 방법.

1. 시스템 입장에서의 성능 척도
  - CPU 하나 가지고 일을 최대한 많이 시키면 좋다.

  - <u>CPU Utilization(이용률)</u>
    - Keep The CPU As Busy As Possible.
  - <u>Throughput(처리량)</u>
    - '#' Of Processes That Complete Their Execution Per Time Unit.

2. 프로세스 입장에서의 성능 척도
  - CPU를 빨리 얻으면 좋다.

  - <u>Turnaround Time(소요시간, 반환시간)</u>
    - Amount Of Time To Execute A Particular Process.
  - <u>Waiting Time(대기시간)</u>
    - Amount Of Time A Process Has Been Waiting In The Ready Queue.
  - <u>Response Time(응답시간)</u>
    - Amount Of Time It Takes From When A Request Was Submitted Until The First Response Is Produced, Not Output.\
      - (For Time-Sharing Environment) 


## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
