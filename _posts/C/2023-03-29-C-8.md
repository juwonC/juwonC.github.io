---
title: "[C]함수"
excerpt: "함수"

categories:
  - C
tags:
  - [C, 함수]

toc: true
toc_sticky: true

date: 2023-03-29
---

## 📚함수의 개념
C 언어에서 함수는 특정한 작업을 수행하도록 설계된 독립적인 프로그램입니다. C 프로그램은 함수들로 구성되어 있고 이 함수들이 정해진 순서에 따라 실행되어 프로그램이 기능을 수행합니다.
<br>
함수를 사용할 때 아래와 같은 장점이 있습니다.

<br>

* 프로그램의 수정이 용이함
* 함수 재사용으로 코드 중복 최소화
* 기능을 파악하기 쉬워 유지 관리 쉬움

<br>

함수는 크게 표준함수와 사용자 정의 함수로 나눌 수 있습니다.

<br><br><br>

## 📚표준 함수
C 언어에서 자체적으로 제공하는 함수입니다. 표준 함수는 표준 라이브러리라는 이름으로 제공됩니다. 표준함수의 원형(prototype)은 헤더 파일에 정의되어 있고 실체는 라이브러리 파일에 있습니다. 함수의 실제 내용은 링킹 시 라이브러리 파일에서 읽혀져 프로그램에 결합됩니다.

| 헤더 파일 | 선언된 함수 | 함수 예 |
| :---: | :---: | :---: |
| stdio.h | 입출력 | printf(), scanf(), getchar(), putchar(), ... |
| stdio.h | 파일 관련 | fopen(), fclose(), fprintf(), ... |
| conio.h | 콘솔 입출력 | putch(), cputs(), cprintf(), getch(), getche(), cscanf(), ... |
| string.h | 문자열 처리 | strcat(), strcmp(), strcpy(), strlen(), strncat(), strncmp(), strncpy(), ... |
| math.h | 수학 | sqrt(), sin(), cos(), tan(), log(), exp(), pow(), abs(), asin(), acos(), atan(), cosh(), ... |
| ctype.h | 문자 형태 판별 | isalpha(), isdigit(), islower(), ... |
| ctype.h | 문자 변환 | tolower(), toupper(), ... |
| stdlib.h | 수치 변환 | atoi(), itoa() |
| stdlib.h | 난수 관련 | rand(), srand() |
| stdlib.h | 정렬/검색 | qsort(), lfind() |

<br>
* 표준 함수 사용 예

```c
#include <stdio.h>
#include <math.h>

void main()
{
  int i = -1, j = 2;

  printf("abs(-1) = %d \n", abs(i));
  printf("sqrt(2) = %f \n", sqrt(j));
}
```

<br><br><br>

## 📚사용자 정의 함수
### 📄함수의 정의
함수가 수행하는 작업을 기술하는 코드입니다. 구조는 아래와 같습니다.

```c
 반환자료형 함수명(자료형 매개변수 1, 자료형 매개변수2, ...)
 {
    함수 몸체
 }
```

* **함수 헤더**
  1. 반환 자료형
  <br>
  - 함수에서 계산된 결과핪을 호출한 함수에 되돌려 줄 때의 자료형
  - 반환값이 없는 함수는 viod형으로 선언
  <br><br>

  2. 함수명
  <br>
  - 변수명을 정하는 규칙과 동일한 방식으로 함수명 정함
  <br><br>

  3. 자료형과 매개변수
  <br>
  - 매개변수는 호출함수와 피호출함수 사이에 자료를 주고받기 위해 사용
  - 매개변수는 해당 함수 내에서 변수처럼 사용
  - 매개변수가 여러 개면 ,로 구분
  - 매개변수가 없으면 쓰지않고 비워둠

<br>

* **함수 몸체**
<br>
함수의 시작과 끝을 나타내고 중괄호{}를 사용합니다.

  - main() 함수의 정의 예

  ```c
  int main(void)
  {

  }

  void main()
  {

  }
  ```
  <br><br>

  - 사용자 함수 정의
  
  ```c
  int sum(int a, int b)
  {
    int c;

    c = a + b;

    return(c);
  }
  ```

<br><br>

### 📄함수의 사용
함수를 사용할 때 함수의 원형 선언, 함수의 호출, 함수의 정의로 구성되어야 합니다.

```c
#include <stdio.h>

int sum(int a, int b);    // 함수 원형 선언

void main()
{
  int x;

  x = sum(1, 2);          // 함수 호출

  printf("%d", x);
}

int sum(int a, int b)     // 함수 정의
{
  int c;

  c = a + b;

  return(c);
}
```

<br><br>

