---
title: "[DiscreteMath]그래프(1)"
excerpt: "그래프"

categories:
  - Discrete
tags:
  - [이산수학, 그래프]

toc: true
toc_sticky: true

date: 2023-05-05
---

## 📚기본사항
### 📄그래프
점과 두 점을 서로 연결하는 선으로 이루어진 도형을 그래프라고 합니다. 점을 꼭지점(Vertex) 또는 노드(Node)라고 하고, 각 점을 연결하는 선을 변(Edge)이라고 합니다.

그래프는 꼭지점의 집합과 변의 집합으로 정의됩니다. 변은 두 꼭지점을 연결하는 역할을 수행하며 변 e가 꼭지점 v와 w를 연결하는 경우 v와 w는 e에 의해 **발생**되었다고 하고 v와 w는 서로 **인접**한다고 합니다. 동일한 꼭지점을 연결하는 변은 **루프**라고 합니다. 두 꼭지점을 연결하는 변이 두 개 이상 있을 때 이런 변들을 **병렬 변**이라고 합니다. 아무 변과도 연결되지 않은 꼭지점은 **고립**되었다고 합니다.

꼭지점과 변의 이름을 제외하고 동일한 그래프를 **동형**이라고 합니다.

<br><br>

### 📄방향 그래프
변이 방향을 가지는 그래프를 **방향 그래프**라고 하고, 방향을 가지지 않으면 **무향 그래프**라고 합니다. 방향 그래프는 꼭지점 사이의 연결에 방향성이 존재할 때 사용되고 리스트나 트리와 같은 자료구조를 도식화하는데 유용합니다. 무향 그래프는 꼭지점들 사이에 전후관계가 없을 때 사용됩니다.

　　　방향 그래프　　　　　　무향 그래프
<br>
![DirectedGraph](\assets\images\DiscreteMath\DirectedGraph.png){: width="200" height="200"}
![UndirectedGraph](\assets\images\DiscreteMath\Undirected.png){: width="200" height="200"}
<br>
[https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))

<br><br>

### 📄단순 그래프
단순 그래프는 루프나 병렬 변을 가지지 않는 무향 그래프입니다.

