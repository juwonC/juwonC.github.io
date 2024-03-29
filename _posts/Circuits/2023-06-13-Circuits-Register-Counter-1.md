---
title: "[Circuits]레지스터와 카운터(1)"
excerpt: "레지스터와 카운터"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 레지스터, 카운터]

toc: true
toc_sticky: true

date: 2023-06-13
---

## 📚레지스터
### 📄개요
레지스터는 데이터를 일시 저장하거나 전송하는 장치로 디지털 컴퓨터에서 매우 중요한 기능을 하고 있습니다. 레지스터는 여러 개의 플립플롭을 연결한 플립플롭의 그룹으로 구성되어 있습니다. n비트 레지스터는 n개의 플립플롭으로 구성되고 n비트의 2진 정보를 저장할 수 있습니다.

레지스터는 여러 비트를 일시적으로 저장하거나, 배열된 비트를 좌우로 자리이동 시키는데 사용될 수 있습니다. 레지스터는 데이터의 입출력방식에 따라 직렬입력-직렬출력, 직렬입력-병렬출력, 병렬입력-직렬출력, 병렬입력-병렬출력 레지스터의 네 가지 기본형태로 분류됩니다.

또한 데이터의 자리이동방식에 따라 왼쪽 시프트 레지스터, 오른쪽 시프트 레지스터, 양방향 시프트 레지스터로 분류됩니다.

<br><br>

### 📄레지스터의 기본 형태
레지스터의 네 가지 기본적인 형태의 블록도입니다. 네 가지 형태의 레지스터는 입력된 정보를 그대로 저장하는 기능과 저장된 정보의 위치를 이동시키는 기능을 수행하게 됩니다.

![BasicRegister](\assets\images\Circuits\BasicRegister.png){: width="600" height="600"}

<br><br>

### 📄데이터 적재 레지스터
레지스터에 새로운 데이터를 기억시키는 과정을 적재한다고 합니다. 입력된 데이터를 그대로 기억하는 역할을 수행하는 레지스터를 **데이터 적재 레지스터**라고 합니다. 이 레지스터는 일반적으로 D 플립플롭을 사용하여 구성합니다. 데이터 입력 방식에 따라 직렬적재, 병렬적재 레지스터로 분류됩니다.

* 직렬적재 레지스터

직렬적재 레지스터는 여러 개의 플립플롭을 연결하여 구성합니다. 직렬적재방식은 데이터를 순차적으로 받아들이는 방식이고 1비트씩 입력하는 것을 말하며 직렬입력-직렬출력 레지스터입니다.

아래 직렬적재 레지스터는 4개의 플립플롭으로 구성되어 있고 4비트를 저장합니다.

![DirectLoad](\assets\images\Circuits\DirectLoad.png){: width="600" height="600"}

<br>

* 병렬적재 레지스터

n개의 플립플롭으로 구성된 병렬적재 레지스터에 한 클럭펄스가 입력되면 n개의 입력 데이터가 병렬로 적재됩니다. 하나로 연결된 클럭 펄스에 의해 동시에 레지스터로 적재하면 이것을 병렬적재라고 합니다.

한 클럭 펄스가 입력되면 데이터가 병렬로 적재되는데 클럭 펄스가 입력되지 않으면 적재된 레지스터의 내용이 그대로 유지됩니다. 즉, 클럭 펄스가 1일 때 입력 데이터가 적재되고, 클럭 펄스가 0이면 레지스터의 내용은 그대로 유지됩니다.

![ParallelLoad](\assets\images\Circuits\ParallelLoad.png){: width="600" height="600"}

<br><br>

### 📄시프트 레지스터
레지스터가 기억하고 있는 정보에 대해 한 방향 혹은 양방향으로 위치를 이동시킬 수 있는 레지스터를 **시프트 레지스터**라고 합니다. 시프트 레지스터의 구성은 플립플롭을 직렬로 연결한 것으로 한 플립플롭의 출력을 다음 플립플롭의 입력에 연결한 것입니다. 모든 플립플롭은 공통의 클럭 펄스를 가지고 클럭 펄스에 따라 한 단씩 이동합니다.

![ShiftRegister](\assets\images\Circuits\ShiftRegister.png){: width="600" height="600"}

<br><br>

### 📄병렬적재 양방향 시프트 레지스터
양쪽 방향으로의 시프트와 병렬적재가 가능한 레지스터를 병렬적재 양방향 레지스터라고 합니다. D 플립플롭과 멀티플렉서로 구성된 블록도는 다음과 같습니다.

![ParallelShiftRegister](\assets\images\Circuits\ParallelShiftRegister.png){: width="600" height="600"}

<br><br><br>

## 📚카운터
### 📄개요
카운터는 플립플롭을 사용하는 순서논리호로로서, 클럭 펄스가 입력될 때마다 미리 정해진 순서에 따라 상태가 변하게 됩니다. 카운터에서 외부 입력이나 출력은 없으며 상태변화는 클럭펄스에 의해 수행됩니다. 카운터를 구성하는 플립플롭은 일반적으로 T 플립플롭이나 JK 플립플롭이 사용됩니다.

카운터는 아래와 같이 분류할 수 있습니다.

![CounterClassification](\assets\images\Circuits\CounterClassification.png){: width="600" height="600"}

하지만 카운터를 분류하는데 클럭 펄스 인가방식과 계수방식이 독립적인 것이 아니라 서로 연관되어 있습니다. 따라서 실제로 카운터를 나타낼 때는 비동기식 2진 카운터 또는 동기식 10진 카운터 등으로 표현됩니다.

<br>

### 📄비동기식 카운터
비동기식 카운터는 카운터를 구성하고 있는 각 플립플롭에 동시에 클럭이 가해지지 않는 카운터를 의미합니다. 입력 클럭 펄스가 앞 단의 출력값에 의해서 영향을 받게 되는 것으로 리플 카운터라고도 합니다.

* 2진 리플 카운터

2진 리플 카운터는 비동기식 2진 카운터를 말하며 카운터를 구성하는 플립플롭의 상태가 동시에 변화하지 않습니다. 클럽입력이 플립플롭의 첫째 단, 즉 가장 낮은 자리의 비트를 저장하는 플립플롭에만 연결되고, 두번째 플립플롭 부터는 앞의 플립플롭의 출력에 의해 트리거됩니다.

![BinaryRippleCounter](\assets\images\Circuits\BinaryRippleCounter.png){: width="600" height="600"}

<br>

* BCD 리플 카운터

BCD 리플 카운터는 대표적인 비동기 10진 카운터로 0 부터 9까지 10개의 상태를 계수하는 카운터입니다. 각 상태는 10진수를 나타내는 2진코드로 표현하므로 적어도 4비트가 필요합니다.

![BCDRippleCounter](\assets\images\Circuits\BCDRippleCounter.png){: width="600" height="600"}

<br><br>