---
title: "[Cpp]포인터"
excerpt: "포인터"

categories:
  - Cpp
tags:
  - [Cpp, 포인터]

toc: true
toc_sticky: true

date: 2023-06-14
---

## 📚포인터
포인터는 변수, 구조체, 객체 등을 가리키는 변수로서 메모리의 주소와 직접적으로 연관됩니다. 포인터 변수는 자료형 명칭에 *를 사용하여 선언합니다. 포인터 변수를 선언만 하고 가리키는 곳이 정의되지 않은 상태에서 사용하면 안 됩니다. 포인터가 적절한 메모리 주소를 가리키게 해주고 포인터를 이용하먄 그 위치의 값에 접근할 수 있습니다.

포인터가 가리키는 메모리 값에 접근할 때 간접 액세스 연산자 *를 사용합니다.

```cpp
TypeName* ptrVar;
```

```cpp
#include <iostream > int main()
{
    int a = 1;
    int* ptr;

    ptr = &a;

    std::cout <<  "ptr이 가리키는 값: " << *ptr << std::endl;

    *ptr = 2;

    std::cout <<  "a: " << a << std::endl;
}

```

<br>

💡부주의한 포인터 사용
<br><br>
포인터가 올바르게 초기화되지 않고 잘못된 위치를 가리키면 프로그램 동작 중에 어느 위치를 액세스하게 될지 알 수 없어 심각한 오류를 일으킬 수 있습니다.
<br>
포인터가 가리키는 대상이 없을 때를 알 수 있도록 하는 값을 저장할 수 있는데 이 때 사용할 수 있는 것이 nullptr이라는 키워드입니다.
{: .notice--warning}

```cpp
int* ptr;
*ptr = 1; // 올바른 초기화가 이뤄지지 않은 포인터 사용
```

<br><br>

### 📄구조체 및 객체의 포인터
구조체나 객체에 대한 포인터도 사용할 수 있습니다.

```cpp
#include <iostream >

struct c2dType 
{
    double x = 0;
    double y = 0;
};

int main() 
{
    c2dType point;
    c2dType* c2dPtr = &point;

    // c2dPtr이 가리키는 구조체의 x, y 항목
    // 멤버 선택 연산자 '.' 우선순위가 간접 액세스 연산자 '*' 보다 높기 때문에 괄호 사용
    std::cout <<  "x: " << (*c2dPtr).x << ", ";
    std::cout <<  "y: " << (*c2dPtr).y << std::endl;

    // 간편하게 사용하기 위해 '->' 연산자 제공
    std::cout <<  "x: " << c2dPtr->x << ", ";
    std::cout <<  "y: " << c2dPtr->y << std::endl;
}

```

<br><br>

### 📄const 한정어와 포인터
포인터에도 const 한정어를 사용할 수 있습니다. const 한정어는 넣는 위치에 따라 의미가 달라지므로 사용에 주의해야 합니다.

* **const int* p1;** - p1은 상수 정수를 가리키는 포인터입니다. p1이 가리키는 값을 수정할 수 없다는 의미입니다. *p1 = 1; // error
* **int* const p2;** - p2는 정수를 가리키는 상수 포인터입니다. p2가 가리키는 값은 변경 가능하지만 포인터 p2는 다른 것을 가리키도록 변경할 수 없습니다. p2 = &a; // error
* **const int* const p3;** - p1, p2 특성을 모두 가져서 p3가 가리키는 값을 변경할 수 없고, p3도 다른 것을 가리키도록 변경할 수 없습니다. *p3 = 10; // error, p3 = &a; // error

<br><br>