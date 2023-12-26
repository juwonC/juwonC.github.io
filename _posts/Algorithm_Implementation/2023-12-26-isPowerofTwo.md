---
title: "[Cpp]숫자가 2의 거듭제곱인지 확인"
excerpt: "숫자가 2의 거듭제곱인지 확인"

categories:
  - Algorithm_Implementation
tags:
  - [알고리즘, 구현, 숫자가 2의 거듭제곱인지 확인]

toc: true
toc_sticky: true

date: 2023-12-26
---

## 🤔숫자가 2의 거듭제곱인지 확인
### 🔑비트 연산자 AND 사용
우선 2의 거듭제곱 4와 8을 이진수로 바꿔본다.

$$
\begin{gather}
4_2 = 100_2 \\
8_2 = 1000_2
\end{gather}
$$

위의 두 수에 1씩 빼보면 아래와 같아진다.

$$
\begin{gather}
3_2 = 011_2 \\
7_2 = 0111_2
\end{gather}
$$

여기서 4와 3, 8과 7을 각각 비트 연산 AND를 하게 되면 결과가 0이 나온다는 것을 알 수 있다.

$$
\begin{gather}
4_2 \, \& \, 3_2 = 100_2 \, \& \, 011_2 = 0  \\
8_2 \, \& \, 7_2= 1000_2 \, \& \, 0111_2 = 0
\end{gather}
$$

하지만 2의 거듭제곱이 아닌 수와 그 수의 1만큼 작은 수를 위와 같이 비트 연산 AND를 하게 되면 결과가 0이 나오지 않게 된다.

$$
7_2 \, \& \, 6_2 = 0111_2 \, \& \, 0110_2 = 0110_2 = 6
$$

<br>

```cpp
#include <iostream>

bool isPowerofTwo(int n)
{
    return (n & (n - 1)) == 0;
}

int main()
{
    // false
    std::cout << std::boolalpha << isPowerofTwo(3) << std::endl;

    // true
    std::cout << std::boolalpha << isPowerofTwo(16) << std::endl;
    
    // 시간 복잡도: O(1)
}
```

<br><br>