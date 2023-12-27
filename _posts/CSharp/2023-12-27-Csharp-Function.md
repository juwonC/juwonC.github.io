---
title: "[Csharp]함수"
excerpt: "함수"

categories:
  - Csharp
tags:
  - [Csharp, 함수]

toc: true
toc_sticky: true

date: 2023-12-27
---

## 📚함수
```cs
<한정자> <반환형> <함수 이름>(<매개변수자료형 매개변수>)
{
  // body
}

```

<br>

### 📄값에 의한 호출
C++처럼 함수에 아래처럼 인자를 전달하면 값을 복사해서 함수 안에서만 연산이 일어나고 실매개변수 num의 값이 변하지 않는다.

num의 값을 1 증가 시키려고 Add 함수를 호출했지만 함수로 전달되는 인자는 값만 복사된 것이므로 함수 안에서만 값 1이 2로 증가하고 이 값은 Add 함수 안에서만 사용 가능하다.

따라서 아래의 Add 함수는 Main 함수 안에 있는 num의 값에 영향을 주지 못한다.

```cs
namespace CSharp
{
    class Program
    {
        static void Add(int a)  // 값에 의한 호출
        {
            ++a;
        }

        static void Main(string[] args)
        {
            int num = 1;

            Program.Add(num);      // 실매개변수 num
            Console.WriteLine(num);
        }
    }
}
```

<br>

### 📄참조에 의한 호출
값을 복사하지 않고 참조로 인자를 전달하여 함수 안에서 연산을 하면 실매개변수의 값이 바뀐다.

따라서 아래의 Add 함수를 호출하면 num의 주소에 있는 값을 1 증가 시킨 것이므로 실매개변수 num이 1 증가하는 것을 알 수 있다.

```cs
namespace CSharp
{
    class Program
    {
        static void Add(ref int a)  // 참조에 의한 호출
        {
            ++a;
        }

        static void Main(string[] args)
        {
            int num = 1;

            Program.Add(ref num);         // 실매개변수 num
            Console.WriteLine(num);
        }
    }
}
```

<br><br>