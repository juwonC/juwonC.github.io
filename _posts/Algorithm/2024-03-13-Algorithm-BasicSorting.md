---
title: "[Algorithm]기초적인 정렬"
excerpt: "기초적인 정렬"

categories:
  - Algorithm
tags:
  - [알고리듬]

toc: true
toc_sticky: true

date: 2024-03-13
---

## 📚정렬
### 📄기본 개념

정렬은 주어진 데이터를 값의 크기 순서에 따라 재배치하는 것이다.

정렬 수행 시점에 데이터가 어디에 저장되어 있는지에 따라 정렬을 내부 정렬과 외부 정렬로 구분할 수 있다.

<br>

### 📄내부 정렬
전체 데이터를 주기억장치에 저장한 후 정렬을 수행

* 비교 기반 알고리듬

두 데이터의 값 전체를 직접적으로 비교하여 정렬 수행. 값의 비교 횟수를 알고리듬의 수행시간으로 간주.

(선택정렬, 버블 정렬, 삽입 정렬, 셀 정렬) -> O(n<sup>2</sup>)

(큌 정렬, 합병 정렬, 힙 정렬) -> O(n log n)

* 데이터 분포 기반 알고리듬

데이터의 분포에 기반한 정보를 바탕으로 정렬 수행. 데이터의 이동 횟수를수행시간으로 간주.

(계수 정렬, 기수 정렬, 버킷 정렬) -> O(n)

<br>

### 📄외부 정렬

모든 데이터를 주기억장치에 저장할 수 없을 때 데이터를 보조기억장치에 저장해 두고 그 중 일부 데이터만을 반복적으로 주기억장치로 옮겨와서 정렬을 수행

<br>

### 📄안정적 정렬

같은 값을 갖는 데이터가 여러 개 있을 때 정렬 전의 상대적 위치가 정렬 후에도 그대로 유지되는 것이 보장되는 정렬.

<br>

### 📄제자리 정렬

입력 배열 이외에 별도로 필요한 저장 공간이 상수 개를 넘지 않는 정렬. 입력 크기가 증가해도 추가적인 저장 공간이 증가하지 않는 정렬이다.

<br><br>

## 📚기초적인 정렬

모든 정렬 알고리듬은 배열 A[0...n-1]에 저장된 n개의 양의 정수에 대해 오름차순으로 정렬한다고 가정한다.

### 📄선택 정렬

입력 배열에서 가장 작은 값부터 순서대로 선택해서 나열하는 방식의 정렬.

```c
#include<stdio.h>

void SelectionSort(int array[], int size)
{
	for (int i = 0; i < size - 1; i++) // n - 1번 반복
	{
		int min = i; // 미정렬 부분의 첫 번째 원소를 최소값으로 지정

		// A[i ... n-1]에서 최소값 찾기
		for (int j = i + 1; j < size; j++)
		{
			if (array[min] > array[j])
			{
				min = j;
			}
		}

		// 미정렬 부분의 첫 번째 원소와 최소값 위치 교환
		int temp = array[i];
		array[i] = array[min];
		array[min] = temp;
	}
}

void Print(int array[], int size)
{
	for (int i = 0; i < size; i++)
	{
		printf("%d ", array[i]);
	}
}

int main()
{
	int array[] = { 60, 20, 70, 10, 80, 30, 50, 40 };
	int arraySize = sizeof(array) / sizeof(int);

	SelectionSort(array, arraySize);
	Print(array, arraySize);

	return 0;
}
```

* 성능과 특징
	- 시간 복잡도: O(n<sup>2</sup>)
	- 입력 데이터의 순서에 민감하지 않다.
	- 제자리 정렬 알고리듬이다.
	- 안정적이지 않은 정렬 알고리듬이다.

<br>

### 📄버블 정렬

모든 인접한 두 데이터를 차례대로 비교해서 왼쪽이 더 큰 경우에 오른쪽과 자리를 바꾸는 과정을 반복하는 정렬.

```c
void BubbleSort(int array[], int size)
{
	for (int i = 0; i < size - 1; i++) // n - 1번 반복
	{
		for (int j = 0; j < size - 1; ++j) // 왼쪽에서 오른쪽으로 진행
		{
			if (array[j] > array[j + 1]) // 왼쪽이 오른쪽 보다 큰 경우
			{
				// 왼쪽과 오른쪽 자리 바꿈
				int temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
			}
		}
	}
}
```

* 성능과 특징
	- 시간 복잡도: O(n<sup>2</sup>)
	- 안정적인 정렬 알고리듬이다.
	- 제자리 정렬 알고리듬이다.
	- 선택 정렬에 비해 데이터 교환이 많이 발생 -> 선택 정렬보다 비효율적
	- 개선의 여지가 있다.

<br>

### 📄개선된 버블 정렬

```c
#include<stdbool.h>

void AdvancedBubbleSort(int array[], int size)
{
	for (int i = 0; i < size - 1; i++)
	{
		bool bIsSorted = true; // 이미 정렬된 상태라고 가정

		for (int j = 0; j < size - 1 - i; j++) // 왼쪽에서 오른쪽으로 진행
		{
			if (array[j] > array[j + 1])
			{
				int temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;

				// 자리바꿈이 발생하면 정렬되지 않은 상태
				// 계속 다음 단계 처리 필요
				bIsSorted = false;
			}
		}

		// 이미 정렬된 상태라서 이후 단계 불필요
		if (bIsSorted)
		{
			break;
		}
	}
}
```

