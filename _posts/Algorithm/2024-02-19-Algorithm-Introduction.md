---
title: "[Algorithm]알고리듬 소개"
excerpt: "알고리듬 소개"

categories:
  - Algorithm
tags:
  - [알고리듬]

toc: true
toc_sticky: true

date: 2024-02-19
---

## 📚알고리듬이란 무엇인가?
### 📄기본 개념
알고리듬은 문제를 해결하기 위한 단계적인 처리 과정을 말한다. 컴퓨터 과학에서의 알고리듬이란 주어진 문제를 해결하거나 함수를 계산하기 위해 따라야할 명령어들을 단계적으로 나열한 것이다.

💡알고리즘이 되기 위한 조건

* 입출력: 외부에서 0개 이상의 입력을 받아 하나 이상의 출력을 생성해야 한다
* 명확성: 각 단계는 모호하지 않고 단순, 명확해야 한다
* 유한성: 일정 단계를 거친 후 반드시 끝나야 한다
* 유효성: 모든 명령은 컴퓨터에서 수행할 수 있어야 한다

위 조건들을 만족하는 알고리듬이라도 효율적, 실용적이지 못하다면 문제를 해결하는데 어려움이 있을 수 있다.

<br><br>

## 📚알고리듬 설계
알고리듬은 다음과 같은 과정을 거쳐 생성된다.

설계 -> 표현/기술 -> 정확성 검증 -> 효율성 분석

알고리듬은 문제의 조건에 따라 해결 방법이 달라질 수 있다. 따라서 일반적, 범용적인 알고리듬 설계 기법은 존재하지 않는다.

하지만 많은 부류의 문제에서 사용할 수 있는 대표적인 알고리듬 설계기법에는 욕심쟁이(greedy) 방법, 분할정복(divide-and-conquer) 방법, 동적 프로그래밍(dynamic programming) 방법이 있다.

<br>

### 📄욕심쟁이(greedy) 방법
해를 구하는 일련의 선택 과정에서 앞뒤의 선택과 상관없이 각 단계(현재 단계)에서 가장 최선이라고 여겨지는 최적해를 선택해 나가면 결과적으로 전체적인 최적해를 구할 수 있을 것이라는 희망적인 전략이다. 이 방법은 주로 최소값, 최대값을 구하는 최적화 문제에 주로 사용된다.

* 장점: 간단하면서 효율적인 알고리듬을 만들 수 있다.

* 단점: 욕심쟁이 방법은 현재 상태에서만 만족하는 최적해를 선택하기 때문에 반드시 최적해를 구할 수 있다는 보장은 하지 못한다.

대표적인 응용문제로는 거스름돈 문제, 배낭 문제, 크루스칼 알고리듬, 프림 알고리듬, 다익스트라 알고리듬 등이 있다.

<br>

📍 거스름돈 문제

고객에게 돌려줄 거스름돈이 있을 때 고객이 받을 동전의 개수가 최소가 되게끔 하는 문제.

```c
#include <stdio.h>

void main()
{
	// 거스름돈 780원이 있을 때 돌려줄 동전의 최소 개수를 구하는 문제
	int change = 780;
	int coins[4] = { 500, 100, 50, 10 };
	int count = 0;
	
	for (int i = 0; i < sizeof(coins) / sizeof(int); ++i)
	{
		// 거스름돈에서 최고 금액의 동전을 계속 빼준다 -> 동전을 뺄 수 있으면 count 1 증가
		// 뺀 결과가 현재 동전의 금액보다 작으면 while문을 빠져나와
		// 다음으로 작은 금액의 동전을 뺀다
		while (change > coins[i])
		{
			change -= coins[i];

			++count;
		}
	}

	printf("%d", count);
}
```

이중 반복문과 뺄셈을 이용해서 문제를 해결할 수도 있지만 나눗셈과 나머지 연산을 통해 문제를 해결할 수 있다.

```c
	for (int i = 0; i < sizeof(coins) / sizeof(int); ++i)
	{
		count += change / coins[i];
		change %= coins[i];
	}
```

<br>

하지만 동전의 금액이 일반적인 경우에 욕심쟁이 방법으로 해결할 수 없다.

```c
#include <stdio.h>

void main()
{
	int change = 650;
	int coins[5] = { 500, 120, 100, 50, 10 };
	int count = 0;
	
	for (int i = 0; i < sizeof(coins) / sizeof(int); ++i)
	{
		while (change >= coins[i])
		{
			change -= coins[i];

			++count;
		}
	}

	printf("%d", count); // count: 5

  // 최적해는 500원 1개, 100원 1개, 50원 1개로 3이다.
}
```

<br>

📍 배낭 문제

배낭의 용량을 초과하지 않는 범위에서 배낭에 들어 있는 물체들의 이익의 합이 최대가 되도록 물체를 넣는 방법을 찾는 문제.(물체를 쪼개서 넣을 수 있다는 가정이 있다.)

