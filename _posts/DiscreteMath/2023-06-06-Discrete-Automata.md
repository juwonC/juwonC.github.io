---
title: "[DiscreteMath]오토마타 및 형식 언어"
excerpt: "오토마타 및 형식 언어"

categories:
  - Discrete
tags:
  - [이산수학, 오토마타 이론, 형식 언어]

toc: true
toc_sticky: true

date: 2023-06-06
---

## 📚오토마타
### 📄오토마타
인류는 오래전 부터 스스로 움직이는 기계인 오토마타에 관심을 가져왔습니다. 이런 관심과 노력으로 오늘날의 컴퓨터까지 만들어 냈습니다. 컴퓨터는 여러 오토마타 중에서도 유한 상태 기계로 알려져 있습니다. 이것은 유한한 개수의 상태를 가질 수 있는 추상 기계라는 의미입니다.

<br><br>

### 📄튜링머신
1936년 앨런 튜링은 계산하는 기계를 대표할 수 있는 가상의 장치를 만들었고 이 장치에 영어 단어인 automatic의 a를 따서 "a-기계"라는 이름을 붙였다. 이 기계가 바로 나중에 창시자인 앨런 튜링의 이름을 따서 튜링 기계라 불리게 되었습니다.

튜링 머신의 네 가지 구성요소는 다음과 같습니다.

1. 테이프: 테이프는 셀로 구분되어 있고 각 셀에는 하나의 기호가 기록되어 있습니다. 테이프의 길이는 양 옆으로 무제한이라고 가정합니다.
2. 헤드: 헤드는 테이프 위의 기호를 읽거나 쓸 수 있습니다. 헤드는 왼쪽 또는 오른쪽으로 한 칸씩 이동합니다.
3. 상태 기록부: 튜링머신의 현재상태를 기록합니다. 기록할 수 있는 상태의 개수는 유한하며, 기계가 작동을 시작할 때 시작 상태를 현재 상태로 기록합니다.
4. 유한한 표: 유한한 표에는 특정한 상태에 있는 튜링머신이 어떤 기호를 읽었을 때, 수행해야 할 작업에 대해 기술되어 있습니다.

<br>

튜링 머신은 다음과 같은 작업을 할 수 있습니다.

* 테이프의 기호를 지우거나 새로운 기호를 쓴다.
* 헤드를 왼쪽 또는 오른쪽으로 이동한다.
* 같은 상태나 기호를 다른 상태로 이동한다.

<br><br>

### 📄촘스키 계층
오토마타는 스스로 움직이는 기계를 추상화한 것이고 형식 언어는 프로그래밍 언어들의 일반적인 특성들을 추상화한 개념이고 형식 문법은 프로그래밍 언어의 생성규칙을 추상화한 개념입니다. 노엄 촘스키는 형식 문법, 형식 언어, 오토마타들 사이의 관계를 정형화하였습니다.

| 계층 | 형식 문법 | 형식 언어 | 오토마타 |
| :---: | :---: | :---: | :---: |
| 제0유형 | 무제약 문법 | 재귀 열거 언어 | 튜링머신 |
| 제1유형 | 문맥 의존 문법 | 문맥 의존 언어 | 선형 유한 오토마타 |
| 제2유형 | 문맥 자유 문법 | 문맥 자유 언어 | 푸시다운 오토마타 |
| 제3유형 | 정규 문법 | 정규 언어 | 유한 상태 오토마타 |

<br><br><br>

## 📚유한 오토마타
### 📄유한 오토마타
유한 오토마타(FA)는 촘스키 계층에 의하면 정규 문법에 의해 만들어진 정규 언어를 인식할 수 있는 오토마타입니다. 유한 오토마타는 유한한 개수의 상태를 가지고 여러 상태 중 오직 하나의 상태만을 현재 상태로 가집니다. 사건의 발생에 따라 현재 상태는 다른 상태로 전이됩니다.

