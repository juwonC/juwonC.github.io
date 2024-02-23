---
title: "[DataStructure]스택"
excerpt: "스택"

categories:
  - DataStructure
tags:
  - [자료구조, 스택]

toc: true
toc_sticky: true

date: 2023-09-27
---

## 📚스택의 개념
스택은 개체와 해당 개체가 저장되는 순서를 기억하는 방법에 대한 추상 자료형이다.

스택은 한 쪽이 막힌 관을 생각하면 이해하기 수월하다. 관에 벽돌을 하나씩 넣을 수 있다고 할 때, 가장 먼저 들어간 벽돌은 가장 마지막에 나올 수 있을 것이다. 그리고 가장 마지막에 들어간 벽돌은 바로 관에서 뺄 수 있을 것이다.

이처럼 스택은 LIFO(후입선출) 구조를 가지며 가장 마지막에 들어간 원소가 가장 처음으로 나올 수 있다.

스택의 크기는 무한하지 않다. 스택에는 크기 제한이 있고 이것은 메모리의 한계와도 관계가 있다.

<br><br>

## 📚스택의 추상 자료형

**ADT Stack**

* Stack CreateStack(maxStackSize) ::==
<br>
스택 크기가 maxStackSize인 빈 스택을 생성하고 반환;

* Boolean StackIsFull(stack, maxStackSize) ::==
<br>
if((stack의 elements의 개수) == maxStackSize)
<br>
then { 'TRUE' 값을 반환; }
<br>
else { 'FALSE' 값을 반환; }

* Stack Push(stack, item) ::==
<br>
if(StackIsFull(stack))
<br>
then { 'stackFull' 출력; }
<br>
else { 스택 가장 위에 item을 삽입하고 스택 반환; }

* Boolean StackIsEmpty(stack) ::==
<br>
if(stack == CreateStack(maxStackSize))
<br>
then { 'TRUE'값 반환; }
<br>
else { 'FALSE'값 반환; }

* Element Pop(stack) ::==
<br>
if(StackIsEmpty(stack))
<br>
then { 'stackEmpty' 출력; }
<br>
else { 스택 가장 위 원소 삭제하고 반환; }

<br><br>

## 📚스택의 응용

* 시스템 스택: 변수에 대한 메모리 할당과 수집. 변수들의 생명주기 관리.

* 서브루틴 호출 관리: 서브루틴의 수행이 끝나고 되돌아갈 함수 주소를 저장.

* 후위 수식 계산: 피연산자와 연산자들관의 관계를 이용하여 계산 순위 결정

* 인터럽트 처리: 인터럽트 처리가 끝나고 되돌아갈 명령 수행지점 저장

* 컴파일러, 순환 호출 관리 등

<br><br>

## 📚스택의 연산
### 📄스택 삭제 연산

```c
int pop()
{
  if(top == -1)
  {
    return StackEmpty();
  }
  else
  {
    return stack[top--];
  }
}
```

<br>

### 📄스택 삽입 연산

```c
void push(int item)
{
  if(top >= STACK_SIZE - 1)
  {
    return StackISFull();
  }
  else
  {
    stack[++top] = item;
  }
}
```

<br><br>

## 📚사칙연산의 전, 중, 후위 표기
### 📄중위 표기법

연산자를 피연산자 사이에 표기하는 방법, 일반적으로 가장 많이 사용되는 표기 방법이다.

A + B * C + D

사칙연산의 우선순위에 따라 위 수식을 세분화해서 표현하면 아래와 같아진다.

((A + (B * C)) + D)

<br>

### 📄전위 표기법

연산자를 피연산자 앞에 표기하는 방법이다. 위 중위 표기법을 전위 표기법으로 표현하면 아래와 같다.

((A + (B * C)) + D)
<br>
= ((A + (*BC)) + D)
<br>
= (+(A*BC) + D)
<br>
= ++A*BCD

<br>

### 📄후위 표기법

연산자를 피연산자의 뒤에 표기하는 방법이다. 위 중위 표기법을 후위 표기법으로 표현하면 아래와 같다.

((A + (B * C)) + D)
<br>
= (A + (BC*) + D)
<br>
= ((ABC*+) + D)
<br>
= ABC*+D+

<br><br>