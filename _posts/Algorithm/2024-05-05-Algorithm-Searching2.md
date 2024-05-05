---
title: "[Algorithm]탐색2"
excerpt: "탐색2"

categories:
  - Algorithm
tags:
  - [알고리듬]

toc: true
toc_sticky: true

date: 2024-05-05
---

## 📚레드-블랙 트리
### 📄레드-블랙 트리

레드-블랙 트리는 이진 탐색 트리이면서 균형 탐색 트리이다. 그리고 다음과 같은 성질을 가진다.

1. 모든 노드는 검정이거나 빨강이다.
2. 루트 노드와 리프 노드는 검정이다.(모든 리프 노드는 NULL 노드이다.)
3. 빨강 노드의 부모 노드는 항상 검정이다.(빨강 노드가 연달아 나타날 수 없다.)
4. 임의의 노드로부터 리프 노드까지의 경로상에는 동일한 개수의 검정 노드가 존재한다.
5. 이진 탐색 트리 성질
6. 이진 탐색 트리 성질

<br>

### 📄탐색 연산

이진 탐색 트리의 탐색 방법과 동일하다. 키 값을 루트 노드 부터 비교를 시작해서 키 값이 루트 보다 작으면 왼쪽, 크면 오른쪽으로 경로를 따라 내려간다.

<br>

### 📄삽입 연산

탐색이 실패한 NULL 노드에 빨강 노드를 추가하고, 두 자식 노드를 NULL 노드로 만든다.
빨강 노드가 연달아 나타나면 루트 노드 쪽으로 올라가면서 노드의 구조와 색깔을 조정해서 레드-블랙 트리의 성질을 만족시켜야 한다.

* 빨강 노드가 연달아 나타나는 경우에 적용하는 규칙은 다음과 같다.

1. 부모 노드의 형제 노드가 빨강인 경우 -> 부모 노드, 부모 노드의 형제노드, 부모 노드의 부모노드의 색깔을 모두 변경

2. 부모 노드의 형제 노드가 검정이고, 현재 노드의 키 값이 부모 노드와 부모 노드의 부모 노드의 키 값의 사이인 경우 -> 현재 노드와 부모 노드를 회전시킴

3. 부모 노드의 형제 노드가 검정이고 현재 노드의 키 값보다 부모 노드와 부모 노드의 부모 노드의 키 값이 큰(또는 작은) 경우 -> 부모 노드와 부모 노드의 부모 노드를 회전시키고 색깔을 변경

<br>

### 📄성능과 특징

균형 탐색 트리

* 어떤 두 리프 노드의 레벨 차이가 2배를 넘지 않는 균형 탐색 트리
	- 성질3 -> 루트 노드에서 리프 노드의 경로상에는 빨강 노드의 개수 < 검정 노드의 개수
	- 성질4 -> 루트 노드에서 리프 노드의 경로상에는 동일한 개수의 검정 노드가 존재

* 탐색, 삽입, 삭제 연산의 시간 복잡도: O(logn)
	- 최악의 경우 트리의 높이 O(logn)

* 사실상 이진 탐색 트리
	- 탐색 연산은 이진 탐색 트리와 같다.
	- 삼입 연산은 회전과 색깔 변경과 같은 추가 연산이 필요하다.

* 2-3-4 트리를 이진 탐색 트리로 표현한 것이 레드-블랙 트리이다. 빨강 노드를 부모 노드와 묶어서 2-3-4 트리 하나의 노드로 표현할 수 있다.

<br><br>

## 📚B-트리
### 📄B-트리

B-트리는 균형 탐색 트리이면서 다음과 같은 성질을 가진다.

1. 루트 노드는 1개 이상 2t개 미만의 오름차순으로 정렬된 키를 가진다.
2. 루트 노드가 아닌 모든 노드는 (t-1)개 이상 2t개 미만의 오름차순으로 정렬된 키를 가짐
3. 내부 노드는 자신이 가진 키의 개수보다 하나 더 많은 자식 노드를 가짐
4. 각 노드의 한 키의 왼쪽 서브트리에 있는 모든 키 값은 그 키값보다 작음
5. 각 노드의 한 키의 오른쪽 서브트리에 있는 모든 키 값은 그 키값보다 큼
6. 모든 리프 노드의 레벨은 동일함

<br>

### 📄탐색 연산

이진 탐색 트리의 탐색 연산과 유사하게 루트 노드에서부터 탐색 키를 가진 원소를 찾아 나가는 방식이다.

<br>

### 📄삽입 연산

