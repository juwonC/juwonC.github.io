---
title: "[UE4]Bulls and Cows 개요"
excerpt: "Bulls&Cows - 개요"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-10
---

## 🎮Bulls and Cows 개요
### ⚙️게임 소개
Bulls and Cows는 두 명 이상의 플레이어가 플레이 하는 게임으로 한 명이 3~4 자리 숫자를 임의로 정하고 나머지 다른 사람이 그 숫자를 맞추는 게임이다.(단어 맞추기도 가능하다.) 영어 이름이라서 생소할 뿐이지 우리에게 익숙한 숫자야구 게임과 같은 게임이다.

정답인 숫자와 플레이어가 추측한 숫자가 같고 숫자의 자릿수도 일치하면 bull 카운트가 올라가고, 숫자만 맞고 자릿수가 틀리면 cow 카운트가 올라가는 방식이다.

예를 들어, 비밀 숫자가 3564라고 했을 때 플레이어가 4865라고 추측하면 bull 카운트는 1, cow 카운트는 2가 됩니다. 다만, 여기서 어떤 숫자가 bull이고 cow인지 알 수 없다.

강의를 통해 제작한 게임은 단어 맞추기 게임으로 제작되었다.

<br>

### ⚙️기능

* 문자를 입력하면 화면에 출력하는 기능(강의에서 제공)
* TEXT() 매크로 사용
* 문자열(FString) 다루기
* const 멤버함수 사용
* 반복문을 사용하여 문자열 길이 확인, 한 단어에 겹치는 문자가 있는지 확인하는 기능
* 논리연산자를 사용하여 비밀 문자와 플레이어가 추측한 문자가 맞는지 확인하는 기능
* 여러 개의 비밀 문자를 배열에 넣고 랜덤하게 뽑는 기능
* Bull, Cow 카운트 세는 기능

<br>

### ⚙️추가 요소

* 카메라 전환
* 레벨 설정

<br>

### ⚙️플레이 영상

{% include video id="mtFgYwasRgk" provider="youtube" %}

<br><br>