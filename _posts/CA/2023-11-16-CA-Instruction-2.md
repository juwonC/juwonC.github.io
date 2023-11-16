---
title: "[CA]컴퓨터 명령어(2)"
excerpt: "주소지정방식"

categories:
  - CA
tags:
  - [컴퓨터 구조, 컴퓨터 명령어, 주소지정방식]

toc: true
toc_sticky: true

date: 2023-11-16
---

## 📚주소지정방식
* 명령어 주소지정방식
  - 프로그램 수행 시 오퍼랜드를 지정하는 방식
  - 명령어의 주소 필드를 변경하거나 해석하는 규칙을 지정하는 형식
  - 주소지정방식을 사용하면 명령어의 수를 줄일 수 있는 효과적인 프로그래밍 가능

* 유효주소: 주조지정방식의 각규칙을 적용하여 만들어진 오퍼랜드의 실제 주소

* 주소지정방식 필드를 가진 명령어 형식
  - 연산코드필드: 수행할 연산 종류 지정
  - 주소지정방식 필드: 연산에 필요한 오퍼랜드 주소를 알아내는데 사용
  - 주소 혹은 오퍼랜드 필드: 기억장치주소 혹은 레지스터를 나타냄

![AddressingMode](\assets\images\CA\AddressingMode.png)

<br><br>

## 📚주소지정방식의 종류
### 📄의미주소지정방식
* 명령어 형식에서 주소 필드를 필요로 하지 않는 방식
* 연산보드 필드에 지정된 묵시적 의미의 오퍼랜드를 지정

예 ADD; TOS <- TOS + TOS<sub>-1</sub>

<br>

### 📄즉치 주소지정방식
* 명령어 자체 내에 오퍼랜드를 지정하고 있는 방식
* 오퍼랜드 필드의 내용이 실제 사용될 데이터
* 레지스터, 변수 초기화에 유용

예 LDI 100, R1; R1 <- 100

<br>

### 📄직접 주소지정방식
* 명령어의 주소필드에 직접 오퍼랜드의 주소를 저장
* 기억장치로 접근이 한번에 이루어짐

예 LDA ADRS; AC <- M[ADRS]

<br>

### 📄간접 주소지정방식
* 명령어의 주소필드에 유효주소가 저장되어 있는 기억장치 주소를 기억시키는 방식

예 LDA [ADRS]; AC <-M[M[ADRS]]

<br>

### 📄레지스터 주소지정방식
* 오퍼랜드 필드에 레지스터가 기억되는 방식
* 레지스터에 오퍼랜드가 들어있음(유효주소 없음)

예 LDA R1; AC <- R1

<br>

### 📄레지스터 간접 주소지정방식
* 레지스터가 실제 오퍼랜드가 저장된 기억장치의 주소 값을 가지고 있는 방식

예 LDA (R1); AC <- M[R1]

<br>

### 📄상대주소주소지정방식
* 유효주소를 계산하기 위해 처리장치 내의 특정 레지스터의 내용에 명령어 주소필드 값을 더하는 방식
* 특정 레지스터로 프로그램카운터(PC)가 주로 사용
* 명령어 주소 부분 내용 + PC 내용 = 유효주소

예 LDA $ADRS; AC <- M[ADRS+PC]

<br>

### 📄인덱스된 주소지정방식
* 인덱스 레지스터 내용을 명령어 주소 부분에 더해서 유효주소를 얻는 방식
* 명령어 주소 부분 내용 + 인덱스 레지스터 내용 = 유효주소

예 LDA ADRS(R1); AC <- M[ADRS+R1]

<br>

## 📚주소지정방식 요약

![AddressingModeSummary](\assets\images\CA\AddressingModeSummary.png)

![AddressingModeSummary2](\assets\images\CA\AddressingModeSummary2.png)

<br><br>

## 📚명령어 종류
### 📄데이터 전송 명령어
* 한 장소에서 다른 장소로 데이터를 전송하는 명령어
* 레지스터와 레지스터 사이, 레지스터와 기억장치 사이, 기억장치와 기억장치 사이에 데이터를 이동하는 기능
* 입출력 명령어가 포함됨

![DataTransferInstruction](\assets\images\CA\DataTransferInstruction.png)

<br>

### 📄데이터 처리 명령어
* 데이터에 대한 연산을 실행, 컴퓨터에 계산능력 제공

1. 산술 명령어
<br>
![OperatorInstruction](\assets\images\CA\OperatorInstruction.png)
<br>
2. 논리와 비트 처리 명령어: 레지스터나 기억장치에 저장된 단어에 대한 2진 연산
<br>
![BitInstruction](\assets\images\CA\BitInstruction.png)
<br>
3. 시프트 명령어: 오퍼랜드 비트를 왼쪽이나 오른쪽으로 이동시키는 명령어
<br>
![ShiftInstruction](\assets\images\CA\ShiftInstruction.png)

<br>

### 📄프로그램 제어 명령어
* 프로그램 수행 흐름을 제어
* 다른 프로그램의 세그먼트로 분기

![FlowControlInstruction](\assets\images\CA\FlowControlInstruction.png)

<br><br>