루트 노드에서부터 탐색을 수행하여 리프 노드에도 존재하지 않으면 해당 노드에 추가한다.

2-3-4 트리와 유사하게 노드 분할이 필요하다. B-트리에서의 노드 분할은 2-3-4 트리 노드 분할을 일반화 시킨 것으로 이해.

* 탐색 과정에서 (2t-1)개의 키를 갖는 노드를 만나면, 이 노드를 (t-1)개의 키를 갖는 2개의 노드와 1개의 키를 갖는 노드로 분할
	- 삽입으로 인해 노드의 키의 개수가 2t개가 되는 것을 방지

<br>

### 📄성능과 특징

* 탐색, 삽입, 삭제 연산의 시간 복잡도: O(logn)

* 내부 탐색과 외부 탐색에 모두 활용 가능하다.

<br><br>

## 📚해시 테이블
### 📄해싱

키 값을 기반으로 데이터의 저장 위치를 직접 계산함으로써 상수 시간 내에 데이터를 저장, 삭제, 탐색할 수 있는 방법

* 해시 테이블: 각 위치마다 주소가 부여되어 있는 저장공간. 배열 형태.

* 슬롯: 해시 테이블에서 각각의 공간.

### 📄해시 함수

키 값을 해시 테이블의 주소로 변환하는 함수

제산 잔여법, 비닝, 중간 제곱법 등 여러 종류가 있다.

* 바람직한 해시 함수
	- 계산이 용이해야 함
	- 적은 충돌 발생 -> 각 키를 테이블의 각 슬롯에 균등하게 사상시킬 수 있어야 함

<br>

### 📄충돌
서로 다른 키 값들이 같은 해시 함수 값을 갖는 경우.

* 충돌 해결 방법

* 개방해싱(연쇄법): 충돌된 데이터를 테이블 밖의 별도의 장소에 저장/관리 -> 연결 리스트 사용

* 폐쇄해싱(개방 주소법): 해시 테이블 내의 다른 슬롯에 충돌된 데이터를 저장/관리 (버킷 해싱, 선형 탐사, 이차 탐사, 이중 해싱)

<br>

### 📄충돌 해결 방법

* 개방 해싱: 해시 테이블의 각 슬롯을 연결 리스트의 헤더로 사용. 해시 테이블과 연결 리스트가 주기억장치 내에 유지될때 적합.

* 폐쇄 해싱
	- 버킷 해싱: 해시 테이블 슬롯을 버킷으로 묶어 버킷 단위로 해싱. 디스크에 저장된 해시 테이블 구현에 적합.

	- 선형 탐사: p(K, i) = (h(K) + i) mod M. 홈 위치가 사용 중이면 빈 슬롯을 찾을 때까지 테이블의 다음 슬롯으로 순차적으로 이동. 가장 간단하지만 최악의 방법.

	- 선형 탐사는 모든 슬롯이 새로운 데이터가 삽입될 후보가 된다. 긴 탐사 순서를 만들어 평균 탐색 시간의 증가를 초래한다.(1차 클러스터링 문제: 데이터들이 연속된 위치를 점유하여 클러스터를 형성하고 점점 커지는 현상)

	- 이차 탐사: 충돌이 발생하는 횟수의 제곱 형태로 탐사 순서를 결정. 서로 다른 홈 위치를 갖는 두 키는 서로 다른 탐사 순서를 가진다.

	- 이차 탐사는 모든 슬롯이 탐사 순서에 사용되지 않는 문제. 동일한 홈 위치를 갖는 두 키는 동일한 탐사 순서를 가지는 문제.(2차 클러스터링 문제: 특정 홈 위치에 대한 클러스터를 만드는 현상)

	- 이중해싱: 1차, 2차 클러스터링 문제 해결. 서로 다른 두 키의 홈 위치가 동일해도 서로 다른 탐사 순서를 가진다.

<br>

### 📄삭제 연산

* 두 가지 고려 사항

	- 데이터의 삭제가 차후의 탐색을 방해하지 말아야 한다.(단순히 빈 슬롯으로 두면 탐색이 해당 슬롯에서 종료되므로 그 이후의 데이터는 고립된다.)

	- 삭제로 생긴 빈 슬롯은 나중에 삽입 과정에서 사용되어야 한다.

* 비석

삭제된 데이터의 위치에 비석이라는 특별한 표시를 하는 방법.

탐색: 탐색하는 동안 비석을 만나면 계속 탐색

삽입: 비석이 표시된 위치를 빈 위치로 간주 -> 새 데이터 삽입

비석의 개수가 증가 -> 평균 탐색 거리 증가