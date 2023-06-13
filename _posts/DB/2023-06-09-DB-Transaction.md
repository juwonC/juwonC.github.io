---
title: "[DB]트랜잭션"
excerpt: "트랜잭션"

categories:
  - DB
tags:
  - [데이터베이스, 트랜잭션]

toc: true
toc_sticky: true

date: 2023-06-09
---

## 📚트랜잭션
### 📄트랜잭션의 개념
동시 데이터 접근 문제
동일 데이터에 다수의 사용자가 접근했을 때 일관성이 훼손되는 문제가 생길 수 있습니다. 이런 문제를 해결하기 위해 하나의 논리적인 작업과 이를 처리하는 데이터베이스 연산을 일치시키기 위한 트랜잭션이라는 개념이 도입되었습니다. 트랜잭션은 데이터베이스를 조작하기 위한 하나의 논리적 단위를 이루는 일련의 연산 집합입니다. 즉, 테이터베이스를 사용하여 처리하는 작업을 하나의 묶음으로 인식하여 묶음 단위로 실행되도록 정의한 개념입니다.

<br><br>

### 📄트랜잭션의 특징

다수의 연산으로 구성된 트랜잭션이 사용자에게 단일작업처럼 다뤄지도록 ACID 특징을 준수해야합니다.

* Atomicity(원자성): 하나의 트랜잭션에 포함된 모든 연산은 완전히 수행되거나 전혀 수행되지 않음
* Consistency(일관성): 특정 트랜잭션이 수행되기 전과 후에 데이터베이스가 일관된 상태를 유지
* Isolation(고립성): 특정 트랜잭션이 데이터베이스를 갱신하는 동안 다른 트랜잭션에 의해 방해받지 않음
* Durability(지속성): 완료된 트랜잭션의 결과는 어떠한 시스템의 장애에도 데이터베이스에 반영되어야 함

<br><br>

### 📄트랜잭션의 동작 방식

* 트랜잭션의 두 연산
  - Read(X): 데이터베이스에서 데이터 X를 읽고, 트랜잭션이 실행되는 메모리의 변수 X에 값을 저장하는 연산
  - Write(X): 트랜잭션이 실행되는 메모리에 변수 X의 값을 데이터베이스에 저장하는 연산

<br>

* 트랜잭션 실행의 연산
  - Commit: 트랜잭션 연산에 의해 갱신된 데이터 항목의 값을 데이터베이스에 반영시키고 지속성을 확보하는 연산
  - Rollback: 트랜잭션이 중된되기 이전까지 수행한 연산에 의해 모든 데이터 항목의 값을 무효화하여 일관성을 확보하는 연산

<br><br>

### 📄트랜잭션의 상태 변화

1. 동작: 트랜잭션이 시작을 준비 또는 실행 중인 상태
2. 부분커밋: 마지막 연산을 실행한 직후의 상태
3. 커밋: 모든 실행이 성공적으로 완료된 후의 상태
4. 실패: 실행이 정상적으로 진행될 수 없는 상태
5. 중단: 실행 실패로 롤백되어 트랜잭션이 시작되기 전으로 환원되고 트랜잭션이 종료된 상태

