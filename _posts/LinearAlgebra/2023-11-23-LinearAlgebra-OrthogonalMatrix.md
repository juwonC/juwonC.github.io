---
title: "[LinearAlgebra]내적공간과 직교행렬"
excerpt: "내적공간과 직교행렬"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 내적공간, 직교행렬]

toc: true
toc_sticky: true

date: 2023-11-23
---

## 📚내적공간과 직교벡터
일반 벡터공간에서의 내적

벡터공간 V의 임의의 두 벡터 A, B에 대해 실수 <A, B>를 대응시키는 관계가 다음을 만족할 때 <A, B>를 A와 B의 내적이라고 한다.

A, B, C ∈ V, k ∈ R(실수집합)

1. <A, B> = <B, A>
2. <A, B + C> = <A, B> + <A, C>
3. <kA, B> = k<A, B>
4. <A, A> >= 0 이고, <A, A> = 0일 필요충분조건은 A = O

<br>

### 📄내적공간
벡터공간에 내적을 고려해서 내적이 포함된 벡터공간을 내적공간이라고 한다.

<, >: 벡터공간 V에 정의된 내적

-> V를 내적공간(inner product space). {V, <, >}로 표시한다.

예) R<sup>n</sup>벡터공간은 내적공간으로서 {R<sup>n</sup>, ·}

<br>

### 📄내적공간의 벡터크기

* R<sup>n</sup> 내적공간의 벡터 A의 크기

$$ | A | = \sqrt{(A \cdot A)} = \sqrt{a^{2}_{1} + a^{2}_{2} + ... + a^{2}_{n}} $$

<br>

* 일반 내적공간 {V, <, >}의 벡터 A의 크기

$$ || A || = \sqrt{<A, A>} $$

<br>

### 📄벡터 사이의 각(사이각)

* Schwarz부등식

내적공간 {V, <, >}에서 임의의 벡터 A, B ∈ V에 대하여

$$ | \; <A, B> | \; \le \; ||A|| \; ||B|| $$

A와 B의 내적의 크기(절대값)는 각각의 A, B크기의 실수 곱 보다 작거나 같다.

<br>

O벡터가 아닌 A, B에 대해 Schwarz 부등식

$$ | \; <A, B> | \; \le \; ||A|| \; ||B|| $$

$$ \frac{| \; <A, B> |}{||A|| \; ||B||} \le 1 $$

$$ -1 \le \frac{<A, B>}{||A|| \; ||B||} \le 1 $$

$$ cos\theta \equiv \frac{<A, B>}{||A|| \; ||B||} (0 \le \theta \le \pi) $$

벡터 A와 B 사이의 각이 $$ \theta $$라고 약속해서 사용.

<br>

### 📄벡터의 직교
<A, B> = 0이면 cosθ = 0이므로 θ = 90도 -> A와 B는 직교(orthogonal)한다.

* 직교벡터들의 일차독립성
내적공간 {V, <, >}에서
<br>
벡터 A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>(단, A<sub>i</sub> ≠ O)이 서로 **직교**하면 이 벡터들은 **일차독립**이다.

* 직교집합(orthogonal set): 서로 직교인 O이 아닌 벡터(직교벡터)들의 집합

* 단위직교집합(orthonormal set): 길이가 1인 직교벡터들의 집합

📍예제

{R<sup>3</sup>, ·}, S = {A<sub>1</sub>, A<sub>2</sub>, A<sub>3</sub>}

$$ A^{T}_{1} = (1 \quad 1 \quad 1), A^{T}_{2} = (1 \quad -2 \quad 1), A^{T}_{3} = (1 \quad 0 \quad -1) $$

$$
\begin{gather}
A_1 \cdot A_2 = 1-2+1 = 0 \\
A_2 \cdot A_3 = 1+0-1 = 0 \\
A_3 \cdot A_1 = 1+0-1 = 0 \\
\rightarrow \text{S는 직교집합(기저)}
\end{gather}
$$

$$
\begin{gather}
|A_1| = \sqrt{3}, \quad |A_2| = \sqrt{6}, \quad |A_3| = \sqrt{2} \\
\rightarrow \text{S는 단위직교집합 아니다.}
\end{gather}
$$

위 집합을 단위직교집합으로 만들려면 어떻게 해야 할까?

-> 벡터 자신을 자기 자신의 길이로 나눠주면 된다.(정규화)

$$
B_i = \frac{A_i}{| A_i |}
$$

$$
\begin{gather}
B_1 = \frac{1}{\sqrt{3}}A_1 \\
B_2 = \frac{1}{\sqrt{6}}A_2 \\
B_3 = \frac{1}{\sqrt{2}}A_3 \\
\rightarrow S_{unit} = \{B_1, B_2, B_3\}\text{는 단위직교집합}
\end{gather}
$$

<br>

### 📄직교보공간
내적공간 {V, <, >}에서
<br>
벡터 A가 V의 부분공간 U의 모든 벡터들과 직교하면, 벡터 A는 U와 직교한다.

U와 직교하는 V의 모든 벡터들의 집합을
<br>
U의 직교보공간(orthogonal complement)이라고 한다.

