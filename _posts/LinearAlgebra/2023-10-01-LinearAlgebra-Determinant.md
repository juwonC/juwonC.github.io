---
title: "[LinearAlgebra]행렬식"
excerpt: "행렬식"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 행렬식]

toc: true
toc_sticky: true

date: 2023-10-01
---

## 📚행렬식
행렬식(Determinant)이란 정방행렬에 고유한 실수 값을 대응시키는 함수입니다. 정방행렬 A의 행렬식은 |A| 또는 det A로 표현합니다.

* 소행렬(submatrix): A=(a<sub>ij</sub>)를 n차 정방행렬이라고 할 때, A에서 i번째 행과 j번째 열을 제거시켜 구성되는 (n - 1)차 정방행렬을 A의 (i, j) 소행렬이라고 합니다.

* 소행렬식(minor): 소행렬의 행렬식을 A의 원소 a<sub>ij</sub>에 대한 소행렬식이라고 하고 M<sub>ij</sub>로 표시합니다.

* 여인수(cofactor): A<sub>ij</sub> = (-1)<sup>i+j</sup>M<sub>ij</sub>로 정의되는 A<sub>ij</sub>를 A의 원소 a<sub>ij</sub>에 대한 여인수라고 합니다.

<br>

1차 정방행렬 A = (a)에 대해 |A| = a이고 n >= 2일 때 n차 정방행렬 A(<sub>ij</sub>)에 대해

<br>

$$
\begin{align}
|A| &= a_{11}A_{11} + a_{12}A_{12} + ... + a_{1n}A_{1n} \\
    &=  \sum^{n}_{j = 1}a_{1j}A_{1j}
\end{align}
$$

<br>

위 식을 첫 번째 행에 의한 행렬식 |A|의 여인수 전개 또는 라플라스 전개라고 합니다.

<br><br>