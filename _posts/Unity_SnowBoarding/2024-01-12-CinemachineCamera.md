---
title: "[Unity]Cinemachine Camera Follow"
excerpt: "SnowBoarding - Cinemachine Camera Follow"

categories:
  - SnowBoarding
tags:
  - [Unity, SnowBoarding]

toc: true
toc_sticky: true

date: 2024-01-12
---

## 🎮Cinemachine Camera Follow
### ⚙️Cinemachine
Cinemachine은 여러 대의 카메라를 동작할 수 있게 하는 패키지이다. 여러 카메라에 적용되는 규칙을 쉽게 만들 수 있다.

메인 카메라에 시네머신 브레인이라는 것을 장착하고 메인 카메라가 어떻게 행동할 것인지 규칙을 정한다.

시네머신 브레인은 여러 대의 가상 카메라를 지정할 수 있는데 이 프로젝트에서는 한 대의 가상 카메라를 이용해서 메인 카메라가 무엇을 할지 지정해 주게 만들 것이다.(가상 카메라들은 시네머신 브레인에 의해 관리된다.)

프로젝트에 시네머신 패키지를 추가하기 위해 Windows-Package Manager로 이동한다.

패키지 매니저 창이 열리면 상단 메뉴에서 Packages: In Project 옵션을 Unity Registry로 바꿔줘서 현재 프로젝트에 존재하는 패키지 뿐만 아니라 유니티가 제공하는 패키지를 검색할 수 있도록 한다.

Cinemachine 패키지를 찾고 우측 하단 Install 버튼을 눌러 설치한다.

Cinemachine 패키지가 설치가 완료되면 Hierachy 창에서 가상 카메라를 한 대 추가해본다. 이제 메인 카메라를 선택해 Inspector 창에서 시네머신 브레인이 자동으로 추가되어 있는 것을 확인할 수 있다.

<br>

### ⚙️가상 카메라

추가한 가상 카메라를 선택하고 CinemachineVirtualCamera에서 바디를 Framing Transposer로 변경한다. 게임 내 특정 대상을 프레이밍해서 가상 카메라 바디를 이동하기 위해서이다.

그리고 CinemachineVirtualCamera를 보면 Follow 옵션이 있는데, 이 옵션에서 카메라가 따라갈 대상을 정할 수 있다. 가상 카메라 바디에서 Screen X를 조정해 화면을 앞이나 뒤를 비추게 할 수 있다.

<br><br>