```c
#include <stdio.h>

void main()
{
	int bagCapacity = 10;
	int count = 4;
	int totalProfit = 0;

	int profit[4] = { 15, 20, 9, 14 };
	int weight[4] = { 3, 5, 3, 4 };
	double profitPerWeight[4];
	int rank[4];

	// 단위 무게 당 이익을 계산하고, 이것이 최대가 되는 물체부터 최대한 배낭에 넣으면 최적해를 구할 수 있다
	for (int i = 0; i < count; ++i)
	{
		profitPerWeight[i] = (double)profit[i] / (double)weight[i];
		rank[i] = 0;
	}

	// 단위 무게 당 이익을 구했으면, 각 단위 무게에 순위를 부여한다
	// 순위가 낮을수록 단위 무게 당 이익이 높고 배낭에 가장 먼저 들어간다
	for (int i = 0; i < count; ++i)
	{
		int index = 1;

		for (int j = 0; j < count; ++j)
		{
			if (profitPerWeight[i] < profitPerWeight[j])
			{
				rank[i] = index++;
			}
		}
	}
	
	for (int i = 0; i < count; ++i)
	{
		for (int j = 0; j < count; ++j)
		{
			if (bagCapacity <= 0)
			{
				break;
			}

			// 단위 무게 당 이익이 가장 높은 순서대로 배낭에 넣는다
			if (i == rank[j])
			{
				// 해당 단위 무게 당 이익과 대응되는
				// 원래 물체의 무게가 배낭 보다 작으면 물체를 배낭에 넣는다
				if (weight[j] < bagCapacity)
				{
					bagCapacity -= weight[j];
					totalProfit += profit[j];
				}
				else // 배낭에 남은 용량이 있다면 물체를 쪼개서 넣는다
				{
					// 단위 무게 당 이익을 알기 때문에 
					// 남은 배냥 용량에 해당 이익을 곱하고 그 결과를 총 이익에 더해준다
					totalProfit += (bagCapacity * (double)profit[j] / (double)weight[j]);
					bagCapacity -= bagCapacity;
				}
			}
		}
	}

	printf("%d", totalProfit);
}
```

물체를 쪼갤 수 없는 형태의 배낭 문제(0/1 배낭 문제)는 욕심쟁이 방법으로 해결할 수 없다.

<br>

### 📄분할정복(divide-and-conquer) 방법

순환적으로 문제를 푸는 하향식 접근 방법이다. 문제의 입력을 더 이상 나눌 수 없을 때까지 2개 이상의 작은 문제들로 순환적으로 분할하고, 분할된 작은 문제들을 해결한 후 이들의 해를 결합하여 원래 문제의 해를 구하는 방식이다.

분할정복 방법은 분할된 작은 문제는 입력의 크기만 작아졌을 뿐이지 원래 문제와 동일하다는 특징이 있다. 그리고 분할된 문제는 서로 독립적이라서 순환적으로 분할이 가능하고 그 결과를 결합할 수 있다.

💡분할정복 방법의 세 가지 단계

* 분할: 주어진 문제의 입력을 여러 개의 작은 문제로 분할한다.
* 정복: 작은 문제들을 순환적으로 분할. 작은 문제가 더 이상 분할되지 않을 정도로 작으면 순환 호출 없이 작은 문제의 해를 구한다.
* 결합: 작은 문제에 대해 정복된 해를 결합하여 원래 문제의 해를 구한다.

분할정복 방법을 적용한 대표적인 알고리듬은 퀵 정렬, 합병 정렬, 이진 탐색 등이 있다.

<br>

📍 이진 탐색

```c
#include <stdio.h>

int BinarySearch(int left, int right, int* array, int key)
{
	if (left > right)
	{
		return -1;
	}

	// 배열의 가운데 원소를 기준으로 왼쪽과 오른쪽 부분배열로 분할
	int mid = (left + right) / 2;

	// 탐색 키와 가운데 원소가 같은면 배열 인덱스 반환
	if (array[mid] == key)
	{
		return mid;
	}
	// 탐색 키가 가운데 원소보다 작으면 왼쪽 부분배열 대상으로 이진 탐색 순환 호출
	else if (key < array[mid])
	{
		BinarySearch(left, mid - 1, array, key);
	}
	// 탐색 키가 가운데 원소보다 크면 오른쪽 부분배열 대상으로 이진 탐색 순환 호출
	else
	{
		BinarySearch(mid + 1, right, array, key);
	}

	// 부분배열에 대한 탐색 결과가 직접 반환 -> 결합 불필요
}

void main()
{
	int array[9] = { 10, 15, 20, 25, 30, 35, 40, 45, 50 };
	int arraySize = sizeof(array) / sizeof(int);

	int targetIndex = BinarySearch(0, arraySize - 1, array, 20);

	printf("%d", targetIndex); // targetIndex: 2
}
```

<br>

### 📄동적 프로그래밍(dynamic programming) 방법

동적 프로그래밍 방법은 입력의 크기가 가장 작은 부분 문제부터 해를 구하여 테이블에 저장하고 이것을 이용해서 입력 크기가 큰 문제의 해를 점진적으로 만들어 가는 상향식 접근 방법이다.

각각의 작은 문제는 입력의 크기만 작을뿐이지 원래 문제와 동일하다는 점에서 분할정복과 유사하지만 작은 문제들은 서로 독립일 필요가 없다는 점에서 분할정복과는 다르다.(작은 문제들이 서로 겹치는 부분이 있다.)

동적 프로그래밍 방법을 적용한 대표적인 알고리듬은 플로이드 알고리듬, 행렬의 연쇄적 곱셈 문제, 최장 공통 부분 수열 문제 등이 있다.

<br><br>