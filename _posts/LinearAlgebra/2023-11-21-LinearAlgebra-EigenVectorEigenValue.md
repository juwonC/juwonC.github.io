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

벡터를 선형변환 해보면 (-1, 1)이 방향은 같고 크기만 두 배 증가된 (-2, 2) 벡터가 나오는 것을 알 수 있다.

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

<br><br>

## 📚특성방정식


<br><br>