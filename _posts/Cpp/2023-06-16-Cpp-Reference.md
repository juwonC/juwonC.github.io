---
title: "[Cpp]참조"
excerpt: "참조"

categories:
  - Cpp
tags:
  - [Cpp, 참조]

toc: true
toc_sticky: true

date: 2023-06-16
---

## 📚참조
포인터와 유사한 개념으로 참조가 있습니다. 어떤 변수에 대한 참조는 그 변수의 별명이라고 할 수 있습니다. 참조는 '&' 기호를 이용하여 선언합니다.

```cpp
TypeName &refVar = varName;
```

참조는 초기화를 통해 참조 대상을 지정해야 합니다. refVar에 varName의 값을 넣는 것이 아니고 refVar가 varName을 참조하도록 지정하여 refVar을 사용하는 것이 varName을 사용하는 것과 같은 결과를 내도록 하는 것입니다. 참조가 어떤 변수를 참조하도록 초기화하는 것은 참조를 선언할 때 하고 이후 참조 위치는 바꿀 수 없습니다.

```cpp
#include <iostream >

int main()
{
    int a = 1, b = 2;

    // ref는 정수형 변수 a에 대한 참조
    int& ref = a;
    std::cout <<  "ref: " << ref << ", a: " << a << std::endl;

    // a에 10을 넣은 것과 동일
    ref = 10;
    std::cout <<  "ref: " << ref << ", a: " << a << std::endl;

    // ref가 변수 b를 참조하도록 하는 것이 아님
    // b의 값을 ref가 참조하는 곳(a)에 값을 넣음
    // 참조는 초기화 이후 참조 위치를 바꿀 수 없음!
    ref = b;
    std::cout <<  "ref: " << ref << ", a: " << a << std::endl;
}

```

<br><br>

### 📄참조와 포인터
참조는 어떤 대상을 가리킨다는 점에서 포인터와 유사하지만 차이점이 있습니다.

* 참조를 이용하여 값을 읽거나 저장할 때 변수를 사용하는 것과 동일합니다. '*'와 같은 연산자를 사용하지 않습니다.

* 참조는 초기화를 통해 반드시 어떤 대상을 참조해야만 합니다. 따라서 아무것도 참조하지 않는 상황은 발생하지 않습니다.
  
* 참조는 초기화를 통해 지정된 참조 대상을 바꿀 수 없습니다. 참조의 유효기간 동안 하나의 대상만 참조할 수 있습니다.

<br><br>

### 📄l-value 참조와 r-value 참조
C++11에서 참조는 l-value 참조와 r-value 참조로 구분합니다.

* l-value 참조

C++11 이전의 참조에 해당되고 값을 저장할 수 있는 대상을 참조하기 위한 참조입니다. const 한정어를 사용하면 l-value 참조를 사용하지만 참조 대상의 값을 바꾸지 못하게 할 수 있습니다.

```cpp
#include <iostream>

int main()
{
    int a{ 1 };

    const int& ref = a;

    std::cout << ref << std::endl;

    // 컴파일 에러 const 참조로 값 수정 불가능
    ref += 2;
}
```

<br>

* r-value 참조

값을 사용한 후에 그 값을 더 이상 가지고 있을 필요가 없는 대상을 참조합니다. 객체의 값을 다른 객체로 이동하는 용도에 유용하게 활용됩니다.

<br><br>