$$
U^\perp = \{A \in V \; | \; \forall B \in U, <A, B> = 0\}
$$

$$
U \cup U^\perp = V \; \text{(보 관계)}
$$

어떤 부분공간에 대응해서 직교하는 벡터들만 모아놓은 부분공간이라고 이해.

<br>

* 직교보공간의 성질

내적공간 {V, <, >}에서 U를 V의 부분공간이라고 할 때

1. \\( U^\perp \lt V \\)
2. \\( U \cap U^\perp = {O} \\)
3. \\( (U^\perp)^\perp = U \\)
4. \\( A \in U^\perp \Leftrightarrow \text{A가 U의 기저와 직교 } \\)

<br><br>

## 📚직교행렬
M: n차 정칙행렬
<br>
M<sup>-1</sup> = M<sup>T</sup> => M을 직교행렬(orthogonal matrix)
<br>
MM<sup>T</sup> = I와 같다.

행렬 M의 역행렬과 행렬 M의 행과 열을 바꾼 전치행렬이 같으면 행렬 M을 직교행렬이라고 한다.

📍예제

$$
M =
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}
\rightarrow
M^{-1} =
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}
=
M^T
$$

<br>

### 📄직교행렬 특징

MM<sup>T</sup> = I

-> M의 행벡터 A<sub>i</sub>에 대해

$$
<A_i, A_j> = \begin{cases} 1 \quad (i = j) \\ 0 \quad (i \neq j) \end{cases}
$$

$$
M \cdot M^T =
\begin{pmatrix}
A_1 \cdot A_1 & A_1 \cdot A_2 \\
A_2 \cdot A_1 & A_2 \cdot A_2
\end{pmatrix}
=
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
$$

자기 자신과 내적하면 1이 되고 그렇지 않으면 0이 된다.

<br>

* 단위직교벡터와의 관련성

n차 정방행렬 M이 직교행렬 <=> M의 열벡터 또는 행벡터들이 단위직교벡터

<br>

### 📄직교행렬의 행렬식

M이 직교행렬 => M의 행렬식은 1또는 -1

$$
M^TM = I \rightarrow |M^TM| = |M||M^T| = |M|^2 = |M| = \pm1
$$

* \|AB\| = \|A\| \|B\|
* \|A<sup>T</sup>\| = \|A\|

<br>

### 📄2차 직교행렬의 특성

2차 정방행렬 M이 직교행렬
<br>
-> M은 평면에서의 회전변환 또는 대칭변환에 대응하는 행렬

1. \|M\| = 1 => M은 회전변환에 대응
2. \|M\| = -1 => M은 대칭변환에 대응

<br>

* 대칭행렬의 대각화

대칭행렬 M은 직교행렬에 의해 대각화된다.

<br><br>

## 📚직교변환
{V, <, >}, {W, <, >}: 내적공간일 때
<br>
T: V -> W 선형변환이고,
<br>
\|\| T(A) \|\| = \|\|A\|\|이면
<br>
T를 직교변환이라고 한다.

직교변환이란 원래 있던 벡터의 길이를 보존하는 선형변환이라고 이해.

<br>

### 📄직교변환의 성질
{V, <, >}, {W, <, >}: 내적공간
<br>
T: V -> W 선형변환이고일 때 다음은 모두 동치이다.

1. T가 직교변환
2. ∀A, B ∈ V, <A, B> = <T(A), T(B)> (내적 보존)
3. 내적공간 V의 단위직교기저 {A<sub>i</sub>}에 대해 {T(A<sub>i</sub>)}는 내적공간 W의 단위직교집합(사이각 보존)
4. 단위직교기저에 의한 T에 대응하는 행렬 M은 M<sup>T</sup>M = I를 만족한다.
<br>
(dim V = dim W = n이면 행렬 M은 n차 직교행렬)

<br>

### 📄직교변환과 직교행렬의 관계
내적공간 {V, <, >}에 대해
<br>
A, B ∈ V이고, T: V -> V가 직교변환,
M을 T의 행렬로서 n차 직교행렬(M<sup>T</sup>M = I)이라고 하면,

* 길이 보존: \|\| T(A) \|\| = \|\|A\|\|

$$
\begin{align}
||MA||^2 &= \; <MA, MA> \; = (MA)^T(MA) \\
&= (A^TM^T)(MA) = A^T(M^TM)A \\
&= A^TIA = A^TA = ||A||^2 = \; <A, A>
\end{align}
$$

<br>

* 각 보존: θ -> θ<sub>T</sub>

$$
cos\theta = \frac{<A, B>}{||A|| \; ||B||}
$$

$$
\begin{align}
cos\theta_T &= \frac{<T(A), T(B)>}{||T(A)|| \; ||T(B)||} = \frac{<MA, MB>}{||MA|| \; ||MB||} \\
&= \frac{<MA, MB>}{||A|| \; ||B||} \quad (||MA|| = ||A||(\text{길이 보존})) \\
&= \frac{(MB)^TMA}{||A|| \; ||B||} = \frac{B^TM^TMA}{||A|| \; ||B||} \\
&= \frac{B^TA}{||A|| \; ||B||} = cos\theta
\end{align}
$$

<br><br>