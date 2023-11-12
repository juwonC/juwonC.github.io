---
title: "[LinearAlgebra]기저와 차원"
excerpt: "기저와 차원"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 기저, 차원]

toc: true
toc_sticky: true

date: 2023-11-12
---

## 📚일차결합
벡터공간 V의 부분공간 S에 대해, 임의의 실수 k<sub>1</sub>, k<sub>2</sub>, ..., k<sub>n</sub>과 S의 원소 A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>의 곱인 k<sub>1</sub>A<sub>1</sub> + k<sub>2</sub>A<sub>2</sub> + ... + k<sub>n</sub>A<sub>n</sub>을 A<sub>1</sub>, A<sub>1</sub>, ..., A<sub>1</sub>의 일차결합(linear combination)이라고 한다.

### 📄벡터의 일차결합 표현

C, A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>m</sub> ∈ R<sup>n</sup>일 때,  C가 A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>m</sub>)의 일차결합으로 표현 가능 <=> 행렬방정식 AK = C의 해가 존재(A, K, C를 열벡터로 한다.)

$$
\begin{pmatrix}
A_1 & A_2 & ... & A_m
\end{pmatrix}
\begin{pmatrix}
k_1 \\ 
k_2 \\
... \\
k_m \\
\end{pmatrix}
=
\begin{pmatrix}
c_1 \\ 
c_2 \\
... \\
c_n \\
\end{pmatrix}
=
C
$$

<=> rank(A) = rank(A\|C)

<br><br>