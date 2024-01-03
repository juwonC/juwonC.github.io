---
title: "[LinearAlgebra]고유값과 고유벡터"
excerpt: "고유값과 고유벡터"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 고유값, 고유벡터]

toc: true
toc_sticky: true

date: 2023-11-21
---

## 📚고유값과 고유벡터
T를 벡터공간 V에서 V로의 선형변환이고, M을 T에 대응하는 행렬이라 할 때, M에 의한 벡터 A의 변환은 일반적으로 벡터 A를 다양한 크기와 방향으로 변환시킨다.

그러나, 어떤 특정한 벡터들은 원래 벡터와 같은 방향이거나 또는 정반대 방향으로만 변환된다. 이런 벡터들을 고유벡터라고 한다.

위 내용을 예를 들어 설명해보면, 선형변환에 대응하는 행렬

$$
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
$$

이 있을 때, 대부분의 벡터는 선형변환 과정에서 크기와 방향이 바뀐다. 예를 들어

$$
\begin{pmatrix}
1 \\
1
\end{pmatrix}
$$

과 같은 벡터가 있다고 하면, 아래와 같이 크기와 방향이 바뀌고 자신의 스팬(벡터를 늘린 직선의 형태)을 벗어난다. (1, 1) 벡터가 (4, 2) 벡터로 변환된 것을 확인할 수 있다.

$$
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
\begin{pmatrix}
1 \\
1
\end{pmatrix}
=
\begin{pmatrix}
4 \\
2
\end{pmatrix}
$$

<br>

하지만 몇몇 특별한 벡터들은 자신의 고유한 스팬에 남아있다. 이것은 벡터에 스칼라 배 한 것과 같이 크기만 늘어나거나 줄어드는 형태이다. 예를 들어,

$$
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
$$

벡터를 선형변환 해보면 (-1, 1)이 방향은 같고 크기만 두 배 증가된 (-2, 2) 벡터가 나오는 것을 알 수 있다. 여기서 (-1, 1) 과 같은 벡터를 고유벡터라고 한다. 그리고 변환 도중 벡터가 늘어나거나 줄어드는 정도의 배수를 고유값이라고 한다. 이 경우에는 2가 변환의 고유값인 것이다.

$$
\begin{pmatrix}
3 & 1 \\
0 & 2
\end{pmatrix}
\begin{pmatrix}
-1 \\
1
\end{pmatrix}
=
\begin{pmatrix}
-2 \\
2
\end{pmatrix}
$$

<br>

### 📄정의
M: n차 정방행렬, λ: 실수
<br>
MA = λA를 만족하는 벡터 A가 존재(단, A ≠ O)

λ: M의 고유값(eigenvalue)
<br>
A: λ에 대응하는 M의 고유벡터(eigenvector). 영벡터 제외!

* 고유벡터: 어떤 벡터에 선형변환을 취했을 때, 방향은 변하지 않고 크기만 변환되는 벡터를 의미한다.

* 고유값: 고유벡터가 변환되는 크기를 의미한다.

<br>

📍예제

$$
M = \begin{pmatrix}
2 & 3 \\
0 & 1
\end{pmatrix}, \quad
A = \begin{pmatrix}
1 \\
0
\end{pmatrix}, \quad
B = \begin{pmatrix}
0 \\
1
\end{pmatrix}
$$ 일 때, A와 B는 M의 고유벡터인가?

(1)
$$
M = \begin{pmatrix}
2 & 3 \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
1 \\
0
\end{pmatrix} =
\begin{pmatrix}
2 \\
0
\end{pmatrix}
= 2A
$$

A는 고유값$$\lambda_1 = 2$$에 대응하는 M의 고유벡터

<br>

(2)
$$
M = \begin{pmatrix}
2 & 3 \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
0 \\
1
\end{pmatrix} =
\begin{pmatrix}
3 \\
1
\end{pmatrix}
≠ kA
$$

B는 M의 고유벡터가 아니다!

### 📄정리
* A, B: 정방행렬 M의 고유값 λ에 대응하는 고유벡터

-> A + B, kA도 λ에 대응하는 고유벡터
-> M(A + B) = MA + MB = λA + λB = λ(A + B)
-> M(kA) = kMA = k(λA) = λ(kA)

<br>

* λ: n차 정방행렬 M의 고유값

->{λ에 대응하는 모든 고유벡터들} ∪ {O}
R<sup>n</sup>공간의 부분공간이 됨.

고유값 λ에 대응하는 M의 고유공간

<br>

📍예제

고유값 λ=5에 대응하는
$$
M = \begin{pmatrix}
1 & 3 \\
4 & 2
\end{pmatrix}
$$의 고유공간을 구하라.

λ=5에 대응하는 고유벡터를
$$
A =
\begin{pmatrix}
x \\
y
\end{pmatrix}
$$라고 하면

$$
MA = 5A \quad \rightarrow \quad
\begin{pmatrix}
1 & 3 \\
4 & 2
\end{pmatrix}
\begin{pmatrix}
x \\
y
\end{pmatrix}
=
\begin{pmatrix}
x & 3y \\
4x & 2y
\end{pmatrix}
=
5\begin{pmatrix}
x \\
y
\end{pmatrix}
$$

