---
title: "[UE4]적 액터 제작"
excerpt: "2D Shooting - 적 액터 제작"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-07-08
---

## 🎮적 액터 제작
### ⚙️적 클래스 생성
적도 총알처럼 사용자의 입력을 받는 오브젝트가 아니라서 Actor 클래스로 제작합니다. 적 클래스 파일이 생성되면 헤더 파일에 외형과 충돌 영역 설정에 필요한 컴포넌트를 추가합니다. 플레이어와 총알을 만들었을 때와 같은 작업이므로 코드는 생략하겠습니다.

박스 충돌체 컴포넌트를 선언했으면 소스 파일로 이동해서 충돌체 컴포넌트를 생성하는 코드를 작성합니다. 그 다음 스태틱 메시 컴포넌트와 충돌 컴포넌트가 제대로 만들어졌는지 플레이어 클래스를 부모로 하는 블루프린트 클래스를 생성하여 확인합니다.

<br><br>

### ⚙️적 이동 방향 결정
적이 플레이어가 있는 방향으로 이동하는 기능을 만들어 봅시다. 플레이어의 위치에 따라 적의 이동 방향을 결정하는 기능을 어떻게 구현할 수 있을지 생각해 봅시다. 일단 액터가 스폰될 때마다 플레이어를 찾아서 그 방향으로 날아가야하기 때문에 BeginPlay()에 반복문을 사용하여 플레이어의 위치를 찾으면 될 것 같다는 생각이 듭니다. 적이 가야할 위치를 안다면 이동 기능은 플레이어와 총알을 만들 때 구현했기 때문에 적이 움직이는 기능은 쉽게 만들 수 있습니다.

우선 방향 벡터를 저장할 변수를 private으로 적 헤더 파일에 선언해줍니다. 그 다음 소스 파일로 이동해서 BeginPlay() 안에 플레이어의 위치를 알아내는 기능을 구현해 봅시다. 

게임 플레이 중에 플레이어를 찾아야하기 때문에 원본 파일(BP_ShootingPlayer)이 아닌 월드 공간에 배치된 모든 액터를 검색하여 그 액터가 플레이어 클래스(AShootingPlayer)인지 알아내야 합니다. 월드 공간에 생성되어 있는 모든 액터를 검색하기 위해 TIterator<T> 클래스를 이용하여 반복문을 만들어줍니다. TIterator 클래스를 사용하기 위해 EngineUtils.h 파일을 포함시켜야 합니다.

월드에 플레이어 클래스를 상속한 블루프린트가 여러개 배치되어 있을 수 있기 때문에 이름을 통해 플레이어를 정확하게 찾아내도록 합시다. GetName() 함수를 이용하여 검색된 플레이어 포인터 변수의 이름을 가져올 수 있습니다. 이렇게 가져온 이름에 Contains() 함수를 이용하여 문자열에 플레이어 블루프린트 이름(BP_ShootingPlayer)이 포함되어 있는지 확인합니다.

🚧GetName() 함수는 포인터 변수가 아니라 문자열(FString)을 반환하기 때문에 멤버 함수 Contains() 함수를 호출할 때 점 연산자를 사용해야 합니다.
{: .notice--warning}

플레이어 클래스와 플레이어 블루프린트 이름과 일치하는 액터를 찾았다면 적 위치에서 플레이어 위치로 향한 방향 벡터를 저장하기 위해 벡터 변수에 플레이어의 위치에 적(자신)의 위치를 뺀 값을 넣어줍니다. 적과 플레이어 사이의 간격은 매번 다르기 때문에 반드시 **정규화**를 해야 합니다.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "EnemyActor.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API AEnemyActor : public AActor
{
	GENERATED_BODY()
	
public:	
	AEnemyActor();

protected:
	virtual void BeginPlay() override;

public:	
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;

private:
	FVector dir;
};
```

<br>

```cpp
#include "EnemyActor.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "ShootingPlayer.h"
#include "EngineUtils.h"

AEnemyActor::AEnemyActor()
{
 	...생략
}

void AEnemyActor::BeginPlay()
{
	Super::BeginPlay();
	
	// 월드 공간에 AShootingPlayer 클래스의 액터를 모두 검색
	for (TActorIterator<AShootingPlayer> player(GetWorld()); player; ++player)
	{
		// 검색된 액터의 이름에 "BP_ShootingPlayer"가 포함되어 있다면
		if (player->GetName().Contains(TEXT("BP_ShootingPlayer")))
		{
			// 플레이어 액터의 위치 - 자신의 위치
			dir = player->GetActorLocation() - GetActorLocation();
			dir.Normalize();
		}
	}
}
```

<br>

적이 이동할 방향이 정해졌다면 이동하는 기능은 등속도 운동 공식 p = p0 + vt을 이용하여 구현하면 됩니다. 앞서 구현했던 이동 기능들 처럼 헤더 파일에 속력 변수를 선언하고 기본 속도를 설정합니다. 현재 적의 위치에 적의 새로운 위치 벡터를 추가로 덮어쓰면 이동 기능의 구현은 해결됩니다.

```cpp
#include "EnemyActor.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "ShootingPlayer.h"
#include "EngineUtils.h"

AEnemyActor::AEnemyActor()
{
 	...생략
}

void AEnemyActor::BeginPlay()
{
	...생략
}

void AEnemyActor::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

	FVector newLocation = GetActorLocation() + dir * moveSpeed * DeltaTime;
	SetActorLocation(newLocation);
}
```

<br><br>