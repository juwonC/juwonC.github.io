---
title: "[UE4]충돌 설정"
excerpt: "2D Shooting - 충돌 설정"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-08-01
---

## 🎮충돌 설정
### ⚙️Collision 채널 설정
언리얼 에디터에서 프로젝트 세팅을 선택해서 프로젝트 설정 창을 열고 Collision 탭을 선택합니다. Object Channels 탭에서 New Object Channels...를 선택하고 Player, Enemy, Bullet 채널을 기본 응답 값 Ignore로 설정하여 생성합니다.

![SetCollisionChannel](/assets/images/2DShooting/SetCollisionChannel.png)

<br><br>

### ⚙️Collision Response 설정
플레이어 블루프린트 파일(BP_ShootingPlayer)을 열고 설정 창에서 좌측 컴포넌트 패널의 BoxComp를 선택합니다.

![SetCollisionChannel](/assets/images/2DShooting/BoxComp.png){: width="300" height="300"}

<br><br>