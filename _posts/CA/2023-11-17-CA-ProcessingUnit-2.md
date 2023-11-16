---
title: "[CA]처리장치(2)"
excerpt: "처지장치"

categories:
  - CA
tags:
  - [컴퓨터 구조, 처리장치]

toc: true
toc_sticky: true

date: 2023-11-17
---

## 📚처리장치 구성요소
### 📄구성요소
* 여러 개의 레지스터(레지스터 세트)
* 산술논리연산장치(ALU)
* 내부 버스

<br>

### 📄내부 구성과 동작원리

![ProcessingUnit](\assets\images\CA\ProcessingUnit.png)

* 처리장치 동작: 마이크로 연산의 수행과정을 통해 처리장치가 동작

* 마이크로 연산의 수행과정(처리장치의 구성요소들의 선택신호에 의해 제어됨)
  1. 지정된 출발 레지스터의 내용이 ALU의 입력으로 전달
  2. ALU에서 그 연산을 실행
  3. 그 결과가 도착 레지스터에 전송

* 마이크로 연산의 예(R0 <- R1 + R2)
  1. 선택신호 A는 R1의 내용을 버스 A로 적재
  2. 선택신호 B는 R2의 내용을 버스 B로 적재
  3. 선택신호 F는 ALU에서 산술연산 A + B를 수행
  4. 선택신호 H는 시프터에서 시프트 연산을 수행
  5. 선택신호 D는 연산결과를 R0으로 적재

### 📄내부버스
레지스터들 간의 데이터 전송을 위한 공통선로의 집합

![InternalBus](\assets\images\CA\InternalBus.png)

<br>

* 내부버스를 구성하는 방법

멀티플렉서(출발 레지스터 선택)와 디코더(도착 레지스터를 선택)를 이용

![BusSystem](\assets\images\CA\BusSystem.png)

<br>

* 내부버스 구성 및 동작

마이크로 연산: R1 <- R0 (R0, R1이 4비트 레지스터인 경우)

내부버스 구성을 위해 2 × 1 MUX 4개, 1 × 2 디코더 1개 필요
마이크로 연산을 위해 MUX의 선택신호는 0(2진수), 디코더의 선택신호는 1(2진수) 부여

![InternalBusExample](\assets\images\CA\InternalBusExample.png)

<br>

### 📄산술논리연산장치
산술연산과 논리연산을 실행하는 조합논리회로(산술연산회로와 논리연산회로의 결합)

![ALU](\assets\images\CA\ALU.png)

<br>

* 산술연산회로
  - 여러 개의 전가산기를 연속적으로 연결한 병렬가산기로 구성
  - 병렬가산기로 들어가는 제어입력 값을 선택하여 여러 가지 형태의 산술연산을 실행

![ArithmeticCircuits](\assets\images\CA\ArithmeticCircuits.png)

* 산술연산 종류

![ArithmeticOperation](\assets\images\CA\ArithmeticOperation.png)

<br>

* 논리연산회로
레지스터에 있는 각 비트를 독립된 2진 변수로 간주하여 비트별 연산을 실행

![LogicalCircuits](\assets\images\CA\LogicalCircuits.png)

* ALU 연산표

![ALUOperataion](\assets\images\CA\ALUOperataion.png)

<br>

### 📄상태 레지스터
ALU에서 산술연산이 수행된 후 연산결과에 의해 나타나는 상태 값을 저장

Carry Bit(C), Sign Bit(S), Zero Bit(Z), Overflow Bit(V)로 구성

![FlagRegister](\assets\images\CA\FlagRegister.png)

<br>

### 📄시프터
입력 데이터의 모든 비트들을 각각 서로 이웃한 비트로 자리를 옮기는 시프트 연산을 수행

<br><br>

## 📚제어단어
제어변수(선택신호)들의 묶음

* 선택신호
  - 처리장치내에서 수행되는 마이크로 연산을 선택하는 변수
  - 처리장치의 버스, ALU, 시프터, 도착 레지스터 등을 제어
  - 선택신호(제어변수)가 특정한 마이크로 연산을 선택
  - 제어변수들의 묶음을 제어단어라고 함

<br>

### 📄처리장치의 구조에서 선택신호와 제어단어 구성

![ControlWord](\assets\images\CA\ControlWord.png)

<br>

### 📄제어단어 각 필드 동작
* A, B필드(각각 3비트): ALU로 입력되는 각각의 출발 레지스터 선택
* D필드(3비트): ALU 결과가 저장될 도착 레지스터 선택
* F필드(4비트): ALU에서 이뤄지는 12가지 연산 중 하나를 선택
* H필드(3비트): 시프터에서의 시프트 연산 중 하나를 선택

전체 16비트로 구성된 선택신호들의 모임을 처리장치의 각 구성요소에 가하면 해당 마이크로 연산이 수행된다.

<br>

### 📄제어단어 내역표

![ControlWordTable](\assets\images\CA\ControlWordTable.png)

<br>

### 📄제어단어 작성방법
제어단어 내역표를 참고하여 R1 <- R2 - R3를 2진 코드로 나타내보면 아래와 같다.

* A필드 R2에 해당하는 2진 코드: 010
* B필드 R3에 해당하는 2진 코드: 011
* D필드 R1에 해당하는 2진 코드: 001
* F필드 뺄셈에 해당하는 2진 코드: 0101
* H필드 시프트 없음에 해당하는 2진 코드: 000

<br>

### 📄제어단어 생성을 위한 효과적인 방법
작성된 제어단어를 기억장치에 저장, 기억장치의 출력을 처리장치의 각 구성요소의 선택신호로 연결 
<br>
-> 기억장치로부터 연속적인 제어단어를 읽음으로써 처리장치에서 마이크로 연산이 정해진 순서대로 연속적으로 수행
<br>
-> 제어장치의 역할

<br><br>