유한 오토마타(Finite-state Automata)는 $$ M = (I, O, Q, f, g, \sigma) $$ 6개의 튜플로 구성됩니다.

1. I: 입력기호의 유한집합
2. O: 출력기호의 유한집합
3. Q: 상태의 유한집합
4. f: Q X I -> Q의 전이함수
5. g: Q X I -> O의 전이함수
6. σ: 초기 상태 (σ ∊ Q)

### 📄결정적 유한 오토마타
결정적 유한 오토마타(DFA)는 유한 오토마타와 비교했을 때 출력이 없어져 출력기호의 집합 O와 출력함수 g가 제거되었습니다. 대신 수락 상태 집합 F가 추가되었습니다. 모든 입력값에 대해서 전이를 마쳤을 때 기계의 현재 상태가 수락 상태일 경우 해당 입력값을 기계가 수락했다고 합니다. 수락 상태는 reject, accept의 값을 가지는 출력이라고 볼 수 있습니다.

결정적 유한 오토마타(Deterministic Finite-state Automata)는 $$ M = (I, Q, f, F, \sigma) $$ 5개의 튜플로 구성됩니다.

1. I: 입력기호의 유한집합
2. Q: 상태의 유한집합
3. f: Q X I -> Q의 전이함수
4. F: 수락 상태 집합 (F ⊆ Q)
5. σ: 초기 상태 (σ ∊ Q)

### 📄비결정적 유한 오토마타
비결정적 유한 오토마타는 대부분 DFA와 동일하고 유일하게 전이함수 부분만 다릅니다. 전이함수에서 입력값으로 주어진 입력기호뿐만 아니라 ε도 입력값으로 사용할 수 있습니다. ε은 빈 문자열을 나타내는 입력기호로서 입력값을 받아들이지 않고도 상태를 전이할 수 있는 여지를 제공합니다. 이런 전이를 ε전이라고 합니다.

결정적 유한 오토마타(Nondeterministic Finite-state Automata)는 $$ M = (I, Q, f, F, \sigma) $$ 5개의 튜플로 구성됩니다.

1. I: 입력기호의 유한집합
2. Q: 상태의 유한집합
3. f: Q X (I ∪ {ε}) -> P(Q)의 전이함수
4. F: 수락 상태 집합 (F ⊆ Q)
5. σ: 초기 상태 (σ ∊ Q)

<br><br><br>

## 📚마르코프 연쇄
유한 오토마타에서 상태전이를 전이함수로 나타내지만 마르코프 연쇄에서는 상태전이를 확률로 나타냅니다. 입력값과 출력값이 단일한 상태 s<sub>1</sub>으로 표현되지 않고 전이가 발생함에 따라 각 상태에 존재할 확률값으로 나타낼 수 있습니다.

<br><br><br>

## 📚형식 언어와 형식 문법
형식 언어와 형식 문법은 프로그래밍 언어들의 일반적인 특성들을 추상화한 개념입니다.

### 📄형식 언어
공집합이 아닌 기호들의 유한 집합을 **알파벳**이라고 합니다. 알파벳에 포함된 기호들의 유한한 순서쌍을 **문자열**이라고 합니다. 문자열 중 아무 기호도 포함하지 않은 문자열을 공 문자열이라고 하고 λ로 표기합니다.

<br>

* 언어
<br>
Σ를 알파벳이라고 했을 때 양의 정수 n에 대하여 Σ<sup>n</sup>, Σ<sup>+</sup>, Σ<sup>*</sup>는 다음과 같이 정의합니다.
<br><br>
Σ<sup>n</sup>: 길이가 n인 Σ의 기호들의 결합으로부터 만들어지는 모든 문자열의 집합
<br><br>
Σ<sup>+</sup>: 길이가 적어도 1 이상인 Σ의 기호들의 결합으로부터 만들어지는 모든 문자열의 집합(λ를 불포함)
<br><br>
Σ<sup>*</sup>: 길이가 0이상인 Σ의 기호들의 결합으로부터 만들어지는 모든 문자열의 집합(λ를 포함)
<br><br>
Σ<sup>*</sup>의 임의의 부분집합을 형식 언어라고 합니다.

