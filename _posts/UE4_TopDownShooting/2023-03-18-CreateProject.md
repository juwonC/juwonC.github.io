---
title: "[UE4]탑다운 2D 슈팅 게임 프로젝트 생성"
excerpt: "탑다운 2D 슈팅 게임 프로젝트 생성"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-03-18
---

## 🎮슈팅 프로젝트 생성
### ⚙️프로젝트 생성
Epic Games Launcher를 실행하고 언리얼 엔진 4.27.2 버전을 실행합니다. 프로젝트 카테고리에서 Games 항목을 선택하고, 템플릿은 Blank로 선택합니다.

언리얼 에디터 좌측 상단 파일 탭에서 New Level을 눌러 Empty Level 템플릿을 선택합니다.

하단 컨텐츠 브라우저에서 Add/Import 버튼을 눌러 Maps라는 새로운 폴더를 생성합니다. 현재 레벨을 저장하기 위해 좌측 상단 파일 탭을 클릭하고 Save Current를 선택합니다. 그리고 Maps라는 폴더에 현재 레벨을 저장해 줍니다.

언리얼 에디터가 종료되고 다시 실행될 때 방금 저장했던 현재 레벨을 불러올 수 있게 설정해줍시다. 상단 Edit 탭에서 Project Settings를 선택하고 좌측에서 Maps & Modes를 선택한 다음 Default Maps 항목에서 Editor Stratup Map과 Game Default Map을 둘 다 MyMap으로 변경해줍니다.

<br><br>

### ⚙️Game Mode Base 제작
Game Mode Base 클래스는 각 레벨에서 플레이의 기본 뼈대가 되는 규칙과 설정 내용을 담는 클래스입니다. Game Mode Base도 따로 관리해주기 위해 Blueprints라는 폴더를 만들고 그 폴더 안에 클래스를 생성해보겠습니다.

컨텐츠 브라우저에서 Add/Import를 눌러 Blueprint Class를 선택합니다. 부모 클래스는 Game Mode Base를 선택합니다. 블루프린트 파일이 생성되면 BP_GameModeBase라고 이름을 수정해줍니다. BP는 블루프린트의 약자입니다.

레벨과 마찬가지로 Game Mode Base도 기본 게임 모드로 설정해줍시다. Project Settings에 들어가서 Maps & Modes를 선택합니다. 그리고 Default Modes 항목에서 Default Game Mode를 방금 생성했던 BP_Game Mode Base로 바꿔줍니다.

<br><br>

### ⚙️카메라와 조명 설치
* 카메라 설치
<br>
언리얼 에디터 왼쪽의 Place Actors 패널에서 All Classes를 선택합니다. 우측의 액터 목록에서 Camera 액터를 마우스로 뷰포트에 드래그하여 놓습니다.
<br><br>
카메라 Transform의 Location X값을 -2000으로 설정하여 원점으로부터 후면 방향에 위치시킵니다.
<br><br>
Transform 아래 Mobility 설정은 Static으로 설정하여 카메라를 고정시켜줍니다.
<br><br>
Details 패널을 아래로 내리다 보면 Auto Player Activation 탭이 있는데 이 설정을 Player0으로 변경합니다. 첫 번째 플레이어가 생성되면서 동시에 카메라 액터도 활성화됩니다.

<br>

* 조명 설치
<br>
에디터 좌측 Place Actors에서 Lights 탭을 선택하고 Directional Light 액터를 뷰포트 쪽으로 드래그해서 배치합니다.
<br><br>
Directional Light를 선택한 상태에서 Details 패널의 Intensity 값을 5럭스로 줄여줍니다. Intensity는 빛의 세기이고 단위는 럭스를 사용합니다.

<br><br>