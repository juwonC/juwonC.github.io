---
title: "[UE5]코딩 표준"
excerpt: "MyUnrealDocs - 코딩 표준"

categories:
  - MyUnrealDocs
tags:
  - [UE5, 코딩 표준]

toc: true
toc_sticky: true

date: 2023-06-30
---

## 🎮코딩 표준
### ⚙️코딩 규칙이 중요한 이유

* 소프트웨어가 수명을 지속하는 동안 들어가는 비용 중 80%는 유지보수에 소모된다.
* 최초 작성자가 소프트웨어의 수명이 다할 때까지 관리하는일은 거의 없다.
* 코딩 규칙을 사용하면 가독성이 향상되어 엔지니어가 새로운 코드를 더 빠르고 완벽히 이해할 수 있다.
* 대다수의 코딩 규칙이 크로스 컴파일러 호환성에 필요하다.

<br>

### ⚙️클래스 체계

클래스는 작성자보다 읽는 사람을 염두에 두고 조직되어야 한다. 읽는 사람은 대부분 클래스의 퍼블릭 인터페이스를 사용할 것이므로, public을 먼저 선언한 후 클래스의 private 구현이 뒤따라야 한다.

<br>

### ⚙️저작권 고지

배포용으로 에픽에서 제공한 모든 소스파일은 파일 첫 번째 줄에 저작권 고지를 포함해야 한다.

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.
```

<br>

### ⚙️명명 규칙

* 모든 코드와 코멘트는 미국 영어의 철자법과 문법을 사용해야 한다.
* (타입 이름 또는 변수 이름) 각 단어의 첫 번째 글자는 대문자로 써야 하며, 일반적으로 단어 사이에 밑줄은 사용하지 않는다.
* 타입 이름에 추가적으로 대문자로 이루어진 접두사를 붙여 변수 이름과 구분합니다. 예를 들어 FSkin은 타입 이름이고, Skin은 FSkin의 인스턴스이다.
* 템플릿 클래스는 접두사 T를 포함한다.
* UObject에서 상속받는 클래스는 접두사 U를 포함한다.
* AActor에서 상속받는 클래스는 접두사 A를 포함한다.
* SWidget에서 상속받는 클래스는 접두사 S를 포함한다.
* 추상적인 인터페이스인 클래스에는 접두사 I를 포함한다.
* 열거형에는 접두사 E를 포함한다.
* 부울 변수는 접두사 b를 포함한다.
* 그 외 대부분의 클래스 접두사 F를 포함한다.

```cpp
float Weight;
int32 Count;
bool bIsDead;
FString name;
UClass* MyClass;
```

<br>

### ⚙️포팅 가능한 C++ 코드

* bool: boolean 값(bool 크기 추정금지). BOOL은 컴파일되지 않는다.
* TCHAR: character(문자)(TCHAR 크기 추정금지)
* uint8: unsigned byte(1byte)
* int8: signed byte(1byte)
* uint16: unsigned short(2byte)
* int16: signed short(2byte)
* uint32: unsigned int(4byte)
* int32: signed int(4byte)
* uint64: unsigned quad word(8byte)
* int64: signed quad word(8byte)
* float: single precision floating point(4byte)
* double: double precision floating point(8byte)
* PTRINT: 포인터를 가질 수 있는 integer(PTRINT 크기 추정 금지)

<br><br>

### ⚙️코드 포맷

* 중괄호

에픽에서는 새 줄에 중괄호를 넣는 것을 권장한다. 단일 문장 블록에도 항상 중괄호를 포함시켜준다.

```cpp
if(bIsDead)
{
  return;
}
```

<br>

* If-Else

if-else 문의 각 실행 블록은 중괄호로 묶어야 한다. 중괄호를 사용하지 않을 경우 다른 사용자가 if 블록에 다른 줄을 추가할 수 있는 실수가 생길 수 있기 때문에 if-else 문은 항상 중괄호로 묶어야 한다.

```cpp
if (Number < 10)
{
  UE_LOG(LogCategory, Log, TEXT("Low"));
}
else if(10 < Number && Number < 50)
{
  UE_LOG(LogCategory, Log, TEXT("Medium"));
}
else
{
  UE_LOG(LogCategory, Log, TEXT("High"));
}
```

<br>

* 탭 및 들여쓰기
  - 실행 블록별로 코드를 들여쓴다.
  - 줄 시작 부분의 공백은 탭을 사용합니다. 탭 크기는 4자로 설정한다.

<br><br>