---
title: "[Cpp]동적 메모리 할당"
excerpt: "동적 메모리 할당"

categories:
  - Cpp
tags:
  - [Cpp, 동적 메모리 할당]

toc: true
toc_sticky: true

date: 2023-06-15
---

## 📚동적 메모리 할당
어떤 프로그램이 실행되면 운영체제는 프로그램 실행을 위해 기억공간을 할당하게 되는데, 이때 할당되는 기억공간의 위치는 데이터, 힙, 스택 영역으로 나누어 볼 수 있습니다.

| 구분 | 설명 |
| :---: | :---: |
| 데이터 영역 | 전역변수와 정적변수가 저장되는 영역 |
| 힙 영역 | 프로그래머의 필요에 의해 할당/소멸이 이루어지는 영역 |
| 스택 영역 | 지역변수와 매개변수가 저장되는 영역 |

<br>

동적 메모리 할당은 힙 영역을 이용하여 프로그램 실행 중에 입력되는 자료에 맞게 기억공간을 확보합니다. 하지만 동적 메모리 할당으로 생성된 저장공간은 이름이 없어 이름을 통해 접근할 수 없습니다.

따라서 이런 문제를 해결하기 위해 포인터를 사용합니다. 즉, 동적으로 할당된 저장공간을 포인터 변수가 가리키게 하여 접근할 수 있습니다.

<br><br>

### 📄new와 delete
동적 메모리 할당은 new 연산자를 이용합니다.

```cpp
// 지정된 자료형의 데이터 1개를 저장할 수 있는 공간 할당
// 그 주소를 포인터 변수에 넣음
// 자료형은 포인터의 자료형과 일치해야 함
ptrVar = new TypeName;

// n은 양의 정수값을 내는 수식(상수가 아니어도 됨)
ptrVar = new TypeName[n];

// 메모리 공간 반환
delete ptrVar;
delete[] ptrVar;
```

<br>

예시

```cpp
#include <iostream >

int main()
{
    int* ptr;
    ptr = new int;

    *ptr = 1;

    delete ptr;
    ptr = nullptr;
}
```

```cpp
#include <iostream>

int main()
{
    int * ptr;
    ptr = new int[3];

    *ptr = 1;
    *(ptr + 1) = 2;
    ptr[2] = 3;

    for (int i = 0; i < 3; ++i)
    {
        std::cout << ptr[i] << std::endl;
    }

    delete[] ptr;
    ptr = nullptr;
}
```

<br><br>