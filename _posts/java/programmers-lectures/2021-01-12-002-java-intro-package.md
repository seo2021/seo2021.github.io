---
title: "[프로그래머스 자바 입문] 접근 제한자(Access Modifier)"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - 접근제한자
  - 자바입문
---

## 접근 제한자란?
- 클래스 내에서 멤버의 접근을 제한하는 역할을 한다.
- 필드, 메소드, 클래스 앞에 붙여서 사용.

## 접근 제한자의 종류
- public
  - **어떤 클래스**든 접근할 수 있다.
  - 모든 접근을 허용(전체 공개).
  - 가장 넓은 의미.
- protected
  - **자기 자신(같은 클래스), 같은 패키지, 서로 다른 패키지라도 상속받은 자식 클래스**에서는 접근할 수 있다.
- private
  - **자기 자신(같은 클래스)만** 접근할 수 있다.
- default
  - 접근 제한자 설정하지 않을 경우
  - **자기 자신과 같은 패키지**에서만 접근할 수 있다.  
- `public > protected > default > private`

  ```java
  public class AccessObj {
    public int p = 3;
    protected int p2 = 4;
    private int i = 1;
    int k = 2; // default 접근 제한자
  }
  ```
  
- ex 1) AccessObj를 다른 클래스에서 사용
  - AccessObj의 **필드 i의 접근 제한자는 private**이므로, 다른 클래스인 AccessObjExam에서 접근할 수 없다.
  
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
  
- ex 2) AccessObj를 다른 패키지에서 사용
  - 패키지가 달라졌기 때문에 **public 접근 제한자**만 접근 가능.
  
  ```java
  public class AccessObjExam {
 
    public static void main(String[] args) {
    
      AccessObj po = new AccessObj();
      
      System.out.println(po.i); // 컴파일 오류 발생(private)
      System.out.println(po.k); // 컴파일 오류 발생(default)
      System.out.println(po.p);
      System.out.println(po.p2); // 컴파일 오류 발생(protected)
    }
  }
  ```
  
- ex 3) AccessObj를 상속받은 AccessObjExam을 사용(서로 다른 패키지)
  - 패키지는 다르지만, 상속관계에 있으므로 protected 접근 제한자로 지정된 필드 p2에 접근할 수 있다.

  ```java
  public class AccessObjExam extends AccessObj {
    
    public static void main(String[] args) {
    
      AccessObjExam obj = new AccessObjExam();
      
      System.out.println(po.i); // 컴파일 오류 발생(private)
      System.out.println(po.k); // 컴파일 오류 발생(default)
      System.out.println(po.p);
      System.out.println(po.p2);
    }
  }
  ```

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 접근제한자](https://programmers.co.kr/learn/courses/5/lessons/187)