![SimpleGraphs](\assets\images\DiscreteMath\SimpleGraphs.jpeg){: width="500" height="500"}
<br>
[https://www.tutorialspoint.com/graph_theory/types_of_graphs](https://www.tutorialspoint.com/graph_theory/types_of_graphs)

<br><br>

### 📄부분 그래프
부분 그래프는 하나의 그래프가 다른 그래프에 포함되어 있는 경우를 말합니다. 그래프 H와 그래프 G가 있다고 할 때, H의 모든 꼭지점이 G의 꼭지점이고 H의 모든 변이 G의 변인 경우 H를 G의 부분 그래프라고 합니다.

<br><br>

### 📄신장 부분 그래프
신장 부분 그래프는 부분 그래프 중 특수한 성질을 만족하는 경우의 그래프를 의미합니다. 부분그래프 H의 꼭지점과 그래프 G의 꼭지점이 완전히 일치하면 H를 G의 신장 부분 그래프라고 합니다. 

<br><br>

### 📄차수
차수는 그래프의 꼭지점에 대해 인접한 변의 수를 의미합니다. 그래프의 총 차수는 모든 꼭지점에 대한 차수들의 합입니다. 변이 루프일 경우 2를 더합니다.

방향 그래프에서 진입차수와 진출차수로 차수가 나뉩니다. 
<br>
* 진입차수
<br>
방향 그래프에서 해당 꼭지점으로 들어오는 변의 수를 나타냅니다.
* 진출차수
<br>
해당 꼭지점에서 다른 꼭지점으로 나가는 변의 수를 나타냅니다.

<br><br>

### 📄워크, 트레일, 경로
* 워크
<br>
그래프 G = (V, E)에서 꼭지점 v<sub>0</sub>와 v<sub>k</sub>가 있다고 했을 때, v<sub>0</sub>에서 v<sub>k</sub>까지의 워크는 유한한 순서쌍의 형태를 가집니다.
<br><br>
$$ W = v_{0}e_{1}v_{1}e_{2}v_{2} \; ... \; e_{k}v_{k} $$
<br><br>
v<sub>0</sub>를 시작점, v<sub>k</sub>를 종점이라고 합니다. v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>k-1</sub>을 내부점이라고 합니다. 정수 k는 W의 길이라고 합니다. 워크 W의 시작점과 종점이 같을 경우 W는 닫혀 있다라고 합니다.

<br>

* 트레일
<br>
워크 W의 변들 e<sub>1</sub>, e<sub>2</sub>, ...,  e<sub>k</sub>가 모두 서로 다르면 W는 트레일이라고 합니다.

<br>

* 경로
<br>
트레일 W의 꼭지점들 v<sub>0</sub>, v<sub>1</sub>, ...,  v<sub>k</sub>가 모두 서로 다르면 W는 경로라고 합니다.

<br><br>

### 📄닫힌 트레일과 사이클
* 닫힌 트레일
<br>
워크 W의 변 e<sub>1</sub>, e<sub>2</sub>, ...,  e<sub>k</sub>가 모두 서로 다르면서 v<sub>0</sub>와 v<sub>k</sub>가 동일한 경우 W는 닫힌 트레일이라고 합니다.

<br>

* 사이클
<br>
닫힌 트레일 중 v<sub>0</sub>, v<sub>1</sub>, ...,  v<sub>k-1</sub>까지의 꼭지점이 모두 서로 다를 경우 사이클이라고 합니다.

<br><br>

### 📄연결성분과 연결 그래프
그래프에서 두 꼭지점을 서로 연결하는 경로가 있을 경우 두 꼭지점은 서로 **연결**되어 있다고 합니다. 꼭지점들은 서로 연결되고 다른 집합과 겹치지 않는 꼭지점의 집합으로 나눌 수 있는데, 이들 각각을 **연결성분**이라고 합니다. 그래프에 오직 하나의 연결성분만 있을 때 **연결 그래프**라고 합니다.

<br><br><br>

## 📚그래프의 종류
### 📄완전 그래프
완전 그래프는 그래프에 속한 모든 꼭지점이 다른 꼭지점과 인접할 경우를 말합니다. n개의 꼭지점을 가지는 완전 그래프는 K<sub>n</sub>으로 표시합니다.

![CompleteGraph](\assets\images\DiscreteMath\CompleteGraph.jpeg){: width="300" height="300"}
<br>
[https://www.geeksforgeeks.org/mathematics-graph-theory-basics/](https://www.geeksforgeeks.org/mathematics-graph-theory-basics/)

<br><br>

### 📄이분 그래프
이분 그래프는 모든 꼭짓점을 빨강과 파랑으로 색칠하되, 모든 변이 빨강과 파랑 꼭짓점을 포함하도록 색칠할 수 있는 그래프입니다. 그래프 G = (V, E)의 V가 2개의 집합 V<sub>1</sub>과 V<sub>2</sub>로 분할되고, 모든 변들이 V<sub>1</sub>의 꼭지점과 V<sub>2</sub>의 꼭지점을 인접시킬 경우입니다.


![Bipartite](\assets\images\DiscreteMath\Bipartite.png){: width="300" height="300"}
<br>
[https://en.wikipedia.org/wiki/Bipartite_graph](https://en.wikipedia.org/wiki/Bipartite_graph)

<br><br>

### 📄완전 이분 그래프
완전 이분 그래프는 꼭짓점의 집합이 서로 겹치지 않는 두 집합 X와 Y의 합집합이고 X의 모든 꼭짓점이 Y의 각각의 꼭짓점과 하나의 변으로 연결되어 있는 이분 그래프입니다. 예를 들어, 이분 그래프 G = (V, E)의 V가  V<sub>1</sub>과 V<sub>2</sub>로 분할되고 V<sub>1</sub>의 모든 꼭지점과 V<sub>2</sub>의 모든 꼭지점이 변으로 인접되어 있을 경우를 말합니다.

![CompleteBipartite](\assets\images\DiscreteMath\CompleteBipartite.png){: width="300" height="300"}
<br>
[https://en.wikipedia.org/wiki/Bipartite_graph](https://en.wikipedia.org/wiki/Bipartite_graph)

<br><br>

### 📄정규 그래프
정규 그래프는 모든 꼭지점들이 동일한 수의 이웃을 가지는 경우를 말합니다. 모든 꼭지점들은 동일한 차수를 가지게 되고, 각 꼭지점의 차수가 k이면 k-정규 그래프라고 합니다.

<br>
　　0-정규 그래프　　　　　1-정규 그래프　　　　　2-정규 그래프
<br>
![0-regularGraph](\assets\images\DiscreteMath\0-regularGraph.png){: width="200" height="200"}
![1-regularGraph](\assets\images\DiscreteMath\1-regularGraph.png){: width="200" height="200"}
![2-regularGraph](\assets\images\DiscreteMath\2-regularGraph.png){: width="200" height="200"}
<br>
[https://en.wikipedia.org/wiki/Regular_graph](https://en.wikipedia.org/wiki/Regular_graph)

<br><br><br>

## 📚그래프의 표현
### 📄발생행렬
발생행렬은 꼭지점을 행렬의 행으로 하고 변을 행렬의 열로 하여 꼭지점과 변의 연결관계를 표현한 것입니다. 변과 꼭지점 사이에 인접관계가 있을 경우 1, 인접관계가 아닐 경우 0의 원소를 가집니다. 그래프의 행렬 표현 중 발생행렬 보다 인접행렬이 더 자주 사용됩니다.

<br><br>

### 📄인접행렬
인접행렬은 꼭지점을 행렬의 행과 열로 하여 꼭지점들 사이의 연결 관계를 표현한 것입니다.

![AdjacencyUndirected](\assets\images\DiscreteMath\AdjacencyUndirected.png){: width="200" height="200"}

<br>

위 그래프에 대한 인접행렬입니다.
<br>
![AdjacencyMatrix](\assets\images\DiscreteMath\AdjacencyMatrix.png){: width="200" height="200"}
<br>
[https://www.geeksforgeeks.org/graph-and-its-representations/](https://www.geeksforgeeks.org/graph-and-its-representations/)

<br><br>

### 📄인접 리스트
인접 리스트는 각 꼭지점에 인접하는 꼭지점들을 차례대로 연결 리스트로 표현한 것입니다. 시작 노드가 주어지고 그 꼭지점으로부터 인접해 있는 꼭지점들을 연결 리스트로 표시합니다. 시작 노드에 연결되는 꼭지점들의 순서는 관계없습니다.

<br>

![AdjacencyUndirected](\assets\images\DiscreteMath\AdjacencyUndirected.png){: width="200" height="200"}

<br>

위 그래프에 대한 인접 리스트입니다.
<br>
![AdjacencyList](\assets\images\DiscreteMath\AdjacencyList.png){: width="400" height="400"}
<br>
[https://www.geeksforgeeks.org/graph-and-its-representations/](https://www.geeksforgeeks.org/graph-and-its-representations/)

<br><br>