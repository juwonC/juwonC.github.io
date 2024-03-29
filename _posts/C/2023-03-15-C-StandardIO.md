---
title: "[C]표준 입출력 함수"
excerpt: "표준 입출력 함수"

categories:
  - C
tags:
  - [C, 표준 입출력 함수]

toc: true
toc_sticky: true

date: 2023-03-15
---

## 📚표준 입출력 함수
컴퓨터에 자료를 기억시키는 것을 입력이라 하고, 기억된 자료를 컴퓨터 외부에 나타내는 것을 출력이라고 한다. C 언어에서 제공하는 표준입출력 함수는 표준 입출력 라이브러리 stdio.h에 정의되어 있다.

<br>

| 표준 출력 함수 | 기능 |
| :---: | :---: |
| printf() | 여러 종류의 자료 출력 |
| putchar() | 1개의 문자 출력 |
| puts() | 문자열 출력 |

<br>

| 표준 입력 함수 | 기능 |
| :---: | :---: |
| scanf() | 키보드로 부터 1개 이상의 자료를 입력 받음 |
| putchar() | 키보드로 부터 1개의 문자를 입력 받음 |
| puts() | 키보드로 부터 문자열을 입력 받음 |

<br><br>

## 📚자료의 입출력
### 📄printf()
모니터에 자료를 출력하고자 할 때 사용되는 양식 지정 출력 함수이다. print formatted의 의미이다.

```c
#include <stdio.h>

void main()
{
  char a = 'a';
  int i = 1, j = 2;

  printf("a = %c, a의 아스키 코드 값은 %d \n", a, a);
  printf("i = %d, j = %d", i, j);
}
```

<br>

* 출력 양식 변환 기호
<br>
% 문자는 출력 양식 변환기호로서 자료의 입출력 양식을 지정한다. '%' 문자 출력은 %%가 사용된다.
<br>

| %문자 | 변환 형식 | 인자의 자료형 |
| :---: | :---: | :---: |
| %d | 부호 있는 10진 정수로 변환 | char, short, int |
| %ld | 부호 있는 10진 long 정수로 변환 | long |
| %lld | 부호 있는 10진 long long 정수로 변환 | long long |
| %u | 부호 없는 10진 정수로 변환 | unsigned int |
| %o | 부호 없는 8진수로 변환 | unsigned int |
| %x, %X | 부호 없는 16진수로 변환 | unsigned int |
| %f | 10진 부동소수점 형식으로 변환 | float, double |
| %lf | 10진 부동소수점 형식으로 변환 | long double |
| %e, %E | 지수 형태로 변환 | float, double |
| %c | 문자 하나로 변환 | char, short, int |
| %s | 문자열로 변환 | char* |
| %p | 포인터 주소값 출력 | void* |

<br>

* 출력 양식의 편집
<br>
출력 양식 편집은 %문자 뒤에 숫자 또는 -를 지정하면 된다.

```c
#include <stdio.h>

void main()
{
  printf("|%d| \n", 12345);     // 숫자 길이만큼 폭 자동 지정
  printf("|%5d| \n", 12345);    // 5자리로 오른쪽부터 채워짐
  printf("|%-5d| \n", 12345);   // 5자리로 왼쪽부터 채워짐
  
  // 7자리로 오른쪽부터 채워지고, 공백은 0으로 채워짐
  printf("|%07d| \n", 12345);

  // 5자리(소수점 포함)로 소수점 이하 1자리 출력
  printf("|%5.1f| \n", 123.45);

  // 7자리(소수점 포함)로 소수점 이하 3자리 출력
  printf("|%07.3f| \n", 123.45);
}
```

<br>

