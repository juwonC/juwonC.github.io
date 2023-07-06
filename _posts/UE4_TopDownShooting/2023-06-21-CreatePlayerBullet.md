---
title: "[UE4]플레이어 총알 제작"
excerpt: "2D Shooting - 플레이어 총알 제작"

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

### ⚙️플레이어 총알 버튼 입력
플레이어가 화살표 버튼을 누르면 움직이듯이 총알도 스페이스 바를 누르면 발사 될 수 있도록 설정해줍니다. Edit 탭의 프로젝트 세팅으로 들어가서 Engine-Input 설정으로 이동합니다. +버튼을 눌러 항목을 추가하고 'Fire'이라고 이름을 설정하고 키보드 Space Bar키를 등록합니다.

<br><br>

### ⚙️플레이어 총알 생성
플레이어 클래스 헤더파일에 플레이어의 총구 위치를 설정하기 위해 UArraowComponent 포인터 변수를 추가합니다. 또한 총알 블루프린트를 생성하기 위해 해당 블루프린트 파일을 지정하기 위한 변수도 추가합니다. 월드에 배치하지 않은 원본 파일을 변수에 할당하기 위해 TSubClassOf<T>라는 자료형을 사용합니다.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Pawn.h"
#include "ShootingPlayer.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API AShootingPlayer : public APawn
{
	GENERATED_BODY()

public:
	// Sets default values for this pawn's properties
	AShootingPlayer();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

	// Called to bind functionality to input
	virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

	void PlayerInvuln();
	void RespawnPlayer();

	UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;

	// 속력 변수
	UPROPERTY(EditAnywhere)
	float moveSpeed = 500;

	// 총구 위치
	UPROPERTY(EditAnywhere)
	class UArrowComponent* firePosition;

	// 총알 블루프린트
	UPROPERTY(EditAnywhere)
	TSubclassOf<class ABullet> bulletFactory;

private:
	float h;
	float v;

	void MoveHorizontal(float value);
	void MoveVertical(float value);
};
```

<br>

플레이어 클래스 소스파일로 이동해서 총구 위치인 UArrowComponent를 생성합니다.

```cpp
#include "ShootingPlayer.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "Components/ArrowComponent.h"

// Sets default values
AShootingPlayer::AShootingPlayer()
{
	PrimaryActorTick.bCanEverTick = true;

	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("My Box Component"));

	SetRootComponent(boxComp);

	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("My Static Mesh"));

	meshComp->SetupAttachment(boxComp);

	FVector boxSize = FVector(50.0f, 50.0f, 50.0f);
	boxComp->SetBoxExtent(boxSize);

	// 총구 위치 컴포넌트를 생성하고 박스 컴포넌트의 자식으로 설정
	firePosition = CreateDefaultSubobject<UArrowComponent>(TEXT("Fire Position"));
	firePosition->SetupAttachment(boxComp);
}

... 생략
```

<br>

총구 설정이 끝났으므로 ShootingPlayer 헤더 파일로 이동해서 스페이스 바 버튼을 누르면 총알이 발사되는 함수를 만들어줍니다. Action 입력 바인딩은 키에 대한 특정 값을 반환하지 않기 때문에 Axis 입력 바인딩과 달리 매개변수가 없는 함수를 만들어줍니다.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Pawn.h"
#include "ShootingPlayer.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API AShootingPlayer : public APawn
{
	... 생략

private:
	float h;
	float v;

	void MoveHorizontal(float value);
	void MoveVertical(float value);

	// 총알 발사 입력 처리 함수
	void Fire();
};
```

<br>

ShootingPlayer 소스 파일에 Fire() 함수를 구현해줍니다.

```cpp
#include "ShootingPlayer.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "Components/ArrowComponent.h"
#include "Bullet.h"

... 생략

void AShootingPlayer::MoveHorizontal(float value)
{
	// Assign input Axis values to h
	h = value;
}

void AShootingPlayer::MoveVertical(float value)
{
	// Assign input Axis values to v
	v = value;
}

void AShootingPlayer::Fire()
{
	// SpawnActor<생성할 액터 클래스>(생성할 파일 변수, 생성할 위치, 생성할 회전값)
	ABullet* bullet = GetWorld()->SpawnActor<ABullet>(bulletFactory, firePosition->GetComponentLocation(),
		firePosition->GetComponentRotation());

	UGameplayStatics::PlaySound2D(GetWorld(), fireSound);
}
```

<br>

Fire() 함수를 구현했다면 Fire 액션 입력에 연결해줍니다.

```cpp
#include "ShootingPlayer.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "Components/ArrowComponent.h"
#include "Bullet.h"

void AShootingPlayer::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

	PlayerInputComponent->BindAxis("Horizontal", this, &AShootingPlayer::MoveHorizontal);
	PlayerInputComponent->BindAxis("Vertical", this, &AShootingPlayer::MoveVertical);

	// Action 바인딩 된 값을 함수에 연결
	// BindAction(액션 이름, 입력 이벤트 타입, 연결할 함수가 있는 클래스, 연결할 함수 주소 값)
	PlayerInputComponent->BindAction("Fire", IE_Pressed, this, &AShootingPlayer::Fire);
}

void AShootingPlayer::MoveHorizontal(float value)
{
	// Assign input Axis values to h
	h = value;
}

void AShootingPlayer::MoveVertical(float value)
{
	// Assign input Axis values to v
	v = value;
}

void AShootingPlayer::Fire()
{
	// SpawnActor<생성할 액터 클래스>(생성할 파일 변수, 생성할 위치, 생성할 회전값)
	ABullet* bullet = GetWorld()->SpawnActor<ABullet>(bulletFactory, firePosition->GetComponentLocation(),
		firePosition->GetComponentRotation());
}
```

<br><br>