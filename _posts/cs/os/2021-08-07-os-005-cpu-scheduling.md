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

  
- <u>Priority Scheduling(우선순위 스케줄링)</u>
  - 각 프로세스마다 우선순위를 나타내는 숫자(정수)가 주어지게 된다.
  - 높은 우선순위(Highest Priority)를 가진 프로세스에게 CPU 할당.
    - Smallest Integer = Highest Priority
  
  - Two Schemes
    - **Nonpreemptive**
    - **Preemptive**

  - **SJF**는 일종의 **Priority Scheduling**이다.
    - SJF에서의 우선순위(Priority)는 Predicted Next CPU Burst Time이다.
  
  - 문제점
    - **Starvation(기아 현상)**: 우선순위가 낮은 프로세스는 영원히 CPU를 얻지 못할 수 있다.
  
  - 해결책
    - **Aging(노화)**: 시간이 지남에 따라 프로세스의 우선순위를 증가시킨다. 
  
- <u>RR(Round Robin)</u>
  - 각 프로세스는 동일한 크기의 **할당 시간(Time Quantum)**을 가진다.
    - 일반적으로 10-100 Milliseconds.
  - 할당 시간이 지나면 프로세스는 **선점(Preempted)**당하고, Ready Queue의 제일 뒤에 가서 줄을 선다.
  - n개의 프로세스가 Ready Queue에 있고 각 할당 시간이 **Q Time Unit**인 경우, 각 프로세스는 최대 Q Time Unit 단위로 **CPU의 시간을 1/n**을 얻는다.
    - 어떤 프로세스도 (n-1)Q Time Unit 이상 기다리지 않는다.
      - n-1개의 프로세스가 q만큼의 시간을 쓰고 나면, 적어도 자기 차례가 1번은 돌아온다.
    - CPU를 짧게 쓰는 프로세스는 1번의 Q Time Unit 만에 CPU를 쓰고 나가고, CPU를 오래 쓰는 프로세스는 Q Time Unit만큼 CPU를 사용하고 뺏기고, 다시 할당 받는 과정을 반복하므로 응답 시간이 빨라진다.
    - 대기 시간이 CPU의 사용 시간에 비례하므로, 공정한 스케줄링이라 볼 수 있다.
  - Performance
    - Q Large(할당시간이 큰 경우) 👉 FCFS
    - Q Small(할당 시간이 작은 경우) 👉 Context Switch 오버헤드가 커진다.
    
    - 따라서, 적당한 Time Quantum(10-100 Milliseconds)을 주는 것이 바람직하다.
  
  - **Example 1**
  
    | Process | Burst Time |
    |:-------:|:----------:|
    | P<sub>1 | 24 |
    | P<sub>2 | 3 |
    | P<sub>3 | 3 |
  
    - 스케줄 순서를 간트 차트로 나타내면 다음과 같다.

      ![Example of Round Robin](https://user-images.githubusercontent.com/76505625/133917999-76b44904-7ce4-4bf6-add7-b6da0d96d64b.PNG)
  
      - CPU Burst Time이 Quantum Time보다 짧은 프로세스는 한 번에 CPU를 사용하고 빠져나가고, 나머지 프로세스는 자신 CPU Burst Time만큼 반복적으로 CPU를 사용한다.

      - 일반적으로 SJF보다 **Average Turnaround Time**이 길지만, **Response Time**은 더 짧다.
        - 프로세스들의 CPU Burst Time이 동일할 경우 CPU를 조금씩 서비스 받으면서 모든 프로세스가 마지막에 동시에 빠져나가게 되고, 이는 대기 시간을 길어지게 할 수 있다.
        - 하지만, 일반적으로는 짧은 프로세스와 긴 프로세스가 섞여 있기 때문에 RR이 더 효과를 발휘한다.
  
- <u>Multilevel Queue</u>
  
  
  ![Multilevel Queue](https://user-images.githubusercontent.com/76505625/133917778-0c5eb289-c21c-47fd-9753-8905c82b586d.PNG)
    
  - 프로세스의 종류에 따라 우선순위가 정해지며(어느 큐에 속할지 정해진다), 이는 바꿀 수 없다.
  - 우선순위가 높은 프로세스가 빨리 CPU를 얻어야 할 때 사용한다.
    
  - Ready Queue를 여러 개로 분할.
    - **Foreground**(Interactive)
    - **Background**(Batch - No Human Interaction)
  
  - 각 큐는 독립적인 스케줄링 알고리즘을 가진다.
    - **Foreground** 👉 RR
    - **Background** 👉 FCFS
    
    - 각 큐의 특성에 맞는 스케줄링 방법을 채택해야 한다.
  
  - 큐에 대한 스케줄링이 필요하다.
    - 어떤 큐에 스케줄링을 줄 것인지 결정.
  
    - **Fixed Priority Scheduling**
      - Serve **All From Foreground** Then From Background. 👉 우선 순위가 높은 큐가 비어 있을 때만, 낮은 순위의 큐에 CPU 할당.
      - Possibility of **Starvation**.
    - **Time Slice**
      - 각 큐에 CPU Time을 **적절한 비율로 할당**.
      - ex) 80% to Foreground in RR, 20% to Background in FCFS.
  
- <u>Multilevel Feedback Queue</u>
  
  ![Multilevel Feedback Queue](https://user-images.githubusercontent.com/76505625/133918698-a704eb51-0cf1-4949-8831-06469202ffcf.PNG)
  
  - 프로세스가 **다른 큐로 이동 가능**.
  - 에이징(Aging)을 이와 같은 방식으로 구현할 수 있다.
  
  - **Multilevel-Feedback-Queue Scheduler**를 정의하는 **파라미터**들.
    - Queue의 수
    - 각 큐의 Scheduling Algorithm
    - Process를 상위 큐로 보내는 기준
    - Process를 하위 큐로 내쫓는 기준
    - 프로세스가 CPU 서비스를 받으려 할 때 들어갈 큐를 결정하는 기준
  
  - 일반적으로 
    1. 처음 들어오는 프로세스를 우선순위가 가장 높은 큐에 넣고, 우선순위가 높은 큐는 RR에서 Time Quantum을 짧게 준다.
    2. 아래의 큐로 내려갈 수록 RR의 Time Quantum을 점점 길게 준다.
    3. 가장 아래의 큐는 FCFS의 방식을 사용한다.
  
    - CPU 사용 시간이 긴 프로세스는 아래의 큐로 점점 이동을 하면서 Time Quantum은 더 받게 되지만, 우선순위는 낮아진다.
    - **CPU 사용 시간이 짧은 프로세스에게 우선순위를 많이 주는 방식**. 
  
  - **Example 1**
    - Three Queues
      - Q<sub>0</sub>: Time Quantum 8 milliseconds
      - Q<sub>1</sub>: Time Quantum 16 milliseconds
      - Q<sub>2</sub>: FCFS
    
    - **Scheduling**
      1. New Job이 Queue Q<sub>0로 들어간다.
      2. CPU를 잡아서 할당 시간 8 milliseconds 동안 수행된다.
      3. 8 milliseconds 동안 다 끝내지 못했으면, Queue Q<sub>1</sub>으로 내려간다.
      4. Q<sub>1</sub>에 줄서서 기다렸다가 CPU를 잡아서 16 milliseconds 동안 수행된다.
      5. 16 milliseconds에 끝내지 못한 경우 Queue Q<sub>2</sub>로 쫓겨난다.
  
- <u>Multiple-Processor Scheduling</u>
  - CPU가 여러 개인 경우 스케줄링은 더욱 복잡해진다.
  
  - **Homogeneous Process**인 경우
    - Queue에 **한 줄로 세워서** 각 프로세서가 알아서 꺼내가게 할 수 있다.
    - 반드시 특정 프로세서에서 수행되어야 하는 프로세스가 있는 경우에는 문제가 더 복잡해진다.
  
  - **Load Sharing** 필요
    - 일부 프로세서에 Job이 몰리지 않도록 **부하를 적절히 공유**하는 메커니즘이 필요하다.
    - 별개의 큐를 두는 방법 vs. 공동 큐를 사용하는 방법.
  
  - **Symmetric Multiprocessing(SMP)**
    - 각 프로세서가 각자 알아서 스케줄링 결정.
  - **Asymmetric Multiprocessing**
    - 하나의 프로세서가 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 거기에 따른다.
  
- <u>Real-Time Scheduling</u>
  - **Hard Real-Time Systems**
    - Hard Real-Time Task는 정해진 시간 안에 반드시 끝내도록 스케줄링해야 한다.
    - 일반적으로 Real-Time Task를 미리 스케줄링해서 데드라인이 보장되도록 한다.

  - **Soft Real-Time Computing**
    - Soft Real-Time Task는 일반 프로세스에 비해 높은 Priority를 갖도록 해야 한다.
    - 데드라인을 반드시 보장하지는 않음.
  
- <u>Thread Scheduling</u>
  - **Local Scheduling**
    - User Level Thread의 경우 사용자 수준의 Thread Library에 의해 어떤 Thread를 스케줄할지 결정.
    - 운영체제는 쓰레드의 존재를 모르므로 운영체제가 하는 것이 아닌, **사용자 프로세스가 직접 스케줄링**을 한다.
  
  - **Global Scheduling** 
    - Kernel Level Thread의 경우 **일반 프로세스와 마찬가지**로 커널의 단기 스케줄러가 어떤 Thread를 스케줄할지 결정.

## Algorithm Evaluation
  
  ![Queueing Models](https://user-images.githubusercontent.com/76505625/133933502-8c8b223e-6c67-43bc-9fa2-b16f7d06d2b0.PNG)
  
- <u>Queueing Models</u>
  - **확률 분포**로 주어지는 **Arrival Rate(도착률)**와 **Service Rate(처리율)** 등을 통해 각종 **Performance Index** 값을 계산.
  - 이론적인 방법.

- <u>Implementation(구현) & Measurement(성능 측정)</u>
  - **실제 시스템**에 알고리즘을 **구현**하여 **실제 작업(Workload)**에 대해서 성능을 측정 비교.

- <u>Simulation(모의 실험)</u>
  - 알고리즘을 **모의 프로그램**으로 작성 후, **Trace**(시뮬레이션 프로그램에 Input으로 들어갈 Data)를 입력으로 하여 결과 비교.
  

## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