![TransactionStates](\assets\images\DB\TransactionStates.png)
<br>
[https://www.tutorialspoint.com/dbms/dbms_transaction.htm](https://www.tutorialspoint.com/dbms/dbms_transaction.htm)

<br><br><br>

## 📚트랜잭션의 동시성
DBMS는 다수의 사용자가 데이터베이스를 공용으로 사용하기 위한 목적으로 도입되었기 때문에 다수의 사용자로부터 여러 트랜잭션을 요청받습니다. 따라서 다수의 요청에 대한 응답 시간을 최소화하여 사용자의 만족도를 높여야합니다.

* 트랜잭션 동시 실행의 이점
  - 트랜잭션 처리율과 자원 이용률 향상
  - 트랜잭션의 대기 시간을 감소

트랜잭션 동시 실행에는 이점들이 있지만 다중 사용자 환경에서 트랜잭션의 동시 실행으로 데이터 갱신시, 일관성 훼손 문제가 발생할 수 있습니다. 따라서 다중 사용자 환경을 지원하는 데이터베이스 시스템에서 다수의 트랜잭션이 일관성을 유지하면서 성공적으로 실행될 수 있도록 지원하는 기능이 필요합니다.

* 동시성 제어: 다수의 트랜잭션이 성공적으로 동시에 실행되어도 일관성을 유지할 수 있도록 지원하는 기법

<br><br>

### 📄스케줄
* 스케줄: 다수의 트랜잭션에 포함된 연산의 실행 순서를 명시한 것

* 직렬 스케줄: 각 트랜잭션에 속한 모든 연산이 순차적으로 실행되는 스케줄

![SerialSchedule1](\assets\images\DB\SerialSchedule1.png)

![SerialSchedule2](\assets\images\DB\SerialSchedule2.png)
<br>
[https://www.javatpoint.com/dbms-schedule](https://www.javatpoint.com/dbms-schedule)

<br>

* 병렬 스케줄: 하나의 트랜잭션이 완료되기 전에 다른 트랜잭션이 실행되는 스케줄(병렬 스케줄의 순서로 연산을 수행할 경우 일관성의 훼손이 발생할 가능성이 있습니다.)

![ParallelSchedule1](\assets\images\DB\ParallelSchedule1.png)

![ParallelSchedule2](\assets\images\DB\ParallelSchedule2.png)
<br>
[https://www.javatpoint.com/dbms-schedule](https://www.javatpoint.com/dbms-schedule)

<br><br>

### 📄트랜잭션의 직렬화


* 직렬 가능 스케줄 정의

**직렬 가능 스케줄**은 복수개의 트랜잭션이 동시에 수행된 결과가 직렬 스케줄의 결과와 동일한 스케줄을 의미합니다. 쉽게 말해 트랜잭션 간 연산 순서를 교환하여 트랜잭션을 직렬 스케줄과 동등하게 변환이 가능한 스케줄을 말합니다.

* 연산 순서의 교환

  - Read, Read -> 두 연산의 순서는 상관없다.
  - Read, Write
  - Write, Read
  - Write, Write

사용된 Read와 Write 연산 교환 시 상황에 따라 실행 결과에 일관성이 훼손되는 현상(충돌)이 발생할 수 있습니다. 최소 하나의 연산이 Write 연산일 경우 서로 충돌합니다. 하지만 서로 다른 데이터에 접근할 경우 충돌하지 않습니다.

* 충돌 동등: 특정 스케줄의 연산 순서를 바꿔서 충돌이 일어나지 않게 스케줄을 변환하는 것

* 충돌 직렬성: 순서 교환이 가능한 연산을 교환하여 직렬 스케줄의 연산과 동등하게 변환이 가능한 스케줄은 충돌 직렬성을 가진다고 합니다.

<br><br><br>

## 📚트랜잭션의 회복
### 📄회복의 개념
원자성을 보장하기 위해 트랜잭션 실패 시 실행된 모든 연산을 실행 이전 상태로 복원하는 기법

회복 불가능한 스케줄: 처리 과정의 값을 읽어다가 커밋을 하면 회복 불가능한 스케줄이 됩니다. 커밋된 이후에 취소가 불가능하기 때문입니다.

<br>

### 📄회복 가능한 스케줄

T<sub>i</sub>와 T<sub>j</sub>에 대해 T<sub>i</sub>가 기록한 데이터를 T<sub>j</sub>가 읽을 때, T<sub>i</sub>의 커밋이 T<sub>j</sub> 보다 먼저 나타나는 스케줄입니다.

* 연쇄적 롤백 유발 가능: 롤백으로 인하여 연쇄적으로 다른 트랜잭션도 롤백되는 현상

<br>

### 📄비연쇄적 스케줄

연쇄적 롤백으로 발생할 수 있는 대량의 회복 연산을 방지하기 위해 연쇄적이지 않은 스케줄로 구성된 스케줄입니다. 모든 비연쇄적인 스케줄은 회복 가능합니다.

T<sub>i</sub>가 기록한 데이터를 읽을 때 T<sub>i</sub>의 커밋이 T<sub>j</sub>의 읽기 연산보다 먼저 나타나는 스케줄

<br><br>