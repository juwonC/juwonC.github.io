---
title: "[Circuits]조합논리회로(3)"
excerpt: "조합논리회로"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 조합논리회로]

toc: true
toc_sticky: true

date: 2023-06-11
---

## 📚MSI를 이용한 조합논리회로
### 📄디코더
디코더는 부호화된 입력을 받아서 부호화되지 않은 출력을 내보내는 복호화기입니다. n 비트의 2진 코드를 최대 2<sup>n</sup>개의 서로 다른 정보로 바꿔주는 조합논리회로입니다. 일반적으로 입력이 n개 출력이 m개인 디코더를 n x m 디코더라고 합니다.

* 디코더 블록도

![Decoder](\assets\images\Circuits\Decoder.png){:  width="500" height="500"}

2 x 4 디코더의 블록도, 진리표, 논리회로도는 아래와 같습니다.

![DecoderCircuits](\assets\images\Circuits\DecoderCircuits.png){:  width="550" height="550"}

<br>

* 구동입력을 가진 디코더

디코더에는 AND 게이트 대신 NAND 게이트로 구성되어 있는 것도 있습니다. NAND 게이트로 구성하면 보수로 표현된 디코더의 최소항을 산출하는데 보다 효과적입니다. 대부분 MSI 디코더는 회로의 동작을 제어하기 위해 구동입력을 가지고 있습니다.

<br>

* 디코더의 확장

작은 디코더를 여러 개 결합하여 필요한 크기의 디코더를 만들 수 있습니다. 6 x 64라인 디코더가 필요한 경우 4개의 4 x 16 라인 디코더를 결합하여 필요한 디코더를 만들 수 있습니다.

아래는 2개의 2 x 4 디코더를 이용하여 3 x 8 디코더 구성입니다.

![ExtendedDecoder](\assets\images\Circuits\ExtendedDecoder.png){:  width="400" height="400"}

<br>

* 디코더를 이용한 부울함수 구현

디코더는 n개의 입력변수에 대해 2<sup>n</sup>개의 최소항을 만들어냅니다. 모든 부울함수는 최소항의 합으로 표현되므로 디코더를 이용하여 부울함수를 구현할 수 있습니다. n개의 입력과 m개의 출력을 가진 조합논리회로는 n x 2<sup>n</sup> 디코더와 m개의 OR 게이트로 만들 수 있습니다.

F(X, Y, Z) = Σ<sub>m</sub>(1, 3, 4, 7)를 디코더를 이용하여 구현하면 아래와 같습니다.

![BoolFunctionDecoder](\assets\images\Circuits\BoolFunctionDecoder.png){:  width="400" height="400"}

<br><br>

### 📄멀티플렉서
멀티플렉서는 여러 개의 입력선 가운데 하나를 선택하여 단일의 출력을 내보내는 조합논리회로입니다. 특정 입력선을 선택하려면 선택변수를 이용하게 됩니다. 2<sup>n</sup>개의 입력선 중 특정 입력선을 선택하려면 n개의 선택변수가 있어야 합니다. 이 n개의 선택변수의 조합에 의해 특정 입력선이 선택됩니다.

멀티플렉서는 많은 입력선 중 하나를 선택하여 선택된 입력선의 2진 정보를 출력선에 넘겨주기 때문에 데이터 선택기라고 부르기도 하고 MUX라는 약어로 표현하기도 합니다.

아래는 4 x 1 멀티플렉서의 논리회로도입니다.

![MUX](\assets\images\Circuits\MUX.png){:  width="600" height="600"}

<br>

* 구동입력을 가진 멀티플레서(멀티플렉서 확장에 이용)

![ExtendedMUX](\assets\images\Circuits\ExtendedMUX.png){:  width="600" height="600"}

<br>

* 멀티플렉서를 이용한 부울함수 구현

멀티플렉서의 논리회로도를 보면 OR 게이트를 가진 디코더와 같은 기능을 수행하고 있는 것을 알 수 있습니다. 멀티플렉서의 선택선으로 입력변수의 최소항을 나타낼 수 있고 입력선을 이용하여 최소항들을 선택할 수 있다는 것을 의미합니다. 따라서 n개의 선탭입력과 2<sup>n</sup>개의 데이터 입력을 가진 멀티플렉서를 이용하면 n + 1개의 변수를 가진 부울함수를 구현할 수 있습니다.

![BoolFunctionMUX](\assets\images\Circuits\BoolFunctionMUX.png){:  width="600" height="600"}

1. 최소항의 변수를 MUX의 입력선과 선택선에 연결합니다.
2. 입력선에 연결되는 최소항을 결정합니다. 이것은 I<sub>0</sub>, I<sub>1</sub>, I<sub>2</sub>, I<sub>3</sub>, ... 를 결정하는 것으로서 구현표에 의해 결정됩니다.
3. 완성된 구현표에 의해 MUX에 입력단을 연결하면 부울함수를 구현할 수 있습니다.

<br>

📍F(A, B, C) = 𝛴<sub>m</sub>(1, 2, 6, 7)의 구현

![MUX_BoolFunction1](\assets\images\Circuits\MUX_BoolFunction1.png){:  width="700" height="700"}

![MUX_BoolFunction2](\assets\images\Circuits\MUX_BoolFunction2.png){:  width="700" height="700"}

<br><br>

### 📄디멀티플렉서
디멀티플렉서는 데이터 분배기라고도 하며 멀티플렉서와 반대되는 연산을 수행하는 조합논리회로입니다. DEMUX라는 약어로 표현하기도 합니다. 1개의 입력선으로부터 정보를 받아 이를 2<sup>n</sup>개의 출력선 중 하나로 내보냅니다. 이때 특정 출력선의 선택은 n개의 선택입력의 조합으로 제어합니다.

디멀티플렉서는 디코더와 유사한 관계가 있습니다. 구동입력을 가진 디코더에서 구동입력을 입력선으로 하고 원래의 입력선을 선택신호로 사용하면 디멀티플렉서가 됩니다.

![DEMUX_Decoder](\assets\images\Circuits\DEMUX_Decoder.png){:  width="600" height="600"}

<br><br>