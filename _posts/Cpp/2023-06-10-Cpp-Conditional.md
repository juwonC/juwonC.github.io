---
title: "[Cpp]조건문"
excerpt: "조건문"

categories:
  - Cpp
tags:
  - [Cpp, 조건문]

toc: true
toc_sticky: true

date: 2023-06-10
---

## 📚조건문
조건문은 지정된 조건에 따라 실행 흐름을 제어하는 문장입니다. 조건문에는 if문과 switch문이 있습니다.

<br>

### 📄if문
if문은 조건의 참, 거짓에 따라 문장을 선택적으로 실행할 수 있도록 하는 구문입니다. else절은 조건이 거짓일 때 처리할 문장이 있을 때만 사용하면 되고 필요 없으면 생략합니다.

```cpp
#include <iostream>

int main()
{
    int num = 0;

    std::cout << "정수 입력: ";
    std::cin >> num;

    if (num >= 0)
    {
	    if (num == 0)
	    {
		    std::cout << "입력한 숫자는 0" << std::endl;
	    }
	    else
	    {
		    std::cout << "입력한 숫자는 양수" << std::endl;
	    }
    }
    else
    {
	    std::cout << "입력한 숫자는 음수" << std::endl;
    }
}
```

<br>

else if문을 사용하면 조건을 추가할 수 있습니다.

```cpp
#include <iostream>

int main()
{
    int score = 0;

    std::cout << "점수 입력: ";
    std::cin >> score;

    if (score >= 90)
    {
	    std::cout << "A" << std::endl;
    }
    else if (score >= 80)
    {
	    std::cout << "B" << std::endl;
    }
    else
    {
	    std::cout << "C" << std::endl;
    }
}
```

<br><br>

### 📄switch문
정수 자료형인 수식의 값에 따라 문장을 실행하고자 할 때 switch문을 사용하면 편리합니다. 지정된 정수형 수식의 값이 나열된 case 값과 일치하면 그 위치에 나열된 문장으로 프로그램의 흐름이 이동됩니다.

case 값들은 문장의 위치를 가리키는 주소 같은 역할만 하기 때문에 분기가 이뤄지면 지정된 위치의 문장만 실행되는 것이 아니라 다음 case 값에 해당되는 문장이 계속 실행됩니다. 이와 같은 진행을 막기 위해 break 명령을 이용하여 switch문을 빠져 나가도록 해야 합니다.

```cpp
#include <iostream>

int main()
{
    int score = 0;

    std::cout << "점수를 입력하세요: ";
    std::cin >> score;

    switch (score / 10)
    {
    case 10:
    case 9:
      std::cout << "A";
      break;

    case 8:
      std::cout << "B";
      break;

    case 7:
      std::cout << "C";
      break;

    case 6:
      std::cout << "D";
      break;

    // 정수형 수식의 값과 일치하는 case 값이 없을 때
    default:
      std::cout << "F";
    }
}
```

<br><br>