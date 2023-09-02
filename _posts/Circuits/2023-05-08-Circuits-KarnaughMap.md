---
title: "[Circuits]카르노도표"
excerpt: "카르노도표"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 부울함수 간소화, 카르노도표]

toc: true
toc_sticky: true

date: 2023-05-08
---

## 📚카르노도표 개요
부울함수를 간소화하는 방법은 세 가지로 구분할 수 있습니다.

* 대수적인 방법
<br>
이전 게시물에서 다룬 대수적인 부울함수의 간소화 방법은 주어진 부울함수에 대해 부울대수 정리를 대수적으로 적용시키는 방법입니다. 이 방법은 일반적으로 잘 사용되지 않지만 아래 두 방법의 이론적 바탕이 됩니다.

* 도표방법
<br>
도표방법은 **카르노도표(Karnaugh map)**를 사용하는 방법입니다. 이 방법은 부울함수의 각 항은 하나의 곱형태로 쉽게 간소화됩니다.

* 테이블 방법
<br>
테이블 방법은 퀸-맥클러스키 방법이라고 합니다. 테이블을 사용하여 간소화 알고리즘을 구현한 방법이라 많은 변수가 있는 부울함수에 적합합니다.

<br><br><br>

## 📚카르노도표 방법
카르노도표는 진리표를 다이어그램 모양으로 나타낸 것입니다. 여러 개의 사각형으로 이루어진 다이어그램이고 사각형은 각각 하나의 최소항 또는 최대항을 나타냅니다. 도표 안의 면적을 가지고 직관적으로 부울함수를 간소화할 수 있습니다.

카르노도표는 부울함수의 입력변수 수에 따라 그 형태가 달라집니다. 입력변수의 수가 n인 경우, n변수 카르노도표라고 하며 2<sup>n</sup>개의 사각형으로 구성됩니다.

카르노도표를 이용하여 부울함수를 간소화할 때 부울함수를 정규형(최소항의 합형태, 최대항의 곱형태) 부울함수로 변형한 다음 카르노도표를 이용하여 표준형(곱의 합형태, 합의 곱형태)으로 표시합니다.

* **최소항의 합형태를 곱의 합형태로 간소화**
  1. 입력변수의 수 n에 따라 n변수 카르노도표 작성. 2<sup>n</sup>개의 정사각형으로 구성.
  2. 정규형 부울함수의 최소항의 인덱스에 대응되는 도표 안의 사각형을 1로 표시.
  3. 1로 표시된 사각형 중 서로 인접한 사각형끼리 묶음. 한 묶음은 크게, 전체 묶음의 수는 작게 묶음.
  4. 각 묶음이 입력변수 각각에 대해 도표의 어느 위치에 있는지 파악. 묶음이 입력변수 X에 대해 X = 1인 곳에만 존재한다면 곱항에 X를 남기고, X = 0인 곳에만 존재한다면 곱항에 $$ \overline{X} $$를 남기고, X = 0인 곳과 X = 1인 곳에 걸쳐서 존재한다면 곱항에서 X를 소거.
  5. 4에서 구한 각 묶음에 대한 곱항을 논리합(OR)으로 연결시켜 간소화된 표준형을 구함.

<br>

* **최대항의 곱형태를 합의 곱형태로 간소화**
  1. 입력변수의 수 n에 따라 n변수 카르노도표 작성. 2<sup>n</sup>개의 정사각형으로 구성.
  2. 정규형 부울함수 최대항의 인덱스에 해당하는 도표 안의 사각형을 0으로 표시.
  3. 0으로 표시된 사각형 중 서로 인접한 사각형끼리 묶음. 한 묶음은 크게, 전체 묶음의 수는 작게 묶음.
  4. 각 묶음이 입력변수 각각에 대해 도표의 어느 위치에 있는지 파악. 묶음이 입력변수 X에 대해 X = 1인 곳에만 존재한다면 합항에 $$ \overline{X} $$를 남기고, X = 0인 곳에만 존재한다면 합항에 X를 남기고, X = 0인 곳과 X = 1인 곳에 걸쳐서 존재한다면 합항에서 X를 소거.
  5. 4에서 구한 각 묶음에 대한 곱항을 논리곱(AND)으로 연결시켜 간소화된 표준형을 구함.

