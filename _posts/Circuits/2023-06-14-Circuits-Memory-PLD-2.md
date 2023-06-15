---
title: "[Circuits]기억장치와 PLD(2)"
excerpt: "기억장치와 PLD"

categories:
  - Circuits
tags:
  - [디지털 논리회로, 기억장치, PLD]

toc: true
toc_sticky: true

date: 2023-06-14
---

## 📚PLD
### 📄PLD의 구조와 종류
PLD는 프로그래밍이 가능한 전자 퓨즈선으로 연결된 게이트의 배열로 구성된 집적회로입니다. 디지털 시스템의 설계를 위해 PLD를 사용하며 복잡한 논리회로를 하나의 집적회로로 프로그래밍 할 수 있어서 필요한 소자들의 수와 비용을 절감할 수 있는 장점이 있습니다.

* PLD 구조

PLD는 주로 AND 게이트와 OR 게이트의 배열구조를 갖는 집적회로입니다. 초기 상태의 PLD는 각 게이트 입력에 전자적 퓨즈가 연결되어 있고 사용자가 원하는 곳의 퓨즈를 전자적으로 끊음으로써 AND-OR 연산(곱의 합)으로 조합논리회로를 구현합니다.

![PLD](\assets\images\Circuits\PLD.png){: width="600" height="600"}

<br>

* PLD 종류

![PLDTypes](\assets\images\Circuits\PLDTypes.png){: width="600" height="600"}

<br><br>

### 📄PLA의 구조
PLA는 ROM과 같은 기능을 수행하며 ROM의 단점을 해소하였습니다. ROM의 크기는 입력의 수에 따라 결정되기 때문에 입력의 수가 많고 실제 사용되는 단어의 수가 적을 때는 많은 기억공간이 낭비된다는 단점이 나타납니다. 그러나 PLA는 모든 입력변수를 디코딩하지 않고 모든 최소항도 만들지 않습니다.

PLA에서 디코더는 AND 게이트의 배열로 구성되고 입력변수의 곱항을 생성합니다. 또한 AND 배열의 출력은 OR 게이트의 배열에 연결되어 필요한 합항을 만듭니다.

![PLA](\assets\images\Circuits\PLA.png){: width="600" height="600"}

<br><br>

### 📄PAL의 구조
PAL은 OR 게이트 배열이 고정되어 있고 AND 게이트 배열은 프로그래밍 가능한 소자입니다. 따라서 PLA 보다는 프로그래밍상 제한이 따릅니다. 하지만 PAL은 PLA 보다 값이 싸고 비교적 간단한 논리함수의 구현에 효과적이기 때문에 가장 보편적으로 사용되고 있습니다. 전형적인 PAL 집적회로는 8개의 입력과 8개의 출력으로 구성되는 것이 일반적입니다.

아래는 4입력-4출력 PAL의 구조입니다.

![PALStructure](\assets\images\Circuits\PALStructure.png){: width="600" height="600"}

<br><br>