---
title: "[C]선택 제어문"
excerpt: "선택 제어문"

categories:
  - C
tags:
  - [C, 선택 제어문]

toc: true
toc_sticky: true

date: 2023-03-23
---

## 📚if문
순차적으로 실행되는 프로그램의 순서를 제어하는 명령문을 제어문이라고 한다. 선택 제어문은 주어진 조건에 따라 실행이 분기하여 다른 명령문을 수행하도록 하는 제어문이다. if문의 주어진 조건을 만족하면 중괄호 안의 명령문을 수행하고, 만족하지 않으면 중괄호 밖의 명령문을 수행한다.

### 📄단순 if문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int a;

  printf("숫자 입력: ");
  scanf_s("%d", &a);

  // a가 10보다 작으면 중괄호 안의 명령문 수행
  // a가 10보다 작지 않으면 중괄호 밖의 명령문 수행
  if(a < 10)
  {
    printf("입력한 숫자가 10보다 작음. \n");
  }

  printf("a = %d", a);
}
```

<br>

### 📄if~else문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int a;

  printf("숫자 입력: ");
  scanf_s("%d", &a);

  if(a < 10)
  {
    printf("입력한 숫자 %d가 10보다 작음. \n", a);
  }
  else
  {
    printf("입력한 숫자 %d가 10보다 큼. \n", a);
  }
}
```

<br>

### 📄다중 if~else문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int a;

  printf("정수 입력: ");
  scanf_s("%d", &a);

  if(a >= 0)
  {
    if(a == 0)
    {
      printf("입력한 숫자는 0입니다.");
    }
    else
    {
      printf("입력한 숫자는 양수입니다.");
    }
  }
  else
  {
    printf("입력한 숫자는 음수입니다.");
  }
}
```

<br>

### 📄다중 if~else if~else문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int score = 0;

  printf("점수 입력: ");
  scanf_s("%d", &score);

  if(score >= 90)
  {
    printf("A학점");
  }
  else if(score >= 80)
  {
    printf("B학점");
  }
  else if(score >= 70)
  {
    printf("C학점");
  }
  else if(score >= 60)
  {
    printf("D학점");
  }
  else
  {
    printf("F학점");
  }
}
```

<br><br>

## 📚switch문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int n;

  printf("숫자 n 입력: ");
  scanf_s("%d", &n);

  printf("n %% 5 = %d \n", n % 5);

  switch(n % 5)
  {
    case 0:
      printf("나머지는 0 \n");
      break;
      
    case 1:
      printf("나머지는 1 \n");
      break;

    case 2:
      printf("나머지는 2 \n");
      break;

    // n % 5 결과 case문에 해당하는 값이 없을 경우 수행
    default:
      printf("나머지는 3이나 4 \n");
      break;
  }
}
```

<br><br>

## 📚goto문

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int n;

  printf("정수 입력: ");
  scanf_s("%d", &n);

  if(n == 1)
  {
    goto ONE;       // 레이블명 ONE으로 무조건 실행을 옮김
  }
  else if(n == 2)
  {
    goto TWO;       // 레이블명 TWO으로 무조건 실행을 옮김
  }
  else
  {
    goto EXIT;      // 레이블명 EXIT으로 무조건 실행을 옮김
  }

ONE:
  printf("입력한 숫자는 1입니다.");
  goto EXIT;

TWO:
  printf("입력한 숫자는 2입니다.");
  goto EXIT;

EXIT:
  printf("프로그램 종료");
}
```

<br><br>