---
title: "[KOCW 운영체제] 5강 CPU 스케줄링(CPU Scheduling)"
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

## CPU and I/O Bursts in Program Execution

  ![프로그램 실행 Path](https://user-images.githubusercontent.com/76505625/129429671-0d399c31-b9e9-4842-bc53-2750ee220cf3.png)

- 프로그램은 **CPU Burst**와 **I/O Burst**를 반복하며 실행되며, 프로그램의 종류의 따라 빈도나 길이가 다르다.
- CPU만 연속적으로 쓰면서 명령어를 실행하는 단계를 **CPU Burst**라고 하고, I/O를 실행하는 단계를 **I/O Burst**라고 한다.

- **CPU-Burst Time의 분포**

  ![CPU-Burst Time의 분포](https://user-images.githubusercontent.com/76505625/129429941-7f4e7f44-25de-43cb-920b-ac48e58c131d.png)
  
  - CPU-Burst Time이 짧을수록 중간에 I/O가 끼어드는 빈도가 많았고(**I/O Bound Job**), CPU-Burst Time이 길수록 I/O가 끼어드는 빈도가 낮았다(**CPU Bound Job**).
  - <u>여러 종류의 Job(Process)이 섞여 있기 때문에 <strong>CPU 스케줄링</strong>이 필요하다</u>.
    - **I/O Bound Job**은 사람과 계속 Interation하는 Job이기 때문에 **적절한 Response 제공이 필요**하다. 
    - CPU와 I/O 장치 등 시스템 자원을 골고루 **효율적으로 사용**(공평성보다는 **사람이 너무 오래 기다리지 않도록** 하는 것이 필요하다).

## 프로세스의 특성 분류
- 프로세스는 그 특성에 따라 다음 두 가지로 나뉜다.
  - <u>I/O-Bound Process</u>
    - CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 Job.
    - Many Short CPU Bursts.
      - CPU Burst가 빈번하고 짧다. 
  - <u>CPU-Bound Process</u>
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
  **1. Running ➡ Blocked** (ex. I/O 요청하는 시스템 콜)
  **2. Running ➡ Ready** (ex. 할당시간만료로 Timer Interrupt) 
  **3. Blocked ➡ Ready** (ex. I/O 완료 후 인터럽트)
    - I/O가 끝난 후 바로 CPU를 주지 않지만, 해당 프로세스의 우선순위가 높을 경우 CPU를 바로 넘겨줘야 하는 경우도 있다.
  **4. Terminate**
    - 프로세스가 종료된 경우.

    - 1, 4에서의 스케줄링은 **nonpreemptive(=비선점형, 강제로 빼앗지 않고 자진 반납)**
    - All Other Schedulling Is **Preemptive(=선점형, 강제로 빼앗음)**

## Scheduling Criteria(Performance Index = Performance Measure = 성능 척도)
- 어떤 스케줄링 알고리즘이 좋은지 평가하기 위한 방법.

- 시스템 입장에서의 성능 척도
  - CPU 하나 가지고 일을 최대한 많이 시키면 좋다.

  - <u>CPU Utilization(이용률)</u>
    - 전체 시간에서 CPU가 일한 시간의 비율.
    - Keep The CPU **As Busy As Possible**.
  - <u>Throughput(처리량)</u>
    - 주어진 시간동안 처리한 작업의 양.
    - **The Number Of Processes** That **Complete** Their Execution Per Time Unit.


- 프로세스 입장에서의 성능 척도
  - CPU를 빨리 얻고 빨리 처리되면 좋다.

  - <u>Turnaround Time(소요시간, 반환시간)</u>
    - CPU를 쓰러 와서 I/O를 하러 나가기까지 걸린 시간. 
    - Amount Of Time To **Execute A Particular Process**.
  - <u>Waiting Time(대기시간)</u>
    - CPU 사용을 위해 기다린 **모든** 시간. 
    - Amount Of Time A Process Has Been **Waiting In The Ready Queue**.
  - <u>Response Time(응답시간)</u>
    - Ready Queue에서 **최초로** CPU를 얻기까지 걸린 시간.
    - Amount Of Time It Takes From When A Request Was Submitted **Until The First Response Is Produced**, Not Output.
      - (For Time-Sharing Environment)

## Scheduling Algorithms 
- <u>FCFS(First-Come First-Served)</u>
  - **먼저 온 순서대로 처리**.
  - 비선점형.
  - 비효율적. 👉 먼저 온 프로세스의 작업 시간이 오래걸리면, 뒤의 프로세스는 그 시간만큼 기다려야 한다.

  - **Example 1**
    - 프로세스의 도착 순서 P<sub>1</sub>, P<sub>2</sub>, P<sub>3</sub> (모두  0초에 도착)

      | Process | Burst Time |
      |:-------:|:----------:|
      | P<sub>1 | 24 |
      | P<sub>2 | 3 |
      | P<sub>3 | 3 |
  
    - 스케줄 순서를 간트 차트로 나타내면 다음과 같다.
  
      ![FCFS Example 1](https://user-images.githubusercontent.com/76505625/129437606-15026e99-2d2a-4124-8df3-fc94031def5e.png)
  
    - Waiting Time For P<sub>1</sub> = 0; P<sub>2</sub> = 24; P<sub>3</sub> = 27
    - Average Waiting Time: (0 + 24 + 27)/3 = 17
  
  - **Example 2**
    - 프로세스의 도착 순서 P<sub>2</sub>, P<sub>3</sub>, P<sub>1</sub>
  
      ![FCFS Example 2](https://user-images.githubusercontent.com/76505625/129468221-e56cbe1d-db76-4b97-ad5f-e88c5fedfd83.png)
  
    - Waiting Time For P<sub>1</sub> = 6; P<sub>2</sub> = 0; P<sub>3</sub> = 3
    - Average Waiting Time: (6 + 0 + 3)/3 = 3
    - Example 1보다 낫다.
    - **Convoy Effect**: Short Process Behind Long Process 


- <u>SJF(Shortest-Job-First)</u>
  - 각 프로세스의 다음번 CPU Burst Time을 가지고 스케줄링에 활용.
  - **CPU Burst Time이 가장 짧은** 프로세스를 제일 먼저 스케줄.
  
  - Two Schemes
    - **Nonpreemptive**
      - 일단 CPU를 잡으면, 이번 CPU Burst가 완료될 때까지 CPU를 선점(preemption) 당하지 않는다.
    - **Preemptive**
      - 현재 수행 중인 프로세스의 남은 Burst Time보다 더 짧은 CPU Burst Time을 가지는 새로운 프로세스가 도착하면 CPU를 빼앗긴다.
      - 이 방법을 **Shortest-Remaining-Time-First(SRTF)**라고도 부른다.
  
  - SJF Is Optimal (Preemptive)
    - 주어진 프로세스들에 대해 **Minimum Average Waiting Time**을 보장.
  
  - **Example of Non-Preemptive SJF**
  
    | Process | Arrival Time | Burst Time |
    |:-------:|:------------:|:----------:|
    | P<sub>1 | 0.0 | 7 |
    | P<sub>2 | 2.0 | 4 |
    | P<sub>3 | 4.0 | 1 |
    | P<sub>4 | 5.0 | 4 |
  
    ![Example of Non-Preemptive SJF](https://user-images.githubusercontent.com/76505625/129479486-1d3dda55-8c36-4faf-8beb-25d9ef7a3450.png)
      
      - 0초에 P<sub>1</sub> 만 도착했으므로 P<sub>1</sub> 이 CPU를 얻게 되고, 7초에 반납을 한다.
      - 7초 시점에서 큐를 살펴보면 P<sub>2</sub>  ~ P<sub>4</sub> 까지 모두 도착해 있다.
      - 이중에서 CPU를 짧게 쓰는 순서대로 CPU를 얻게 된다.
  
    - Average Waiting Time = (0 + 6 + 3 + 7)/4 = 4
  
  - **Example of Preemptive SJF**
    
    ![Example of Preemptive SJF](https://user-images.githubusercontent.com/76505625/129479736-c08ecc5a-54e0-4b43-8909-d8fe86afa1f2.png)
  
    - Average Waiting Time = (9 + 1 + 0 + 2)/4 = 3
  
  - SJF의 문제점
    - **Starvation(기아 현상)**: Low Priority Processes May Never Execute.
    - CPU Burst Time을 미리 알 수 없다.
      - 프로그램은 Input을 받아서 실행되기도 하고, 분기가 일어나기도 하는 등의 상황 때문에 CPU Burst Time을 미리 알 수 없다.
      - 과거의 CPU Burst Time을 이용해서 **추정**만 가능하다. 👉 Exponential Averaging
        1. t<sub>n</sub> = n번째 CPU Burst의 실제 CPU 사용 시간
        2. 𝜏<sub>n+1</sub> = 다음 CPU Burst의 예측 시간
        3. 𝛼, 0 <= 𝛼 <= 1
        4. Define: 𝜏<sub>n+1</sub> = 𝛼t<sub>n</sub> + (1 - 𝛼)𝜏<sub>n</sub>
          - n번째 실제 CPU 사용 시간과 n번째 예측했던 시간을 일정 비율씩 곱해서 더해준다.
          - 식을 풀면 다음과 같다.
            - 𝜏<sub>n+1</sub> = 𝛼t<sub>n</sub> + (1 - 𝛼)t<sub>n-1</sub> + ... + (1 - 𝛼)<sup>j</sup>𝛼t<sub>n-j</sub> + ... + (1 - 𝛼)<sup>n+1</sup>𝜏<sub>0</sub>
            - 𝛼와 (1 - 𝛼)가 둘 다 1 이하이므로, 후속 term은 선행 term보다 적은 가중치 값을 가진다.
              - 뒤로 갈수록 (1 - 𝛼) 점점 더 곱해지게 되고, 1보다 작은 값을 더 곱하면 값이 더 작아지므로.
              - 가장 최근의 과거는 가중치를 높게 반영하고, 오래 전의 것은 가중치를 낮게 반영한 결과가 얻어진다.

  
- <u>Priority Scheduling</u>

  

  

  


4. <u>Priority Scheduling</u>
5. <u>RR(Round Robin)</u>
6. <u>Multilevel Queue</u>
7. <u>Multilevel Feedback Queue</u>


## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
