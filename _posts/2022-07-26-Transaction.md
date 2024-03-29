---
title: 'Transaction'
date: 2022-07-26 00:00:00
featured_image: 
excerpt: Transaction에 대해
---

## 트랜잭션

* 여러 개의 DML 명령문을 하나의 논리적인 작업 단위로 묶어서 관리하는것
* All 또는 Nothing방식으로 작업을 처리함으로써 작업의 일관성을 유지함
* 웹 애플리케이션에선 Service 클래스의 각 메서드가 애플리케이션의 단위 기능을 수행

## 스프링의 여러 가지 트랜잭션 속성들

|속성|기능|
|-----|------|
|propagation|트랜잭션 전파 규칙 설정|
|isolation|트랜잭션 격리 레벨 설정|
|realOnly|읽기 전용 여부 설정|
|rollbackFor|트랜잭션을 롤백할 예외 타입 설정|
|norollbackFor|트랜잭션을 롤백하지 않을 예외 타입 설정|
|timeout|트랜잭션 타임아웃 시간 설정|

### propagation 속성이 가지는 값

* REQUIRED
  * 트랜잭션 필요, 진행중인 트랜잭션이 있는 경우 해당 트랜잭션 사용
  * 트랜잭션이 없으면  새로운 트랜잭션 생성, 디폴트 값
* MANDATORY
  * 트랜잭션 필요
  * 진행 중인 트랜잭션이 없는 경우 예외 발생
* REQUIRED_NEW
  * 항상 새로운 트랜잭션 생성
  * 진행중인 트랜잭션이 있는 경우 기존 트랜잭션을 일시 중지시킨 후 새로운 트랜잭션 시작
  * 새로 시작된 트랜잭션이 있는 경우 해당 트랜잭션 사용
* SUPPORTS
  * 트랜잭션 필요 없음
  * 진행 중인 트랜잭션이 잇는 경우 해당 트랜잭션 사용
* NOT_SUPPORTED
  * 트랜잭션 필요 없음
  * 진행 중인 트랜잭션이 있는 경우 기존 트랜잭션을 일시 중지시킨 후 메서드 실행
  * 메서드 실행이 종료되면 기존 트랜잭션 계속 진행
* NEVER
  * 트랜잭션 필요 없음
  * 진행 중인 트랜잭션이 있는 경우 예외 발생
* NESTED
  * 트랜잭션 필요
  * 진행 중인 트랜잭션이 있는 경우 기존 트랜잭션에 중첩된 트랜잭션에서 메서드 실행
  * 트랜잭션이 없으면 새로운 트랜잭션 생성

###  isolation 속성이 가지는 값

|속성|기능|
|------|------|
|DEFAULT|데이터베이스에서 제공하는 기본 설정 사용|
|READ_UNCOMMITED|다른 트랜잭션에서 커밋하지 않은 데이터 읽기 가능|
|READ_COMMITED|커밋한 데이터만 읽기 가능|
|REPEATABLE_READ|현재 트랜잭션에서 데이터를 수정하지 않았다면 처음 읽어온 데이터와 두 번째 읽어온 데이터가 동일|
|SERIALIZABLE|같은 데이터에 대해 한 개의 트랜잭션만 수행 가능|
  
  
