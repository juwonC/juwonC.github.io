---
title: "[Cpp]이중 연결 리스트 구현"
excerpt: "이중 연결 리스트 구현"

categories:
  - DataStructure_Implementation
tags:
  - [자료구조, 구현, 이중 연결 리스트]

toc: true
toc_sticky: true

date: 2023-05-02
---

## 🤔이중 연결 리스트(Doubly Linked List)
단일 연결리스트는 포인터가 하나라 한 방향만 가리킬 수 있는 특징 때문에 특정 위치의 원소를 삭제할 때 처음 부터 탐색해야한다는 단점이 있었습니다. 이중 연결리스트는 현재 노드의 앞, 뒤 노드를 가리킬 수 있는 포인터 두개를 가지고 있어 정방향, 역방향 모두 쉽게 탐색이 가능합니다.

<br>

### 🔑이중 연결 리스트 구현
노드 구조체에 앞, 뒤를 가리키는 포인터 두개를 만들어 줍니다.

```cpp
struct Node
{
    char name[15];
    int number;
 
    Node* pNext;
    Node* pPrev;
};
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
    Node* pPrev;
};
 
struct DoubleList
{
    Node* pHead = nullptr;
    Node* pTail = nullptr;
};
 
Node* CreateNode(DoubleList& list, const char* name, const int num);
int GetCountList(DoubleList& list);
void PrintList(DoubleList& list);
Node* FindNode(DoubleList& list, const char* name);
void DeleteList(DoubleList& list);
bool DeleteNode(DoubleList& list, const char* name);
 
int main()
{
    DoubleList myList;
 
    CreateNode(myList, "A", 1);
    CreateNode(myList, "B", 2);
    CreateNode(myList, "C", 3);
    CreateNode(myList, "D", 4);
 
    std::cout << GetCountList(myList) << std::endl;
    PrintList(myList);
    std::cout << std::endl;
 
    DeleteNode(myList, "A");
    std::cout << GetCountList(myList) << std::endl;
    PrintList(myList);
    std::cout << std::endl;
 
    DeleteNode(myList, "C");
    std::cout << GetCountList(myList) << std::endl;
    PrintList(myList);
 
}
 
Node* CreateNode(DoubleList& list, const char* name, const int num)
{
    Node* element = new Node();
 
    strcpy_s(element->name, 15, name);
    element->number = num;
    element->pNext = nullptr;
    element->pPrev = nullptr;
 
    if (list.pTail == nullptr)
    {
        list.pHead = element;
        list.pTail = element;
    }
    else
    {
        element->pPrev = list.pTail;
        list.pTail->pNext = element;
        list.pTail = element;
    }
 
    return element;
}
 
int GetCountList(DoubleList& list)
{
    Node* element = list.pHead;
 
    int count{};
 
    while (element != nullptr)
    {
        count++;
        element = element->pNext;
    }
 
    return count;
}
 
void PrintList(DoubleList& list)
{
    Node* element = list.pHead;
 
    while (element != nullptr)
    {
        std::cout << element->name << " " << element->number << std::endl;
        element = element->pNext;
    }
}
 
Node* FindNode(DoubleList& list, const char* name)
{
    Node* result = nullptr;
    Node* element = list.pHead;
 
    while (element != nullptr)
    {
        if (strcmp(element->name, name) == 0)
        {
            return element;
        }
 
        element = element->pNext;
    }
 
    return nullptr;
}
 
void DeleteList(DoubleList& list)
{
    Node* element = list.pHead;
    Node* next;
 
    while (element != nullptr)
    {
        next = element->pNext;
        delete element;
 
        element = next;
    }
 
    list.pHead = nullptr;
    list.pTail = nullptr;
}
 
bool DeleteNode(DoubleList& list, const char* name)
{
    Node* element = FindNode(list, name);
    
    if (element != nullptr)
    {
        if (element->pPrev == nullptr)
        {
            list.pHead = element->pNext;
        }
        else
        {
            element->pPrev->pNext = element->pNext;
        }
 
        if (element->pNext == nullptr)
        {
            list.pTail = element->pPrev;
        }
        else
        {
            element->pNext->pPrev = element->pPrev;
        }
 
        delete element;
 
        return true;
    }
 
    return false;
}
```

<br><br>