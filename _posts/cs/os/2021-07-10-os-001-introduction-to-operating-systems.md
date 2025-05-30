---
title: "[KOCW 운영체제] 1강 운영체제 개요(Introduction to Operating Systems)"
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

## 운영체제(Operating Systen, OS)란 무엇인가?
- 컴퓨터와 하드웨어 바로 위에 설치되어 사용자 및 다른 모든 소프트웨어와 하드웨어를 연결하는 소프트웨어 계층.

  <p align="center"><img src="https://user-images.githubusercontent.com/76505625/125147209-d6b38300-e164-11eb-9951-026dc93c4d7b.png" alt="운영체제란 무엇인가"></p>
  
- 협의의 운영체제(커널)
  - 운영체제의 핵심 부분으로 메모리에 상주하는 부분.
- 광의의 운영체제
  - 커널뿐 아니라 각종 주변 시스템 유틸리티를 포함한 개념.
  - 메모리에 상주하지 않는 별도의 프로그램들.

## 운영체제의 목적
- 컴퓨터 시스템을 편리하게 사용할 수 있는 환경을 제공.
  - 운영체제는 동시 사용자/프로그램들이 각각 독자적 컴퓨터에서 수행되는 것 같은 환상을 제공.
  - 하드웨어를 직접 다루는 복잡한 부분을 운영체제가 대행.

  <p align="center"><img src="https://user-images.githubusercontent.com/76505625/125147069-20e83480-e164-11eb-812c-f509fa062cf9.png" alt="운영체제의 목적"></p>
  
- 컴퓨터 시스템의 **자원을 효율적으로 관리**.
  - 프로세서, 기억장치, 입출력 장치 등의 효율적 관리(하드웨어 관리).
    - 주어진 자원으로 **최대한의 성능**을 낼 수 있어야 한다.
    - 사용자 간의 **형평성** 있는 자원 분배를 해야 한다.
  - 사용자 및 운영체제 자신의 보호.
  - 프로세스, 파일, 메시지 등을 관리(소프트웨어 관리).
  
  <p align="center"><img src="https://user-images.githubusercontent.com/76505625/125149327-7ed04880-e173-11eb-9eda-722c5f6379f8.png" width="530" alt="컴퓨터 시스템 자원 관리"></p>

## 운영체제의 분류
- 동시 작업 가능 여부
  - 단일 작업(single tasking)
    - 한 번에 하나의 작업만 처리.
    - ex) MS-DOS 프롬프트 상에서는 한 명령의 수행을 끝내기 전에 다른 명령을 수행시킬 수 없음.
  - 다중 작업(multi tasking)
    - 동시에 두 개 이상의 작업 처리.
    - ex) UNIX, MS Windows 등에서는 한 명령의 수행이 끝나기 전에 다른 명령이나 프로그램을 수행할 수 있음.

- 사용자의 수
  - 단일 사용자(single user)
    - ex) MS-DOS, MS Windows
  - 다중 사용자(multi user)
    - ex) UNIX, NT server 
  - 여러 사용자의 계정을 만들어서 동시접근을 할 수 있는지가 기준.

- 처리 방식
  - 일괄 처리(batch processing)
    - 작업 요청의 일정량 모아서 한꺼번에 처리.
    - 작업이 완전 종료될 때까지 기다려야 한다.
    - ex) 초기 Punch Card 처리 시스템
  - 시분할(time sharing)
    - 여러 작업을 수행할 때, 컴퓨터 처리 능력을 일정한 시간 단위로 분할하여 사용.
    - 일괄 처리 시스템에 비해 짧은 응답 시간을 가진다.
      - ex) UNIX
    - Interactive한 방식
      - 사용자는 컴퓨터를 사용하면서 바로 결과가 나온다고 느낄 수 있다.

  <p align="center"><img src="https://user-images.githubusercontent.com/76505625/125147740-15970800-e168-11eb-958c-26ac375010b1.png" alt="시분할 처리 방식"></p>
  
  - 실시간(Realtime OS)
    - 정해진 시간 안에 어떠한 일이 반드시 종료됨이 보장되어야 하는 실시간 시스템을 위한 OS.
    - ex) 원자로/공장 제어, 미사일 제어, 반도체 제어, 로보트 제어.

  - 💡 **시분할 방식**은 일반적인 범용적 컴퓨터에서 사용하는 방식이고, **실시간 운영체제**는 특수한 목적을 가진 시스템에서 사용하는 방식.

  - 실시간 시스템의 개념 확장(2가지로 나눠진다).
    - Hard realtime system
    - Soft realtime system

## 용어 정리
- Multitasking
- Multiprogramming
- Time sharing
- Multiprocess  

- 구분
  - 위의 용어들은 컴퓨터에서 **여러 작업을 동시에 수행**하는 것을 의미한다.
  - Multiprogramming은 여러 프로그램이 메모리에 올라가 있음을 강조(메모리 측면을 강조).
  - Time Sharing은 CPU의 시간을 분할하여 나누어 쓴다는 의미를 강조(CPU 측면을 강조).

- 💡 Multiprocessor
  - 하나의 컴퓨터에 **CPU(processor)가 여러 개** 붙어 있음을 의미.
    - 위의 용어에서 말하는 것과 하드웨어적으로 다른 시스템(CPU가 1개 있는 범용적 운영체제).

## 운영체제의 예
- 유닉스(UNIX)
  - 대형 컴퓨터를 위해 만들어진 운영체제.
    - 멀티태스킹이 되는 여러 사용자를 위한 환경으로 만들어졌다.
  - 코드의 대부분을 C언어(유닉스 운영체제를 만들기 위해 만든 언어)로 작성.
    - C언어는 기계와 사람에게 모두 가까운 언어.  
  - 높은 이식성.
    - 특정 컴퓨터의 기계어에만 국한되어 있지 않다.
  - 최소한의 커널 구조.
  - 복잡한 시스템에 맞게 확장 용이.
  - 소스 코드 공개.
  - 프로그램 개발에 용이.
  - 다양한 버전.
    - System V, FreeBSD, SunOS, Solaris
    - Linux

- DOS(Disk Operating System)
  - 개인용 컴퓨터(PC)를 위해 만들어진 운영체제.
  - MS사에서 1981년 IBM-PC를 위해 개발.
  - 단일 사용자용 운영체제, 메모리 관리 능력의 한계(주 기억장치: 640KB).
- MS Windows
  - MS사의 다중 작업용 GUI 기반 운영체제.
  - Plug and Play, 네트워크 환경 강화.
  - DOS용 응용 프로그램과 호환성 제공.
  - 불안정성.
  - 풍부한 지원 소프트웨어.

- Handheld device를 위한 OS
  - PalmOS, Pocket PC(WinCE), Tiny OS
  
## 💡 운영체제 과목의 수강 태도
- OS 사용자 관점이 아니라 OS 개발자 관점에서 수강.
- 본인이 운영체제라고 생각하고, 본인이 할 일이 무엇인지 생각해보자.
 
## 출처
- [KOCW \| 운영체제(2014-1) \| 이화여대 \| 반효경](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
