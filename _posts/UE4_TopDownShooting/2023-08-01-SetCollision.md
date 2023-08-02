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
플레이어 클래스의 소스파일로 이동해서 생성자 함수 안에 충돌 설정 기능을 추가합니다. 

우선 플레이어의 박스 컴포넌트의 오버랩 이벤트를 활성화합니다. 플레이러가 적과 겹쳐질 때(오버랩) 이벤트가 발생되려면 액터에 Generate Overlap Events 옵션이 켜져있어야 합니다.

다음으로 박스 컴포넌트의 충돌 응답을 설정합니다. 충돌 응답의 종류에는 NoCollision, QueryOnly, PhysicsOnly, Collision Enabled(QueryAndPhysics) 네 가지가 있습니다. 플레이어의 충돌 응답은 QueryAndPhysics로 설정해줍니다.

<br>

💡충돌 활성 옵션
* NoCollision: 콜리전 없음(물리 엔진 내 어떤 표현도 없음)
* QueryOnly: 공간 쿼리에만 사용(raycasts, sweeps, and overlaps)
* PhysicsOnly: 물리 시뮬레이션에만 사용(Rigid Body, Constraints)
* Collision Enabled(QueryAndPhysics): 콜리전 켜짐(공간 쿼리와 물리 시뮬레이션 둘 다 사용 가능)

<br>

마지막으로 Collision Object Type을 설정해줍니다. Object Type을 설정할 때 ECC_GameTraceChannel1은 바로 위에서 만들었던 콜리전 오브젝트 채널을 의미합니다. 채널 정보는 해당 프로젝트가 있는 경로의 Config 폴더 안에 DefaultEngine.ini 파일에서 확인할 수 있습니다.

```cpp
#include "ShootingPlayer.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "Components/ArrowComponent.h"
#include "Bullet.h"
#include "Kismet/GameplayStatics.h"

AShootingPlayer::AShootingPlayer()
{
	PrimaryActorTick.bCanEverTick = true;

	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("My Box Component"));

	SetRootComponent(boxComp);

	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("My Static Mesh"));

	meshComp->SetupAttachment(boxComp);

	FVector boxSize = FVector(50.0f, 50.0f, 50.0f);
	boxComp->SetBoxExtent(boxSize);

	firePosition = CreateDefaultSubobject<UArrowComponent>(TEXT("Fire Position"));
	firePosition->SetupAttachment(boxComp);

	// 오버랩 이벤트 활성화
	boxComp->SetGenerateOverlapEvents(true);

	// 충돌 활성 옵션 설정 -> Query And Physics
	boxComp->SetCollisionEnabled(ECollisionEnabled::QueryAndPhysics);

	// Object Type을 channel 1으로 설정
	boxComp->SetCollisionObjectType(ECC_GameTraceChannel1);
}
```

<br>

코드를 빌드한 다음 플레이어 블루프린트(BP_ShootingPlayer) 설정 창으로 이동하고 좌측 컴포넌트 패널에서 BoxComp를 선택합니다. 다음으로 우측 Details 패널의 Collision 탭을 확인합니다. 

플레이어 블루프린트 충돌 설정이 코드에서 변경한 설정 값들로 적용이 안되어 있는 것을 확인할 수 있습니다. 블루프린트 파일은 원본 클래스 파일을 상속하기 때문에 원본이 바뀌더라도 상속된 블루프린트에는 원본이 가졌던 기존의 설정 값들을 유지하고 있습니다.

하지만 원본 클래스의 코드를 수정하고 빌드했기 때문에 기존에 볼 수 없었던 Collision Presets 항목 오른쪽에 노란색 화살표 버튼이 생김으로써 블루프린트 설정 값을 원본 파일의 설정 값으로 복구할 수 있게 되었습니다. 노란색 버튼을 발견하였다면 버튼을 눌러 블루프린트 설정 값을 원본 설정 값과 같게 변경시켜줍니다.

<br>

충돌 기본 설정이 끝났다면 각 콜리전 채널에 대한 개별 응답 값을 설정합니다.

```cpp
AShootingPlayer::AShootingPlayer()
{
	PrimaryActorTick.bCanEverTick = true;

	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("My Box Component"));

	SetRootComponent(boxComp);

	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("My Static Mesh"));

	meshComp->SetupAttachment(boxComp);

	FVector boxSize = FVector(50.0f, 50.0f, 50.0f);
	boxComp->SetBoxExtent(boxSize);

	firePosition = CreateDefaultSubobject<UArrowComponent>(TEXT("Fire Position"));
	firePosition->SetupAttachment(boxComp);

	boxComp->SetGenerateOverlapEvents(true);

	boxComp->SetCollisionEnabled(ECollisionEnabled::QueryAndPhysics);

	boxComp->SetCollisionObjectType(ECC_GameTraceChannel1);

	// 모든 채널 충돌 응답 안 함으로 설정
	boxComp->SetCollisionResponseToAllChannels(ECR_Ignore);

	// 적 채널에만 오버랩 설정
	boxComp->SetCollisionResponseToChannel(ECC_GameTraceChannel2, ECR_Overlap);
}
```

<br><br>