---
title: "[Circuits]조합논리회로(2)"
excerpt: "조합논리회로"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 조합논리회로]

toc: true
toc_sticky: true

date: 2023-06-11
---

## 📚여러 가지 조합논리회로
### 📄코드변환기
디지털 시스템에서 서로 다른 시스템끼리 동일한 정보를 교환할 때 다른 코드를 사용한다면 코드 변환이 필요합니다. 이때 사용되는 코드변환기는 하나의 2진 코드를 다른 2진 코드로 바꿔주는 조합논리회로입니다.

* **BCD-3초과 코드변환기**
<br>
BCD 코드를 3초과 코드로 바꾸는 변환기입니다. BCD와 3초과 코드는 모두 4비트를 이용하여 10진수를 표현하기 때문에 변환회로는 4개의 입력과 4개의 출력이 필요합니다.

  - 설계과정
    + 진리표작성
    + 카르노도표를 이용하여 간소화(부울함수 유도)
    + 출력 부울함수 유도
    + 논리회로도 작성

![BCD_Excess-3](\assets\images\Circuits\BCD_Excess-3.png){: width="500" height="500"}

![BCD_Excess-3Circuits](\assets\images\Circuits\BCD_Excess-3Circuits.png){: width="400" height="400"}

<br>

* **BCD-9의 보수변환기**
<br>
BCD 코드가 입력되면 9의 보수값으로 변환되는 코드변환기입니다.

![BCD_9Complement](\assets\images\Circuits\BCD_9Complement.png){: width="500" height="500"}

![BCD_9ComplementCircuits](\assets\images\Circuits\BCD_9ComplementCircuits.png){: width="350" height="350"}

<br><br>

### 📄패리티 발생기/검사기
디지털 시스템에서 2진 정보를 전송하거나 대량의 정보를 주고받을 때 잡음이나 회로상의 문제로 정보가 손상되어 에러가 발생할 수 있습니다. 이러한 에러 검출을 위해 전송되는 정보에 에러 검출용 비트를 추가해 전송하는 방법이 있습니다. 이때 사용되는 에러 검출용 비트를 **패리티 비트**라고 합니다.

* 패리티 비트를 이용하는 방식
  - 짝수 패리티 검출 방식: 2진 정보 속에 1의 개수가 패리티 비트를 포함하여 짝수가 되도록 패리티 비트를 부가하는 방식.

  - 홀수 패리티 검출 방식: 일반적인 검출 방식. 2진 정보 속에 1의 개수가 패리티 비트를 포함하여 홀수가 되도록 패리티 비트를 부가하는 방식.

![ParityCheck](\assets\images\Circuits\ParityCheck.png){: width="500" height="500"}

위와 같은 패리티 비트를 사용하면 전송된 2진 정보에서 1개의 에러가 발생하였을 때 2진 정보 속의 1의 개수를 확인해 봄으로써 에러를 검출 할 수 있지만 동시에 2개의 에러가 포함되어 있으면 에러를 검출할 수 없다는 문제가 있습니다. 이때 사용되는 방법이 이중 패리티 검출 방식입니다.

* **이중 패리티 검출 방식**
<br>
이중 패리티 검출 방식은 코드를 한 묶음으로 하여 그 묶음의 수직 방향과 수평 방향으로 패리티 비트를 부여합니다. 패리티 비트는 수평 방향의 에러 유무를 검출하고 패리티 워드는 수직 방향의 에러를 검출합니다. 에러로 검출된 비트 1은 잘못된 정보이고 올바른 정보는 0으로 나타나야 합니다.

![DoubleParityCheck](\assets\images\Circuits\DoubleParityCheck.png){: width="500" height="500"}

<br>

* **패리티 발생기**
<br>
에러 검출이나 정정을 위해 송신측에서 전송정보에 패리티 비트를 부가하는데 이러한 패리티 비트를 생성하는 조합논리회로입니다. 3비트 데이터 비트에 하나의 패리티 비트를 부가하는 홀수 패리티 비트 발생기의 진리표와 논리회로도입니다.

![ParityGenerator](\assets\images\Circuits\ParityGenerator.png){: width="500" height="500"}

![ParityGeneratorCircuits](\assets\images\Circuits\ParityGeneratorCircuits.png){: width="400" height="400"}

<br>

* **패리티 검사기**
<br>
수신측에서 송신된 정보의 에러를 검출하기 위해 페리티를 검사하는 조합논리회로입니다. 패리티 발생기에 의해 만들어진 4비트 전송정보에 대한 홀수 패리티 검사기의 진리표와 논리회로도입니다.

![ParityChecker](\assets\images\Circuits\ParityChecker.png){: width="500" height="500"}

![ParityCheckerCircuits](\assets\images\Circuits\ParityCheckerCircuits.png){: width="400" height="400"}

<br><br><br>

## 📚MSI를 이용한 조합논리회로
디지털 시스템에서 효과적인 조합논리회로를 설계하려면 주어진 함수를 실현하는데 필요한 게이트의 수를 최소화 시켜야합니다. 이를 위해 집적회로를 사용하면 여러 개의 논리게이트가 1개의 IC 내에 포함되어 있기 때문에 패키지화된 IC의 내부 게이트를 이용함으로써 경제적인 설계가 될 수 있습니다.

이미 제작되어 있는 MSI나 LSI 장치를 이용하면 다양한 조합논리회로를 설계가 가능합니다. MSI 장치에는 인코더, 디코더, 멀티플레서, 디멀티플레서 등이 있습니다.

<br>

### 📄인코더
인코더는 부호화되지 않는 입력을 받아서 부호화된 출력으로 내보내는 부호화기입니다. 10진수나 8진수를 입력으로 받아들여 2진수나 BCD 같은 코드로 변환해주는 조합논리회로입니다. 인코더는 2<sup>n</sup>개의 입력과 n개의 출력으로 구성되고 출력은 입력값에 대응하는 2진 코드를 생성합니다.

* 인코더 블록도

![Encoder](\assets\images\Circuits\Encoder.png){:  width="400" height="400"}

8진을 2진으로 바꾸는 인코더에 대한 진리표와 논리회로도는 아래와 같습니다.

![EncoderTruthTable](\assets\images\Circuits\EncoderTruthTable.png){:  width="400" height="400"}

![EncoderCircuits](\assets\images\Circuits\EncoderCircuits.png){:  width="400" height="400"}

인코더는 임의의 순간 오직 하나의 입력만 1인 될 수 있다고 가정합니다. D<sub>3</sub>, D<sub>6</sub>가 동시에 1인 된다면 세 출력 A<sub>2</sub>, A<sub>1</sub>, A<sub>0</sub>가 모두 1이 되므로 인코더의 출력은 111이 되지만 이 출력은 2진수로 3을 의미하는 것도 6을 의미하는 것도 아닙니다.

이 문제를 해결하기 위해 인코더에 입력의 우선순위를 부여해야 합니다. 입력 첨자가 높을수록 높은 우선순위를 줘서 D<sub>6</sub>와 D<sub>3</sub>가 동시에 1이 되어도 D<sub>6</sub>가 D<sub>3</sub>보다 우선순위가 높기 때문에 출력은 110이 되어 6이 되도록 합니다. 우선순위를 부여하는 인코더를 우선순위 인코더라고 합니다.

<br><br>