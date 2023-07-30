---
title: "[Cpp]상수 표현"
excerpt: "상수 표현"

categories:
  - Cpp
tags:
  - [Cpp, 상수 표현]

toc: true
toc_sticky: true

date: 2023-06-06
---

## 📚상수 표현
기본 자료형의 값을 직접 표현한 것을 **리터럴**이라고 합니다. 리터럴은 값을 프로그램에서 바꿀 수 없기 때문에 상수에 해당됩니다.

### 📄정수형 리터럴 표현

| 표현 | 의미 | 설명 |
| :---: | :---: | :---: |
| 11 | 10진수 11 | int형 |
| 0b1011 | 11의 2진수 표현 | 2진수는 0b로 시작 |
| 013 | 11의 8진수 표현 | 8진수는 0으로 시작 |
| 0xb | 11의 16진수 표현 | 16진수는 0x로 시작 |
| 123u | usigned형 리터럴 | 접미사 u, U는 unsigned |
| 123L | long형 리터럴 | 접미사 l, L은 long |
| 123ul | usigned long형 리터럴 | 접미사 혼합 |
| 123LL | usigned long형 리터럴 | 접미사 ll, LL은 long long |
| 'a' | 정수 97 | ASCII 코드에 해당되는 정수값 |
| '\141' | 'a'와 동일 | \와 8진 숫자는 8진수 문자 코드 |
| '\x61' | 'a'와 동일 | \x와 16진 숫자는 16진수 문자 코드 |

<br>

### 📄실수형 리터럴 표현

| 표현 | 의미 | 설명 |
| :---: | :---: | :---: |
| 1100. | double형 값 1100 | 실수형 표현은 기본적으로 double |
| 1100.0 | double형 값 1100 | 실수형 표현은 기본적으로 double |
| 11e2 | double형 값 1100 | 11✕10<sup>2</sup> = 1100 |
| 1.1e+3 | double형 값 1100 | 1.1✕10<sup>3</sup> = 1100 |
| 11000e-1 | double형 값 1100 | 11000✕10<sup>-1</sup> = 1100 |
| 1100.0f | float형 값 1100 | 접미사 f,F는 float |
| 11e2f | float형 값 1100 | 접미사 f,F는 float |
| 1100.0l | long double형 값 1100 | 접미사 l,L은 long double |
| 11e2L | long double형 값 1100 | 접미사 l,L은 long double |

<br><br>