### 📄scanf()
scanf() 함수는 키보드로부터 자료를 입력받을 때 사용되는 양식 지정 입력 함수이다. 입력 양식 %문자가 아닌 다른 문자를 포함시켜서는 안되고 모든 변수 앞에 주소를 의미하는 &를 붙여야 한다. 문자열이나 배열의 이름은 그 자체로 주소의 의미를 가지고 있어서 &를 생략한다.

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int i;

  scanf("%d", &i);

  printf("입력한 숫자: %d \n", i);
}
```

<br>

* 입력 양식 변환 기호
<br>

| %문자 | 변환 기능 |
| :---: | :---: |
| %d | 정수형 입력받음 |
| %ld | long 정수형 입력받음 |
| %lld | long long 정수형 입력받음 |
| %o | 8진수 자료 입력받음 |
| %x | 16진수 자료 입력받음 |
| %f | 실수형 입력받음 |
| %lf | double 실수형 입력받음 |
| %c | 문자형 입력받음 |
| %s | 문자열 입력받음 |

<br><br>

* 자료의 입력

자료를 입력할 때 자료가 하나 이상일 경우 자료 사이에 공백을 두어야 한다.

💡scanf() 사용
<br>
Visual Studio는 scanf() 함수를 권장하지 않는 함수로 지정하여 해당 함수가 포함된 소스 코드를 컴파일하지 않는다. Visual Studio에서 scanf() 함수를 사용하기 위해서 코드 도입부에 #pragma warning(disable:4996)이나 #define _CRT_SECURE_NO_WARNINGS를 포함시켜줘야 한다. 또한 scanf_s() 함수를 사용할 수 있다.
<br><br>
scanf_s()로 문자열을 입력할 때 인자가 하나 더 필요하다. scanf_s("입력 양식", &변수, 문자열 크기)와 같이 문자열 크기도 인자로 넘겨주어야 한다.
{: .notice--warning}

<br>

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void main()
{
	int i;
	char a[25];

	printf("숫자 입력: ");
	scanf_s("%d", &i);
	printf("입력한 숫자: %d \n", i);

	printf("문자열 입력: ");
	scanf_s("%s", a, sizeof(a));
	printf("%s \n", a);
}
```

<br><br>

## 📚문자 단위 입출력
### 📄getchar()
getchar() 함수는 하나의 문자를 키보드를 통해 입력받아 변수가 가리키는 기억 공간에 저장하는 문자 입력 함수이다. 문자를 받아들여 저장하는 변수는 정수형이나 문자형으로 선언되어야 한다.
<br>

```c
#include <stdio.h>

void main()
{
  char a;

  a = getchar();
  printf("char = %c \n", a);
}
```

<br>

### 📄putchar()
putchar() 함수는 문자 단위 출력함수이다. 사용 형식에서 문자 형태는 정수형 변수, 정수형 상수, 문자형 변수, 문자 및 수식을 사용하면 된다.
<br>

```c
#include <stdio.h>

void main()
{
  char a = 'a';

  putchar(a);
  putchar(a + 1);

  putchar('c');
  putchar('\n');
  putchar('c' + 1);
}
```

<br><br>

## 📚문자열 단위 입출력
### 📄gets()
gets() 함수는 문자열을 키보드를 통해 입력받아 변수가 가리키는 기억공간에 저장하는 문자열 입력 함수이다. 변수는 배열이나 포인터 변수를 사용해야 한다. 문자열을 입력하고 엔터 키를 누르면 null 문자가 입력되어 문자열의 끝을 나타낸다. gets() 함수가 사용이 안되면 gets_s() 함수를 사용한다.
<br>

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
	char a[10];
	char b[10];

	printf("gets()로 문자열 입력: ");
	gets_s(a);
	printf("%s \n", a);

	printf("scanf()로 문자열 입력: ");
	scanf("%s", b);
	printf("%s \n", b);
}
```

<br>

### 📄puts()
puts() 함수는 문자열 출력 함수이다. printf() 함수와 달리 문자열을 출력하고 자동으로 줄이 바뀐다.

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  char a[] = "abc";
  char b[] = "def";

  puts(a);
  puts(b);

  printf("%s", a);
  printf("%s", b);
}
```

<br><br>