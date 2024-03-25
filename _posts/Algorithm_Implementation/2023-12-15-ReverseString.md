---
title: "[Cpp]문자열 뒤집기"
excerpt: "문자열 뒤집기"

categories:
  - Algorithm_Implementation
tags:
  - [알고리즘, 구현, 문자열 뒤집기]

toc: true
toc_sticky: true

date: 2023-12-15
---

## 🤔문자열 뒤집기
### 🔑배열 사용
뒤집은 문자열을 저장할 배열을 하나 더 만든다.

기존 배열의 마지막 문자 부터 첫 문자까지 반대로 새로운 배열에 대입한다.

배열의 인덱스는 0번부터 시작하는 것과 문자열 끝에는 null 문자가 있다는 것에 주의해서 문자열을 다룬다.

```cpp
#include <iostream>

int main()
{
    char str[14] = "ReverseString";
    char reverse[14] = {0,};

    for (int i = 0; i < sizeof(str); ++i)
    {
        // 문자열 마지막에 반드시 null 문자를 넣어줘야 한다
        if (i == sizeof(str) - 1)
        {
            reverse[sizeof(str) - 1] = '\0';
            break;
        }
        
        // 배열의 인덱스는 0부터 시작
        // null 문자 제외
        // 따라서 (문자열 길이 - 2) 하면 마지막 문자에 접근 가능
        reverse[i] = str[sizeof(str) - i - 2];
    }

    std::cout << "Reversed: " << reverse << std::endl;
}
```

<br>

### 🔑포인터 사용
첫 글자의 포인터와 마지막 글자의 포인터를 이용해서 문자열을 뒤집을 수 있다.

포인터의 역참조를 통해 첫 글자와 마지막 글자의 위치를 바꿔주는데 아래와 같은 조건이 있다.

첫 글자의 주소가 마지막 글자의 주소보다 커지거나 같아질 때까지 첫 글자의 주소는 증가시키고 마지막 글자의 주소는 감소시킨다.

첫 글자의 주소가 마지막 글자의 주소보다 커지거나 같아지면 뒤집을 문자가 없기 때문에 반복을 종료하는 것이다.

```cpp
#include <iostream>

int main()
{
    char str[14] = "ReverseString";
    
    // 문자열의 첫 글자 주소
    char* head = str;
    // 문자열의 마지막 글자 주소(null 문자 제외)
    char* tail = str + sizeof(str) - 2;

    while (head < tail)
    {
        // 문자 뒤집기
        char temp = *head;
        *head = *tail;
        *tail = temp;

        ++head;
        --tail;
    }

    std::cout << "Reversed: " << str << std::endl; // 결과: gnirtSesreveR
}
```

<br><br>