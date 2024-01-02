---
title: "[LinearAlgebra]행렬연산"
excerpt: "행렬연산"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 행렬연산]

toc: true
toc_sticky: true

date: 2023-09-14
---

## 📚기본 개념
### 📄정방행렬
행의 수와 열의 수가 같은 n x n 행렬을 n차 **정방행렬**이라고 한다. n을 정방행렬의 차수라고 한다. a<sub>11</sub>, a<sub>22</sub>, a<sub>33</sub>, ..., a<sub>nn</sub> 원소를 주대각원소라고 한다. 주대각원소를 포함하는 대각선을 주대각선이라고 한다.

<br>

📍정방행렬

$$
\begin{pmatrix}
1 & 1 & 1 \\ 
1 & 1 & 1 \\
1 & 1 & 1 \\ 
\end{pmatrix}
$$

<br>

### 📄대각행렬
n차 정방행렬에서 대각원소 이외의 모든 원소가 0인 행렬을 **대각행렬**이라고 한다. 대각원소가 모두 같은 값인 대각행렬을 스칼라 행렬이라고 한다.

<br>

📍대각행렬

$$ 
\begin{pmatrix}
1 & 0 & 0 \\ 
0 & 2 & 0 \\
0 & 0 & 2 \\ 
\end{pmatrix}
$$

<br>

### 📄단위행렬
n차 정방행렬에서 대각원소가 모두 1이고 나머지 원소는 모두 0인 행령을 n차 **단위행렬**이라고 한다. I<sub>n</sub> 기호로 나타낸다.

<br>

📍단위행렬

$$
I_3 =   \begin{pmatrix}
        1 & 0 & 0 \\ 
        0 & 1 & 0 \\
        0 & 0 & 1 \\ 
        \end{pmatrix}
$$

<br>

### 📄영행렬
모든 원소가 0인 행렬을 영행렬이라고 한다. 아래 행렬을 3 x 3인 영행렬이다.

$$ \begin{pmatrix}
    0 & 0 & 0 \\ 
    0 & 0 & 0 \\
    0 & 0 & 0 \\
    \end{pmatrix} 
$$

<br>

### 📄삼각행렬
n차 정방행렬에서 주대각선 아래에 있는 모든 원소들이 0인 경우 **상삼각행렬**, 주대각선 위에 있는 모든 원소들이 0인 경우 **하삼각행렬**이라고 한다. 상삼각, 하삼각행렬을 삼각행렬이라고 부른다.

<br>

📍삼각행렬
<br>
* 상삼각행렬
$$  \begin{pmatrix}
    2 & 5 & 2 \\ 
    0 & 3 & 4 \\
    0 & 0 & 1 \\ 
    \end{pmatrix}
$$
<br><br>
* 하삼각행렬
$$  \begin{pmatrix}
    2 & 0 & 0 \\ 
    4 & 3 & 0 \\
    2 & 1 & 0 \\ 
    \end{pmatrix}
$$

<br><br>

## 📚행렬의 합
행렬이 수를 배열한 것이므로 더하려는 두 행렬의 크기가 같다면 쉽게 합을 정의할 수 있다. 두 행렬의 합은 우선 행렬의 크기가 서로 같은 경우를 전제로 한다. 행렬에 대한 합 연산의 정의는 다음과 같다.

A = (a<sub>ij</sub>)와 B = (b<sub>ij</sub>)를 m × n행렬이라 하면 두 행렬 A, B의 합은 m × n행렬 C = (c<sub>ij</sub>)로 다음과 같이 정의한다.

$$
c_{ij} = a_{ij} + b_{ij} (1 <= i <= m, 1 <= j <= n)
$$

두 행렬의 합은 A + B = C로 나타낸다.

<br>

* 행렬의 합
<br>
같은 크기의 행렬 A, B가 있을 때 같은 위치의 A의 원소로부터 B원소를 더해서 구해지는 행렬이다.

* 행렬의 차
<br>
같은 크기의 행렬 A, B가 있을 때 같은 위치의 A의 원소로부터 B원소를 빼서 구해지는 행렬이다.

<br>

📍두 행렬의 합에 대한 결과를 구하시오.
<br><br>
$$ A =  \begin{pmatrix}
          5 & 3 \\ 
          1 & 1 \\
          \end{pmatrix}
\quad
    B =  \begin{pmatrix}
          0 & 1 \\ 
          2 & 2 \\
          \end{pmatrix}
$$

<br>

1. A + B = ?
<br>
$$ A + B =  \begin{pmatrix}
            5 & 4 \\ 
            3 & 3 \\
            \end{pmatrix}
$$

2. A - B = ?
<br>
$$ A - B =  \begin{pmatrix}
            5 & 2 \\ 
            -1 & -1 \\
            \end{pmatrix}
$$

<br>

M<sub>mn</sub>이 m × n행렬 전체의 집합이고 A, B, C가 M<sub>mn</sub>의 임의의 원소라고 하면 행렬의 합은 다음과 같은 성질이 성립한다.

1. A + B = B + A
2. A + (B + C) = (A + B) + C
3. A + O = A (행렬 O를 m × n크기의 영행렬이라고 한다.)

