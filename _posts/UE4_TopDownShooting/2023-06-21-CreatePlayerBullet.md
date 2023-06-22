---
title: "[UE4]플레이어 총알 제작"
excerpt: "플레이어 총알 제작"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-06-21
---

## 🎮플레이어 총알 제작
### ⚙️플레이어 총알 클래스 생성
총알은 사용자의 입력을 받는 오브젝트가 아니라서 Actor 클래스로 제작합니다. 총알 클래스도 플레이어 클래스와 같이 헤더 파일에 플레이어 외형과 충돌 영역 설정에 필요한 컴포넌트를 추가합니다.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Bullet.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API ABullet : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ABullet();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;
};
```

<br>

박스 충돌체 컴포넌트를 선언했으면 소스 파일로 이동해서 충돌체 컴포넌트를 생성하는 코드를 작성합니다.

```cpp
#include "Bullet.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"

// Sets default values
ABullet::ABullet()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("Box Collider"));
	SetRootComponent(boxComp);
	boxComp->SetBoxExtent(FVector(50.0f, 50.0f, 50.0f));

	// 박스 컴포넌트 크기 변경(각 축의 배율 변경)
	boxComp->SetWorldScale3D(FVector(0.75f, 0.25f, 1.0f));

	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Static Mesh Component"));
	meshComp->SetupAttachment(boxComp);
}

...생략
```

스태틱 메시 컴포넌트와 충돌 컴포넌트가 제대로 만들어졌는지 플레이어 클래스를 부모로 하는 블루프린트 클래스를 생성하여 확인합니다.

<br><br>

### ⚙️플레이어 총알 이동
플레이어 이동을 구현했던 것 처럼 총알 이동은 프레임 마다 반영되어야 하기 때문에 Tick() 함수 안에 구현합니다.

먼저 총알을 이동시키려면 속력이 필요하므로 헤더 파일에 속력 변수를 추가합니다.

```cpp
...생략

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	float bulletSpeed = 800.0f;

	UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;
};
```

<br>

이제 소스 파일로 이동해서 Tick() 함수에 총알 이동 코드를 추가합니다.

```cpp
...생략

void ABullet::BeginPlay()
{
	Super::BeginPlay();

}

void ABullet::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

	// 이동할 새로운 위치 좌표를 구함(등속도 운동 공식 p = p0 + vt)
	// 액터의 전방 벡터는 GetActorForwardVector() 함수 사용
	FVector newLocation = GetActorLocation() + GetActorForwardVector() * moveSpeed * DeltaTime;

	// 현재 액터 위치 좌표를 앞에서 구한 새 좌표로 갱신
	SetActorLocation(newLocation);
}
```

<br><br>