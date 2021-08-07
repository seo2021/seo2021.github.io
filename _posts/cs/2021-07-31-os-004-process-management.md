---
title: "[KOCW 운영체제] 4강 프로세스 관리(Process Management)"
layout: single
related: true
categories:
- CS
tags:
  - 운영체제
  - KOCW
---
 
> KOCW 이화여대 반효경 교수님의 운영체제(2014-1) 강의 정리입니다.

## 프로세스 생성(Creation)
- 부모 프로세스(Parent Process)가 자식 프로세스(Children Process) 생성.
- 프로세스의 트리(계층 구조) 형성.

- 프로세스는 자원을 필요로 한다.
  - 운영체제로부터 받는다.
  - 부모와 공유한다.

  - 자원의 공유
    - 원칙적으로는 공유하지 않으므로, 공유하지 않는 모델이 일반적이다.

    1. 부모와 자식이 모든 자원을 공유하는 모델.
    2. 일부를 공유하는 모델.
    3. 전혀 공유하지 않는 모델.

- 주소 공간(Address space)
  - 자식은 부모의 주소 공간을 복사한다.
  - 자식은 그 공간에 새로운 프로그램을 올린다.

- 유닉스의 예
  - `fork()` **시스템 콜**이 새로운 프로세스를 생성
  - `fork()` 다음에 이어지는 `exec()` 시스템 콜을 통해 새로운 프로그램을 메모리에 올린다.       

## 프로세스 수행(Execution)
- 부모와 자식이 공존하며 수행되는 모델.
- 자식이 종료(Terminal)될 때까지 부모가 기다리는(Wait) 모델.

## 프로세스 종료(Termination)
- 프로세스가 마지막 명령을 수행한 후 운영체제에게 이를 알려준다. 👉 `exit`
  - 자식이 부모에게 Output Data를 보낸다(via `wait`).
  - 프로세스의 각종 자원들이 운영체제에게 반납된다.

- 부모 프로세스가 자식의 수행을 종료시킨다. 👉 `abort`
  - 자식이 할당 자원의 한계치를 넘어선 경우.
  - 자식에게 할당된 태스크가 더 이상 필요하지 않은 경우.
  - 부모가 종료(`exit`)하는 경우
    - 운영체제는 부모 프로세스가 종료하는 경우 자식이 더 이상 수행되도록 두지 않는다.
    - 단계적인 종료.

## 프로세스와 관련한 시스템 콜
- `fork()`
  - Create A Child (Copy)
- `exec()`
  - Overlay New mage
- `wait()`
  - Sleep Until Child Is Done
- `exit()`
  - Frees All The Resources, Notify Parent   

## fork() 시스템 콜
- 프로세스는 `fork()` 시스템 콜로 생성된다.

  ```c
  int main() 
  {
    int pid;
    pid = fork(); /*시스템 콜을 통해 자식 프로세스가 만들어진다*/
    if (pid == 0) /*child*/
      printf("\n Hello, I am child!\n");
    else if (pid > 0) /*parent*/
      printf("\n Hello, I am parent!\n);
  }
  ```
  - 자식 프로세스는 부모 프로세스의 문맥을 그대로 복사하므로, 부모 프로세스가 `fork()`를 수행한 다음 시점부터 실행된다.
  - `fork()` 함수의 **반환 값**으로 부모와 자식 프로세스를 구분할 수 있다.
    - **부모 프로세스는 양수**(자식 프로세스의 pid), **자식 프로세스는 0**.

## exec() 시스템 콜
- 프로세스는 `exec()` 시스템 콜을 통해 **자식 프로세스**에 **새로운 프로그램**을 실행시킬 수 있다.

  ```c
  int main()
  {
    int pid;
    pid = fork();
    if (pid == 0) /*child*/
    {
      printf("\n Hello, I am child! Now I'll run date \n");
      execlp("/bin/date", "/bin/date", (char *) 0); /*execlp()는 exec()을 호출한다*/
    }
    else if (pid > 0) /*parent*/
      printf("\n Hello, I am parent! \n");
  }
  ```
  - `execlp("프로그램 이름", "프로그램 이름", "프로그램에 전달할 인자1", "프로그램에 전달할 인자2", "...", "null 포인터");`
    - 자식이 인자로 주어진 프로그램으로 새로 덮어 씌워지고, 새로운 프로그램의 처음부터 실행된다.


