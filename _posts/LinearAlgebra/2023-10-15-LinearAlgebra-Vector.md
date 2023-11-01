---
title: "[LinearAlgebra]평면벡터와 공간벡터"
excerpt: "평면벡터와 공간벡터"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 평면벡터와 공간벡터]

toc: true
toc_sticky: true

date: 2023-10-15
---

## 📚평면벡터
A를 평면 R<sup>2</sup>상의 벡터라고 하고, 벡터 A의 시작점을 평면의 원점에 맞출 때 끝점 P를 (a, b)라고 하면 벡터 A를 다음과 같이 정의할 수 있다.

$$
A = \overrightarrow{OP} = (a, b)
$$

<br>

평면벡터 A = (a, b)가 주어졌을 때 벡터 A의 크기를 \|A\|으로 쓰고 다음과 같이 정의한다.

$$
|A| = \sqrt{a^2 + b^2}
$$

<br><br>

## 📚공간벡터
벡터를 이용하여 R<sup>3</sup> 공간의 직선에 대한 벡터 방정식을 구하는 방법을 정리하면 다음과 같다.

* R<sup>3</sup> 공간의 두 벡터 A = (x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>), B = (x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)의 끝점을 지나는 직선의 벡터 방정식은 C = A = k(B - A)이고, 이 방정식의 성분 표현은 다음과 같다.

$$
\frac{x - x_1}{x_2 - x_1} = \frac{y - y_1}{y_2 - y_1} = \frac{z - z_1}{z_2 - z_1}
$$

<br>

* R<sup>3</sup> 공간의 벡터 A = (x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)에 평행하고 한 점 B = (x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>)을 지나는 직선의 벡터방정식은 C = B + kA이고, 이 방정식의 성분 표현은 다음과 같다.

$$
\frac{x - x_1}{x_2} = \frac{y - y_1}{y_2} = \frac{z - z_1}{z_2}
$$

<br><br>

## 📚R<sup>n</sup> 공간벡터
### 📄유클리드 n차원 공간
n개의 실수들의 순서조(ordered pair) 전체의 집합

(1, 2) ≠ (2, 1)

\\( R^{2} = R \times R \\)

\\( R^{n} = R \times ... \times R \text(n번 곱함) \\)

<br>

### 📄벡터의 정의 및 상등

| R<sup>2</sup> | R<sup>3</sup> | R<sup>n</sup> |
| :---: | :---: | :---: |
| A = (a<sub>1</sub>, a<sub>2</sub>) | A = (a<sub>1</sub>, a<sub>2</sub>, a<sub>3</sub>) | A = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>) |
| A = (a<sub>1</sub>, a<sub>2</sub>) <br> B = (b<sub>1</sub>, b<sub>2</sub>) <br> (a<sub>1</sub> = b<sub>1</sub>, a<sub>2</sub> = b<sub>2</sub>) <br> -> A = B | A = (a<sub>1</sub>, a<sub>2</sub>, a<sub>3</sub>) <br> B = (b<sub>1</sub>, b<sub>2</sub>, b<sub>3</sub>) <br> (a<sub>1</sub> = b<sub>1</sub>, a<sub>2</sub> = b<sub>2</sub>, a<sub>3</sub> = b<sub>3</sub>) <br> -> A = B | A = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>) <br> B = (b<sub>1</sub>, b<sub>2</sub>, ..., b<sub>n</sub>) <br> (∀i, a<sub>i</sub> = b<sub>i</sub>) <br> -> A = B |

두 벡터가 같으려면 성분끼리 같아야 한다.

<br>

### 📄벡터의 크기\|A\|

* R<sup>2</sup>

A = (a<sub>1</sub>, a<sub>2</sub>)

\\( \|A\| = \sqrt{a_{1}^{2} + a_{2}^{2}} \\)

<br>

* R<sup>3</sup>

A = (a<sub>1</sub>, a<sub>2</sub>, a<sub>3</sub>)

\\( \|A\| = \sqrt{a_{1}^{2} + a_{2}^{2} + a_{3}^{2}} \\)

<br>

* R<sup>n</sup>

A = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>)

\\( \|A\| = \sqrt{a_{1}^{2} + a_{2}^{2} + ... + a_{n}^{2}} \\ = \sqrt{\sum_{1}^{n}a_{i}^{2}} \\)

<br>

### 📄벡터의 실수곱
벡터의 실수곱 kA는 모든 벡터의 성분에 스칼라 k를 곱해준다.

(ka<sub>1</sub>, ka<sub>2</sub>)

(ka<sub>1</sub>, ka<sub>2</sub>, ka<sub>3</sub>)

(ka<sub>1</sub>, ka<sub>2</sub>, ..., ka<sub>n</sub>)

<br>

### 📄벡터의 합
벡터의 벡터 합 A + B

