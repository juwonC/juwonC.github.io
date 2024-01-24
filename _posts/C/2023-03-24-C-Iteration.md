---
title: "[C]반복 제어문"
excerpt: "반복 제어문"

categories:
  - C
tags:
  - [C, 반복 제어문]

toc: true
toc_sticky: true

date: 2023-03-24
---

## 📚for문
1번 초기식은 for문이 시작되는 처음 한 번만 수행된다. 다음으로 2번 조건식은 반복 수행의 종료 시점을 조사하는 부분으로 반복 수행 여부를 점검한다. 조건식이 참이면 루프 안의 명령문을 수행하고 증감식을 수행한다. 만약 조건식이 거짓이면 루프를 빠져나간다.

```c
    //1     //2     //4
for(초기식; 조건식; 증감식)
{
  //3
  // 반복할 문장들;
}
```

<br>
for문 사용 예

```c
#include <stdio.h>

void main()
{
  int i, sum = 0;

  for(i = 1; i <= 10; ++i)
  {
    sum += i;
    printf("%d번째 실행 : sum : = %d \n", i, sum);
  }

  printf("1부터 %d까지의 합 = %d \n", i - 1, sum);
}
```

<br>
다양한 for문 사용

```c
// 초기식이나 증감식이 여러 개 존재하는 경우
for(int i = 1, int j = 1; i <= 100; ++i, j = j + 2)
{
  // 반복할 문장들;
}


// 초기식이 생략된 경우: 루프 변수를 반복문 앞에 초기화
int i = 0;

for( ; i <= 10; ++i)
{
  // 반복할 문장들;
}


// 조건식이 생략된 경우: 반복문 안에 if문 사용하여 조건식을 대행
for(int i = 0; ; ++i)
{
  if(i <= 10)
  {
    // 반복할 문장들;
  }
  else
  {
    break;
  }
}


// 증감식이 생략된 경우: 반복문 안에 증감식 수행
int sum = 0;

for(int i = 0; i <= 10; )
{
  sum += i;

  ++i;
}


// 초기식, 조건식, 증감식 모두 생략된 경우: 무한 루프
for( ; ;)
{
  // 반복할 문장들;
}
```

<br><br>

## 📚while문
while문을 만나면 조건식이 검사되고 조건이 참이면 while 안의 명령문이 실행된다. 그 다음 다시 while 조건식으로 돌아가 조건식이 검사되고 참이면 다시 반복문 안의 명령문이 실행된다. 만약 조건식이 거짓이면 반복문을 빠져나오게 된다.

```c
while(조건식)
{
  // 반복할 문장들;
}
```
<br>
while문 사용 예

```c
#include <stdio.h>

void main()
{
  int i = 1, sum = 0;

  while(i <= 10)
  {
    sum += i;

    printf("%d번째 실행 : sum = %d \n", i, sum);

    ++i;
  }

  printf("1부터 %d까지의 합 = %d \n", i - 1, sum);
}
```

<br>

### 📄while문의 무한 루프 구성
```c
#include <stdio.h>

void main()
{
  while(1)
  {
    // 반복할 문장;
  }

  while(true)
  {
    // 반복할 문장;
  }
}
```

<br>

### 📄while문 사용 시 유의 사항
```c
#include <stdio.h>

void main()
{
  float x = 0.0;
  float sum = 0.0;

  // x가 9.9가 되는 순간 무한 루프에 빠짐. 실수 표현에 있어 0.0에 0.1을 99번 더하면 정확히 9.9가 되지 않기 때문. while(x < 9.9)로 수정.
  while(x != 9.9)
  {
    sum += x;
    x += 0.1;
  }

  printf("sum = %f \n", sum);
}
```

<br><br>

## 📚do~while문
for문이나 while문은 조건식을 먼저 검사하고 그 결과에 따라 반복문을 실행하지만 do~while문은 반복문을 먼저 실행하고 조건을 검사하여 반복 실행 여부를 결정한다.

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int i = 0, n;
  int sum = 0;

  printf("n=? ");
  scanf("%d", &n);

  do
  {
    sum += i;
    ++i;
  }
  while(i <= n);

  printf("i = %d \n", i);
  printf("i ~ %d까지 합 = %d \n", n, sum);
}
```

<br><br>

## 📚기타 제어문
### 📄break문
break문은 반복 명령 실행 도중에 반복문을 강제적으로 빠져나오는데 사용된다. 자신이 포함된 하나의 루프나 블록만 벗어나게 된다.

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
  int num, sum = 0;

  while(1)
  {
    printf("number(Enter the '0' to Quit): ");
    scanf("%d", &num);

    if(num == 0)
    {
      break;
    }

    sum += num;
  }

  printf("sum = %d", sum);
}
```

<br>

### 📄continue문
continue문은 루프를 다시 실행하고자 할 때 사용한다. switch~case문에서는 사용되지 않고 반복 구조에서만 사용된다.

```c
#include <stdio.h>
#include <math.h>
#pragma warning(disable:4996)

void main()
{
  int num = 1;

  while(num != 0)
  {
    printf("number(Enter the '0' to Quit): ");
    scanf("%d", &num);

    if(num <0)
    {
      printf("num : Negative number! \n\n");
      continue;
    }

    printf("Sqaureroot of %d = %f \n\n", num, sqrt(num));
  }
  printf("END \n");
}
```

<br><br>