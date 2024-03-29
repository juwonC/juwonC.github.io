---
title: "[Circuits]NAND, NOR 게이트를 이용한 논리회로 구현"
excerpt: "NAND, NOR 게이트를 이용한 논리회로 구현"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 부울함수 간소화, NAND 게이트, NOR 게이트]

toc: true
toc_sticky: true

date: 2023-05-15
---

## 📚개요
모든 부울함수는 AND, OR, NOT 게이트를 사용하여 간단하게 구현할 수 있습니다. 하지만 실제 회로 설계에서는 대부분 NAND와 NOR 게이트를 사용하여 부울함수를 구현합니다. NAND와 NOR 게이트가 전자회로로 제작하기 쉽고, NAND와 NOR 게이트를 사용하여 AND, OR, NOT을 모두 구현할 수 있기 때문입니다.

부울함수는 정규형(최소항의 합 또는 최대항의 곱)으로 나타낼 수 있는데 최소항의 합형태는 간소화를 통해 곱항의 합으로 표현될 수 있습니다. 곱합의 합은 NAND 게이트만을 사용하여 부울함수를 구현할 수 있습니다. 또한 최대한의 합형태는 간소화를 통해 합항의 곱으로 표현될 수 있습니다. 합항의 곱은 NOR 게이트만을 사용하여 부울함수를 구현할 수 있습니다.

<br><br><br>

## 📚NAND 게이트를 이용한 논리회로 구현
### 📄NAND 게이트 개념 및 구성
NAND 게이트는 논리곱의 보수(AND-NOT)를 수행하는 기능을 합니다. 2개 이상의 입력과 1개의 출력으로 구성되고 입력 중 1개 이상의 입력이 논리-0이면 출력은 논리-1이고, 모든 입력이 논리-1이면 출력은 논리-0이 됩니다.

NAND 게이트만으로 AND, OR, NOT 논리연산을 구현할 수 있습니다. 아래 그림은 위 부터 차례대로 NOT, AND, OR 논리연산입니다.

![NANDgate](\assets\images\Circuits\NAND.png)

AND-NOT의 NAND 게이트는 출력부에 작은 원을 붙인 AND 기호입니다. NOT-OR의 NAND 게이트는 모든 입력에 작은 원을 붙인 OR 기호입니다. 이 둘은 서로 같고 드모르간 법칙에 의해 NAND 게이트로 나타낼 수 있다는 것을 알 수 있습니다.

![NANDgate2](\assets\images\Circuits\NAND2.png)

<br><br>

### 📄2단계 구현
임의의 부울함수를 NAND 게이트만을 사용하여 2단계로 논리회로도를 구현할 수 있습니다.

1. 부울함수를 간소화하여 곱의 합형태로 나타낸다.
2. 2개 이상의 입력의 곱항을 NAND 게이트로 나타내고, 하나의 입력 곱항을 NOT 게이트로 나타낸다.
3. 2번에서의 출력을 AND-NOT 또는 NOT-OR 형태를 사용하여 2단계 게이트를 그린다.

F = XYZ + WX를 NAND 게이트로 구현하면 아래와 같습니다.

![TwoLevelNAND](\assets\images\Circuits\TwoLevelNAND.png)

<br><br>

### 📄다단계 구현
표준형으로 고친 부울함수를 NAND 게이트를 사용하여 2단계로 논리회로도를 구성할 수 없을 경우 다단계의 논리회로도로 구현할 수 있습니다. 다단계 구현과정은 아래와 같습니다.

1. 모든 AND 게이트를 AND-NOT 기호의 NAND 게이트로 변환.
2. 모든 OR 게이트를 NOT-OR 기호의 NAND 게이트로 변환.
3. 논리회로도의 모든 작은 원을 확인한다. 동일 선상의 두 원은 상쇄시키고 상쇄되지 않은 원은 NOT 게이트를 추가하거나 입력변수에 보수를 취한다.

$$ F = (X\overline{Y} + Z)(W + \overline{X}) $$를 NAND 게이트로 구현하면 다음과 같습니다.

![MultiLevelLevelNAND](\assets\images\Circuits\MultiLevelNAND.png)

<br><br><br>

## 📚NOR 게이트를 이용한 논리회로 구현
### 📄NOR 게이트 개념 및 구성
NOR 게이트는 논리 합의 보수(OR-NOT)를  수행합니다. 2개 이상의 입력과 1개의 출력으로 구성되고 입력 중 어느 1개의 입력이라도 논리-1인 경우 출력은 논리-0이고 그렇지 않은 경우 논리-1이 됩니다.

NOR 게이트만으로도 AND, OR, NOT 게이트를 구현할 수 있습니다.

![NORgate](\assets\images\Circuits\NORgate.png)

OR-NOT의 NOR게이트는 출력부에 작은 원을 붙인 OR 기호로 나타내고 NOT-AND의 NOR 게이트는 모든 입력부에 작은 원을 붙인 AND 기호로 나타냅니다. 이 둘은 서로 같고 드모르간 법칙에 의해 NOR 게이트로 나타낼 수 있다는 것을 알 수 있습니다.

![NORgate2](\assets\images\Circuits\NORgate2.png)

<br><br>

### 📄2단계 구현

임의의 부울함수를 NOR 게이트만을 사용하여 2단계로 논리회로도를 구현할 수 있습니다.

1. 부울함수를 간소화하여 합의 곱형태로 나타낸다.
2. 2개 이상의 입력의 합항을 NOR 게이트로 나타내고, 하나의 입력 합항을 NOT 게이트로 나타낸다.
3. 2번에서의 출력을 OR-NOT 또는 NOT-AND 형태를 사용하여 2단계 게이트를 그린다.

F = W(X + Y)를 NOR 게이트로 구현하면 다음과 같습니다.

![TwoLevelNOR](\assets\images\Circuits\TwoLevelNOR.png)

<br><br>

### 📄다단계 구현
표준형으로 고친 부울함수를 NOR 게이트를 사용하여 2단계로 논리회로도를 구성할 수 없을 경우 다단계의 논리회로도로 구현할 수 있습니다. 다단계 구현과정은 아래와 같습니다.

1. 모든 OR 게이트를 OR-NOT 기호의 NOR 게이트로 변환.
2. 모든 AND 게이트를 NOT-AND 기호의 NOR 게이트로 변환.
3. 논리회로도의 모든 작은 원을 확인한다. 동일 선상의 두 원은 상쇄시키고 상쇄되지 않은 원은 NOT 게이트를 추가하거나 입력변수에 보수를 취한다.

$$ F = W(XY + Z)(\overline{Y}\overline{Z} + \overline{W}) $$를 NOR 게이트로 구현하면 다음과 같습니다.

![MultiLevelLevelNOR](\assets\images\Circuits\MultiLevelNOR.png)

<br><br>