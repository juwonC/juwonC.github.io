---
title: "[Cpp]반복문"
excerpt: "반복문"

categories:
  - Cpp
tags:
  - [Cpp, 반복문]

toc: true
toc_sticky: true

date: 2023-06-11
---

## 📚반복문

반복문은 일정 범위의 문장을 반복하여 실행하고 싶을 때 사용하는 구문입니다. for, while, do while 구문이 있습니다.

<br>

### 📄for문

일반적으로 하나의 루프 제어 변수를 두고 이 변수를 초기화한 후 반복조건이 참이면 지정된 문장을 반복합니다.

```cpp
for(초기화식; 반복 조건식; 증감식)
{
  반복할 문장;
}
```

```cpp
#include <iostream>

int main()
{
    int sum = 0;

    for (int i = 1; i <= 10; ++i)
    {
      sum += i;
    }

    std::cout << sum << std::endl;
}
```

<br>

C++11에는 범위 기반 for 루프라는 구문이 추가되었습니다. 범위 기반 for 루프는 여러 원소로 구성된 데이터 집합에 대해 첫 원소부터 마지막 원소까지 반복하여 실행하도록 지시합니다.

```cpp
for(원소선언: 데이터 집합)
{
  반복할 문장;
}
```

```cpp
#include <iostream>

int main()
{
    int arr[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int sum = 0;

    // element는 arr 각각의 원소 값을 받음
    for (int element : arr)
    {
      sum += element;
    }

    std::cout << sum << std::endl;
}
```

<br><br>

### 📄while문

반복조건이 참이면 주어진 문장을 반복하는 형태입니다. 아래 코드의 반복문은 양의 정수가 입력되면 계속 반복되고 0 또는 음의 정수를 입력하면 반복 조건이 거짓이기 때문에 반복을 중단합니다.

```cpp
while(반복조건)
{
  반복할 문장;
}
```

```cpp
#include <iostream>

int main()
{
    int val, total = 0;
    std::cin >> val;

    while (val > 0)
    {
      total += val;
      std::cin >> val;
    }

    std::cout << total << std::endl;
}
```

<br><br>

### 📄do while문

do while문은 while문과 유사하지만 블록 안에 있는 문장을 먼저 실행하고 반복 여부를 결정합니다.

```cpp
do
{
  반복할 문장;
}while(반복조건);
```

```cpp
#include <iostream>

int main()
{
    int i = 0, n;
    int sum = 0;

    std::cout << ("양의 정수 입력: ");
    std::cin >> n;

    do
    {
      sum += i;
      ++i;
    } while (i <= n);

    std::cout << "0 ~ " << n << "까지 합 = " << sum << std::endl;
}
```

<br><br>

### 📄break, continue

break 명령은 반복문을 빠져나가게 하고 continue 명령은 반복문 블록의 나머지를 건너뛰고 다시 반복문으로 돌아갑니다.

```cpp
#include <iostream>

int main()
{
    int num, sum = 0;

    while (true)
    {
    std::cout << "number(Enter the '0' to Quit): ";
    std::cin >> num;

    if (num == 0)
    {
      break;
    }

      sum += num;
    }

    std::cout << "sum = " << sum << std::endl;
}
```

<br>

```cpp
#include <iostream>

int main()
{
    int num = 1;

    while (num != 0)
    {
        std::cout << "number(Enter the '0' to Quit): ";
        std::cin >> num;

        if (num < 0)
        {
            std::cout << "num : Negative number!" << std::endl;
            continue;
        }

        std::cout << "Sqaureroot of " << num << " = " << sqrt(num) << std::endl;
    }
}
```

<br><br>