<br>

* **인접 사각형**
<br><br>
카르노도표에서 각 정사각형은 하나의 최소항입니다. 입력변수 X, Y, Z인 경우 최소항 $$ m_{4} = X\overline{YZ} $$와 $$ m_{6} = XY\overline{Z} $$는 카르노도표 안에 2개의 정사각형을 의미합니다.
<br>
위 두 최소항을 더하면 $$ m_{4} + m_{6} = X\overline{YZ} + XY\overline{Z} = X\overline{Z}(\overline{Y} + Y) = X\overline{Z} $$로 간소화됩니다.
<br>
두 정사각형에 대응되는 각 최소항의 구성문자 중 다른 모든 문자는 서로 동일하되 오직 하나의 문자만 서로 보수관계에 있을 때 서로 인접하다고 정의합니다.

<br>

* **인접 사각형끼리 묶는 방법**

  1. 한 묶음 내의 정사각형 수는 2<sup>n</sup>개가 되도록 묶는다.
  2. 한 묶음은 크게, 전체 묶음의 수는 작게 묶는다.
  <br><br>
  한 묶음 안의 정사각형 수는 1개, 2개, 4개, 8개, ... 등으로 묶어야 합니다.
  <br>
  한 묶음을 크게 묶으면 곱항 내의 문자의 수가 줄어들고, 전체 묶음의 수를 작게 묶으면 곱항의 수가 줄어듭니다. 곱항 안에서 문자 수가 줄어들면 AND 연산 수 또는 AND 연산의 입력수가 줄어들고, 곱항의 수가 줄어들면 OR 연산 수 또는 OR 연산 입력수가 줄어듭니다.

<br>

### 📄2변수 카르노도표
2개 변수를 가지는 부울함수는 4개의 최소항이 있습니다. 2변수 카르노도표는 4개의 정사각형을 구성됩니다. 0과 1을 기입한 도표의 왼쪽 면과 윗면은 각각 변수 x<sub>1</sub>과 x<sub>2</sub>의 값을 나타냅니다. 2변수 부울함수는 도표에서 함수의 최소항에 해당하는 정사각형을 1로 표시하여 나타낼 수 있습니다.

아래 도표를 보면 인접 사각형끼리 묶여 있습니다. 이를 도표 간소화 방법에 따라 간소화 해보겠습니다.

1. 가로로 묶여 있는 인접 사각형을 보면 입력 변수 x<sub>1</sub>에 대해 x<sub>1</sub> = 0인 곳에만 존재하기 때문에 곱항에서 $$ \overline{x_{1}} $$를 남기고, 입력 변수 x<sub>2</sub>에 대해 x<sub>2</sub> = 0과 x<sub>2</sub> = 1인 곳에 걸쳐있기 때문에 곱항에서 x<sub>2</sub>변수는 소거합니다.

2. 세로로 묶여 있는 인접 사각형은 입력 변수 x<sub>1</sub>에 대해 x<sub>1</sub> = 0과 x<sub>1</sub> = 1인 곳에 걸쳐있기 때문에 곱항에서 x<sub>1</sub>변수는 소거하고, 입력 변수 x<sub>2</sub>에 대해 x<sub>2</sub> = 1인 곳에만 존재하기 때문에 곱항에서 $$ x_{2} $$를 남깁니다.

3. 각 묶음에 대한 곱항을 논리합(OR)으로 연결시킵니다.

위 방법대로 2변수 카르노도표를 간소화하면 다음과 같습니다.

$$ f = \overline{x_{1}} + x_{2} $$

