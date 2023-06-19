---
title: "[DiscreteMath]그래프(2)"
excerpt: "그래프"

categories:
  - Discrete_Math
tags:
  - [이산수학, 그래프]

toc: true
toc_sticky: true

date: 2023-05-13
---

## 📚그래프의 탐색
### 📄평면 그래프
평면 그래프는 그래프의 모든 변을 서로 교차하지 않게 그릴 수 있는 그래프입니다. 첫 번째 그래프는 선이 겹쳐있어 평면 그래프로 보이지 않을 수 있는데 두 번째 그림처럼 변을 조정하면 변이 서로 겹치지 않게 그릴 수 있으므로 평면 그래프에 해당됩니다.

* 평면 그래프
<br>

![PlanarGraph](\assets\images\DiscreteMath\PlanarGraph.jpeg){: width="350", height="350"}
<br>
[https://www.geeksforgeeks.org/mathematics-planar-graphs-graph-coloring/](https://www.geeksforgeeks.org/mathematics-planar-graphs-graph-coloring/)

<br>

* 평면 그래프가 아닌 것
<br>

![PetersenGraph](\assets\images\DiscreteMath\PetersenGraph.png){: width="150", height="150"}
![K33Graph](\assets\images\DiscreteMath\K33Graph.png){: width="150", height="150"}
<br>
[https://en.wikipedia.org/wiki/Planar_graph](https://en.wikipedia.org/wiki/Planar_graph)


<br><br>

### 📄오일러의 공식
연결된 평면 그래프에서 꼭지점의 수 v, 변의 수 e, 면의 수 f라고 할 때, v - e + f = 2입니다.

오일러 공식은 변의 수 e에 대해 수학적 귀납법을 통해 증명할 수 있습니다. 변의 개수를 하나 증가시키기 위해 새로운 꼭지점을 추가하고 연결하거나, 기존의 두 꼭지점을 연결시키는 방법으로 이뤄집니다.

<br><br>

### 📄4색정리
평면 그래프가 주어졌을 때, 각 꼭지점에 대해 인접한 꼭지점과 다른 색으로 칠하는데 필요한 색은 네 가지면 충분하다는 정리입니다.

![FourColourPlanarGraph](\assets\images\DiscreteMath\FourColourPlanarGraph.png){: width="500", height="500"}
<br>
[https://en.wikipedia.org/wiki/Four_color_theorem](https://en.wikipedia.org/wiki/Four_color_theorem)

<br><br>

### 📄오일러 트레일, 오일러 투어
그래프의 모든 변을 각각 한 번만 지나는 트레일을 **오일러 트레일**이라고 합니다. 그래프의 모든 변을 오직 한 번만 지나기 때문에 '한붓그리기'라고도 부릅니다.

![EulerianTrail](\assets\images\DiscreteMath\EulerianTrail.png){: width="400", height="400"}

<br>

**오일러 투어**는 시작점과 종점이 동일한 오일러 트레일입니다. 또한 오일러 투어는 닫힌 오일러 트레일로서 시작점에서 출발해서 모든 변을 한 번씩만 지나 처음으로 되돌아오는 그래프 탐색 방법입니다. 오일러 투어는 오일러 사이클, 오일러 회로라고도 부릅니다. 오일러 투어를 갖는 그래프를 오일러 그래프라고 합니다.

![EulerianCycle](\assets\images\DiscreteMath\EulerianCycle.png){: width="400", height="400"}
<br>
[https://www.geeksforgeeks.org/eulerian-path-and-circuit/](https://www.geeksforgeeks.org/eulerian-path-and-circuit/)

<br>

### 📄오일러 그래프 정리
연결 그래프가 오일러 투어를 가진다면 그래프의 모든 꼭지점의 차수가 짝수입니다.

그래프 G = (V, E)는 연결 그래프이고 모든 꼭지점의 차수는 짝수라 가정할 때 G의 오일러 투어는 아래의 알고리즘을 통해 구할 수 있습니다.

1. G의 임의의 꼭지점 v를 고른다.
2. v에서 시작하고 v에서 끝나는 임의의 사이클 C를 선택한다.
3. C가 오일러 투어이면 증명을 끝낸다. 아니라면 아래 과정을 반복한다.
4. G에서 C에 속하는 모든 변을 제거하고 새로운 G'을 만든다.
5. C와 G'가 공유하는 꼭지점 중 하나를 고르고 w라고 한다.
6. G'에서 w로부터 시작하여 w에서 끝나는 임의의 사이클 C'를 선택한다.
7. 기존의 C와 새로 선택된 C'를 합쳐서 새로운 C를 만든다.

<br><br>

### 📄해밀턴 경로, 해밀턴 사이클
그래프의 모든 꼭지점을 각각 한 번씩만 지나는 경로를 **해밀턴 경로**라고 합니다.

![HamiltonianPath](\assets\images\DiscreteMath\HamiltonianPath.png){: width="300", height="300"}

<br>

**해밀턴 사이클**은 시작점과 종점이 동일한 해밀턴 경로입니다.

![HamiltonianCycle](\assets\images\DiscreteMath\HamiltonianCycle.png){: width="300", height="300"}
<br>
[https://en.wikipedia.org/wiki/Hamiltonian_path](https://en.wikipedia.org/wiki/Hamiltonian_path)

<br>

지나는 모든 변이 서로 다르면 **트레일**, 지나는 모든 꼭지점이 다르면 **경로**라고 합니다.

<br><br><br>

## 📚그래프의 활용
### 📄가중 그래프
그래프 각 변에 실수가 붙여진 그래프를 **가중 그래프**라고 합니다. 변에 부여된 값은 **가중치**라고 합니다. 가중 그래프는 그래프 이론은 활용한 많은 이론에서 응용됩니다.

<br>

### 📄최단경로 문제
출발지와 목적지를 정해 주었을 때, 어떤 경로가 가장 짧은 거리인지 찾는 문제입니다. 에츠허르 다익스트라(Edsger Dijkstra)라는 컴퓨터 과학자는 어떤 변도 음수값의 가중치를 갖지 않는 방향 그래프에서 주어진 출발점과 도착점 사이의 최단경로를 찾아주는 알고리즘을 고안해 냈습니다.

다익스트라 유사코드
```cpp
function Dijkstra(G, w, S)
{
  foreach vertex v in V[G]
  {
    d[v] <- ∞;
  }

  d[s] <- 0;
  Q <- V[G];
  while Q ≠ ∅ do
  {
    d[u]의 값이 최소인 꼭지점 u ∈ Q를 선택:
    Q <- Q - {u};
    Q' <- {v ∈ Q | v는 u와 인접}
    foreach vertex v in Q'
    {
      d[v] <- min{ d[v], d[u] + w(u, v)};
    }
  }
}
```

<br><br>

### 📄교착상태 찾기
둘 이상의 프로세스가 서로 상대방의 프로세스 결과를 무한정 기다리는 상황을 의미합니다.

교착상태를 발견하는 방법은 방향 그래프에서 방향 사이클을 발견하는 알고리즘과 동일합니다.

1. 진출 차수가 0인 꼭지점을 찾는다.
2. 진출 차수가 0인 꼭지점에 들어오는 변을 모두 제거한다.
3. 진입 차수가 0인 꼭지점을 찾는다.
4. 진입 차수가 0인 꼭지점에서 밖으로 나가는 변을 모두 제거한다.
5. 남아 있는 꼭지점이 방향 사이클에 포함되는지 판단한다.

<br><br>