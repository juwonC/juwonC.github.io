---
title: "[C]자료형과 변수 선언"
excerpt: "자료형과 변수 선언"

categories:
  - C
tags:
  - [C, 자료형, 변수, 선언]

toc: true
toc_sticky: true

date: 2023-03-07
---

## 📚자료형
기억 공간에 이름을 부여하는 것을 변수 선언이라고 한다. 변수 선언을 위해 C 언어에서는 자료형이라는 것을 제공한다. 자료형이란 사용하는 자료의 종류나 크기 등의 특징을 나타낸다.

<br>

### 📄자료형의 종류
* 기본형
  - 정수형(int, short, long, unsigned)
  - 실수형(float, double, long double)
  - 문자형(char, unsigned char)
  - 열거형(enum)
  - 형 없음(void)

<br>

* 확장형
  - 배열형(array type)
  - 함수형(function type)
  - 포인터형(pointer type)
  - 구조체형(structure type)

<br><br>

### 📄기본 자료형의 크기와 범위
* 정수 자료형
<br>

  | 정수 자료형 | 범위 | 크기 |
  | :---: | :---: | :---:|
  | short <br> (int) short <br> (signed) short <br> (signed) short (int) | -32768 ~ 32767 | 2byte |
  | unsigned short <br> unsigned short (int) | 0 ~ 65535 | 2byte |
  | int <br> (signed) int | -2,147,483,648 ~ 2,147,483,647 | 4byte |
  | unsigned <br> unsigned int | 0 ~ 4,294,967,295 | 4byte |
  | long <br> long (int) <br> (signed) long <br> (signed) long (int) | -2,147,483,648 ~ 2,147,483,647 | 4byte |
  | unsigned long <br> unsigned long (int) | 0 ~ 4,294,967,295 | 4byte |
  | long long <br> long long (int) <br> (signed) long long (int) | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 | 8byte |
  | unsigned long long <br> unsigned long long (int) | 0 ~ 18446744073709551615 | 8byte |

<br><br>

* 실수 자료형
<br>

  | 실수형 | 범위 | 크기 |
  | :---: | :---: | :---: |
  | float | 3.4 X 10<sup>-38</sup> ~ 3.4 X 10<sup>38</sup> | 4byte |
  | double | 1.7 X 10<sup>-308</sup> ~ 1.7 X 10<sup>308</sup> | 8byte |
  | long double | 1.7 X 10<sup>-308</sup> ~ 1.7 X 10<sup>308</sup> | 8byte |

<br><br>

* 문자형
<br>
C 언어에서 문자형은 ASCII 코드를 사용하여 처리한다.
<br>

  | 문자형 | 범위 | 크기 |
  | :---: | :---: | :---: |
  | char | -128 ~ 127 | 1byte |
  | unsigned char | 0 ~ 255 | 1byte |

<br><br>

* 8진수, 16진수의 지정
<br>

  | 진수 | 지정 방법 | 예 |
  | :---: | :---: | :---: |
  | 8진수 | 숫자 앞에 0 | int octal_value = 011 |
  | 16진수 | 숫자 앞에 0x | int hex_value = 0x1A |

<br><br>

* 열거형
<br><br>
형식 : enum 태그명 {열거자 1, 열자 2, ... }

<br>

선언 예

```c
// 디폴트로 첫 번째 열거자(SUN)의 값은 0이다.
enum day {SUN, MON, TUE, WED, THU, FRI, SAT};

// enum day형인 변수 d1과 d2를 만들었다.
enum day d1, d2;

// 초기값을 지정해주면 다음 열거자는 초기값 +1
enum day2
{
  SUN = 1,
  MON,      // 2
  TUE,      // 3
  WED,
  THU,
  FRI,
  SAT
} d1, d2;
```

<br><br><br>

## 📚변수 선언
모든 변수는 어떤 형태의 자료를 저장할 것인지 미리 결정하여 사용하기 전에 정의해야 한다. 변수 선언은 변수명과 변수의 자료형을 지정하여 변수를 위한 기억공간을 할당하는 것이다.

<br>

### 📄변수에 저장될 값의 크기

변수를 선언할 때는 저장하게될 자료의 범위를 고려하여 자료형을 지정해야 한다. 변수가 가지는 범위를 넘어서거나 너무 작은 값을 대입하면 오버플로 또는 언더플로가 발생하여 원치 않는 결과가 나올 수 있다.

<br>

### 📄변수의 선언 위치

변수는 함수의 외부와 내부에 선언할 수 있다. 함수 외부에서 선언된 변수를 전역변수라고 하며 프로그램 어디에서나 사용할 수 있다.

함수 내부에서 선언된 변수는 지역변수라고 하며 함수 내부에서만 사용할 수 있다.

전역변수는 프로그램이 종료되기 전까지 기억공간에 존재하게 되고, 지역변수는 함수가 호출될 때 생성되어 함수의 실행이 종료되면 기억공간에서 소멸된다.

전역변수는 프로그램이 실행되는 동안 항상 존재하는 자료 영역에 저장되고, 지역 변수는 임시 기억공간인 스택 영역에 저장된다.

전연변수는 0으로 자동 초기화되지만 지역변수는 자동 초기화되지 않는다.

<br>

### 📄변수의 초기화

모든 변수는 선언이 이루어지면 변수에 특정 값을 부여해야 한다. 이것을 변수의 초기화라고 하는데 C 언어에서 변수를 초기화하지 않으면 에러가 발생할 수 있다. 초기화하지 않은 변수에는 기억공간에 존재하고 있던 기존의 값(쓰레기값)이 남아있을 수 있기 때문이다.

```c
#include <stdio.h>

void main()
{
  int i;        // 변수 i 선언
  int j = 1;    // 변수 j를 1로 초기화
}
```

<br><br>