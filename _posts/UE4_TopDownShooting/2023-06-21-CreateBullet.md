---
title: "[UE4]총알 제작"
excerpt: "총알 제작"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-06-21
---

## 🎮총알 제작
### ⚙️총알 클래스 생성
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