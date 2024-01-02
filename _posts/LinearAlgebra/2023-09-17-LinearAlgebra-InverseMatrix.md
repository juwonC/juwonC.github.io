---
title: "[LinearAlgebra]역행렬"
excerpt: "역행렬"

categories:
  - Linear_Algebra
tags:
  - [선형대수, 역행렬]

toc: true
toc_sticky: true

date: 2023-09-17
---

## 📚정칙행렬과 역행렬
n차 정방행렬 A에 대해 행렬 B가 존재하여 AB = BA = I<sub>n</sub> 을 만족할 때 A를 정칙행렬(nonsingular matrix) 또는 역연산이 가능한 행렬(invertible matrix)이라고 하며, B를 A의 역행렬(inverse matrix)이라고 하고 B = A<sup>-1</sup>으로 나타낸다.(I<sub>n</sub>는 단위행렬)

A가 정칙행렬이면 A<sup>-1</sup>은 유일하다. 즉, A의 역행렬은 하나만 존재한다는 의미이다.

<br><br>

## 📚역행렬 구하는 방법
n차 정방행렬의 역행렬을 구하는 방법에 대해 알아보려고 한다.

n차 단위행렬 I에 기본행연산을 한 번만 적용하여 얻는 행렬 E를 기본행렬이라고 한다. 기본행연산이 세 종류가 있듯이 기본행렬도 세 종류가 있다. 기본행연산 R<sub>ij</sub>, R<sub>i</sub>(c), R<sub>ij</sub>(c) 각각에 대응하여 기본행렬도 E<sub>ij</sub>, E<sub>i</sub>(c), E<sub>ij</sub>(c)가 있다.

<br><br>