* 성능과 특징
	- 시간 복잡도: O(n<sup>2</sup>)
	- 입력 데이터의 상태에 따라 성능 달라짐. 최악의 경우: O(n<sup>2</sup>), 최선의 경우: O(n)

<br>

### 📄삽입 정렬

주어진 데이터를 하나씩 뽑고 이미 나열된 데이터가 항상 정렬된 상태를 유지하도록 뽑은 데이터를 바른 위치에 삽입하는 방식의 정렬.

```c
void InsertionSort(int array[], int size)
{
	int i;
	int j;
	int val;

	for (i = 1; i < size; i++) // 1, ..., n - 1 까지 반복
	{
		val = array[i]; // 미정렬 부분 array[i, ..., n - 1]의 첫 번째 데이터 선택

		for (j = i; j > 0 && array[j - 1] > val; j--) // 정렬 부분에서 삽입할 위치 찾기
		{
			array[j] = array[j - 1]; // 정렬 부분의 array[j - 1]이 크면 뒤로 한 칸 이동
		}

		array[j] = val; // 찾은 위치에 선택된 데이터 삽입
	}
}
```

* 성능과 특징
	- 시간 복잡도: O(n<sup>2</sup>)
	- 안정적인 정렬 알고리듬이다.
	- 제자리 정렬 알고리듬이다.
	- 입력 데이터의 순서에 민감하다.

<br>

### 📄셸 정렬

도널드 셸이 삽입 정령의 단점을 보완하기 위해 고안한 정렬 알고리듬이다.

삽입 정렬은 현재 삽입하고자 하는 데이터가 삽입될 제 위치에서 많이 벗어나 있어도 한 번에 한 자리씩만 이동해서 찾아가야 하는 단점이 있다.

셸 정렬은 멀리 떨어진 데이터와 비교, 교환으로 한 번에 이동할 수 있는 거리를 늘려서 처리 속도를 향상하기 위한 정렬이다.

처음에는 멀리 떨어진 두 데이터를 비교해서 필요시 위치를 교환하고 점차 가까운 위치의 데이터를 비교, 교환한뒤, 맨 마지막에 인접한 데이터를 비교, 교환하는 방식이다.

입력 배열을 부분배열로 나눠서 삽입 정렬을 수행하는 과정을 부분배열의 크기와 개수를 변화시켜 가면서 반복하는 방식으로도 말할 수 있다.

* 부분배열의 개수를 정하는 방법

	- 양수로 이루어진 임의의 순열 h<sub>1</sub>, ..., h<sub>k-1</sub>, h<sub>k</sub>을 사용
		+ 1 < i < k인 i에 대해 h<sub>i-1</sub> < h<sub>i</sub> < h<sub>i+1</sub>를 항상 만족
		+ 임의의 i, j에 대해 i < j이면 h<sub>j</sub>는 h<sub>i</sub>의 배수가 되지 않음
		+ 항상 h<sub>1</sub> = 1이 되어야 한다.

	- 순열의 역순으로 적용(h<sub>k</sub> -> h<sub>k-1</sub> -> ... -> h<sub>1</sub>)

첫 번째 단계 -> 전체 배열을 h<sub>k</sub>개의 부분배열로 나눠 처리(삽입 정렬 수행)

두 번째 단계 -> 부분 정렬된 전체 배열을 h<sub>k-1</sub>개의 부분배열로 나눠 처리

...

마지막 단계 -> 부분 정렬된 전체 배열을 h<sub>1</sub> = 1개의 부분배열, 즉 전체에 대해 처리

<br>

* 순열값 h<sub>k</sub>의 의미
	- 부분배열의 개수
		+ 전체 배열을 h<sub>k</sub>개의 부분배열로 나누어 각 부분배열에 대해 삽입 정렬을 적용
	- 각 부분배열 내에서 이웃한 데이터 간의 거리
		+ i번째 부분배열을 구성하는 데이터 -> 배열 인덱스를 h<sub>k</sub>로 나눴을 때 나머지가 i - 1인 데이터
		+ 각 부분배열은 전체 배열에서 h<sub>k</sub>씩 떨어진 데이터로 구성

<br>

```c
void ShellSort(int array[], int size)
{
	int i;
	int j;
	int gap;
	int val;

	for (gap = size / 2; gap >= 1; gap /= 2)
	{
		for (i = gap; i < size; i++)
		{
			val = array[i];

			for (j = i; j >= gap && array[j - gap] > val; j -= gap)
			{
				array[j] = array[j - gap];
			}

			array[j] = val;
		}
	}
}

// 하나의 입력 배열을 물리적(메모리 할당)으로 여러 개의 부분배열로 분할하지 않는다.

// 각 부분배열을 번갈아 가면서 미정렬 부분의 첫 번째 데이터를 뽑은 후
// gap만큼씩 떨어진 정렬 부분에서 제자리를 찾아서 삽입하는 방식이다.
```

* 성능과 특징
	- 사용하는 순열(부분배열의 개수)에 따라 성능이 달라짐
	- 가장 좋은 간격(순열)을 찾는 것은 미해결 과제
	- 시간복잡도: 최선 O(n log n) ~ 최악 O(n<sup>2</sup>)
	- 제자리 정렬 알고리듬이다.
	- 안정적이지 않은 정렬 알고리듬이다.

<br><br>