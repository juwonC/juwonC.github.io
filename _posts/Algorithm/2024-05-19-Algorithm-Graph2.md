---
title: "[Algorithm]그래프2"
excerpt: "그래프2"

categories:
  - Algorithm
tags:
  - [알고리듬]

toc: true
toc_sticky: true

date: 2024-05-19
---

## 📚크루스칼 알고리듬

최소 신장 트리를 구하는 알고리듬

### 📄최소 신장 트리

* 신장 트리(spanning tree): 가중 무방향 그래프에서 모든 정점을 포함하는 트리. 트리이기 때문에 사이클이 없다.(정점의 개수가 n이면 신장 트리에는 정확히 n - 1개의 간선이 존재한다.)

* 최소 (비용) 신장 트리: 간선 (u, v)마다 가중치 w(u, v)를 가진 연결된 무방향 그래프 G=(V, E)에 대해서 다음을 만족하는 트리 G'=(V', E')
	- 신장 트리 중에서 가중치의 합이 가장 작은 것

<br>

### 📄최소 신장 트리 알고리듬

모든 간선 중에서 정점을 모두 연결하면서 가중치의 합을 가장 작게 만드는 (n-1)개의 간선을 고르는 과정

```c
Greedy_MST(G)
{
	T = Ø; // 최소 신장 트리의 간선 집합 초기화

	while(T가 신장 트리를 만들지 않았음)
	{
		// 사이클을 형성하지 않으며 최소의 가중치를 갖는 간선
		최선의 간선(u, v) 선택;
		T = T ∪ {(u, v)};
	}

	return(T);
}
```

* 욕심쟁이 방법 적용한 최소 신장 트리 알고리듬: 크루스칼, 프림 알고리듬

<br>

### 📄크루스칼 알고리듬

간선이 하나도 없는 상태에서 시작해서 가중치가 가장 작은 간선부터 하나씩 골라서 사이클을 형성하지 않으면 해당 간선을 추가하는 방식

* 사이클 형성 여부 판단
	- 간선(u, v)의 두 정점 u, v가 서로 다른 연결 성분에 속하면 사이클을 형성하지 않음

* n개의 정점이 각각의 서로 다른 연결 성분으로 구성된 상태에서 시작해서 간선을 추가할 때마다 연결 성분들이 하나씩 합쳐지고 최종적으로 하나의 연결성분을 형성함

```c
Kruskal(G)
{
	T = Ø;

	for(G의 각 정점 v에 대해)
	{
		정점 v로 구성된 연결 성분 초기화;
	}
	가중치가 증가하는 순으로 모든 간선 정렬;

	for(가중치가 가장 작은 간선부터 모든 간선 (u,v)∈E에 대해)
	{
		// 사이클을 형성하지 않으면
		if(u와 v가 서로 다른 연결 성분에 속하면)
		{
			T = T ∪ {(u, v)}; // 선택된 간선 (u, v)를 T에 추가
			u가 속한 연결 성분과 v가 속한 연결 성분을 합침;
		}
		else
		{
			간선 (u, v)를 버림
		}
	}

	return(T);
}
```

<br><br>

## 📚프림 알고리듬

임의의 한 정점에서 시작해서 연결된 정점을 하나씩 선택해 나가는 방법

* 이미 선택된 정점들에 부수된 가중치가 가장 작은 간선을 선택해서 추가

* 어떤 순간에 이미 선택된 정점의 집합 S와 선택되지 않은 정점의 집합 V - S를 잇는 간선 중에서 가중치가 가장 작은 간선을 선택해서 추가하는 방법
	- 임의의 정점 하나를 S로 지정한 후 시작해서 S=V가 될 때까지 S를 점점 키워 나가는 방법

```c
Prim(G)
{
	T = Ø;

	S = {1}; // 임의의 정점으로 초기화

	while(S != V)
	{
		u ∈ S, v ∈ V - S인 것 중 가중치가 최소인 간선(u, v) 선택;
		T = T ∪ {(u, v)};
		S = S ∪ {v};
	}

	return(T);
}
```

<br><br>

## 📚다익스트라 알고리듬

최단 경로를 구하는 알고리듬

### 📄최단 경로

두 정점 u와 v간의 최단 경로

* 가중 그래프에서 두 정점 u에서 v를 연결하는 경로 중 간선의 가중치 합이 가장 작은 경로

* 최단 경로 문제의 유형
	- 단일 출발점 최단 경로 문제(다익스트라 알고리듬, 벨만-포드 알고리듬)
	- 단일 도착점 최단 경로 문제
	- 단일 쌍 최단 경로 문제
	- 모든 쌍 최단 경로 문제(플로이드 알고리듬)

### 📄다익스트라 알고리듬

* 단일 출발점 최단 경로 알고리듬
	- 하나의 출발 정점에서 다른 모든 정점으로 최단 경로를 찾는 알고리듬
	- 욕심쟁이 방법이 적용된 알고리듬
	- 음의 가중치를 갖는 간선이 없다는 가정이 필요

* 거리
	- 출발점에서 현재까지 선택된 정점 집합 S를 경유하여 정점 v에 이르는 최소 경로의 길이

* 출발점에서 시작하여 거리 d[]가 최소인 정점을 차례대로 선택하여 최단 경로를 구하는 방법
	- 초기화: 출발점 s의 거리 d[s] = 0, 나머지 모든 정점 v의 거리 d[v]=∞, 선택된 정점의 집합 S={}
	- S = V가 될 때까지 반복
		+ 미선택 정점 집합 V - S에서 거리 d[]가 가장 작은 정점 u를 선택
		+ u의 인접 정점에 대해 u를 경유하는 거리와 기존 거리를 비교해서 작은 값을 새로운 거리값으로 조정

```c
Dijkstra(G, s)
{
	S = {}; d[s] = 0;

	for(모든 정점 v ∈ V)
	{
		d[v] = ∞;
		prev[v] = NULL;
	}

	while(S != V)
	{
		d[u]가 최소인 정점 u ∈ V - S를 선택;
		S = S ∪ {u};

		for(u에 인접한 모든 정점 v)
		{
			if(d[v] > d[v] + W(u, v))
			{
				d[v] = d[u] + W(u, v);
				prev[v] = u;
			}
		}
	}

	return(d[], prev[]);
}
```

<br><br>