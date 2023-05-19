---
title: "[C]연산자"
excerpt: "연산자"

categories:
  - C
tags:
  - [C, 연산자]

toc: true
toc_sticky: true

date: 2023-03-18
---

## 📚산술 연산자
### 📄이항 연산자
2개의 자료를 대상으로 산술적인 처리를 수행하는 연산자입니다.

| 연산자 | 기능 |
| :---: | :---: |
| + | 덧셈 |
| - | 뺄셈 |
| * | 곱셈 |
| / | 나눗셈 |
| % | 나눗셈의 나머지 계산 |

<br>

```c
#include <stdio.h>

void main()
{
  int a, b;

  a = 1;
  b = 2;

  printf("a + b = %d \n", a + b);
  printf("b - a = %d \n", b - a);
  printf("a * b = %d \n", a * b);
  printf("a / b = %d \n", a / b);
  printf("a %% b = %d \n", a % b);
}
```

<br><br>

### 📄단항 연산자
1개의 자료만을 대상으로 산술적인 처리를 수행하는 연산자입니다. ++, -- 연산자를 증감 연산자라고도 합니다. 피연산자의 값을 1 증가시키거나 1 감소시킵니다. 증감 연산자는 사용 위치에 따라 기능이 달라질 수 있습니다.
<br>

i++와 i = i + 1과 같습니다.
<br>
i`--`와 i = i - 1과 같습니다.

* 전위연산
<br>
++i와 같이 피연산자 앞에 연산자를 붙입니다. i 값을 먼저 사용한 후 1 증가시킵니다.
<br>

* 후위연산
<br>
 i++와 같이 피연산자 뒤에 연산자를 붙입니다. i 값을 먼저 1 증가시킨 후 사용합니다.

```c
#include <stdio.h>

void main()
{
  int a = 0, b = 0, c = 0;

  // b와 c를 1씩 증가 시킨 후 사용하여 a = 2, b = 1, c = 1
  a = (++b) + (++c);
  printf("a = (++b) + (++c) 결과: a = %d, b = %d, c = %d \n", a, b, c);

  // b와 c를 먼저 사용한 후 1씩 증가해서 a = 2, b = 2, c = 2
  a = (b++) + (c++);
  printf("a = (b++) + (c++) 결과: a = %d, b = %d, c = %d \n", a, b, c);
}
```

<br><br><br>

## 📚관계 연산자
관계 연산자는 피연산자의 대소 관계를 비교하는 연산자입니다. 결과는 참과 거짓이 됩니다.

| 연산자 | 기능 |
| :---: | :---: |
| == | 같은가 여부 비교 |
| != | 다른가 여부 비교 |
| >, >=, <, <= | 대소 관계 비교 |

```c
#include <stdio.h>

void main()
{
  int a = 2, b, c, d;

  // 거짓
  b = a > 2;
  printf("b = %d \n", b);

  // 참
  c = a <= 2;
  printf("c = %d \n", c);

  // 참
  d = (a != 3);
  printf("d = %d \n", d);
}
```

<br><br><br>

## 📚논리 연산자
논리 연산자는 피연산자에 대해 논리연산을 수행하는 연산자입니다. 결과는 참과 거짓으로 나타납니다. 값이 0인 경우 거짓이고 0이 아닌 값은 참이 됩니다.

| 연산자 | 기능 |
| :---: | :---: |
| && | 논리곱(AND) 양쪽 모두 참일 때 참 |
| `||` | 논리합(OR) 양쪽 중 하나라고 참이면 참 |
| ! | 논리부정(NOT) 참이면 거짓, 거짓이면 참 |

```c
#include <stdio.h>

void main()
{
  int a = 1, b = 3, c, d, e;

  // 양쪽 모두 참이므로 참
  c = (a < 2) && (b >= 3);
  printf("c = %d \n", c);

  // a가 참이므로 참
  d = (a < 2) || (b > 3);
  printf("d = %d \n", d);

  // a가 참이므로 거짓
  e = !a;
  printf("e = %d \n", e);
}
```

<br><br><br>

## 📚대입 연산자
대입 연산자는 연산자의 오른쪽을 왼쪽에 대입하는데 사용합니다.

| 연산자 | 기능 |
| :---: | :---: |
| = | 오른쪽을 왼쪽에 대입 |
| += | i = i + 1; i에 1을 더한 후 결과를 i에 대입 |
| -= | i = i - 1; i에 1을 뺀 후 결과를 i에 대입 |
| *= | i = i * 1; i에 1을 곱한 후 결과를 i에 대입 |
| /= | i = i / 1; i에 1을 나눈 후 결과를 i에 대입 |
| %= | i = i % 1; i에 1을 나눈 후 나머지 결과를 i에 대입 |
| &= | i = i & 1; i와 1에 대해 bit단위의 AND 연산을 하고 결과를 i에 대입 |
| `|=` | i = i `|` 1; i와 1에 대해 bit단위의 OR 연산을 하고 결과를 i에 대입 |
| ^= | i = i ^ 1; i와 1에 대해 bit단위의 XOR 연산을 하고 결과를 i에 대입 |
| <<= | i = i << 1; i 값을 1bit 왼쪽으로 이동 후 결과를 i에 대입 |
| >>= | i = i >> 1; i 값을 1bit 오른쪽으로 이동 후 결과를 i에 대입 |