벡터의 성분끼리 더하면 된다.

A = (a<sub>1</sub>, a<sub>2</sub>, a<sub>3</sub>)
B = (b<sub>1</sub>, b<sub>2</sub>, b<sub>3</sub>)

A + B = (a<sub>1</sub> + b<sub>1</sub>, a<sub>2</sub> + b<sub>2</sub>, a<sub>3</sub> + b<sub>3</sub>)

<br>

### 📄R<sup>n</sup> 공간 벡터의 성질

A, B, C ∈ R<sup>n</sup>, k, l ∈ R

1. A + B = B + A(덧셈의 교환법칙)
2. A + (B + C) = (A + B) + C(덧셈의 결합법칙)
3. A + O = O + A = A (덧셈의 항등원)
4. A + (-A) = (-A) + A = O (덧셈의 역원)
5. k(A + B) = kA + kB (실수곱의 분배법칙)
6. (k + l)A = kA + lA (실수곱의 분배법칙)
7. k(lA) = (kl)A (실수곱의 결합법칙)
8. 1A = A (실수곱의 항등원)

<br><br>

## 📚R<sup>3</sup> 공간에서의 직선의 방정식
* 두 점 P와 Q를 지나는 곡선

P(x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>), Q(x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)

$$
\vec{PQ} // \vec{PX} => B - A // C - A => C - A = k(B - A)
$$

$$ C = A +k(B - A) $$

$$
(x, y, z) = (x_1, y_1, z_1) + k(x_2 - x_1, y_2 - y_1, z_2 - z_1)
$$

$$
\begin{cases}
&x = x_1 + k(x_2 - x_1) \\
&y = y_1 + k(y_2 - y_1) \\
&z = z_1 + k(z_2 - z_1)
\end{cases}
$$

$$
k = \frac{x - x_1}{x_2 - x_1} = \frac{y - y_1}{y_2 - y_1} = \frac{z - z_1}{z_2 - z_1}
$$

<br>

* 한 점P를 지나고 벡터 A에 평행한 직선

P(x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>), A(x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)

$$
\vec{PX} // A => C - B // A => C - B = kA
$$

$$ C = B + kA $$

$$
(x, y, z) = (x_1, y_1, z_1) + k(x_2, y_2, z_2)
$$

$$
\begin{cases}
&x = x_1 + kx_2 \\
&y = y_1 + ky_2 \\
&z = z_1 + kz_2
\end{cases}
$$

$$
k = \frac{x - x_1}{x_2} = \frac{y - y_1}{y_2} = \frac{z - z_1}{z_2}
$$

<br><br>

## 📚벡터의 내적
R<sup>n</sup> 공간의 두 벡터
A = (a<sub>1</sub>, a<sub>2</sub>, ...,a<sub>n</sub>)
B = (b<sub>1</sub>, b<sub>2</sub>, ...,b<sub>n</sub>)

벡터 A와 벡터 B의 내적을 A · B = a<sub>1</sub>b<sub>1</sub> + a<sub>2</sub>b<sub>2</sub> + ... + a<sub>n</sub>b<sub>n</sub> 으로 정의한다.

(각 성분끼리 곱해서 모두 더한다.)

* A · B = AB<sup>T</sup>
(벡터 A와 B의 내적은 n×1행렬 A와 1×n행렬 B의 행렬 곱)

<br>

### 📄내적의 성질

1. A · B = B · A (교환법칙)
2. A · (B + C) = A · B + A · C (분배법칙)
3. (kA) · B = k(A · B) = A · (kB) (결합법칙)
4. A · A = \|A\|<sup>2</sup>≥0 이다.
<br>
A · A = 0 일 필요충분조건은 A = O이다.

<br>

### 📄벡터의 내적과 사이각
R<sup>2</sup>나 R<sup>3</sup>에서
벡터 A와 B의 사이각을 θ라 하면 A · B = \|A\| \|B\| cosθ가 성립한다.

$$
\cos\theta = \frac{A · B}{|A||B|}
$$

<br>

* 벡터의 내적과 사이각, 정사영(그림자) 벡터

$$ A · B = |A|(|B|\cos\theta) = (|A|\cos\theta)|B| $$

$$ A · B = |A| \overline{OH_1} $$

$$ \vec{OH_1} = \overline{OH_1} · U_A (\text{단위벡터}, U_A = \frac{A}{|A|}) $$

<br>

### 📄두 벡터의 수직 조건
R<sup>2</sup>나 R<sup>3</sup>에서
영벡터가 아닌 두 벡터 A, B가 수직인 것은 A · B = 0인 것과 동치이다.

$$
\cos\theta = \frac{A · B}{|A||B|} = 0
$$

cosθ = 0 (θ = 90°)

<br><br>

## 📚벡터의 외적


<br><br>