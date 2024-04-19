---
title: Spring (2) - Controller Repository Service
author: jay
date: 2024-04-19
categories:
  - Spring
  - Spring_Start
tags:
  - Java
  - Spring
source: https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8#
---
## **Controller Repository Service**


<br />
 
---

<br/>

강의에서 Member, MemberRepository, MemberService, MemberController로 나누어서 회원 관리 예제를 진행했습니다. `Controller Service Repository` 패턴은 스프링에 어노테이션으로 있을 정도로 정형화된 패턴이고, 3개의 주요 구성 요소를 통해서 관심사를 분리하는 방식입니다.

- `Controller`: 사용자의 요청을 받아 적절한 서비스를 호출하고 응답을 반환합니다.
- `Service`: 비즈니스 로직을 담당하며, 컨트롤러와 리포지토리 사이의 중간 역할을 합니다
- `Repository`: 데이터베이스와 상호작용을 담당하고, 서비스 계층에 데이터를 제공합니다.

<br/>
### **Controller**

클라이언트의 요청이 들어오면 Controller가 그 요청을 받습니다. 요청에 따라 어떤 처리를 할지 결정하게 되고, 서비스에 관련 메소드를 호출합니다. 이후 서비스에서 반환된 데이터를 적절한 형태로 클라이언트에 보냅니다. 

ex) 회원가입 요청이 들어오면 서비스에 회원가입 메소드를 호출하고 기다렸다가 처리가되면 응답을 보내주는 역할을 합니다.

<br/>
### **Service**

컨트롤러와 리포지토리 사이에서 비즈니스 로직을 수행합니다. 컨트롤러에서 받은 요청을 처리하기 위해 필요한 데이터를 리포지토리에 요청합니다. 데이터를 가공하고 변환하는 등의 작업을 수행합니다. 

ex) 회원가입 요청이 들어오면 중복id처리 등을 하고, 리포지토리에 데이터 저장 요청을 보냅니다.


<br/>
### **Repository**

리포지토리는 데이터베이스와의 상호작용을 담당합니다. 데이터 조회, 생성, 수정, 삭제 등의 CRUD 작업을 수행합니다. 

ex) 서비스에서 회원정보 저장 요청이 들어오면 데이터베이스에 저장합니다. 

<br/>
### **의존관계**
<img align="center" src="https://ifh.cc/g/cgxcC1.png">
Controller가 Service에 의존하고 Service가 Repository에 의존하는 형태로 주로 이루어집니다.


<br/>
### **장점**

- 관심사를 분리하여 각각 고유한 책임, 역할을 갖게되어 코드의 가독성과 유지보수성의 향상
- 새로운 기능 추가시 관련된 계층만 수정하면 되므로 확장성이 높음
- 각 계층의 책임이 명확해서 단위 테스트 용이