### 📄함수의 원형 선언
함수는 사용되기 전에 먼저 선언되어야 합니다. 컴파일러는 함수 호출을 만나면 함수 헤더 모양과 함수 호출 모양을 비교하여 오류를 검사합니다. 함수는 호출되기 전에 미리 그 모양이 컴파일러에게 알려져야 하고 함수 호출 문장 전에 호출되는 함수가 정의되어 있어야 합니다.

* 함수 원형 선언이 필요한 경우

```c
#include <stdio.h>

int sum(int a, int b);    // 함수 원형 선언 필요

void main()
{
  printf("%d", sum(1, 2));
}

int sum(int a, int b)     // 피호출함수가 main() 함수 뒤에 정의됨
{
  return(a + b);
}
```

<br>

* 함수 원형 선언이 필요없는 경우

```c
#include <stdio.h>

int sum(int a, int b)     // 피호출함수가 main() 함수 앞에 정의됨
{
  return(a + b);
}

void main()
{
  printf("%d", sum(1, 2));
}
```

<br><br>

### 📄함수의 호출
함수는 스스로 수행될 수 없기 때문에 호출하지 않으면 사용할 수 없습니다. 함수를 사용하려면 함수를 호출해야하는데 함수의 호출은 함수명과 넘겨 주고자 하는 매개변수를 열거함으로써 이루어집니다.

* **매개변수**
<br>
호출하는 함수에 쓰이는 매개변수를 실매개변수, 호출당하는 함수에 쓰이는 매개변수를 형식매개변수라고 합니다. 호출함수는 실매개변수를 통해 피호출함수의 형식매개변수에게 자료를 넘기고 피호출함수에서 형식매개변수를 이용하여 계산된 결과값을 호출함수에게 되돌려줍니다. 따라서 실매개변수와 형식매개변수의 자료형, 변수 개수는 일치해야합니다.

```c
void main()
{
  int a = 1, b = 2, c = 3;

  func(a, b, c);                // a, b, c는 실매개변수
}

int func(int x, int y, int z)   // x, y, z 형식매개변수
{
  return(x + y + z);
}
```

<br>

* **return문**
<br>
형식매개변수에 의해 계산된 피호출함수의 결과값은 호출함수에 반환해야하는데 이때 return문이 사용됩니다. return문은 함수 내부에 어느 곳에서든지 한 번 이상 사용될 수 있고, 어느 하나가 수행되면 함수는 종료됩니다. 함수의 자료형이 void형일 경우 return;을 사용하거나 이를 생략할 수 있습니다.

```c
return(수식);
return 수식;

return 0;             // 상수 0 반환(정상적인 프로그램 종료)
return x;             // x값 반환
return(a + b + c);    // 수식의 결과값 반환
```

<br><br>

### 📄매개변수 사이의 자료 전달 방법

* **값에 의한 자료 전달(Call by value)**
<br>
실매개변수 값이 형식매개변수로 그대로 복사됩니다. 값에 의한 자료 전달 방법은 피호출함수의 형식매개변수 값이 변해도 호출함수의 실매개변수의 값은 원래 값을 유지합니다.

```c
#include <stdio.h>

void swap(int x, int y)
{
  int temp;

  temp = x;
  x = y;
  y = temp;

  printf("함수 내 x = %d, y = %d, \n", x, y);
}

void main()
{
  int a = 1, b = 2;

  printf("호출 전 a = %d, b = %d, \n", a, b);
  swap(a, b);
  printf("호출 후 a = %d, b = %d, \n", a, b);
}
```

<br>

* **참조에 의한 자료 전달(Call by reference)**
<br>
참조에 의한 자료 전달 방법은 호출함수와 피호출함수의 매개변수 값을 서로 교환할 수 있는 자료 전달 방법입니다. 단순히 값이 전달 또는 복사되는 것이 아니라 실매개변수의 값이 들어있는 주소값이 전달되기 때문에 형식매개변수의 값이 변한 후 호출함수로 되돌아가면 실매개변수 값도 변한 값을 갖게 됩니다.

```c
#include <stdio.h>

void swap(int *x, int *y)
{
  int temp;

  temp = *x;
  *x = *y;
  *y = temp;

  printf("함수 내 x = %d, y = %d, \n", x, y);
}

void main()
{
  int a = 1, b = 2;

  printf("호출 전 a = %d, b = %d, \n", a, b);
  swap(&a, &b);
  printf("호출 후 a = %d, b = %d, \n", a, b);
}
```

<br><br>

## 💡main() 함수
C 프로그램은 반드시 하나의 main() 함수를 갖습니다. 컴퓨터는 프로그램이 실행될 때 자동적으로 main()이라는 함수를 호출해서 프로그램을 실행합니다. 이런 main() 함수를 프로그램의 진입점(entrypoint)라고 부릅니다.