![2VarKmap](\assets\images\Circuits\Kmap2Var.png){: width="400" height="400"}
<br>
[https://www.oreilly.com/library/view/introduction-to-digital/9780470900550/chap6-sec004.html](https://www.oreilly.com/library/view/introduction-to-digital/9780470900550/chap6-sec004.html)

<br>

위 도표를 대수적으로 간소화하면 다음과 같습니다.

$$ 
\begin{aligned}
f &= \overline{x_{1}x_{2}} + \overline{x_{1}}x_{2} + x_{1}x_{2} \\
  &= \overline{x_{1}}(\overline{x_{2}} + x_{2}) + x_{1}x_{2} \\
  &= \overline{x_{1}} + x_{1}x_{2} \\
  &= (\overline{x_{1}} + x_{1})(\overline{x_{1}} + x_{2}) \\
  &= \overline{x_{1}} + x_{2}
\end{aligned}
$$

<br>

### 📄3변수 카르노도표
3변수 카르노 도표는 8개의 정사각형으로 구성됩니다. 왼쪽 면 A값으로 윗면은 B,C 값을 나타냅니다. 여기서 B와 C의 값이 순차적이 아니라는 것에 주의해야 합니다.

B, C값이 00, 01, 10, 11이 아닌 이유는 인접 사각형 정의에 의해 인접한 사각형 최소항의 구성 문자 중 다른 모든 문자는 서로 동일하되 오직 하나의 문자만 서로 보수 관계에 있어야 하기 때문입니다.

![3VarKmap](\assets\images\Circuits\Kmap3Var.png){: width="400" height="400"}
<br>
[https://www.geeksforgeeks.org/introduction-of-k-map-karnaugh-map/](https://www.geeksforgeeks.org/introduction-of-k-map-karnaugh-map/)

<br>

### 📄4변수 카르노도표

![4VarKmap](\assets\images\Circuits\Kmap4Var.png){: width="400" height="400"}
<br>
[https://www.geeksforgeeks.org/introduction-of-k-map-karnaugh-map/](https://www.geeksforgeeks.org/introduction-of-k-map-karnaugh-map/)

<br>

### 📄5변수 카르노도표

![5VarKmap](\assets\images\Circuits\Kmap5Var.png){: width="400" height="400"}
<br>
[https://www.electricaltechnology.org/2018/05/karnaugh-map-k-map.html](https://www.electricaltechnology.org/2018/05/karnaugh-map-k-map.html)

<br>

### 📄6변수 카르노도표

![6VarKmap](\assets\images\Circuits\Kmap6Var.png){: width="400" height="400"}
<br>
[https://www.electricaltechnology.org/2018/05/karnaugh-map-k-map.html](https://www.electricaltechnology.org/2018/05/karnaugh-map-k-map.html)

<br>

### 📄무관조건
디지털 논리회로에서 진리표는 입력변수의 조합에 따라 함수값이 0 또는 1을 가집니다. 함수값이 1인 입력변수를 논리곱 연산의 항으로 표시한 것이 최소항이고, 이런 최소항들을 논리합 연산으로 결합한 것이 최소항의 합 형태의 정규형 부울함수 입니다. 함수값은 일정한 입력변수의 조합에서 언제나 일정한 출력값을 가집니다. 하지만 어떤 논리회로에서는 입력변수 조합에 따라 함수값이 발생하지 않는 경우, 출력값이 일정한 값이 되지 않는 경우도 있습니다.

BCD 코드는 2진수 네 자리로 모든 10진수를 2진수로 표현합니다. 하지만 2진수의 4비트, 16개의 조합에서 10개만 숫자표현에 사용하고 나머지 6개 비트 조합은 사용되지 않습니다. 여기서 6개의 사용되지 않는 비트 조합에 대해서 무관하게 논리회로를 구성하기 때문에 이 입력변수 조합들에 대한 함수 출력값은 어떤 값을 가지더라도 무관합니다. 이런 조건을 **무관조건**이라고 합니다. 무관조건은 함수를 더 간소화하는데 사용됩니다.

<br>

### 📄기타 카르노도표
* XOR 카르노도표
<br>

| A | B | $$ f $$ |
| :---: | :---: | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

$$
\begin{aligned}
f &= \overline{A}B + \overline{B}A \\
  &= A \oplus B
\end{aligned}
$$

<br>

![XorKmap](\assets\images\Circuits\KmapXOR.jpeg){: width="300" height="300"}
<br>
[https://www.electronicshub.org/exclusive-or-gatexor-gate/](https://www.electronicshub.org/exclusive-or-gatexor-gate/)

<br>

* XNOR 카르노도표
<br>
XNOR 카르노도표는 XOR 카르노 도표에서 0과 1을 뒤바꿔서 그리면 되고, XNOR 논리도는 XOR 논리도의 출력에 NOT 게이트를 추가하면 됩니다.

<br><br>