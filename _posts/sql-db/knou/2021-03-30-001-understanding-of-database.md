---
title: "[2021-1 데이터베이스시스템] 1강 데이터베이스의 이해"
layout: single
related: true
categories:
  - SQL-DB
  - KNOU-DATABASE-SYSTEMS
tags:
  - 방송대
---

## 데이터베이스 시스템의 개요
- 데이터베이스는 간단히 말해 **대량의 데이터를 저장 및 관리**하고 **필요한 데이터를 신속히 검색**할 수 있도록 보조하는 장치라고 할 수 있다.

    <p align="center"><img src="/assets/images/sql-db/001-definition-of-database.png"></p>
  
- **데이터베이스 관리 시스템(DBMS: Database Management System)**은 한 조직의 연관된 데이터 집합을 다수의 사용자가 공용으로 사용하기 위해 통합 저장하는 소프트웨어 패키지이다.
- DBMS와 함께 사용자에게 서비스 형태로 제공되는 애플리케이션이 포함된 일체의 시스템을 **데이터베이스 시스템(Database System)**이라고 한다.

## 파일 처리 시스템 : 전통적 데이터 관리 방식
- 파일 처리 시스템은 운영체제에 의해 지원되며, **파일을 사용하여 특정 업무에 해당하는 데이터를 관리**하는 방식이다.
  - 업무별 애플리케이션이 개별 데이터를 데이터 파일에 저장 및 관리. 

    ![파일 처리 시스템](/assets/images/sql-db/001-file-processing-system.png)

- DBMS가 사용되기 이전, 대다수의 시스템은 **파일 처리 시스템(File Processing System)** 방식을 기반으로 운용되었다.
- 하지만, 파일 처리 시스템은 데이터 관리에 여러 **문제점**을 가지고 있다.

  1. 데이터 종속(Data Dependency)의 문제
    - 저장된 데이터가 **특정 하드웨어**에서 또는 **특정 사용자 및 소프트웨어**에서만 사용될 수 있도록 제한되는 문제.
    - **물리적 데이터 종속**과 **논리적 데이터 종속**으로 구분할 수 있다.
    - DBMS는 데이터를 프로그램과 완전히 독립시킴으로써, 종속으로 인한 문제를 근본적으로 배제시킨다.
    
         ![데이터 종속](/assets/images/sql-db/001-data-dependency.png)
        
  2. 데이터 중복(Data Redundancy)의 문제
    - 하나의 사항에 대한 데이터가 **여러 파일에 중복적으로 저장**될 수 있다.
    - 동일한 사항에 대한 중복 데이터는 **일관성, 보안성, 경제성** 측면에서 문제를 발생시킨다.
      - 일관성(consistency): 하나의 사실을 나타내는 여러 개의 데이터가 논리적으로 같은 값을 유지하는 것.
      - 보안성(security): 논리적으로 동등한 내용의 데이터에 대해 똑같은 수준의 보안을 유지하는 것.
      - 경제성(economy): 최소한의 저장공간과 낮은 시스템 갱신 비용.
      
        ![데이터 중복](/assets/images/sql-db/001-data-redundancy.png)
        
  3. 데이터 무결성(Data Integrity) 훼손의 문제

 
## 출처
- [정재화 \| 데이터베이스 시스템 \| 한국방송통신대학교출판문화원(2020) \| p.2-33](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920035500&condLscValue=001&condYr=&condSmst=)
- [정재화 \| 데이터베이스시스템 \| 1강. 데이터베이스의 이해 \| 한국방송통신대학교 \| 2021-1 강의](https://ucampus.knou.ac.kr/ekp/user/course/initUCRCourse.sdo?pageIndex=1&recordCountPerPage=4&sbjtId=KNOU1411001&cntsId=KNOU1411&atlcNo=6889724&tespNo=&lectPldcTocNo=&examApexNo=&burSbjtCd=&tabNo=01&curSbjtId=&curLectPldcTocNo=&systemDiv=H&searchCntsCateNo=34&searchShgr=&searchSeme=&epTicket=LOG)
