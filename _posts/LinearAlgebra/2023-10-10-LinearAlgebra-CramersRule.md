---
title: "[LinearAlgebra]크래머 공식과 역행렬"
excerpt: "크래머 공식과 역행렬"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 크래머 공식]

toc: true
toc_sticky: true

date: 2023-10-10
---

## 📚크래머 공식
크래머 공식은 일차연립방정식의 수와 미지수의 수가 서로 같을 때 행렬식을 이용해서 미지수의 해를 구하는 해법입니다. 아래 식의 분모는 계수행렬의 행렬식을 의미하고, 분자는 계수행렬의 j열 대신 상수행렬을 열로 써 넣은 행렬식입니다.

$$
X_j = \frac{|A_j|}{|A|} (단, |A| \ne 0)
$$

📍예시

$$
\begin{cases}
3x + 2y = -4 \\
x + 2y = -2
\end{cases}
$$

<br>

$$
\begin{pmatrix}
3 & 2 \\ 1 & 2
\end{pmatrix}
\begin{pmatrix}
x \\ y
\end{pmatrix}
=
\begin{pmatrix}
-4 \\ -2
\end{pmatrix}
$$

<br>

$$
x = \frac{det\begin{pmatrix}
-4 & 2 \\ -2 & 2
\end{pmatrix}}{det\begin{pmatrix}
3 & 2 \\ 1 & 2
\end{pmatrix}}

\quad\quad

y = \frac{det\begin{pmatrix}
3 & -4 \\ 1 & -2
\end{pmatrix}}{det\begin{pmatrix}
3 & 2 \\ 1 & 2
\end{pmatrix}}
$$

$$
x = -1 \quad\quad y = -\frac{1}{2}
$$

<br><br>

## 📚행렬식과 역행렬
n차 정방행렬 A = (a<sub>ij</sub>)에 대해 (i, j) 원소 a<sub>ij</sub>가 A의 원소 a<sub>ij</sub>에 대한 여인수 A<sub>ij</sub>인 행렬을 A의 여인수행렬이라 하며 A의 여인수행렬의 전치행렬을 A의 수반행렬이라고 하고 adjA라 표시합니다.

<br>

n차 정방행렬 A = (a<sub>ij</sub>)에 대해 \|A\| ≠ 0일 때 A<sup>-1</sup>은 다음과 같습니다.

$$
A^{-1} = \frac{adjA}{|A|}
$$

<br><br>