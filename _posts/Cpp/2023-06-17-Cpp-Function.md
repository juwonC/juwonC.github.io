---
title: "[Cpp]함수"
excerpt: "함수의 정의와 호출"

categories:
  - Cpp
tags:
  - [Cpp, 함수]

toc: true
toc_sticky: true

date: 2023-06-17
---

## 📚함수의 정의와 호출
함수는 C++ 프로그램을 구성하는 기본 단위입니다. 모든 프로그램은 최소 1개의 함수로 구성됩니다. 함수는 작업을 수행하는 프로그램 문장들을 하나의 단위로 모아 놓고, 여기에 이름을 붙인 것입니다.

이렇게 정의한 함수는 프로그램의 다른 부분에서 필요할 때 호출하여 사용할 수 있습니다. 함수를 호출할 때 함수가 필요로 하는 데이터 또는 객체를 인수로 전달해야 하고 함수는 정의된 처리를 한 후 필요하면 그 결과를 호출한 문장으로 되돌려 줍니다.

<br><br>

### 📄함수의 정의

```cpp
// 머리부
returnType FunctionType(fParameterList)    // fParameterList는 형식 매개변수
{                                         // 몸체 블럭
  Type1 localVar1;                        // 지역변수 선언
  Type2 localVar2;

  statement1;                             // 처리할 작업
  statement2;

  return returnExpression                 // 결과값 반환
}
```

<br><br>

### 📄함수의 호출

```cpp
FunctionName(aParameterList);   // aParameterList는 실 매개변수

// 함수를 수식에 직접 넣어 반환되는 값을 연산에 바로 사용 가능
varName = FunctionName(aParameterList);
```

<br>

예제

```cpp
#include <iostream >

float FahrToC(float fahr)
{
    return (fahr - 32) * 5 / 9;
}

int main()
{
    float fTemp, cTemp;

    std::cout <<  "화씨온도: ";
    std::cin >> fTemp;

    cTemp = FahrToC(fTemp);

    std::cout <<  "---> 섭씨온도: " << cTemp << std::endl;
}
```

### 📄함수의 호출
C++에서 모든 식별자는 사용되기 전에 선언되어 있어야 합니다. 함수도 마찬가지인데 앞서 만들어봤던 FahrToC() 함수를 호출할 수 있는 것은 main() 함수 앞에 정의했기 때문입니다. 하지만 프로그램을 만들다 보면 순서에 맞춰 함수를 배치하는 것이 어렵거나 가능하지 않을 수 있습니다.

함수 순서에 문제가 있을 경우 main() 함수 앞에 호출할 함수를 완전히 정의하는 대신 함수의 원형을 프로그램 앞부분에 선언할 수 있습니다. 함수의 원형은 함수가 반환하는 값의 자료형, 함수의 이름, 함수가 인수를 전달받기 위한 매개변수들의 자료형을 명시함으로써 컴파일러가 그 함수를 알 수 있게 합니다.

```cpp
returnType FunctionName(fParameterList);
```

<br>

```cpp
#include <iostream >

float FahrToC(float fahr);    // 함수 전방 선언

int main()
{
    float fTemp, cTemp;

    std::cout <<  "화씨온도: ";
    std::cin >> fTemp;

    cTemp = FahrToC(fTemp);

    std::cout <<  "---> 섭씨온도: " << cTemp << std::endl;
}

float FahrToC(float fahr)
{
    return (fahr - 32) * 5 / 9;
}
```

<br><br>