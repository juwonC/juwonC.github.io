---
title: "[LinearAlgebra]행렬의 대각화"
excerpt: "행렬의 대각화"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 행렬의 대각화]

toc: true
toc_sticky: true

date: 2023-11-22
---

## 📚행렬의 대각화 가능성
### 📄대각행렬의 특성
M, N: n차 대각행렬(주대각 원소 이외의 원소들이 모두 0인 행렬)

1. MN도 대각행렬: 두 대각행렬의 곱은 대각행렬이다.

2. 대각행렬의 행렬식: 주대각 원소들을 모두 곱한 값이다.

3. 대각행렬의 역행렬: 대각행렬 형태이다. 주대각 원소들의 역원 형태.

4. 대각행렬의 고유값: 주대각 원소들이 고유값이 된다.

5. 대각행렬의 거듭제곱: 여전히 대각행렬 형태이다. 주대각 원소들을 거듭제곱한 형태.

대각행렬이 아닌 행렬을 거듭제곱하는 것은 쉽지 않다.
<br>
-> 대각행렬이 아닌 행렬을 대각행렬처럼 만들면 계산 수월해질 것이다.

<br>

### 📄대각화 가능성
$$
M =
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix},
A =
\begin{pmatrix}
1 \\
1
\end{pmatrix},
B =
\begin{pmatrix}
1 \\
0
\end{pmatrix},
C =
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
$$

$$
MB =
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
\begin{pmatrix}
1 \\
0
\end{pmatrix},
=
\begin{pmatrix}
3 \\
0
\end{pmatrix}
=
3
\begin{pmatrix}
1 \\
0
\end{pmatrix}
= 3B
$$

$$
MC =
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
\begin{pmatrix}
-1 \\
1
\end{pmatrix},
=
\begin{pmatrix}
-2 \\
2
\end{pmatrix}
=
2
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
= 2C
$$

$$
M(B \quad C) =
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
\begin{pmatrix}
1 & -1 \\
0 & 1
\end{pmatrix},
=
\begin{pmatrix}
3 & -2 \\
0 & 2
\end{pmatrix}
=
(3B \quad 2C)
=
\begin{pmatrix}
B & C \\
\end{pmatrix}
\begin{pmatrix}
3 & 0 \\
0 & 2
\end{pmatrix}
$$

위 식을 살펴보면 행렬 M에 고유벡터들로 만들어진 행렬(B C)를 곱하면 고유벡터들로 구성된 행렬(B C)와 고유값들을 주대각 원소로 갖는 대각행렬의 곱과 같다는 것을 알 수 있다.

MP = PN

* P = (B C) (eigenvector matrix)
* N =
$$\begin{pmatrix}
3 & 0 \\
0 & 2
\end{pmatrix}$$ (eigenvalue matrix) 이것은 대각행렬이다!

위 식으로 부터 아래와 같은 식을 만들어 볼 수 있다.

M = PNP<sup>-1</sup>

<br>

* 대각화 가능

M, N: n차 정방행렬
D: 대각행렬

1. N = PMP<sup>-1</sup>를 만족하는 P가 존재 <=> M과 N이 유사하다(M과 N은 닮은 행렬, 또는 상사행렬) N = PMP<sup>-1</sup> <=> M = P<sup>-1</sup>NP

2. M과 D(대각행렬)가 유사하다. 즉, M = PDP<sup>-1</sup> <=> M이 대각화 가능하다

📍대각화 불가능

$$
M =
\begin{pmatrix}
0 & 0 \\
1 & 0
\end{pmatrix}
$$

$$
D =
\begin{pmatrix}
p & 0 \\
0 & q
\end{pmatrix},
\quad
P =
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$

$$
\begin{pmatrix}
p & 0 \\
0 & q
\end{pmatrix}
=
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
\begin{pmatrix}
0 & 0 \\
1 & 0
\end{pmatrix}
\frac{1}{ad - bc}
\begin{pmatrix}
d & -b \\
-c & a
\end{pmatrix}
=
\frac{1}{ad - bc}
\begin{pmatrix}
bd & -b^2 \\
-d^2 & bd
\end{pmatrix}
$$

대각행렬이 되려면 b와 d가 0이 되어야하는데 그러면 행렬식(판별식)이 0이 되므로 정칙행렬 P는 존재하지 않게 된다.(역행렬이 존재하지 않는다.) 따라서 행렬 M은 대각화가 불가능하다.

<br><br>

## 📚행렬의 대각화
n차 정방행렬 M이 대각화 가능하다. -> M의 거듭제곱도 쉽게 구할 수 있다.

1. 어떤 행렬이 대각화 가능할까?
2. 대각화 가능하다면 M = PDP<sup>-1</sup>를 만족하는 정칙행렬 P와 대각행렬 D는 어떻게 구할까?

<br>

### 📄어떤 행렬이 대각화 가능할까?
n차 정방행렬 M이 서로 **일차독립**인 **n개의 고유벡터**를 가지면 => M은 대각화 가능하다.

예를 들어, 3차 정방행렬 M이 있을 때, 행렬 M이 3개의 고유벡터를 가지고 그 고유벡터들이 서로 일차독립이면 M은 대각화 가능하다.

