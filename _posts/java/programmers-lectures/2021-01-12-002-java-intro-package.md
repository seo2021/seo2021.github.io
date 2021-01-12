---
title: \[프로그래머스 \| 자바 입문\] 접근 제한자(Access Modifier)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - 접근제한자
  - AccessModifier
---

## 접근 제한자란?
- 클래스 내에서 멤버의 접근을 제한하는 역할을 한다.

## 접근 제한자의 종류
- public
  - <u>어떤 클래스</u>든 접근할 수 있다.
- protected
  - <u>자기 자신(같은 클래스), 같은 패키지, 서로 다른 패키지이지만 상속받은 자식 클래스</u>에서는 접근할 수 있다.
- private
  - <u>자기 자신(같은 클래스)만</u> 접근할 수 있다.
- default
  - 접근 제한자 설정하지 않을 경우
  - <u>자기 자신(같은 클래스)과 같은 패키지</u>에서만 접근할 수 있다.

  ```java
  public class AccessObj {
    public int p = 3;
    protected int p2 = 4;
    private int i = 1;
    int k = 2; // default 접근 제한자
  }
  ```
  
- ex 1) AccessObj를 사용하는 AccessObjExam
  
  ```java
  public class AccessObjExam {
 
    public static void main(String[] args) {
    
      AccessObj po = new AccessObj();
      
      System.out.println(po.i); // 컴파일 오류 발생
      System.out.println(po.k);
      System.out.println(po.p);
      System.out.println(po.p2);
    }
  }
  ```
  - AccessObj의 **필드 i의 접근 제한자는 private**이므로, <u>다른 클래스인 AccessObjExam에서 접근할 수 없다.</u>


## 💡 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [Kephi Javatory \| 4. Java 자바 - 연산자 종류, 연산자 우선순위](https://kephilab.tistory.com/28)



