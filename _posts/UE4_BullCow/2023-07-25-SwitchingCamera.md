---
title: "[UE4]카메라 전환"
excerpt: "Bulls&Cows - 카메라 전환"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-25
---

## 🎮카메라 전환
### ⚙️카메라 배치
기존에 제공된 게임을 진행하다가 카메라 이동과 관련해서 불편한 점이 있어 간단하게 이 문제를 해결해보고자 하였다. 게임을 플레이 할 때 Tab키를 눌러 터미널을 활성화 시켜도 W, A, S, D키를 누르면 플레이어가 움직이면서 카메라도 움직이는 문제가 있었다.

따라서 터미널 근처로 플레이어가 다가가면 현재 플레이어에 붙어있는 카메라가 터미널을 바라보는 고정된 카메라로 전환되도록 기능을 수정하였다.

우선 언리얼 에디터의 Place Actors 패널에서 카메라 액터를 검색하고 카메라 액터를 터미널을 바라보게끔 레벨에 배치하였다.

![Camera](/assets/images/BullCow/Camera.png){: width="600" height="600"}

<br><br>

### ⚙️박스 트리거 배치
플레이어가 터미널에 다가가면 카메라 전환이 일어나는 기능을 만들기 위해 박스 트리거를 사용하였다. 박스 트리거는 플레이어와 겹쳐질 때 카메라 전환이 일어나도록 하는 장치이다.

언리얼 에디터의 Place Actors 패널 Basic에서 Box Trigger 액터를 찾아서 터미널을 감싸도록 레벨에 배치하였다.

![BoxTrigger](/assets/images/BullCow/BoxTrigger.png){: width="600" height="600"}

<br><br>

### ⚙️블루프린트 작성
카메라와 박스 트리거 액터를 레벨에 모두 배치했다면 배치한 카메라를 선택한 상태에서 에디터 상단의 Blueprints 버튼을 클릭한 다음 Open Level Blueprint 를 선택한다.

![LevelBluprint](/assets/images/BullCow/LevelBluprint.png){: width="600" height="600"}

<br>

다음으로 레벨 블루프린트에서 빈 화면을 마우스 우클릭한 다음 Create References to selected Actors를 선택합니다. 이러면 레벨에 배치한 카메라 액터에 참조가 추가된다.

![ReferencetoCamera](/assets/images/BullCow/ReferencetoCamera.png){: width="600" height="600"}

<br>

이제 다시 언리얼 에디터로 돌아가서 레벨에 배치된 트리거 박스를 선택하고 레벨 블루프린트에서  빈 화면을 마우스 우클릭한 다음 Add Event for Selected Actors and Collision 아래 AddOnActorBeginOverlap을 선택한다. OnActorBeginOverlap으로 인해서 플레이어가 트리거 박스와 겹쳐질 때 이벤트가 발생한다.

![BeginOverlap](/assets/images/BullCow/BeginOverlap.png){: width="600" height="600"}

<br>

이제 플레이어가 트리거 박스와 겹쳐질 때 카메라가 전환되는 이벤트를 만들어야 한다. 레벨 블루프린트에서 마우스 우클릭하여 Get Player Controller노드와 Set View Target with Blend노드 를 추가합니다.

![GetPlayerController](/assets/images/BullCow/GetPlayerController.png){: width="600" height="600"}
![SetViewTargetBleding](/assets/images/BullCow/SetViewTargetBleding.png){: width="600" height="600"}

💡노드를 검색해도 찾을 수 없는 경우 Context Sensitive를 해제하면 된다.

<br>

이제 다음과 같이 각각의 노드들을 연결해주고 컴파일하고 게임을 실행하면 플레이어가 트리거 박스와 겹쳐질 때 플레이어 시점의 카메라에서 터미널을 바라보는 고정된 카메라로 전환되는 것을 볼 수 있다.

![SwitchingCamera](/assets/images/BullCow/SwitchingCamera.png){: width="600" height="600"}

<br><br>

### ⚙️DefaultPawn
터미널을 바라보는 고정된 카메라로 시점을 바꾸는 것은 성공적으로 만들었지만 W, A, S, D키를 눌렀을 때 회색의 구체가 화면에 나타나는 것을 발견하였다.

현재 게임모드의 Default Pawn Class가 DefaultPawn으로 설정되어 있어서 아래와 같은 문제가 발생한 것으로 확인하였다.

![DefaultPawn](/assets/images/BullCow/DefaultPawn.png){: width="600" height="600"}

따라서 언리얼에서 기본으로 제공해주는 일인칭 에셋 팩을 임포트해서 Default Pawn Class를 새로운 일인칭 플레이어로 바꿔서 이 문제를 해결했다.

![FirstPerson](/assets/images/BullCow/FirstPerson.png){: width="600" height="600"}

![DefaultPawnClass](/assets/images/BullCow/DefaultPawnClass.png){: width="600" height="600"}

<br><br>