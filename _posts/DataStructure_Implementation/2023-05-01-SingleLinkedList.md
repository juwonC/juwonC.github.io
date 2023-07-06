---
title: "[Cpp]단일 연결 리스트 구현"
excerpt: "단일 연결 리스트 구현"

categories:
  - DataStructure_Implementation
tags:
  - [자료구조, 구현, 단일 연결 리스트]

toc: true
toc_sticky: true

date: 2023-05-01
---

## 🤔단일 연결 리스트(Single Linked List)
단일 연결 리스트는 일렬로 나열된 동적 자료구조 입니다. 단일 연결 리스트를 구현하기 위해 동적 자료구조에 대해 간단하게 알아보겠습니다.

### 🔑정적 자료구조와 동적 자료구조
정적 자료구조는 구조의 크기가 고정되어있는 자료구조입니다. 프로그램이 실행되기 전 컴파일할때 크기를 정확하게 알 수 있어야 사용 가능합니다. 예를들어 배열의 크기를 정할 때 변수를 사용할 수 없고 상수를 사용해야하는 경우입니다.

```cpp
int size = 5;
int array[size];            // 불가능


const int ARRAY_SIZE = 10;
int array[ARRAY_SIZE];      // 가능
```

<br>

반면에, 동적 자료구조는 구조의 크기가 고정되어 있지 않고 프로그래머가 원할 때 그 크기를 바꿀 수 있는 자료구조입니다. 프로그래머가 메모리를 얼마나 사용할 것인지 직접 지정할 수 있어 자료구조의 크기가 런타임에 결정될 수 있습니다.

아래 코드로 예를들면 프로그램이 실행되고 있는 중에 배열의 크기를 우리가 직접 정해 줄 수 있습니다. 

```cpp
#include <iostream>
 
int main()
{	
    int size{};
    
    std::cin >> size;
    
    if(size <= 0)
    {
    	return 0;
    }
    
    int* pArray = new int[size]{};
    
    delete[] pArray;
    pArray = nullptr;
}
```

<br><br>

### 🔑자기 참조 구조체(Self Referential Structures)
동적 자료구조를 만들기위해 new와 delete를 이용해 배열을 동적으로 할당해보겠습니다.

```cpp
int* array = new int[50];
```

<br>

배열 크기가 50까지는 동적으로 메모리에 할당되고 제거되겠지만 더 큰 크기의 배열이 필요하게 되면 어떻게 해야될까요? 기존에 있는 것에서 늘릴 수 없으니 새로 배열을 만들어야합니다.

```cpp
int* temp = new int[100];
 
for(int i = 0; i < 50; i++)
{
    temp[i] = array[i];
}
 
delete[] array;
array = temp;
```

<br>

기존의 데이터들도 그대로 가져오려면 배열을 복사하고 기존의 포인터를 해제한 후 새로운 배열 포인터를 할당해주면 됩니다. 메모리가 할당된채 남아 있을 수 있어서 해체를 꼭 해줍시다. 동적으로 할당된 메모리를 제어하는 realloc()이라는 함수를 사용하면 코드가 좀 더 짧아지지만 컴퓨터 내부에서 하는 일은 크게 달라지지 않습니다. 데이터 양이 많아질수록 메모리를 재할당하고 복사해주는 과정에서 비효율적인 오버헤드가 발생합니다.

위의 과정처럼 데이터를 복사하지 않고 동적 자료구조를 상수 시간으로 관리하기 위해 자기 참조 구조체라는 걸 만들어 봅시다.

```cpp
struct Node
{
    char name[15];
    int number;
    
    Node* pNext;
};
```

<br>

자기 참조 구조체는 멤버에 한 개 또는 그 이상의 자기 자신과 같은 타입의  포인터를 가지고 있습니다. 이 포인터를 이용하여 구조체들을 연결하는 것입니다.

두 개의 구조체를 만들어 서로 연결해보면 아래와 같습니다.

```cpp
Node* nodeA = new Node{ "A", 10, nullptr };
Node* nodeB = new Node{ "B", 20, nullptr };
 
nodeA->pNext = nodeB;
```

<br><br>

### 🔑단일 연결 리스트 구현

```cpp
#include <iostream>
#include <string.h>
 
struct Node
{
    char name[15];
    int number;
    
    Node* pNext;
};
 
struct SingleList
{
    Node* pHead = nullptr;
    Node* pTail = nullptr;
};
 
Node* CreateNode(SingleList& list, const char* name, const int num);
int GetCountList(SingleList& list);
void PrintList(SingleList& list);
Node* FindNode(SingleList& list, const char* name);
void DeleteList(SingleList& list);
bool DeleteNode(SingleList& list, const char* name);
 
int main()
{
    SingleList myList;
 
    CreateNode(myList, "A" , 1);
    CreateNode(myList, "B" , 2);
    CreateNode(myList, "C" , 3);
    CreateNode(myList, "D" , 4);
 
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
 
Node* CreateNode(SingleList& list, const char* name, const int num)
{
    Node* element = new Node();
 
    strcpy_s(element->name, 15, name);
    element->number = num;
 
    if(list.pTail == nullptr)
    {
        list.pHead = element;
        list.pTail = element;
    }
    else
    {
        list.pTail->pNext = element;
        list.pTail = element;
    }
 
    return element;
}
 
int GetCountList(SingleList& list)
{
    Node* element = list.pHead;
 
    int count{};
 
    while(element != nullptr)
    {
        count++;
        element = element->pNext;
    }
 
    return count;
}
 
void PrintList(SingleList& list)
{
    Node* element = list.pHead;
 
    while(element != nullptr)
    {
        std::cout << element->name << " " << element->number << std::endl;
        element = element->pNext;
    }
}
 
Node* FindNode(SingleList& list, const char* name)
{
    Node* result = nullptr;
    Node* element = list.pHead;
 
    while(element != nullptr)
    {
        if(strcmp(element->name, name) == 0)
        {
            return element;
        }
 
        element = element->pNext;
    }
 
    return nullptr;
}
 
void DeleteList(SingleList& list)
{
    Node* element = list.pHead;
    Node* next;
 
    while(element != nullptr)
    {
        next = element->pNext;
        delete element;
 
        element = next;
    }
 
    list.pHead = nullptr;
    list.pTail = nullptr;
}
 
bool DeleteNode(SingleList& list, const char* name)
{
    Node* element = list.pHead;
    Node* previous = nullptr;
 
    while(element != nullptr)
    {
        if(strcmp(element->name, name) == 0)
        {
            break;
        }
 
        previous = element;
        element = element->pNext;
    }
 
    if(element == nullptr)
    {
        return false;
    }
 
    if(list.pHead == list.pTail)
    {
        list.pHead = list.pTail = nullptr;
    }
    else if(previous == nullptr)
    {
        list.pHead = element->pNext;
    }
    else if(element == list.pTail)
    {
        previous->pNext = nullptr;
        list.pTail = previous;
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