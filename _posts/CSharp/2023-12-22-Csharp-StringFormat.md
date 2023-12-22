---
title: "[Csharp]String Format"
excerpt: "String Format"

categories:
  - Csharp
tags:
  - [Csharp, String Format]

toc: true
toc_sticky: true

date: 2023-12-22
---

## 📚String Format
### 📄stirng에서 int로 변환

```cs
// string -> int
string input = "100";
int number = int.Parse(input);
```

<br>

### 📄String Format
개체, 변수 또는 식의 값을 다른 문자열에 삽입해야 하는 경우 를 사용한다.

```cs
// int -> string
int hp = 90;
int maxHp = 100;

string message = string.Format("HP: {0}, MaxHP: {1}", hp, maxHp);
Console.WriteLine(message);
```

<br>

### 📄String Interpolation
문자열 리터럴을 보간된 문자열로 식별하려면 $ 기호를 사용하여 추가한다.

```cs
// string interpolation
string message = $"HP: {hp}, MaxHP: {maxHp}";
Console.WriteLine(message);
```

<br><br>

```cs
namespace CSharp
{
    class Program
    {
        static void Main(string[] args)
        {
            // string -> int
            string input = "100";
            int number = int.Parse(input);

            Console.WriteLine(number);

            // int -> string
            int hp = 90;
            int maxHp = 100;

            //string message = string.Format("HP: {0}, MaxHP: {1}", hp, maxHp);
            //Console.WriteLine(message);

            // string interpolation
            string message = $"HP: {hp}, MaxHP: {maxHp}";
            Console.WriteLine(message);
        }
    }
```

<br><br>