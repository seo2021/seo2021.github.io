---
title: "[프로그래머스 자바 중급] Annotation"
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS-LECTURES
tags:
  - annotation
  - 자바중급
---

## Annotation이란?
- 자바 소스 코드에 추가하여 사용할 수 있는 **메타데이터**의 일종.
- **클래스**나 **메소드** 위에 붙으며, **@(at)** 기호로 시작한다.
- **JDK 1.5** 버전 이상에서 사용 가능하다.

- **클래스 파일에 임베디드**되어 **컴파일러에 의해 생성**된 후 **자바 가상머신에 포함되어 작동**한다.
  - 클래스가 컴파일되거나 실행될 때 Annotation 유무나 Annotation에 설정된 값을 통하여 클래스가 다르게 실행되도록 할 수 있다.

## Custom Annotation 작성
- Annotation은 자바가 기본으로 제공해주는 것도 있고, **사용자가 직접 작성**할 수도 있다.

- **Custom Annotation 사용 방법**
  1. Annotation 정의
  2. Annotation을 클래스에서 사용(타겟에 적용)
  3. Annotation을 이용하여 실행

- **Annotation 정의**
  - 패키지 익스플로러에서 [new - Annotation]을 이용하여 `Count100` Annotation 생성.
  - `Count100` Annotation을 JVM 실행 시에 감지할 수 있도록 하려면 `@Retention(RetentionPolicy.RUNTIME)`을 붙여줘야 한다.
  
  ```java
  import java.lang.annotation.Retention;
  import java.lang.annotation.RetentionPolicy;

  @Retention(RetentionPolicy.RUNTIME)
  public @interface Count100 { }
  ```
  
- **Annotation을 클래스에서 사용**
  - `hello()` 메소드를 가지는 `MyHello` 클래스 작성.
  - `hello()` 메소드 위에 `@Count100` Annotation을 붙인다.
  
  ```java
  public class MyHello {
    @Count100
    public void hello() {
      System.out.println("hello");
    }
  }
  ```
  
- **Annotation을 이용하여 실행**
  - `MyHello` 클래스를 사용하는 `MyHelloExam` 클래스 작성.
  - `MyHello`의 `hello()` 메소드가 `@Count100` Annotation이 설정되어 있을 경우, `hello()` 메소드를 100번 호출하도록 작성.

  ```java
  import java.lang.reflect.Method;

  public class MyHelloExam {

    public static void main(String[] args) {
      // MyHello 인스턴스 생성
      MyHello hello = new MyHello();

      try {
        // MyHello 클래스의 메소드 정보 가져옴
        Method method = hello.getClass().getDeclaredMethod("hello");

        // 메소드에 `@Count100` 애노테이션이 적용되어 있다면 
        if(method.isAnnotationPresent(Count100.class)) {
          // 메소드 100번 실행
          for(int i = 0; i < 100; i++) {
            hello.hello();
          }
        }
        else {
          hello.hello();
        }

      } catch (Exception e) {
        e.printStackTrace();
      }

    }//--main()

  }//--class
  ```
  
- 💡 Custom Annotation을 사용하는 경우는 많지 않다.

## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 중급 \| 어노테이션](https://programmers.co.kr/learn/courses/9/lessons/269)
- [위키백과 \| 자바 애너테이션](https://ko.wikipedia.org/wiki/자바_애너테이션)
