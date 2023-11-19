---
title: "[LinearAlgebra]선형변환"
excerpt: "선형변환"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 선형변환]

toc: true
toc_sticky: true

date: 2023-11-19
---

## 📚사상
선형변환을 다루기 앞서 사상에 대해 살펴본다.

ƒ ⊂ A ✕ B가 A에서 B로 함수 또는 사상이라고 하는 것은 A의 임의의 원소 a에 대해 B의 원소 b가 유일하게 존재해서 (a, b) ∈ ƒ가 성립한다는 것이다.

순서열 (A, B, ƒ)를 ƒ : A → B로 나타내고 A에서 B로의 사상 ƒ라고 한다. 사상 (A, B, ƒ)에서 A를 정의역, B를 공번역, ƒ를 그래프라고 한다.

* A' ⊂ A일 때, A'의 ƒ에 의한 상

ƒ(A') = { f(a) \| a ∈ A' } ⊂ B

<br>

* B' ⊂ B일 때, B'의 ƒ에 의한 원상

ƒ<sup>-1</sup>(B') = { a ∈ A \| ƒ(a) ∈ B' } ⊂ A

<br>

A에서 B로의 사상 ƒ(ƒ: A → B)
1. ƒ(A) = B를 만족하면 전사사상이라고 한다.(공역 = 치역)
2. B의 임의의 원소 b에 대해 ƒ<sup>-1</sup>(B')가 공집합 또는 오직 하나의 원소일 때 ƒ를 단사사상이라고 한다.
3. 전사이면서 단사인 경우 전단사사상이라고한다.

<br>

사상 T에 대응하는 행렬

T: R<sup>2</sup> → R<sup>3</sup>

T(x, y) = (x + y, x - y, 2x + y)를 행렬로 표현이 가능하다.

$$
\begin{pmatrix}
1 & 1 \\ 
1 & -1 \\
2 & 1 \\
\end{pmatrix}
\begin{pmatrix}
x \\ 
y \\
\end{pmatrix}
=
\begin{pmatrix}
x + y \\ 
x - y \\
2x + y \\
\end{pmatrix}
$$

MA = T(x, y) 형태로 표현이 가능하다.

<br><br>

## 📚선형변환
V, W: 벡터공간
<br>
T: V → W(사상)
<br>
벡터공간 V의 두 벡터 A, B와 실수체의 원소 k에 대해 다음 두 성질을 만족할 때 T를 V에서 W로의 선형변환이라고 한다.

1. T(A + B) = T(A) + T(B)
2. T(kA) = kT(A)

선형변환은 **두 연산(벡터끼리의 덧셈연산, 벡터와 실수와의 곱셈연산)을 보존한다.**

그리고 선형변환은 **일차결합도 보존한다.**

T(kA + lB) = T(kA) + T(lB) = kT(A) + lT(B)

벡터 A, B의 일차결합인 kA + lB를 선형변환 T로 보내면 실수 k, l을 보존하고 T(A)와 T(B)의 일차결합으로 변환시킨다.

<br>

T: V → W(선형변환)
<br>
A, B를 벡터공간 V의 벡터라고 하면 다음이 성립한다.

1. T(O) = O (덧셈의 항등원 보존)
2. T(-A) = -T(A) (덧셈에 대한 역원 보존)
3. T(A - B) = T(A) - T(B) (뺄셈도 보존)

<br>

### 📄선형변환 행렬 표현
R<sup>n</sup> 벡터공간에서 정의된 선형변환이 주어졌을 때 이에 대응하는 행렬을 구한다.

T: R<sup>m</sup> → R<sup>n</sup>(선형변환)

T에 대응되는 행렬 M(n × m행렬)

$$
M = (T(E_1) T(E_2) ... T(E_m))
$$

E<sub>1</sub>, E<sub>2</sub>, ..., E<sub>m</sub>은 기본벡터이고 T(E<sub>i</sub>)는 열벡터로 쓴다.

<br>

📍예제

T: R<sup>3</sup> → R<sup>2</sup>(선형변환)

T가 T(E<sub>1</sub>) = (2, 1), T(E<sub>2</sub>) = (-2, 5), T(E<sub>3</sub>) = (7, 3)으로 주어질 때 T에 대응하는 행렬과 선형변환 T를 구하라.

R<sup>3</sup>의 임의의 벡터를 A = (x, y, z)라고 하면 아래와 같이 나타낼 수 있다.

$$
T(A) = T(x, y, z) =
\begin{pmatrix}
2 & -2 & 7 \\ 
1 & 5 & 3 \\
\end{pmatrix}
\begin{pmatrix}
x \\ 
y \\
z \\
\end{pmatrix}
$$

따라서 T에 대응하는 행렬은
$$
\begin{pmatrix}
2 & -2 & 7 \\ 
1 & 5 & 3 \\
\end{pmatrix}
$$
이고,

선형변환은 T(x, y, z) = (2x -2y + 7z, x + 5y + 3z) 이다.

<br>

### 📄선형변환의 합성
S: U → V, T: V → W(선형변환)
<br>
U의 임의의 벡터 A에 대해
<br>
T ∘ S(A) = T(S(A))로 정의한다.

그러면 T ∘ S: U → W는 선형변환이다. (T ∘ S는 U에서 W로의 선형변환)
<br><br>
위의 정리에서 S에 대응하는 행렬을 **M**,
<br>
T에 대응하는 행렬을 **N**이라고 할 때,
<br>
T ∘ S에 대응하는 행렬은 **NM**이다.

<br><br>

## 📚선형변환 성질
### 📄기본성질
T: V → W(선형변환)

$$
\begin{gather}
T(k_1A_1 + k_2A_2 + ... + k_nA_n) \\
= k_1T(A_1) + k_2T(A_2) + ... + k_nT(A_n) \\
\\
\\
T(\sum{k_iA_i}) = \sum{k_i}T(A_i)
\end{gather}
$$

<br>

### 📄기저의 상으로 선형변환 결정
T: V → W

$$
\begin{gather}
\tilde{A} = \{A_1, A_2, ..., A_n\} = \text{V의 기저 (dimV = n)}
\\
\forall B_i \in W(i = 1, 2, ..., n)
\\
T(A_i) = B_i \text{만족하는 선형변환 유일하게 존재}
\end{gather}
$$

<br>

### 📄부분공간
T: V → W
<br>
V' < V → T(V') < W

T가 벡터공간 V에서 벡터공간 W로의 선형변환일 때 V'을 V의 부분공간이라고 하면 T(V')은 W의 부분공간이다.

T(V) < W

T(V)는 W의 부분공간이 된다. T(V)를 T에 의한 V의 상이라고 하고 Im(T)로 표기한다. (W 안에 있는 치역)

<br><br>