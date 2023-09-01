---
title: "[UE4]충돌 설정"
excerpt: "2D Shooting - 충돌 설정"

categories:
  - TopDown_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-08-01
---

## 🎮충돌 설정
### ⚙️충돌 채널 설정
언리얼 에디터에서 프로젝트 세팅을 선택해서 프로젝트 설정 창을 열고 Collision 탭을 선택합니다. Object Channels 탭에서 New Object Channels...를 선택하고 Player, Enemy, Bullet 채널을 기본 응답 값 Ignore로 설정하여 생성합니다.

![SetCollisionChannel](/assets/images/2DShooting/SetCollisionChannel.png)

<br><br>

### ⚙️충돌 기본 설정
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

<br><br>

### ⚙️충돌 채널에 대한 개별 응답 값 설정
충돌 기본 설정이 끝났다면 각 콜리전 채널에 대한 개별 응답 값을 설정합니다. 우선 플레이어의 모든 충돌 채널에 대한 응답을 Ignore 상태로 변경합니다. 그 다음 적 채널(ECC_GameTraceChannel2)에 대해서만 오버랩 설정을 해줘서 적과 겹쳤을 때만 이벤트가 발생할 수 있게 해줍니다.

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

<br>

위 코드를 빌드해도 플레이어 블루프린트의 충돌 설정은 변경되지 않은 것을 확인할 수 있습니다. 이는 생성자 함수가 블루프린트 생성보다 먼저 이뤄지기 때문입니다.

블루프린트가 생성될 때 상속받지 않은 부분이 추가되면 이를 새로 읽어 들이지만 충돌 응답 같은 이미 있는 설정은 부모 클래스에서 설정을 변경해도 블루프린트에서 다시 읽어오지 않습니다.

따라서 이 문제를 해결하기 위해 기존의 블루프린트 파일을 지우고 다시 생성하면 됩니다. 파일을 지우고 다시 만들면 번거롭기 때문에 일반적으로 생성자 함수를 완성한 상태에서 블루프린트 파일을 만듭니다.

<br><br>

### ⚙️충돌 프리셋 설정
충돌 채널 응답 설정을 개별로 매번 만드는 것은 번거로운 일입니다. 이런 번거러운 작업을 조금 줄이기 위해 콜리전 프리셋을 이용하면 편하게 충돌 응답을 설정할 수 있습니다.

Project Settings 창을 열고 Collision 탭의 Preset 항목으로 이동합니다.

![CollisionPreset](/assets/images/2DShooting/CollisionPreset.png){: width="600" height="600"}

<br>

New 버튼을 눌러 새로운 충돌 응답 프리셋을 설정합니다. 프리셋 이름을 'Enemy'로 하고 Player와 Bullet 채널에 대해 Overlap 응답을 하고 나머지는 Ignore 응답을 하도록 설정합니다.

![EnemyProfile](/assets/images/2DShooting/EnemyProfile.png){: width="250" height="250"}

<br>

프리셋을 만들고 EnemyActor.cpp 에서 생성자에 충돌 프리셋을 설정하는 코드를 추가합니다. SetCollisionProfileName() 함수를 사용하는데 매개변수에 사용할 프리셋 이름을 넣어주면 됩니다.

```cpp
#include "EnemyActor.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "ShootingPlayer.h"
#include "EngineUtils.h"

AEnemyActor::AEnemyActor()
{
	PrimaryActorTick.bCanEverTick = true;

	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("Box Collider"));
	SetRootComponent(boxComp);
	boxComp->SetBoxExtent(FVector(50.0f, 50.0f, 50.0f));

	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Static Mesh"));
	meshComp->SetupAttachment(boxComp);

	enemyFirePosition = CreateDefaultSubobject<UArrowComponent>(TEXT("Fire Position"));
	enemyFirePosition->SetupAttachment(boxComp);

	// Collision Preset을 Enemy 프리셋을 변경
	boxComp->SetCollisionProfileName(TEXT("Enemy"));
}
```

<br><br>