$$\rightarrow \quad x + 3y = 5x, 4x + 2y = 5y \quad \rightarrow \quad 4x = 3y$$

$$
\rightarrow \quad
A =
\begin{pmatrix}
x \\
y
\end{pmatrix}
=
k\begin{pmatrix}
3 \\
4
\end{pmatrix}
\text{(단, k≠0)}
$$


M의 고유공간은
$$\{A|A=k\begin{pmatrix}
3 \\
4
\end{pmatrix}, \; k \in R\}$$로 1차원이다.

<br>

* 고유값과 고유벡터의 일차독립성

M: n차 정방행렬

λ<sub>1</sub>, λ<sub>2</sub>, ..., λ<sub>n</sub>: M의 서로 다른 고유값(고유값은 최대 n개 나올 수도 있고 안 나올수도 있음.)

A<sub>i</sub>: λ<sub>i</sub>에 대응하는 고유벡터

-> A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> 들은 일차독립

n차 정방행렬 M이 n개의 서로 다른 고유값을 가지면 서로 일차독립인 n개의 고유벡터를 가진다는 의미이다.

<br><br>

## 📚특성방정식
λ가 정방행렬 M의 고유값
<br>
<=> MA = λA (A ≠ O)
<br>
<=> MA - λA = MA - λIA = (M - λI)A = O
<br>
<=> \|M - λI\| = 0 (행렬 M의 특성방정식)

* 동차연릭방정식 AX = O가 오직 자명한 해만 가질 필요충분조건: \|A\| ≠ 0
* 동차연릭방정식 (M - λI)A = O가 O이 아닌 해 A를 가질 필요충분 조건: \|M - λI\| = 0

### 📄고유값과 특성방정식
M: n차 정방행렬

실수 λ가 M의 고유값 <=> λ가 M의 특성방정식의 해

* M이 삼각행렬이라면 특성방정식은?

M이 삼각행렬이라면 주대각 원소들이 고유값이다. 삼각행렬의 행렬식 값은 주대각 원소들을 곱한 것이기 때문이다.

$$
\begin{align}
&M =
\begin{pmatrix}
2 & 1 & 4 \\
0 & 1 & 5 \\
0 & 0 & 3
\end{pmatrix}\\
\\
&|M - \lambda I_3| =
\begin{vmatrix}
2 - \lambda & 1 & 4 \\
0 & 1 - \lambda & 5 \\
0 & 0 & 3 - \lambda
\end{vmatrix} \\
\\
&\lambda = 1, 2, 3
\end{align}
$$

<br>

### 📄특성방정식의 활용
M: n차 정방행렬

1. 특성방정식을 이용하여 고유값을 구한다.
<br>
-> \|M - λI<sub>n</sub>\| = 0를 풀어서 고유값 λ를 구할 수 있다.
<br><br>
2. 각 고유값에 대응하는 고유벡터를 구한다.
<br>
-> (M - λI<sub>n</sub>)A = O를 풀어서 고유벡터 A를 구할 수 있다.
<br><br>
3. 각 고유값에 대응하는 고유벡터를 표현해주는 일차독립인 벡터를 구하여 고유공간의 기저를 구한다.

📍예제

다음 행렬의 고유값과 고유벡터를 구하시오.

$$
M =
\begin{pmatrix}
1 & 9 \\
0 & 4
\end{pmatrix}
$$

(1) 고유값

$$
\begin{align}
|M - \lambda I_2| &=
\begin{vmatrix}
1 - \lambda & 9 \\
0 & 4 - \lambda
\end{vmatrix} \\
\\
&= (1 - \lambda)(4 - \lambda) = 0 \\
&\lambda = 1, 4
\end{align}
$$

(2)고유벡터 A = (x, y)<sup>T</sup>

* λ<sub>1</sub> = 1일 때

$$
(M - \lambda_1 I_2)A =
\begin{pmatrix}
0 & 9 \\
0 & 3
\end{pmatrix}
\begin{pmatrix}
x \\
y
\end{pmatrix}
=
\begin{pmatrix}
9y \\
3y
\end{pmatrix}
=
\begin{pmatrix}
0 \\
0
\end{pmatrix}
$$

$$ \text{y = 0, x는 임의의 실수} $$

$$ A = (x, 0)^T, \; (x \neq 0) $$

* λ<sub>2</sub> = 4일 때

$$
(M - \lambda_2 I_2)A =
\begin{pmatrix}
-3 & 9 \\
0 & 0
\end{pmatrix}
\begin{pmatrix}
x \\
y
\end{pmatrix}
=
\begin{pmatrix}
-3x + 9y \\
0
\end{pmatrix}
=
\begin{pmatrix}
0 \\
0
\end{pmatrix}
$$

$$ 3x = 9y \rightarrow x = 3y $$

$$ A = (3y, y)^T, \; (y \neq 0) $$

<br><br>