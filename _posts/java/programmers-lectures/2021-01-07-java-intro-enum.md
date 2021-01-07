---
title: \[프로그래머스 \| 자바 입문\] 열거형(Enum)
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 열거형
  - Enum
  - 상수
---

## 자바는 열거형을 이용하여 변수를 선언함으로써, 이를 변수 타입으로 사용할 수 있다.
- 열거형은 JDK5에서 추가되었다.
- JDK5 이전에는 상수를 열거형 대신 사용

## 열거형 대신 상수를 사용하는 방법
  ```java
  public class EnumExam {
    
    public static final String MALE = "MALE";
    public static final String FEMALE = "FEMALE";
    
    public static void main(String[] args) {
      
      String gender1;
      
      gender1 = EnumExam.MALE;
      gender1 = EnumExam.FEMALE;
    }
  }
  ```
- 상수를 사용했을 때 문제점
  - String으로 선언된 gender1이 MALE, FEMALE 둘 중 한 가지 값만을 가질 수 있을 때, gender1의 type이 String이기 때문에 'gender1 = "소년";' 이렇게 수행되어도 전혀 문제가 되지 않는다.
  - 따라서 실행할 때, 원했던 값인 MALE, FEMALE이 아닌 다른 값이 들어오게 되므로 문제를 발생시킬 수 있다.

## 열거형의 사용
- 위와 같은 문제를 발생시키지 않기 위해 열거형을 사용
- 열거형의 정의 방법
```java
enum Gender {
  MALE, FEMALE;
}
```
- 열거형 사용 방법
```java
Gender gender2;

// Gender 타입의 변수에는 MALE이나 FEMALE만 대입 가능. 다른 값은 저장할 수 없다.
gender2 = Gender.MALE;
gender2 = Gender.FEMALE;
```

## 선택 정렬(selection sort) c언어 코드
~~~javascript
# include <stdio.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
# define MAX_SIZE 5

// 선택 정렬
void selection_sort(int list[], int n){
  int i, j, least, temp;

  // 마지막 숫자는 자동으로 정렬되기 때문에 (숫자 개수-1) 만큼 반복한다.
  for(i=0; i<n-1; i++){
    least = i;

    // 최솟값을 탐색한다.
    for(j=i+1; j<n; j++){
      if(list[j]<list[least])
        least = j;
    }

    // 최솟값이 자기 자신이면 자료 이동을 하지 않는다.
    if(i != least){
        SWAP(list[i], list[least], temp);
    }
  }
}

## 특정 값만 가져야 한다면 열거형을 사용하는 것이 좋다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 열거형(enum)](https://programmers.co.kr/learn/courses/5/lessons/423)
