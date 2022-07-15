---
title: 'Web'
date: 2022-07-14 00:00:00
featured_image: 
excerpt: Web에 대해
---

## 목차

- [DBMS(database management system)](#dbms-database-management-system-)
- [미들웨어(MiddleWare)](#미들웨어-middleware-)
- [WAS(Web Applicatoin Server)](#was-web-applicatoin-server-)
  * [WAS의 주요기능](#was의-주요기능)
  * [웹서버 vs WAS](#웹서버-vs-was)
  * [장애 극복기능](#장애-극복기능)
- [Scope](#scope)



## DBMS(database management system)

다수의 사용자들이 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어를 말합니다. [ex)MySQL, Oracle, MariaDB...]

---

## 미들웨어(MiddleWare)

비즈니스 로직을 클라이언트와 DBMS사이의 미들웨어 서버에서 동작하도록 함으로써 클라이언트는 입력과 출력만 담당하도록 합니다. 이로써 프로그램 로직이 변경이 되더라도 클라이언트 수정없이 중앙의 미들웨어만 변경하면 되는 장점을 가지게 됩니다.

---

## WAS(Web Applicatoin Server)

WAS는 일종의 미들웨어로 웹 클라이언트의 요청 중 보통 웹 에플리케이션 동작하도록 지원하는 목적을 가집니다.

### WAS의 주요기능

1. 프로그램 실행 환경과 데이터베이스 접속 기능을 제공합니다.
2. 여러 개의 트랜젝션을 관리합니다.
3. 업무를 처리하는 비즈니스 로직을 수행합니다.

### 웹서버 vs WAS

* WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있습니다.
* 현재는 WAS가 가지고 있는 웹 서버도 정적인 컨텐츠를 처리하는데 있어서 성능상 큰 차이가 없습니다.
* 규모가 커질수록 웹 서버와 WAS를 분리한다. 그 목적은 장애 극복기능(failover)인 경우가 많습니다.

### 장애 극복기능

웹 서버가 WAS 앞단에 배치되어 있을때, WAS에 문제가 발생해 WAS를 재시작해야 하는 경우 앞단의 웹 서버에서 먼저 해당 WAS를 이용하지 못하도록 하고 WAS를 재시작한다면 해당 웹 애플리케이션을 사용하는 사람은 WAS의 문제가 발생하였는지를 모르고 이용할 수 있습니다. 이러한 처리를 장애 극복 기능이라고 하는데 이는 대용량 웹 애플리케이션에는 무중단으로 운영하기 위해서 상당히 중요한 기능입니다.

---

## Scope

![](/images/web/scope.jpg)

* Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지된다. 모든 클라이언트가 공통으로 사용해야할 값들이 있을 때 사용합니다.
* Session : 세션 객체가 생성돼서 소멸될 떄 까지 유지된다. 웹 브라우저 별로 변수가 관리되는 경우 사용합니다.
* Request : 하나의 요청이 들어와서 응답이 나갈 떄까지 유지된다.. http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용합니다.
* Page : 페이지 내에서 지역변수처럼 사용. jsp에서 pageScope에 값을 저장 한 후 해당 값을 EL표기법등에서 사용할 때 사용됩니다.











출처: https://www.boostcourse.org/web326/lecture
