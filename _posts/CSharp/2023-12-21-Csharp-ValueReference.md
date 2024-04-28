---
title: "[Csharp]값 타입과 참조 타입"
excerpt: "값 타입과 참조 타입"

categories:
  - Csharp
tags:
  - [Csharp, Value Types, Reference Types]

toc: true
toc_sticky: true

date: 2023-12-21
---

## 📚값 타입과 참조 타입
### 📄스택과 값 타입
값 타입은 변수가 값을 담는 데이터 타입을 말한다. 값 타입과 참조 타입을 이해하기 위해 두 가지 메모리 영역을 알아야 한다. 두 메모리 영역 중 값 타입과 관련이 있는 것은 스택 영역, 참조 타입과 관련 있는 것은 힙 영역이다.

스택은 후입선출의 자료구조로서 접시를 쌓는 것과 같다고 생각하면 된다. 예를 들어 접시가 여러 장 쌓여 있다고 생각했을 때 가장 마지막에 쌓은 접시를 가장 먼저 꺼낼 수 있고 가장 처음에 쌓은 접시는 쌓여 있는 접시들을 모두 꺼내고 가장 마지막에 꺼낼 수 있는 것과 같다.

```cs
{
    int a = 1;
    int b = 2;
    int c = 3;
}
```

변수 a, b, c 세 개가 스택에 차례대로 쌓였다가 코드 블록이 끝나면 스택에서 하나씩 빠지면서 제거된다고 생각하면 된다. 여기서 a, b, c가 값 타입의 변수이다. 따라서 값 타입의 변수는 모두 스택에 저장된다.

<br>

### 📄힙과 참조 타입
참조 타입은 변수가 값 대신 값이 있는 곳의 위치(참조)를 담는 데이터 타입을 말한다.

스택은 코드 블록이 끝나면 가장 마지막에 들어온 순서부터 스스로 제거되는 메모리 구조이지만 힙은 저장된 데이터를 스스로 제거하지 않는 메모리 구조이다. 대신 힙은 가비지 컬렉터라는 것을 이용해 더이상 사용하지 않는 데이터를 관리한다.

힙을 사용하는 이유는 데이터가 코드 블록이 끝나는 시점과 상관 없이 데이터를 유지하고 싶을 때 사용할 수 있다는 장점이 있다. 프로그래머가 힙에 데이터를 저장해 놓으면 코드 블록의 종료 시점과 상관 없이 그 데이터는 계속 생명을 유지할 수 있다. 그리고 프로그래머가 더이상 이 데이터를 사용(참조)하지 않을 때 가비지 컬렉터가 해당 데이터를 수거해가고 메모리에서 사라진다.

참조 타입의 변수는 힙과 스택을 모두 사용한다. 힙 영역에는 데이터를 저장하고 스택 영역에는 데이터가 저장된 힙 메모리의 주소를 저장한다. 데이터를 직접 저장하는 대신 데이터가 저장된 주소를 **참조**한다고 해서 참조 타입인 것이다.

아래 코드는 C#의 참조 타입 중 object 타입 변수 두 개를 선언해서 각각 1과 2를 대입한 것이다.

```cs
{
    object a = 1;
    object b = 2;
}
```

<br><br>