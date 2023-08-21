---
title: "[Cpp]구조체"
excerpt: "구조체"

categories:
  - Cpp
tags:
  - [Cpp, 구조체]

toc: true
toc_sticky: true

date: 2023-06-12
---

## 📚구조체
기본 자료형과 별개로 프로그래머가 필요에 따라 새로운 자료형을 만들 수 있는데 이것을 사용자 정의 자료형이라고 합니다. 사용자 정의 자료형은 구조체(struct)를 사용하여 만들 수 있습니다.

구조체 내부에 선언된 타입들은 기본 자료형의 하나일 수도 있고 먼저 정의된 사용자 정의 자료형일 수도 있습니다. 그리고 서로 달라도 관계없습니다. 각각의 항목들은 지정된 자료형의 값을 저장합니다.

따라서 구조체는 여러 개의 데이터를 저장하는 항목들을 묶어 새롭게 정의한 자료형이라고 생각할 수 있습니다.

```cpp
struct StructName
{
  Type1 item1;
  Type2 item2;
  ...
};
```

<br>

2차원 좌표를 표현하는 구조체와 원을 나타내는 구조체를 선언하였습니다.

```cpp
struct C2dType
{
  double x;
  double y;
};
```

```cpp
struct CircleType
{
  // 사용자 정의 자료형
  C2dType center;
  double radius;
};
```

<br>

선언된 구조체를 저장하는 변수는 아래와 같이 선언합니다.

```cpp
StructName varName;
```

구조체 내부 각각의 항목에 접근할 때 멤버 선택 연산자 '.'을 구조체 변수 이름과 항목 이름 사이에 넣어 표기합니다. 이런 표기법을 점 표기법이라고 합니다.

### 📄예제 코드

```cpp
#include <iostream>
#include <cmath>

const double PI = 3.141593;

struct C2dType 
{
    double x;
    double y;
};

struct CircleType 
{
    C2dType center; // 중심좌표
    double radius; // 반지름
};

double CircleArea(CircleType c);
bool CheckOverlap(CircleType c1, CircleType c2);
void PrintCircle(CircleType c);

int main() 
{
    CircleType c1 = { {0, 0} , 10 };  // 원 구조체를 저장하는 변수 초기화
    CircleType c2 = { {30, 10 }, 5 };

    std::cout << "Circle1" << std::endl;
    PrintCircle(c1);
    std::cout << " Circle1 Area: " << CircleArea(c1) << std::endl;

    std::cout << "Circle2" << std::endl;
    PrintCircle(c2);
    std::cout << " Circle2 Area: " << CircleArea(c2) << std::endl << std::endl;

    if (CheckOverlap(c1, c2)) 
    {
        std::cout << "Overlap" << std::endl;
    } 
    else 
    {
        std::cout << "No Overlap" << std::endl;
    }
}

double CircleArea(CircleType c) 
{
    // .연산자를 사용하여 원 구조체 안의 radius에 접근
    return c.radius * c.radius * PI;
}

bool CheckOverlap(CircleType c1, CircleType c2) 
{
    double dx = c1.center.x - c2.center.x;
    double dy = c1.center.y - c2.center.y;

    double dCenter = sqrt(dx * dx + dy * dy);

    return dCenter < c1.radius + c2.radius;
}

void PrintCircle(CircleType c) 
{
    std::cout << " Center: (" << c.center.x << ", " << c.center.y << ")";
    std::cout << " Radius: " << c.radius << std::endl;
}
```

<br><br>