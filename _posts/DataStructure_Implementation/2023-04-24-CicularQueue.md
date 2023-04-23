---
title: "[C++]소수 구하기"
excerpt: "소수 구하기"

categories:
  - Algorithm_Implementation
tags:
  - [알고리즘, 구현, 소수]

toc: true
toc_sticky: true

date: 2023-04-24
---

## 🤔원형 큐
### 🔑배열로 원형 큐 구현
원형 큐는 배열로 구현했던 큐를 활용하면 쉽게 구현할 수 있습니다.

![CircularQueue](/assets/images/Implementation/CircularQueue.png){: width="200" height="200"}
<br>
[https://www.geeksforgeeks.org/introduction-to-circular-queue/](https://www.geeksforgeeks.org/introduction-to-circular-queue/)

일반 큐에 정수를 넣고자(Enqueue) 할 때 tail 인덱스를 하나 증가시킨 곳에 해당 정수를 큐 배열에 넣었습니다. 여기서 원형 큐는 한가지 더 작업이 필요합니다. tail 인덱스를 하나 증가시킨 값에 큐의 크기로 나눈 나머지를 구하고 그 값의 인덱스에 정수를 넣어주면 됩니다.

예를 들어, 5 크기의 큐가 있을 때 1씩 커지는 tail 값에 큐의 크기로 나눈 나머지 값의 인덱스는 1에서 5까지 반복됩니다. 따라서 인덱스가 반복되므로 원형 큐를 만들 수 있습니다.

```cpp
void Enqueue(Queue& queue, int value)
{
    if ((queue.tail + 1) % QUEUE_SIZE == queue.head)
    {
        return;
    }
    queue.tail = (queue.tail + 1) % QUEUE_SIZE;
    queue.container[queue.tail] = value;
}
```

<br>

정수를 원형 큐에서 빼는(Dequeue) 방법은 정수를 넣는 방식과 비슷합니다. 큐 배열에서 head 인덱스를 하나 증가시키고 큐의 크기로 나눈 나머지 값을 head에 저장하면 됩니다.

```cpp
void Dequeue(Queue& queue)
{
    if (queue.head == queue.tail)
    {
        std::cout << -1 << '\n';
        return;
    }
    queue.head = (queue.head + 1) % QUEUE_SIZE;
    std::cout << queue.container[queue.head] << '\n';
}
```

<br><br>

### 🔑전체 소스 코드
```cpp
#include <iostream>
#include <string>
const int QUEUE_SIZE = 5;
struct Queue
{
    int container[QUEUE_SIZE]{};
    int head{-1};
    int tail{-1};
};
void UserInput(Queue& queue, std::string temp);
void Enqueue(Queue& queue, int value);
void Dequeue(Queue& queue);
void Size(Queue& queue);
void Empty(Queue& queue);
void Front(Queue& queue);
void Back(Queue& queue);
void Print(Queue& queue);
int main()
{
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    std::cout.tie(nullptr);
    Queue myQueue;
    int n;
    std::cin >> n;
    for (int i = 0; i < n; i++)
    {
        std::string temp;
        std::cin >> temp;
        UserInput(myQueue, temp);
    }
}
void UserInput(Queue& queue, std::string temp)
{
    if (temp == "Enqueue")
    {
        int value;
        std::cin >> value;
        Enqueue(queue, value);
    }
    else if (temp == "Dequeue")
    {
        Dequeue(queue);
    }
    else if (temp == "size")
    {
        Size(queue);
    }
    else if (temp == "empty")
    {
        Empty(queue);
    }
    else if (temp == "front")
    {
        Front(queue);
    }
    else if (temp == "back")
    {
        Back(queue);
    }
    else if (temp == "print")
    {
        Print(queue);
    }
    else
    {
        return;
    }
}
void Enqueue(Queue& queue, int value)
{
    if ((queue.tail + 1) % QUEUE_SIZE == queue.head)
    {
        return;
    }
    queue.tail = (queue.tail + 1) % QUEUE_SIZE;
    queue.container[queue.tail] = value;
}
void Dequeue(Queue& queue)
{
    if (queue.head == queue.tail)
    {
        std::cout << -1 << '\n';
        return;
    }
    queue.head = (queue.head + 1) % QUEUE_SIZE;
    std::cout << queue.container[queue.head] << '\n';
}
void Size(Queue& queue)
{
    std::cout << queue.tail - queue.head << '\n';
}
void Empty(Queue& queue)
{
    if (queue.head == queue.tail)
    {
        std::cout << 1 << '\n';
    }
    else
    {
        std::cout << 0 << '\n';
    }
}
void Front(Queue& queue)
{
    if (queue.head == queue.tail)
    {
        std::cout << -1 << '\n';
        return;
    }
    std::cout << queue.container[queue.head + 1] << '\n';
}
void Back(Queue& queue)
{
    if (queue.head == queue.tail)
    {
        std::cout << -1 << '\n';
        return;
    }
    std::cout << queue.container[queue.tail] << '\n';
}
void Print(Queue& queue)
{
    int i = queue.head;
    while (i != queue.tail)
    {
        i = (i + 1) % QUEUE_SIZE;
        std::cout << queue.container[i] << " ";
    }
    std::cout << '\n';
}
```

<br><br>