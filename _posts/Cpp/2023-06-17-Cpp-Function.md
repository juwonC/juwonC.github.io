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