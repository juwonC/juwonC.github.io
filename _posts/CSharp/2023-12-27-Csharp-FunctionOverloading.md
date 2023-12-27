---
title: "[Csharp]함수 오버로딩"
excerpt: "함수 오버로딩"

categories:
  - Csharp
tags:
  - [Csharp, 함수 오버로딩]

toc: true
toc_sticky: true

date: 2023-12-27
---

## 📚함수 오버로딩
함수 이름을 재사용하는 것을 오버로딩이라고 한다. 즉 같은 이름의 함수를 사용할 수 있다는 것이다. 하지만 같은 이름의 함수들의 매개변수는 서로 달라야 한다.

다만, 반환형식은 오버로딩에 영향을 주지 않는다. 예를 들어 이름과 매개변수가 같은 함수가 있는데 반환형만 다르다면 오버로딩되지 않는다.

```cs
namespace CSharp
{
    class Program
    {
        static int Add(int a, int b)
        {
            Console.WriteLine("int Add 호출");
            return a + b;
        }

        // 컴파일 에러(반환형은 함수 오버로딩에 영향을 주지 않는다.)
        //static void Add(int a, int b)
        //{
        //    Console.WriteLine("void Add 호출");
        //    a + b;
        //}

        static float Add(float a, float b)
        {
            Console.WriteLine("float Add 호출");
            return a + b;
        }

        static void Main(string[] args)
        {
            int a = 1;
            int b = 1;

            float c = 3.14f;
            float d = 2.17f;

            Console.WriteLine(Add(a, b));   // int Add 호출
            Console.WriteLine(Add(c, d));   // float Add 호출
        }
    }
}
```

<br><br>