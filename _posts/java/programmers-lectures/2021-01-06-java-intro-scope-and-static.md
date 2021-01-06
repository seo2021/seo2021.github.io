---
title: \[프로그래머스 \| 자바 입문\] 변수의 Scope와 Static
layout: single
related: true
categories:
  - JAVA
  - PROGRAMMERS LECTURES
tags:
  - java
  - 변수
  - scope
  - static
---

## 변수의 scope
- 변수가 선언된 블럭이 그 변수의 사용범위이다.
```java
public class VariableScopeExam {

  int globalScope = 10; // 인스턴스 변수
  
  public void
}
```

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

void main(){
  int i;
  int n = MAX_SIZE;
  int list[n] = {9, 6, 7, 3, 5};

  // 선택 정렬 수행
  selection_sort(list, n);

  // 정렬 결과 출력
  for(i=0; i<n; i++){
    printf("%d\n", list[i]);
  }
}
~~~

## 정리
- 단항, 이항, 삼항 연산자 순으로 우선순위를 갖는다.
- 산술, 비교, 논리, 대입 연산자 순으로 우선순위를 갖는다.
- 단항과 대입 연산자를 제외한 모든 연산 방향은 왼쪽에서 오른쪽이다.
 
## 출처
- [프로그래머스 \| 프로그래밍 강의 \| 자바 입문 \| 연산자우선순위](https://programmers.co.kr/learn/courses/5/lessons/116)
- [Kephi Javatory \| 4. Java 자바 - 연산자 종류, 연산자 우선순위](https://kephilab.tistory.com/28)
