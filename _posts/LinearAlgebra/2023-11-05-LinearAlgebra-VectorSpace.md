---
title: "[LinearAlgebra]벡터공간"
excerpt: "벡터공간"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 벡터공간]

toc: true
toc_sticky: true

date: 2023-11-05
---

## 📚체(field)
대표적인 체로 유리수 집합, 실수 집합, 복소수 집합이 있다.

덧셈과 곱셈을 집합안에서 소화할 수 있는 집합을 체라고 한다.

연산 -> 사칙연산 -> 덧셈, 곱셈

뺄셈과 나눗셈은 덧셈과 곱셈의 역연산을 이용해서 역원을 더하거나 곱해서 구할 수 있다.

a - b = a + (-b)<br>
a / b = a * b<sup>-1</sup>

집합 F의 원소를 k, l, m으로 표시할 때, 집합 F가 두 연산 덧셈과 곱셈에 대해 닫혀 있고 다음의 성질을 만족할 때 이 집합 F를 체(field)라고 한다. 체의 원소를 스칼라(scalar)라고 한다.

▶체의 표기
<br>
<F, +, •>

1. k + l = l + k (덧셈의 교환법칙)
2. k + (l + m) = (k + l) + m (덧셈의 결합법칙)
3. 덧셈의 항등원 0이 있어, k + 0 = k가 성립
4. 덧셈의 역원인 -k가 있어 k + (-k) = 0이 성립
5. k • l = l • k (곱셈의 교환법칙)
6. k • (l • m) = (k • l) • m (곱셈의 결합법칙)
7. 곱셈의 항등원 1이 있어 k • 1 = k가 성립
8. 0이 아닌 k에 대해 곱셈의 역원 k<sup>-1</sup>이 있어 k • k<sup>-1</sup> = 1이 성립
9. k • (l + m) = k • l + k • m (분배법칙)

💡닫혀있다<br>
어느 수 집합에 속한 두 수를 연산 했을 때 그 결과가 두 수와 같은 집합에 속하면 닫혀있다고 한다. 예를 들어, 두 실수를 더한 결과는 실수이므로 실수는 덧셈에 대해 닫혀있다고 할 수 있다.
{: .notice--warning}

<br><br>

## 📚벡터공간(vector space)
집합 V의 원소를 A, B, C... 로 표시하고,
체 F의 원소를 k, l로 표시할 때, 두 가지 연산(덧셈과 곱셈)에 대해 다음 조건을 만족하면 V를 체 F위에 정의된 벡터공간이라고 하며, V의 원소를 벡터라고 한다.

▶벡터공간 V의 표기
<br>
<V, +, •, F> 또는 <V, +, •> over F

1. V는 덧셈에 관해 닫혀있고 다음을 만족
* A + B = B + A
* (A + B) + C = A + (B + C)
* 임의의 원소 A∈V에 대해 항등원 O이 있어 A + O = A가 성립.(항등원 O를 영벡터라고 한다.)
* 임의의 원소 A∈V에 대해 덧셈의 역원 -A가 있어 A + (-A) = O가 성립

2. V는 곱셈에 관해 닫혀있고 다음을 만족
* (kl)•A = k•(l•A)
* k • (A + B) = k • A + k • B
* (k + l) • A = k • A + l • A
* 1 • A = A

<br>

* 벡터공간의 예

원소가 실수인 m × n 행렬 전체 집합 M<sub>mn</sub>(R)은 체를 실수 집합 R로 선택하고, 벡터 공간의 두 연산(합, 곱)을 각각 행렬의 합과 행렬의 스칼라 곱으로 정의하면 벡터 공간이 된다.

1. m = 1인 경우 (M<sub>1n</sub>(R))를 n차 행벡터공간이라고 한다.
2. n = 1인 경우 (M<sub>m1</sub>(R))를 m차 열벡터공간이라고 한다.

<br><br>

## 📚부분공간(subspace)
V를 체 F위의 벡터공간이라 할 때 V의 부분집합 S가 다음 두 가지 성질을 만족하면 집합 S를 벡터공간 V의 부분공간이라 한다.

1. A, B ∈ S이면 A + B ∈ S이다.
2. A ∈ S, k ∈ F 이면 kA ∈ S이다.
<br>
-> S가 덧셈과 곱세에 관해 닫혀있다.
<br>
-> A, B ∈ S, k,l ∈ F이면 kA + lB ∈ S이다.

▶부분공간 표기
<br>
S < V(S는 V의 부분공간)

<br><br>

## 📚정리
### 📄체
유리수, 실수, 복소수 등의 집합과 그 집합에 정의된 2가지 연산(덧셈과 곱셈)에 관해 닫혀 있고 아래 성질을 만족하면 체라고 한다.
<br>
▶ 각 연산에 관해 닫혀 있고
<br>
▶ 각 연산에 관해
<br>
　　▷교환법칙, 결합법칙, 분배법칙이 가능
<br>
　　▷항등원과 역원이 존재

<br>

### 📄벡터공간
R<sup>n</sup>공간에서의 성질의 확장
* 두 연산(벡터의 합, 벡터의 스칼라 곱)
* 두 연산의 성질 8가지(교환법칙, 결합법칙, 항등원, 역원, 분배법칙)

벡터공간의 예
1. 실수 성분으로 된 행렬들의 집합; M<sub>mn</sub>(R)
2. 실수에서 정의된 다항식들의 집합; P(R)
3. 정의구역이 실수인 연속함수들의 집합; C(R)

위의 예들을 모두 벡터라고 부를 수 있다. -> 두 연산의 8가지 성질을 모두 만족하고 벡터공간의 원소는 벡터라고 부르기로 약속했기 때문이다.

<br>

### 📄부분공간
* 벡터공간 V의 부분집합 S (S ⊂ V)
* 벡터공간 V의 연산을 유지하되, 다음 조건을 만족

1. A, B ∈ S이면 A + B ∈ S이다.
2. A ∈ S, k ∈ F 이면 kA ∈ S이다.
<br>
-> A, B ∈ S, k,l ∈ F이면 kA + lB ∈ S이다.

<br><br>