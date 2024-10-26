---
title: "[ICTicket] - Redis 분산 락을 걸때 발생한 Transaction 문제"
author: jay
date: 2024-10-12
categories:
  - Projcet
tags:
  - Spring
  - ICTicket
  - Redis
  - 분산락
  - 트러블슈팅
  - Transaction
source:
---
## 문제 상황

---

좌석 선택 기능에 분산 락을 적용한 후 테스트를 진행했는데, 좌석 상태가 DB에 정상적으로 업데이트되지 않는 문제가 발생했다. 원인을 확인해본 결과, 트랜잭션이 제대로 적용되지 않은 것을 발견했다.

## 왜 트랜잭션이 안걸렸을까?

---

- 아래 그림의 outerMethod는 분산 락을 획득하고, 해제하는 역할을 하고, innerMethod는 좌석 선택 로직이다.
- SeatService 안에 outerMethod는 @Transactional이 없고 innerMethod는 @Transactional이 있다. 이때, outerMethod를 통해서 innerMethod를 실행하게 되면 어떻게 될까?
- innerMethod가 실행될 때 @Transactional이 적용되어서 트랜잭션이 시작되고, innerMethod가 종료될 때 트랜잭션이 커밋될 것으로 예상했지만, 그렇지 않았다.


<img align="center" src="https://ifh.cc/g/x7B3zr.png">

- 그 이유는 @Transactional을 적용하면 프록시 객체가 요청을 먼저 받아서 트랜잭션을 처리하고, 실제 객체를 호출하기 때문이다. 스프링에서 트랜잭션을 적용하려면 항상 프록시를 통해서 대상 객체를 호출해야 한다.

- 아래 그림처럼 API가 호출되었을 때, Proxy를 거쳐서 transaction begin이 실행되고, 타깃 객체의 메서드가 실행되고 다시 transaction commit이 실행되면서 트랜잭션이 끝난다.

<img align="center" src="https://ifh.cc/g/9ahat1.png">

- 하지만 아래 그림처럼 @Transactional이 없는 outerMethod를 실행하면 Proxy를 통하지 않고, 바로 타깃 객체의 메서드를 실행해버리기 때문에, innerMethod에 @Transactional이 있더라도 트랜잭션이 적용되지 않는 것이다.


<img align="center" src="https://ifh.cc/g/rdfCLo.png">

## ❌ 해결방법 1 - .save() (실패)

---

- 첫 번째 적용해본 방법은 가장 간단하게 .save()를 명시적으로 작성해주어 세이브하는 방법을 썼다. 테스트 해봤을 때 업데이트가 적용되어서 해결된 것으로 생각했었지만, 사실상 트랜잭션을 사용하지 않는 방법이다 보니 여러개의 좌석을 예매할 때 문제가 발생했다.
- 아래 그림처럼 여러개의 좌석 중에 3번 하나만 좌석 예매를 실패하더라도 전부 실패하게 되어야 하는데, 트랜잭션이 적용되지 않아서 roll back이 되지 않기 때문에 DB에는 해당 유저가 1,2번 좌석을 점유해버린 것으로 나타나게 되었다.
<img align="center" src="https://ifh.cc/g/wwkaVl.png">


## 🟡 해결방법 2 - 클래스 분리 (실패)

---

- 다음으로 시도해본 방법은 innerMethod와 outerMethod를 다른 서비스 클래스로 분리하는 방법이었다.
- 아래 코드처럼 SeatService에 innerMethod, LockHandler에 outerMethod를 두어 분리하게 되면, outerMethod에서 innerMethod를 호출할때, seatService를 호출하면서 Proxy를 통하기 때문에 Transaction이 적용된다.
- Transaction, 동시성 제어 모두 정상적으로 작동했지만, controller에 LockHandler 객체를 하나 더 불러와야 하는 등의 코드의 일관성, 유지보수성을 해치기 때문에 다른 방법을 찾기로 했다.

<img align="center" src="https://ifh.cc/g/DF7WkV.jpg">

## 🟢 해결방법 3 - AOP, 클래스 분리 (성공)

---

- 마지막 해결방법으로 AOP로 락을 관리하고, outerMethod joinpoint를 전달하여 innerMethod를 호출하도록 코드를 작성했다.
- 좌석 선택 API가 실행되면 AOP가 실행되고, Lock을 획득하게 된다. 이제 Transactional을 적용한 outerMethod가 실행되면서 프록시를 통해 Transaction begin이 실행된다. innerMethod 로직을 수행하고 다시 Transaction commit 되면서 Transaction이 끝나고, 락 해제 해주면서 동시성제어까지 잘 작동하게 되었다.

<img align="center" src="https://ifh.cc/g/g7qMhq.png">
