---
title: "[Csharp]깊은 복사"
excerpt: "깊은 복사"

categories:
  - Csharp
tags:
  - [Csharp, 깊은 복사]

toc: true
toc_sticky: true

date: 2024-01-05
---

## 📚복사와 참조
C#의 클래스는 기본적으로 참조로 동작하고 구조체는 복사로 동작한다.

```cs
        // 참조
        class Knight
        {
            public int hp;
            public int attack;

            public void Move()
            {
                Console.WriteLine("Knight Move");
            }

            public void Attack()
            {
                Console.WriteLine("Knight Attack");
            }
        }

        // 복사
        struct SMage
        {
            public int hp;
            public int attack;
        }

        static void KillMage(SMage mage)
        {
            mage.hp = 0;
        }

        static void KillKnight(Knight knight)
        {
            knight.hp = 0;
        }

        static void Main(string[] args)
        {
            SMage mage;
            mage.hp = 100;      // KillMage 함수를 호출해도 값이 변하지 않음
            mage.attack = 3;
            KillMage(mage);     // mage가 복사로 전달됨

            Knight knight = new Knight();
            knight.hp = 100;    // KillKnight 함수를 호출하면 값이 0으로 변함
            knight.attack = 5;
            knight.Move();
            knight.Attack();
            KillKnight(knight); // knight가 참조로 전달됨
        }
```

<br><br>

## 📚얕은 복사
기존에 만들었던 기사 개체(object)를 다른 기사 클래스에 대입해보면 아래와 같다.

```cs
        static void Main(string[] args)
        {
            Knight knight = new Knight();
            knight.hp = 100;

            Knight knight2 = knight;    // 얕은 복사
            knight2.hp = 0;
        }
```

knight2에 knight를 복사하고 knight2의 hp를 0으로 수정하면 클래스는 참조로 동작하기 때문에 knight의 hp도 0이 되는 것을 확인 할 수 있다.

![CSharpShallowCopy](/assets/images/CSharp/CSharpShallowCopy.png){: width="700" height="700"}{: .align-center}

첫 번째 기사 개체를 만든 다음 이후에 만들 기사 개체들은 독립적으로 관리하면서 처음 만들었던 기사의 속성(hp, attack)만 초기값으로 가지고 있게 하려면 깊은 복사가 필요하다.

<br><br>

## 📚깊은 복사
얕은 복사가 되지 않게 새로운 개체를 하나더 만들어서 그 곳에 복사를 해도 되지만 기사 클래스 안에서 깊은 복사가 되게끔 함수를 추가해서 해결할 수 있다.

Knight를 반환하는 Clone() 이라는 함수를 정의하면 아래와 같다. Clone() 함수를 호출하면 기사 개체를 새로 만들고 그 개체의 hp와 attack 값에 원래 기사가 가지고 있던 값을 대입한다. 마지막으로 새로 만든 기사의 개체를 반환한다.

```cs
        class Knight
        {
            public int hp;
            public int attack;

            // 깊은 복사
            public Knight Clone()
            {
                Knight knight = new Knight();
                knight.hp = hp;
                knight.attack = attack;

                return knight;
            }

            public void Move()
            {
                Console.WriteLine("Knight Move");
            }

            public void Attack()
            {
                Console.WriteLine("Knight Attack");
            }
        }
```

얕은 복사와 달리 깊은 복사를 하면 기존 knight의 hp가 0으로 바뀌지 않고 새로 만든 기사 개체의 hp만 0으로 바뀌는걸 확인할 수 있다.

```cs
        static void Main(string[] args)
        {
            Knight knight = new Knight();
            knight.hp = 100;

            Knight cloneKnight = knight.Clone();    // 깊은 복사
            cloneKnight.hp = 0;
        }
```

![CSharpDeepCopy](/assets/images/CSharp/CSharpDeepCopy.png){: width="700" height="700"}{: .align-center}

<br><br>