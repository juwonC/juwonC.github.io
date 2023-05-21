---
title: "[UE4]플레이어 제작"
excerpt: "플레이어 제작"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-05-21
---

## 🎮플레이어 제작
### ⚙️플레이어 클래스 생성
컨텐츠 브라우저에서 Add/Import-New C++ Class를 눌러 새로운 C++ 클래스를 생성합니다. 부모 클래스는 폰(Pawn) 클래스를 상속받습니다. 플레이어 클래스 이름을 지어주고 오른쪽의 Public을 눌러 Public 폴더에 헤더 파일이 생성되도록 합니다. 플레이어 클래스 헤더 파일에 플레이어 외형과 충돌 영역 설정에 필요한 컴포넌트를 추가합니다.

```cpp
...생략

public:
  virtual void Tick(float DeltaTime) override;

  virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

  // 박스 충돌체 컴포넌트
  UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

  // 스태틱 메시 컴포넌트
	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;
};
```

<br>

박스 충돌체 컴포넌트를 선언했으면 소스 파일로 이동해서 충돌체 컴포넌트를 생성하는 코드를 작성합니다.

```cpp
#include "ShootingPlayer.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"

// Sets default values
AShootingPlayer::AShootingPlayer()
{
 	// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	// 박스 콜라이더 컴포넌트 생성
	boxComp = CreateDefaultSubobject<UBoxComponent>(TEXT("My Box Component"));

	// 생성한 박스 콜라이더 컴포넌트를 최상단 컴포넌트로 설정
	SetRootComponent(boxComp);

	// 스태틱 메시 컴포넌트 생성
	meshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("My Static Mesh"));

	// 박스 콜라이더 컴포넌트의 자식 컴포넌트로 설정
	meshComp->SetupAttachment(boxComp);

	// 박스 콜라이더 크기 기본 큐브 사이즈인 50 x 50 x 50으로 설정
	FVector boxSize = FVector(50.0f, 50.0f, 50.0f);
	boxComp->SetBoxExtent(boxSize);
}

...생략
```

스태틱 메시 컴포넌트와 충돌 컴포넌트가 제대로 만들어졌는지 플레이어 클래스를 부모로 하는 블루프린트 클래스를 생성하여 확인합니다.

<br><br>

### ⚙️입력 키 바인딩
Edit 탭의 프로젝트 세팅으로 들어가서 Engine-Input 설정으로 이동합니다. Axis Mappings에 좌우 이동에 대한 입력을 추가합니다. +버튼을 눌러 항목을 추가하고 'Horizontal'이라고 이름을 설정하고 키보드 D키를 등록합니다. 오른쪽은 양수 방향이라서 Sclae 값은 1.0으로 설정합니다. 좌측 방향은 음수 방향이 되도록 Scale 값을 -1.0으로 설정하고 키보드 A키를 등록합니다.

상하 입력 Axix도 추가해줍니다. 'Vertical'이라는 항목을 추가하고 위로 이동 Scale 값은 1.0으로 설정하고 키보드 W를 등록합니다. 아래로 이동 Scale 값은 -1.0으로 설정하고 키보드 S를 등록합니다.

<br><br>

### ⚙️플레이어 이동
사용자 키 입력을 -1, 0, 1 값으로 변환한 값을 변수에 저장해야 합니다. 먼저 변수들을 선언해주고 사용자 입력 처리 함수를 만들어 줍니다.

```cpp
...생략

public:
  virtual void Tick(float DeltaTime) override;

  virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

  // 박스 충돌체 컴포넌트
  UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

  // 스태틱 메시 컴포넌트
	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;

private:
	// 사용자 키 입력 값을 저장할 변수
	float h;
	float v;

	// 사용자 입력 처리 함수
	void MoveHorizontal(float value);
	void MoveVertical(float value);
};
```

<br>

사용자 키 입력 값을 받기 위해 입력 값을 처리하는 함수를 소스 파일에 구현합니다. 입력 처리 함수를 구현했으면 언리얼 엔진 시스템에서 입력 처리 함수를 처리할 수 있도록 PlayerInputComponent에 연결합니다.

```cpp
...

// Called to bind functionality to input
void AShootingPlayer::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

  // Axis 바이딩된 값을 함수에 연결
	PlayerInputComponent->BindAxis("Horizontal", this, &AShootingPlayer::MoveHorizontal);
	PlayerInputComponent->BindAxis("Vertical", this, &AShootingPlayer::MoveVertical);
}

void AShootingPlayer::MoveHorizontal(float value)
{
	// 사용자 입력 값을 h 변수에 저장
	h = value;
}

void AShootingPlayer::MoveVertical(float value)
{
	// 사용자 입력 값을 v 변수에 저장
	v = value;
}
```

<br>

이제 키를 누를 때마다 값이 변수에 저장되고 이 값들을 이용해 플레이어의 위치를 변경하면 됩니다. 이동은 프레임 마다 반영되어야 하기 때문에 Tick() 함수 안에 구현합니다.

```cpp
...

// Called every frame
void AShootingPlayer::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

	// 상하좌우 입력 값을 이용해 방향 벡터 만듦
	FVector dir = FVector(0, h, v);

    // 어느 키를 눌러도 모두 동일한 속도를 만들기 위해
	// 방향 벡터의 길이가 1이 되도록 벡터 정규화
	dir.Normalize();

	// 이동할 새로운 위치 좌표를 구함(등속도 운동 공식 p = p0 + vt)
	FVector newLocation = GetActorLocation() + dir * moveSpeed * DeltaTime;

	// 현재 액터 위치 좌표를 앞에서 구한 새 좌표로 갱신
	SetActorLocation(newLocation);
}

...
```

<br>

새로운 좌표를 구하는 코드를 보면 이동 공식을 사용하기 위해 속력이 필요합니다. 헤더 파일에 속력 변수를 선언합니다.

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

private:
	float h;
	float v;

	void MoveHorizontal(float value);
	void MoveVertical(float value);
};
```

마지막으로 프로젝트를 빌드하고 에디터를 플레이하면 키 입력에 따라 플레이어가 이동하는 것을 확인할 수 있습니다.

<br><br>