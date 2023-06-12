---
title: "[Circuits]순서논리회로(3)"
excerpt: "순서논리회로"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 순서논리회로]

toc: true
toc_sticky: true

date: 2023-06-12
---

## 📚순서논리회로의 설계
### 📄순서논리회로의 설계과정
순서논리회로의 설계과정은 다음과 같습니다.

1. 주어진 문제 설명이나 상태도로부터 상태표를 작성한다.
2. 플립플롭의 종류, 개수, 이름을 결정한다.
3. 상태표의 다음 상태로부터 플립플롭의 입력방정식을 구한다.
4. 상태표에 출력이 있으면 출력방정식을 구한다.
5. 구한 입력방정식과 출력방정식을 간소화한다.
6. 간소화된 입출력방정식을 이용하여 논리회로도를 그린다.

<br>

* 상태표 작성

![DesignStateTable](\assets\images\Circuits\DesignStateTable.png){: width="600" height="600"}

<br>

* 플립플롭의 결정

순서논리회로에 사용될 플립플롭의 종류와 개수를 결정하고 그 플립플롭에 기호를 할당하는 것입니다.

  1. F/F의 개수 결정
    <br>
    - F/F의 개수는 순서논리회로 내의 상태수로 결정
    <br>
    - 2<sup>n</sup>개의 상태를 표현하기 위해서는 n개의 F/F 필요
  <br><br>
  2. F/F에 기호 할당(F/F의 종류 결정)
    <br>
    - 정해진 F/F에 A, B 등으로 기호 할당
    <br>
    - 사용될 F/F의 종류 결정은 설계자에 따라 결정

데이터 전송을 위한 설계에는 D 플립플롭, 보수를 포함한 응용에는 T 플립플롭이 사용되지만, JK 플립플롭이 일반적으로 많이 사용됩니다.

![FFDecision](\assets\images\Circuits\FFDecision.png){: width="600" height="600"}

<br>

* 입력방정식의 유도

플립플롭 입장에서 보면 입력방정식은 조합논리회로의 출력값이 됩니다. 입력방정식 즉, 플립플롭의 출력값은 조합논리회로의 입력으로 외부입력과 플립플롭의 현재상태에 의해 결정됩니다.

따라서 만약 플립플롭의 현재상태와 다음상태를 안다면 플립플롭의 입력조건을 구할 수 있습니다. 결국 플립플롭의 입력조건에 대한 부울함수가 입력방정식입니다. 여기서 현재상태에서 다음상태로의 변화를 일으키는 입력조건의 리스트를 플립플롭의 **여기표**라고 합니다.

<br>

* 플립플롭의 여기표

여기표는 현재 상태 Q(t)와 다음상태 Q(t+1) 그리고 각각의 상태변화를 나타내는 입력을 보여줍니다.

![ExcitationTable](\assets\images\Circuits\ExcitationTable.png){: width="600" height="600"}

<br><br>

### 📄D 플립플롭을 이용한 설계

![DesignDFF1](\assets\images\Circuits\DesignDFF1.png){: width="600" height="600"}

![DesignDFF2](\assets\images\Circuits\DesignDFF2.png){: width="600" height="600"}

![DesignDFF3](\assets\images\Circuits\DesignDFF3.png){: width="600" height="600"}

<br><br>

### 📄JK 플립플롭을 이용한 설계

![DesignJKFF1](\assets\images\Circuits\DesignJKFF1.png){: width="600" height="600"}

![DesignJKFF2](\assets\images\Circuits\DesignJKFF2.png){: width="600" height="600"}

![DesignJKFF3](\assets\images\Circuits\DesignJKFF3.png){: width="600" height="600"}

![DesignJKFF4](\assets\images\Circuits\DesignJKFF4.png){: width="600" height="600"}

<br><br>