- `exec()`은 **자기 자신**을 **새로운 프로그램**으로 덮어 씌우는데도 사용할 수 있다.

  ```c
  int main()
  {
    printf("1");
    execlp("echo", "echo", "3", (char *) 0);
    printf("2");
  }
  ```
  - `fork()`의 수행 없이, `execlp()`를 만나면 새로운 프로그램으로 덮어 씌워진다.
  - 1이 화면에 출력되고, `echo` 프로그램(명령어)으로 덮어 씌워져서 3이 화면에 종료되고 프로세스가 종료된다.
  - 2는 출력이 안 된다.
  
    > - `echo`는 뒤에 나오는 인자를 화면에 그대로 출력해준다.

## wait() 시스템 콜
- 프로세스 A가 `wait()` 시스템 콜을 호출하려면
  - 커널은 Child가 종료될 때까지 프로세스 A를 Sleep시킨다. 👉 Block 상태
  - Child Process가 종료되면 커널은 프로세스 A를 깨운다. 👉 Ready 상태

  ![wait() 시스템 콜](https://user-images.githubusercontent.com/76505625/128584568-869898a7-91f3-4b64-b9a0-2f536626cadc.png)

## exit() 시스템 콜
- 프로세스의 종료
  - **자발적 종료**
    - 마지막 Statement 수행 후, 명시적으로 `exit()` 시스템 콜을 통해 종료.
      - 프로그램에 명시적으로 적어주지 않아도 `main` 함수가 리턴되는 위치에 컴파일러가 넣어준다.
  - **비자발적 종료**
    - 부모 프로세스가 자식 프로세스를 강제 종료하는 경우.
      - 자식 프로세스가 한계치는 넘어서는 자원 요청 시.
      - 자식에게 할당된 태스크가 더 이상 필요하지 않을 시.
    - 키보드로 `kill`, `break` 등을 친 경우.
    - 💡 부모가 종료하는 경우 부모 프로세스가 종료되기 전에 자식들이 먼저 종료된다. 

## 프로세스 간 협력
- **독립적 프로세스(Independent Process)**
  - 프로세스는 각자의 주소 공간을 가지고 수행되므로, 원칙적으로 하나의 프로세스는 다른 프로세스의 수행에 영향을 미치지 못한다.
- **협력 프로세스(Cooperating Process)**
  - 프로세스 협력 메커니즘을 통해 하나의 프로세스가 다른 프로세스의 수행에 영향을 미칠 수 있다.

- **프로세스 간 협력 메커니즘(IPC: Interprocess Communication)**

  ![IPC, 프로세스 간 협력 메커니즘](https://user-images.githubusercontent.com/76505625/128586998-f73e3dff-6622-4ea4-996c-489920e8249b.png)

  - <u>메시지를 전달하는 방법</u>
    - **Message Passing**
      - **커널을 통해** 전달
      - Message System
        - 프로세스 사이에 공유 변수(Shared Variable)을 일체 사용하지 않고 통신하는 시스템
        
      1. Direct Communication
        - 통신하려는 프로세스의 **이름을 명시적으로 표시**  
          ![Direct Communication](https://user-images.githubusercontent.com/76505625/128586753-37a8b85a-456f-4577-a014-c97adb564ae4.png)
        
      2. Indirect Communication
        - **Mailbox(또는 Port)를 통해** 메시지를 간접 전달(메시지를 주고 받을 프로세스를 명시하지 않는다).  
          ![Indirect Communication](https://user-images.githubusercontent.com/76505625/128586821-d1d167fa-3586-43dd-9607-62f57f018a42.png)
 
  - <u>주소 공간을 공유하는 방법</u>
    - **Shared Memory**
      - 서로 다른 프로세스 간에도 일부 주소 공간을 공유하는 Shared Memory 메커니즘이 있다.
    - **cf) Thread 간 협력**
      - Thread는 사실상 하나의 프로세스이므로 프로세스 간 협력으로 보기는 어렵지만, 동일한 Process를 구성하는 Thread들 간에는 주소 공간을 공유하므로 협력이 가능하다.

## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
