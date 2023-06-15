---
title: "[Circuits]순서논리회로(2)"
excerpt: "순서논리회로"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 순서논리회로]

toc: true
toc_sticky: true

date: 2023-06-12
---

## 📚순서논리회로의 분석
### 📄순서논리회로의 분석과정

* 순서논리회로의 분석
  - 주어진 순서논리회로의 입출력 관계를 규명하는 것입니다.
  - 시간지연요소인 플립플롭이 포함되어 있으므로 회로의 시간적 변화를 고려해야 합니다.
  - 회로동작의 시간적 변화를 현재상태와 다음상태로 표현해야 합니다.
  - 순서논리회로의 동작은 입출력 상태와 플립플롭의 상태에 따라 결정되므로 플립플롭의 상태와 입출력 상태의 시간적 변화를 적절히 나타내야 합니다.
  - **순서논리회로의 분석은 상태표를 완성하는 것입니다.**

<br>

* 순서논리회로의 상태표 작성 방법
  - 순서논리회로에 있는 플립플롭의 상태변화를 알아야 합니다.
  - 플립플롭의 상태변화는 플립플롭에 들어오는 입력을 알면 구할 수 있습니다.
  - 플립플롭의 입력은 입력방정식으로 표현됩니다.

<br>

1. 입력 방정식 유도
  - 플립플롭의 입력으로는 조합논리회로의 출력이 연결됩니다.
  - 조합논리회로의 출력함수가 플립플롭의 입력함수가 되고 이를 플립플롭의 입력 방정식이라고 합니다.
  <br><br>
  ![SequentialCircuitsAnalysis](\assets\images\Circuits\SequentialCircuitsAnalysis.png){: width="400" height="400"}
  <br><br>
2. 상태표 작성
  - 순서논리회로에서 플립플로의 상태와 입력, 출력의 시간적 변화를 표로 나타낸 것이 상태표입니다.
  - 상태표는 입력, 현재 상태, 다음 상태, 출력의 네 부분으로 구성됩니다.
  <br>
  ![StateTable](\assets\images\Circuits\StateTable.png){: width="600" height="600"}

<br><br>

### 📄D 플립플롭을 가진 순서논리회로의 분석

1. 상태표 작성을 위해 입력방정식 유도
<br>
![D_FF_Analysis](\assets\images\Circuits\D_FF_Analysis.png){: width="600" height="600"}
<br><br>
2. 상태표 작성을 위해 입력방정식에서 다음상태와 출력 결정
<br>
![D_FF_Analysis2](\assets\images\Circuits\D_FF_Analysis2.png){: width="600" height="600"}
<br><br>
3. 상태표 작성
<br>
![D_FF_Analysis3](\assets\images\Circuits\D_FF_Analysis3.png){: width="600" height="600"}

<br><br>

### 📄JK 플립플롭을 가진 순서논리회로의 분석
JK 플립플롭을 가진 순서논리회로의 분석을 위해서는 특성표가 필요합니다. 특성표는 플립플롭의 논리적 성질을 정의하고 그 동작 특성을 표로 나타낸 것입니다.

JK 플립플롭의 분석에 특성표가 필요한 이유는 D 플립플롭과는 달리 JK 플립플롭을 가진 순서논리회로는 다음상태가 입력방정식만으로 구해지지 않기 때문입니다. 따라서 다음상태를 구하기 위해 플립플롭의 특성표를 이용하여 플립플롭의 응답을 알아야 합니다.

* 특성표
  - 플립플롭의  함수표를 말합니다.

![CharacteristicTable](\assets\images\Circuits\CharacteristicTable.png){: width="600" height="600"}

<br>

* 특성표를 이용한 상태표 작성
  1. JK 플립플롭의 입력을 구하기 위해 입력방정식 유도
  2. 입력방정식으로부터 JK 플립플롭의 입력 유도
  3. 다음상태 결정(JK 플립플롭의 입력과 특성표를 이용)

<br><br>

### 📄상태도
상태도는 상태표로 주어진 정보를 그림으로 나타낸 것입니다. 상태표는 주어진 논리회로도와 입력방정식으로부터 작성할 수 있고 상태도는 상태표에서 쉽게 구해집니다. 상태도는 회로의 상태변화를 도형으로 나타내기 때문에 회로분석을 보다 쉽게 할 수 있습니다.

![StateDiagram1](\assets\images\Circuits\StateDiagram1.png){: width="600" height="600"}

<br>

![StateDiagram2](\assets\images\Circuits\StateDiagram2.png){: width="600" height="600"}