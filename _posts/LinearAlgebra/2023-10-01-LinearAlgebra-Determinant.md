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
행렬식(Determinant)이란 정방행렬에 고유한 실수 값을 대응시키는 함수이다. 정방행렬 A의 행렬식은 |A| 또는 det A로 표현한다.

* 소행렬(submatrix): A=(a<sub>ij</sub>)를 n차 정방행렬이라고 할 때, A에서 i번째 행과 j번째 열을 제거시켜 구성되는 (n - 1)차 정방행렬을 A의 (i, j) 소행렬이라고 한다.

* 소행렬식(minor): 소행렬의 행렬식을 A의 원소 a<sub>ij</sub>에 대한 소행렬식이라고 하고 M<sub>ij</sub>로 표시한다.

* 여인수(cofactor): A<sub>ij</sub> = (-1)<sup>i+j</sup>M<sub>ij</sub>로 정의되는 A<sub>ij</sub>를 A의 원소 a<sub>ij</sub>에 대한 여인수라고 한다.

<br>

1차 정방행렬 A = (a)에 대해 \|A\| = a이고 n >= 2일 때 n차 정방행렬 A(<sub>ij</sub>)에 대해

$$
\begin{align}
|A| &= a_{11}A_{11} + a_{12}A_{12} + ... + a_{1n}A_{1n} \\
    &= \sum_{j = 1}^{n} a_{1j}A_{1j}
\end{align}
$$

위 식을 첫 번째 행에 의한 행렬식 \|A\|의 여인수 전개 또는 라플라스 전개라고 한다.

<br><br>

## 📚행렬식의 성질

* n차 정방행렬 A=(a<sub>ij</sub>)가 영행을 갖는다면 \|A\|=0이다.

* n차 정방행렬 A=(a<sub>ij</sub>)에 기본행연산 R<sub>i,j</sub>를 적용하여 얻은 행렬을 B라 하면 \|B\|=-\|A\|이다.

* n차 정방행렬 A=(a<sub>ij</sub>)에 기본행연산 R<sub>i</sub>(c)를 적용하여 얻은 행렬을 B라 하면 \|B\|=c\|A\|가 성립된다.

* n차 정방행렬 A=(a<sub>ij</sub>)에 기본행연산 R<sub>i,j</sub>(c)를 적용하여 얻은 행렬을 B라 하면 \|B\|=\|A\|이다.

* n차 삼각행렬 A=(a<sub>ij</sub>)의 행렬식 \|A\|는 다음과 같다.

$$ |A|=a_{11}a_{12}...a_{nm} = \prod_{i=1}^{n} a_{ii} $$

<br><br>

## 📚행렬연산과 행렬식

기본행연산 R<sub>ij</sub>, R<sub>i</sub>(c), R<sub>i,j</sub>(c)에 대한 n차 기본행렬을 각각 E<sub>ij</sub>, E<sub>i</sub>(c), E<sub>i,j</sub>(c)라고 하면 다음이 성립한다.

1. \\(\|E_{i,j}\|=-1\\)
2. \\( \|E_{i}(c)\|=c \\)
3. \\( \|E_{i,j}(c)\|=1 \\)

<br><br>