```c
#include <stdio.h>

void main()
{
  int a = 1, b = 2, c = 3;

  a += (b * 2);
  b *= 3;
  c /= 3;

  printf("a = %d, b = %d, c = %d \n", a, b, c);

  // i = i + 1;과 i += 1;과 i++은 모두 같습니다.
}
```

<br><br><br>

## 📚조건 연산자
조건 연산자는 조건의 만족 여부에 따라 지정된 수식을 수행하는 연산자입니다. 3개의 피연산자를 가지고 있어 3항 연산자입니다.

```c
#include <stdio.h>

void main()
{
  int a = 5, b;

  // a > 4이 참이면 a + 2를 수행, 거짓이면 a - 1을 수행
  b = (a > 4) ? (a + 2) : (a - 1);
  printf("b = %d \n", b);
}
```

<br><br><br>

## 📚비트 연산자
비트 연산자는 수치를 2진수로 변환하여 bit 단위의 연산을 수행하는 연산자입니다. 비트 연산자는 정수형 자료에서만 사용이 가능합니다.

| 연산자 | 기능 |
| :---: | :---: |
| &(bit AND) | 대응되는 두 bit가 모두 1일 때 결과는 1 |
| `|`(bit OR) | 대응되는 두 bit 중 하나라도 1이면 결과는 1 |
| ^(bit XOR) | 대응되는 두 bit가 서로 다를 때만 결과는 1 |
| ~(bit NOT) | 1은 0으로 0은 1로 바꿈 |
| << | bit 왼쪽으로 이동 |
| >> | bit 오른쪽으로 이동 |

```c
#include <stdio.h>

void main()
{
  int r = 255, g = 255, b = 0;

  unsigned int color;

  color = r << 16 | g << 8 | b;

  printf("%x \n", color);

  // 비트마스크 0xFF를 이용하여 r, g, b 추출
  r = color >> 16 & 0xFF;
  g = color >> 8 & 0xFF;
  b = color & 0xFF;

  printf("r = %x, g = %x, b = %x \n", r, g, b);
}
```

<br><br><br>

## 📚기타 연산자
기타 연산자로 sizeof(), cast, &, * 연산자가 있습니다.

| 연산자 | 기능 |
| :---: | :---: |
| sizeof() | 지정한 자료형, 변수, 수식이 차지하는 기억공간의 크기(byte)를 구함 |
| cast | 지정된 자료형을 다른 자료형으로 강제 형변환 시킴 |
| & | 주소 연산자로서 피연산자의 주소를 나타냄 |
| * | 내용 연산자로서 피연산자의 내용을 가져옴 |

<br>
형변환에는 자동 형변환과 강제 형변환이 있습니다. 대입 연산자의 왼쪽과 오른쪽에 존재하는 두 피연산자의 자료형이 불일치하거나, 산술연산에서 2개의 피연산자의 자료형이 불일치하는 경우에 자동 형변환이 일어납니다.

```c
#include <stdio.h>

void main()
{
  // sizeof() 사용
  float a = 3.1415;

  printf("int형 크기: %dbyte \n", sizeof(int));
  printf("float형 변수 a의 크기: %dbyte \n", sizeof(a));

  // 자동 형변환
  int b = 1, c = 2;
  float d;

  d = b / c;
  printf("d = %f \n", d);

  // 강제 형변환
  d = (float)b / c;
  printf("d = %f \n", d);
}
```

<br><br><br>

## 📚연산자 우선순위
수학과 마찬가지로 C 언어에서도 연산자 우선 순위가 정해져 있습니다. 하나의 연산식에 여러 개의 연산자가 사용될 경우 연산자 우선순위에 의해 연산이 이루어집니다. 우선순위가 같은 연산자가 있을 경우 연산자의 결합 방향에 의해 연산이 이루어집니다. 괄호를 사용하여 연산을 먼저 수행하게 하는 방법도 있습니다.
<br><br>
우선순위와 결합 방향에 대한 내용은 아래 링크를 참고하시길 바랍니다.
[https://learn.microsoft.com/ko-kr/cpp/c-language/precedence-and-order-of-evaluation?view=msvc-170](https://learn.microsoft.com/ko-kr/cpp/c-language/precedence-and-order-of-evaluation?view=msvc-170)

```c
#include <stdio.h>

void main()
{
  int a = 1, b = 2, c = 5;

  printf("%d \n", a + b * c);

  // a = 12, b = 12
  printf("%d \n", a = b += 2 * c);

  // b = 10
  printf("%d \n", a *= b = c + 5);
}
```

<br><br>