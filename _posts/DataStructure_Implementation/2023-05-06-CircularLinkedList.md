---
title: "[C++]원형 연결 리스트 구현"
excerpt: "원형 연결 리스트 구현"

categories:
  - DataStructure_Implementation
tags:
  - [자료구조, 구현, 원형 연결 리스트]

toc: true
toc_sticky: true

date: 2023-05-06
---

## 🤔원형 연결 리스트(Circular Linked List)
### 🔑이중 연결 리스트 구현
원형 연결 리스트는 마지막 노드를 처음 노드에 연결 시켰다는 점에서 단일 연결 리스트와 차이가 있습니다.

전에 구현했던 단일 연결 리스트를 조금 바꿔 원형 연결 리스트를 구현해보겠습니다.

원형 연결 리스트의 노드 생성은 단일 연결 리스트처럼 맨 뒤에 추가하는 방식으로만 구현했습니다. 하지만 노드 삽입은 단일 리스트의 삽입과 달리 아래 그림처럼 추가될 노드가 처음 노드를 가리키도록 한 다음 pHead가 추가될 노드를 가리키도록 하였습니다.

![CircularQueue](/assets/images/Implementation/CircularLinkedList.png){: width="400" height="400"}
<br>
[https://www.geeksforgeeks.org/circular-linked-list/](https://www.geeksforgeeks.org/circular-linked-list/)

```cpp
Node* CreateNode(CircularList& list, const char* name, const int num)
{
    Node* element = new Node();
 
    strcpy_s(element->name, 15, name);
    element->number = num;
    element->pNext = nullptr;
 
    if (list.pHead == nullptr)
    {
        // pHead가 추가될 노드를 가리키고
        // 첫 노드는 자기 자신을 가리킴
        list.pHead = element;
        element->pNext = list.pHead;
    }
    else
    {
        // 추가될 노드가 추가했던 전 노드를 가리키고
        // 추가했던 전 노드가 추가될 노드를 가리킴
        // 마지막으로 pHead가 추가시킬 노드를 가리킴
        element->pNext = list.pHead->pNext;
        list.pHead->pNext = element;
        list.pHead = element;
    }
 
    return element;
}
```

<br><br>

### 🔑전체 소스 코드

```cpp
#include <iostream>
#include <string.h>
 
struct Node
{
    char name[15];
    int number;
 
    Node* pNext;
};
 
struct CircularList
{
    Node* pHead{ nullptr };
};
 
Node* CreateNode(CircularList& list, const char* name, const int num);
int GetCountList(CircularList& list);
void PrintList(CircularList& list);
Node* FindNode(CircularList& list, const char* name);
void DeleteList(CircularList& list);
bool DeleteNode(CircularList& list, const char* name);
 
int main()
{
    CircularList myList;
 
    CreateNode(myList, "A", 1);
    CreateNode(myList, "B", 2);
    CreateNode(myList, "C", 3);
    CreateNode(myList, "D", 4);
 
    std::cout << GetCountList(myList) << std::endl;
 
    PrintList(myList);
    std::cout << std::endl;
 
    std::cout << FindNode(myList, "B")->number << std::endl;
    std::cout << std::endl;
 
    DeleteNode(myList, "A");
    DeleteNode(myList, "D");
    
    PrintList(myList);
 
    DeleteList(myList);
}
 
Node* CreateNode(CircularList& list, const char* name, const int num)
{
    Node* element = new Node();
 
    strcpy_s(element->name, 15, name);
    element->number = num;
    element->pNext = nullptr;
 
    if (list.pHead == nullptr)
    {
        list.pHead = element;
        element->pNext = list.pHead;
    }
    else
    {
        element->pNext = list.pHead->pNext;
        list.pHead->pNext = element;
        list.pHead = element;
    }
 
    return element;
}
 
int GetCountList(CircularList& list)
{
    Node* element = list.pHead->pNext;
 
    int count{};
 
    while (element != list.pHead)
    {
        if (list.pHead == nullptr)
        {
            return false;
        }
 
        ++count;
        element = element->pNext;
    }
 
    return ++count;
}
 
void PrintList(CircularList& list)
{
    Node* element = list.pHead;
 
    if (list.pHead == nullptr)
    {
        return;
    }
    
    do
	{
        element = element->pNext;
        std::cout << element->name << " " << element->number << std::endl;
	}
    while (element != list.pHead);
}
 
Node* FindNode(CircularList& list, const char* name)
{
    Node* element = list.pHead;
 
    while (element != nullptr)
    {
        if (strcmp(element->name, name) == 0)
        {
            return element;
        }
 
        element = element->pNext;
    }
 
    return element;
}
 
void DeleteList(CircularList& list)
{
    Node* element = list.pHead;
    Node* next;
 
    while (element != list.pHead)
    {
        next = element->pNext;
        delete element;
 
        element = next;
    }
 
    list.pHead = nullptr;
}
 
bool DeleteNode(CircularList& list, const char* name)
{
    Node* element = list.pHead->pNext;
    Node* previous = list.pHead;
 
    while (element != list.pHead)
    {
        if (strcmp(element->name, name) == 0)
        {
            break;
        }
 
        previous = element;
        element = element->pNext;
    }
 
    if (element == nullptr)
    {
        return false;
    }
 
    if (list.pHead == nullptr)
    {
        list.pHead = nullptr;
    }
    else if (element == list.pHead)
    {
        if (list.pHead == list.pHead->pNext)
        {
            list.pHead = nullptr;
        }
        else
        {
            list.pHead = previous;
            previous->pNext = element->pNext;
        }
    }
    else
    {
        previous->pNext = element->pNext;
    }
 
    delete element;
 
    return true;
}
```

<br><br>