<br>

* 언어의 연산
<br>
두 형식 언어 L<sub>1</sub>과 L<sub>2</sub>가 있을 때 다음과 같은 연산들을 정의합니다. L<sub>1</sub>과 L<sub>2</sub>의 접속은 L<sub>1</sub>의 문자열 v와 L<sub>2</sub>의 문자열 w를 접속시켜 만든 문자열의 집합입니다.
<br><br>
$$ L_1L_2 = \{xy|x \in L_1, y \in L_2\} $$
<br><br>
L<sub>1</sub>과 L<sub>2</sub>의 교집합은 L<sub>1</sub>과 L<sub>2</sub>에 동시에 속해 있는 문자열의 집합입니다.
<br><br>
$$ L_1 \cap L_2 = \{x|x \in L_1 \wedge x \in L_2\} $$
<br><br>
L<sub>1</sub>과 L<sub>2</sub>의 합집합은 L<sub>1</sub>또는 L<sub>2</sub>에 속해 있는 문자열의 집합입니다.
<br><br>
$$ L_1 \cap L_2 = \{x|x \in L_1 \vee x \in L_2\} $$

<br><br>

### 📄형식 문법
형식 문법은 형식 언어를 정의하는 방법 중 하나입니다. 유한개의 규칙을 통해 특정 언어에 해당되는 문자열들을 생성하거나 기존의 문자열이 특정 언어에 포함되는지 판단합니다.

* 구구조 문법
<br>
4개 원소의 순서쌍으로 정의되는 G = (V, T, P, S)를 구구조 문법이라고 합니다.
<br><br>
V: 비단말 기호들의 유한집합
<br>
T: 단말 기호들의 유한집합
<br>
P: 생성규칙
<br>
α -> β, α, β∈(V⋃T)<sup>*</sup>, α는 적어도 하나의 비단말 기호를 포함
<br>
S: V에 속하는 변수로서 시작 기호

<br>

* 문법에 의해 생성된 언어
<br>
G = (V, T, P, S)를 문법이라고 할 때, 시작 기호 S로부터 유도될 수 있는 단말들로 이루어진 문자열 집합 L(G)를 문법 G에 의해 생성된 언어라고 부릅니다.

<br>

* 촘스키 계층에 따른 형식 문법의 네 가지 분류

  - 무제약 문법: 문자열 생성에 제약이 없는 문법입니다. 튜링머신은 무제약 문법을 통해 만들어진 문자열을 인식할 수 있고 이 문자열들의 집합을 재귀 열거 언어라고 합니다.
  
  - 문맥 의존 문법: αAβ -> αγβ 형태의 생성규칙을 가지는 문법입니다. A는 비단말 기호이고 α, γ, β는 비단말이거나 단말 기호입니다. α와 β는 비어 있어도 되지만 γ는 비어있는 기호이면 안됩니다. 이는 A가 앞뒤의 문맥이 허용될 때만 대치될 수 있는 것을 의미합니다.
  
  - 문잭 자유문법: A -> β 형태의 생성규칙을 가지는 문법입니다. A는 비단말 기호이고 β는 비단말이거나 단말 기호입니다. 생성규칙 좌측에 하나의 비단말 기호가 오며 이 기호의 앞뒤에 어떠한 문자열이 오든 상관없이 우측 기호로 바꿀 수 있는 것을 의미합니다.

  - 정규 문법: A -> aB 형태의 생성규칙을 가지는 문법입니다. A는 비단말 기호이고 a는 단말, B는 비단말 기호입니다. B는 생략될 수 있습니다.


<br><br>