<br><br>

## 📚행렬의 스칼라곱
하나의 행렬에 하나의 수를 곱하는 연산을 행렬의 스칼라 곱이라고 한다.

A = (a<sub>ij</sub>)가 m × n행렬이고 c를 임의의 수라고 하면 행렬 A와 수 c의 스칼라곱 cA는 m × n행렬이고 다음과 같이 정의한다.

$$
cA = (ca_{ij}) (1 <= i <= m, 1 <= j <= n)
$$

스칼라곱하여 얻어지는 행렬의 크기는 m × n행렬이고 (i, j) 행렬원소는 ca<sub>ij</sub>이다.

<br>

📍다음 행렬의 스칼라곱의 결과를 구하시오.

$$ 
A =  \begin{pmatrix}
      2 & 1 \\ 
      1 & -1 \\
      \end{pmatrix}
$$

* 2A = ?
<br>
$$ 2A = \begin{pmatrix}
        4 & 2 \\ 
        2 & -2 \\
        \end{pmatrix}
$$

<br>

M<sub>mn</sub>이 m × n행렬 전체의 집합이고 A, B가 M<sub>mn</sub>의 임의의 원소이며 c, d는 임의의 수라고 하면 행렬의 스칼라곱은 다음과 같은 성질이 성립한다.
1. (c + d)A = cA + dA
2. c(A + B) = cA + cB
3. c(dA) = (cd)A
4. 1A = A

<br><br>

## 📚행렬의 곱
행렬의 스칼라곱과 달리 행렬의 곱은 두 행의 곱을 의미한다. 행렬의 곱은 크기가 같은 두 행렬에 대해 대응되는 성분끼리 곱하는 것이 아니다!

두 행렬의 곱 AB를 정의하려면 A의 열의 개수와 B의 행의 개수가 같아야 한다. A가 m × p 행렬이고 B가 p × n 행렬일 때, 행렬의 곱은 m × n 행렬이 된다.

<br>

📍행렬 곱의 결과를 구하시오.
<br><br>
$$ A =  \begin{pmatrix}
          5 & 3 \\ 
          1 & 1 \\
          \end{pmatrix}
\quad
    B =  \begin{pmatrix}
          0 & 1 \\ 
          2 & 2 \\
          \end{pmatrix}
$$

* AB = ?
<br>
$$ 
AB = \begin{pmatrix}
      (5 * 0) + (3 * 2) & (5 * 1) + (3 * 2) \\ 
      (1 * 0) + (1 * 2) & (1 * 1) + (1 * 2) \\
      \end{pmatrix}
      =
      \begin{pmatrix}
      6 & 11 \\ 
      2 & 3 \\
      \end{pmatrix}
$$

<br>

행렬의 합은 일반적인 수에서의 대수적 성질과 유사하지만 행렬의 곱은 그렇지 않다. A + B = B + A는 성립하지만 AB = BA는 언제나 성립하는 것은 아니라서 행렬의 곱은 교환법칙이 성립하지 않는다.

행렬의 곱은 또 다른 특이함이 있다. 영행렬이 아닌 두 행렬의 곱이 영행렬이 되는 경우가 있다. 또한 행렬 A, B, C가 있을 때, B ≠ C임에도 AB = AC가 되기도 한다.

<br><br>

## 📚전치행렬
주어진 행렬에 대해서 원소들의 행과 열을 서로 바꾸어 배치하는 것을 행렬의 전치라고 한다.

A = (a<sub>ij</sub>)를 m × n행렬이라 하면 A의 전치행렬은 n × m행렬 A<sup>T</sup> = a<sub>ij</sub><sup>T</sup>로 다음과 같이 정의한다.

$$
(a_{ij})^{T} = a_{ji} (1 <= i <= m, 1 <= j <= n)
$$

<br>

📍행렬 A의 전치행렬을 구하시오.

$$ 
A = \begin{pmatrix}
    2 & 1  \\ 
    4 & 3  \\
    \end{pmatrix}
\quad
B = \begin{pmatrix}
    2 & 1 & 3  \\ 
    \end{pmatrix}
$$

<br>

$$
A^{T} = \begin{pmatrix}
        2 & 4  \\ 
        1 & 3  \\
        \end{pmatrix}
\quad
B^{T} = \begin{pmatrix}
        2 \\ 
        1 \\
        3 \\
        \end{pmatrix}
$$

<br>

행렬의 전치는 다음과 같은 성질이 있다.
1. (A<sup>T</sup>)<sup>T</sup> = A
2. (A + B)<sup>T</sup> = A<sup>T</sup> + B<sup>T</sup>
3. (AB)<sup>T</sup> = B<sup>T</sup>A<sup>T</sup>
4. (cA)<sup>T</sup> = cA<sup>T</sup>

A<sup>T</sup> = A인 행렬 A를 대칭행렬이라고 한다. 행렬 A가 대칭행렬이 되려면 정방행렬이어야 하고 a<sub>ij</sub> = a<sub>ji</sub>를 만족해야 한다. 따라서 대칭행렬 A는 주대각원소를 기준으로 대칭되는 위치의 행렬원소가 서로 같은 행렬이다.

<br><br>