<br>

### 📄정칙행렬 P와 대각행렬 D는 어떻게 구할까?
M의 고유값 λ<sub>1</sub>, λ<sub>1</sub>, ..., λ<sub>1</sub>에 각각 대응하는 M의 고유벡터 λ<sub>1</sub>, λ<sub>1</sub>, ..., λ<sub>1</sub>이 서로 일차독립이면 정칙행렬 P, 대각행렬 D가 존재하여 M = PDP<sup>-1</sup>을 만족한다.

$$
P =
\begin{pmatrix}
A_1 & A_2 & ... & A_n
\end{pmatrix}
\quad
D =
\begin{pmatrix}
\lambda_1 & 0 & ... & 0 \\
0 & \lambda_2 & ... & 0 \\
... & ... &  & ... \\
0 & 0 & ... & \lambda_n \\
\end{pmatrix}
$$

<br>

* 대각화 가능 따름정리

n차 정방행렬 M이 n개의 서로 다른 **고유값**을 가지면 M은 대각화 가능하다.

-> 바로 전에 알아보았던 n차 정방행렬 M이 n개의 서로 다른 고유값을 가지면 서로 일차독립인 n개의 고유벡터를 가진다는 정리에 의해 위의 따름정리로 정방행렬 M이 대각화 가능하다는 것을 알 수 있다.

위 정리를 반대로 생각해보면 다음과 같다.

n차 정방행렬 M이 대각화 가능하면 M은 서로 일차 독립인 n개의 고유벡터를 가진다.

정칙행렬 P, 대각행렬 D가 존재하여 M = PDP<sup>-1</sup>을 만족하고 이때

$$
P^{-1}MP = D =
\begin{pmatrix}
d_1 & 0 & ... & 0 \\
0 & d_2 & ... & 0 \\
... & ... &  & ... \\
0 & 0 & ... & d_n \\
\end{pmatrix}
$$

d<sub>1</sub>, d<sub>2</sub>, ..., d<sub>n</sub>은 M의 고유값이고,
<br>
P의 i번째 열벡터는 d<sub>i</sub>에 대응하는 M의 고유벡터이다.

<br>

📍예제 P와 D 구하기

$$
M =
\begin{pmatrix}
3 & 2 & 1 & 0 \\
0 & -1 & -2 & -3 \\
0 & 0 & 1 & -1 \\
0 & 0 & 0 & 0 \\
\end{pmatrix}
$$

* 대각행렬 D

M은 상삼각행렬이므로 주대각원소들이 고유값이다. 그리고 이 고유값들(3, -1, 1, 0)이 모두 다르기 때문에 이 행렬은 대각화 가능하다.

대각행렬 D는 고유값들을 주대각원소로 갖는 대각행렬이므로 아래와 같다.

$$
D =
\begin{pmatrix}
3 & 0 & 0 & 0 \\
0 & -1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 0 \\
\end{pmatrix}
$$

<br>

* 정칙행렬 P

정칙행렬 P는 순서대로 각 고유값에 대응하는 고유벡터들을 열벡터로 구성한 행렬이다.

P에 들어갈 첫 번째 열벡터를 A<sub>1</sub>=(a b c d)<sup>T</sup>라 두고 (M - 3I)A<sub>1</sub> = O를 구해보면 아래와 같다.

$$
(M - 3I_2)A_1 =
\begin{pmatrix}
3 - 3 & 2 & 1 & 0 \\
0 & -1 - 3 & -2 & -3 \\
0 & 0 & 1 - 3 & -1 \\
0 & 0 & 0 & 0 - 3 \\
\end{pmatrix}
\begin{pmatrix}
a \\
b \\
c \\
d
\end{pmatrix}
=
\begin{pmatrix}
0 \\
0 \\
0 \\
0
\end{pmatrix}
$$

$$
\begin{cases}
-4b -2c -3d = 0 \\
-2c -d = 0 \\
-3d = 0
\end{cases}
$$

$$
A_1 = k_1
\begin{pmatrix}
1 \\
0 \\
0 \\
0
\end{pmatrix}
(k_1 \neq 0)
$$

위 과정을 반복해서 각 고유값에 대응하는 고유벡터들을 구하면 다음과 같다.

$$
A_1 = k_1
\begin{pmatrix}
1 \\
0 \\
0 \\
0
\end{pmatrix}
(k_1 \neq 0)
\quad
A_2 = k_2
\begin{pmatrix}
1 \\
-2 \\
0 \\
0
\end{pmatrix}
(k_2 \neq 0)
$$

$$
A_3 = k_3
\begin{pmatrix}
1 \\
-2 \\
2 \\
0
\end{pmatrix}
(k_3 \neq 0)
\quad
A_4 = k_4
\begin{pmatrix}
3 \\
-5 \\
1 \\
1
\end{pmatrix}
(k_4 \neq 0)
$$

마지막으로 정칙행렬 P를 구해보면 아래와 같다.

$$
P =
\begin{pmatrix}
1 & 1 & 1 & 3 \\
0 & -2 & -2 & -5 \\
0 & 0 & 2 & 1 \\
0 & 0 & 1 & 1
\end{pmatrix}
$$

<br><br>