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
A를 평면 R<sup>2</sup>상의 벡터라고 하고, 벡터 A의 시작점을 평면의 원점에 맞출 때 끝점 P를 (a, b)라고 하면 벡터 A를 다음과 같이 정의할 수 있습니다.

$$
A = \overrightarrow{OP} = (a, b)
$$

<br>

평면벡터 A = (a, b)가 주어졌을 때 벡터 A의 크기를 \|A\|으로 쓰고 다음과 같이 정의합니다.

$$
|A| = \sqrt{a^2 + b^2}
$$

<br><br>

## 📚공간벡터
벡터를 이용하여 R<sup>3</sup> 공간의 직선에 대한 벡터 방정식을 구하는 방법을 정리하면 다음과 같습니다.

* R<sup>3</sup> 공간의 두 벡터 A = (x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>), B = (x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)의 끝점을 지나는 직선의 벡터 방정식은 C = A = k(B - A)이고, 이 방정식의 성분 표현은 다음과 같습니다.

$$
\frac{x - x_1}{x_2 - x_1} = \frac{y - y_1}{y_2 - y_1} = \frac{z - z_1}{z_2 - z_1}
$$

<br>

* R<sup>3</sup> 공간의 벡터 A = (x<sub>2</sub>, y<sub>2</sub>, z<sub>2</sub>)에 평행하고 한 점 B = (x<sub>1</sub>, y<sub>1</sub>, z<sub>1</sub>)을 지나는 직선의 벡터방정식은 C = B + kA이고, 이 방정식의 성분 표현은 다음과 같습니다.

$$
\frac{x - x_1}{x_2} = \frac{y - y_1}{y_2} = \frac{z - z_1}{z_2}
$$

<br><br>