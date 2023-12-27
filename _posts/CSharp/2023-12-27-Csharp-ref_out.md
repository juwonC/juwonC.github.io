---
title: "[Csharp]ref와 out"
excerpt: "ref와 out"

categories:
  - Csharp
tags:
  - [Csharp, ref, out]

toc: true
toc_sticky: true

date: 2023-12-27
---

## 📚ref
ref를 이용해 두 변수의 값을 바꾸는 Swap함수를 만들어보자.(ref 키워드를 사용하지 않은 CopySwap 함수는 Main 함수 안에서의 a, b가 서로 바뀌지 않은 것을 알 수 있다.)

```cs
namespace CSharp
{
    class Program
    {
        static void Swap(ref int a, ref int b)
        {
            int temp = a;
            a = b;
            b = temp;
        }

        static void CopySwap(int a, int b)
        {
            int temp = a;
            a = b;
            b = temp;
        }

        static void Main(string[] args)
        {
            int a = 1;
            int b = 2;
            ref int c = ref a;

            Program.CopySwap(a, b);     // a, b 값이 바뀌지 않음
            Console.WriteLine(a);
            Console.WriteLine(b);

            Program.Swap(ref a, ref b);
            Console.WriteLine(a);
            Console.WriteLine(b);
        }
    }
}
```

<br>

## 📚out
out 키워드를 사용하면 quotient나 remainder 처럼 변수에 값을 할당하지 않아도 함수에 사용할 수 있다.

```cs
namespace CSharp
{
    class Program
    {
        static void Divide(int a, int b, out int result1, out int result2)
        {
            result1 = a / b;
            result2 = a % b;
        }

        static void Main(string[] args)
        {
            int a = 5;
            int b = 2;

            int quotient;
            int remainder;

            Program.Divide(a, b, out quotient, out remainder);
            Console.WriteLine(quotient);
            Console.WriteLine(remainder);
        }
    }
}
```

<br><br>