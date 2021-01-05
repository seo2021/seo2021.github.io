---
title: \[프로그래머스 \| 자바 입문\]연산자 우선순위(Operator Precedence)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 프로그래머스
  - 강의정리
  - java
  - 연산자
---

## 연산자 우선순위
\* 위에서 아래로 내려갈수록 연산자 우선순위가 낮아진다.
- 최우선 연산자&nbsp;&nbsp;&nbsp; . [] ()
- 단항 연산자&nbsp;&nbsp;&nbsp; 증감(++, --), 부호(+, -), 비트(~), 논리(!)
  - 부정, bit 반전 > 부호 > 증감
- 산술 연산자&nbsp;&nbsp;&nbsp; * / % + -
  - \* / % > + -
- 시프트 연산자&nbsp;&nbsp;&nbsp; shift(>>, <<, >>>)
- 비교 연산자&nbsp;&nbsp;&nbsp; > < >= <= == !=
- 비트 연산자&nbsp;&nbsp;&nbsp; & | ^
- 논리 연산자&nbsp;&nbsp;&nbsp; && ||
  - && > ||
- 삼항연산자&nbsp;&nbsp;&nbsp; 조건식 ? :
- 대입 연산자&nbsp;&nbsp;&nbsp; = *= /= %= += -=

| 연산자 종류 | 연산자 | 비고 |
|:------:|:------|:------|
| 최우선 연산자 | . [] () |  |
| 과자 | 900원 | 20개 |
 
## 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [Kephi Javatory \| 4. Java 자바 - 연산자 종류, 연산자 우선순위](https://kephilab.tistory.com/28)