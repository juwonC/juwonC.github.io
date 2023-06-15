---
title: "[Circuits]레지스터와 카운터(2)"
excerpt: "레지스터와 카운터"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 레지스터, 카운터]

toc: true
toc_sticky: true

date: 2023-06-13
---

## 📚동기식 카운터
### 📄동기식 카운터
리플 카운터(비동기식 카운터)는 구조가 간단하고 동작이 단순한 반면 동시에 트리거되지 않기 때문에 속도상의 제약을 받습니다.

하지만 동기식 카운터는 카운터를 구성하고 있는 모든 플립플롭에 동시에 클럭 펄스가 가해지고 모든 플립플롭이 한꺼번에 동작하기 때문에 동작속도의 향상을 기할 수 있습니다.

* 동기식 2진 카운터

동기식 2진 카운터는 모든 플립플롭에 클럭 펄스를 동시에 가합니다. 그리고 2진 순서를 따르는 카운터입니다.

![SyncBinaryCounter](\assets\images\Circuits\SyncBinaryCounter.png){: width="600" height="600"}

동기식 2진 카운터는 2진수를 상향으로 계수하는 업 카운터로 모든 플립플롭의 클럭 단자는 공통 클럭 펄스에 연결되어 있고 맨 왼쪽 플립플롭의 JK 입력은 계수 구동입력이 1이 되는 것과 동시에 모두 1이 됩니다.

<br>

* 모듈로-N 카운터

모듈로-N 카운터는 N개의 계수의 순서를 반복하여 계수하는 카운터로 모드 N-카운터라고도 합니다. 예를 들어 모듈로-8 카운터는 0 부터 7까지 계수하는 카운터입니다.

![Modulo-8Counter](\assets\images\Circuits\Modulo-8Counter.png){: width="600" height="600"}

<br><br>

### 📄시프트 카운터
* 링 카운터

앞서 살펴보았던 대부분의 카운터는 2진수로 계수하였습니다. 하지만 링 카운터는 시프트 레지스터를 응용한 카운터로 출력 비트 중 1비트만 1이 되고 입력 펄스에 의해 한쪽 방향으로 1의 위치가 순환됩니다.

![RingCounter](\assets\images\Circuits\RingCounter.png){: width="600" height="600"}

<br>

* 존슨 카운터

존슨 카운터는 링 카운터와 마찬가지로 시프트 레지스터에 피드백을 이용한 구조이며 트위스트 링 카운터라고도 부릅니다. 존슨 카운터는 링 카운터와 유사하지만 시프트 레지스터의 최종단 플립플롭의 출력 $$ Q $$가 아닌 $$ \bar{Q} $$에서 입력 쪽으로 피드백시키는 것이 링 카운터와 다른 점입니다.

존슨 카운터의 계수 동작은 링 카운터의 2배가 됩니다. 즉, N개의 플립플롭을 사용하면 2N개의 출력 상태가 나타납니다.

![JohnsonCounter](\assets\images\Circuits\JohnsonCounter.png){: width="600" height="600"}

<br><br>

### 📄카운터의 설계
동기식 카운터의 설계는 순서논리회로의 설계 과정과 동일합니다. 일반적으로 카운터는 클럭 펄스를 제외하고 외부입력 없이도 동작할 수 있고 카운터의 출력 역시 외부 데이트 없이 플립플롭의 출력으로부터 직접 얻을 수 있습니다.

* BCD 카운터 설계

![DesignBCDCounter1](\assets\images\Circuits\DesignBCDCounter1.png){: width="600" height="600"}

![DesignBCDCounter2](\assets\images\Circuits\DesignBCDCounter2.png){: width="600" height="600"}

![DesignBCDCounter3](\assets\images\Circuits\DesignBCDCounter3.png){: width="600" height="600"}

<br><br>