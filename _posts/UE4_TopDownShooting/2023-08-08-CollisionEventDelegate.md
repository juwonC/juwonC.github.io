---
title: "[UE4]충돌 이벤트 구현"
excerpt: "2D Shooting - 충돌 이벤트와 델리게이트"

categories:
  - 2D_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임, Delegate]

toc: true
toc_sticky: true

date: 2023-08-08
---

## 🎮충돌 이벤트 구현
### ⚙️델리게이트
델리게이트는 이벤트가 발생했을 때 만들어 놓은 함수를 실행하면서 매개변수에 자동으로 값을 넘겨주는 기능을 말합니다. 이벤트가 발생되었을 때 함수가 실행되게 하려면 델리게이트의 매개변수와 함수의 매개변수 형태가 같아야 합니다.

언리얼 엔진에서 함수를 미리 알고 있어야 하기 때문에 델리게이트에 연결할 함수는 반드시 UFUNCTION 옵션을 가져야 합니다. UFUNCTION 옵션은 리플렉션 시스템입니다.

💡**리플렉션 시스템**
<br>
리플렉션(Reflection)은 프로그램이 실행시간에 자기 자신을 조사하는 기능입니다. 이것은 엄청나게 유용하고 언리얼 엔진 기술의 근간을 이루는 것으로, 에디터의 디테일 패널, 시리얼라이제이션, 가비지 콜렉션, 네트워크 리플리케이션, 블루프린트/C++ 커뮤니케이션 등 다수의 시스템에 탑재되었습니다.
<br><br>
그러나 C++ 는 어떠한 형태의 리플렉션도 지원하지 않아, 언리얼 자체적으로 C++ 클래스, 구조체, 함수, 멤버 변수, 열거형 관련 정보를 수집, 질의 등을 조작하는 별도의 시스템이 구축되어 있습니다.
<br><br>
리플렉션 시스템은 옵션입니다. 리플렉션 시스템에 보이도록 했으면 하는 유형이나 프로퍼티에 주석을 달아주면, Unreal Header Tool (UHT)가 그 프로젝트를 컴파일할 때 해당 정보를 수집합니다.
{: .notice--warning}

<br><br>

### ⚙️총알 충돌 이벤트
총알과 충돌할 때 실행할 함수를 선언합니다. 델리게이트에 연결할 함수의 반환형은 void가 되어야 합니다. 앞서 언급했듯이 델리게이트에 연결할 함수는 반드시 UFUNCTION 옵션을 가져야 합니다. 델리게이트에 연결할 함수에 UFUNCTION 옵션이 없다면 빌드가 실패합니다.

```cpp
// Bullet.h

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Bullet.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API ABullet : public AActor
{
	GENERATED_BODY()
	
public:	
	ABullet();

protected:
	virtual void BeginPlay() override;

public:	
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	float moveSpeed = 800.0f;

	UPROPERTY(EditAnywhere)
	class UBoxComponent* boxComp;

	UPROPERTY(EditAnywhere)
	class UStaticMeshComponent* meshComp;

	UFUNCTION()
	void OnBulletOverlapEnemy(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, 
			        UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, 
			        bool bFromSweep, const FHitResult& SweepResult);
};
```

<br>

Bullet.cpp로 와서 델리게이트와 함수를 연결해줍니다. boxComp 변수의 멤버 함수 OnComponentBeginOverlap 델리게이트에 .AddDynamic() 함수를 사용하여 델리게이트와 함수를 연결시킵니다. .AddDynamic() 함수의 매개변수에 연결할 함수의 클래스와 주소 값을 전달합니다. 연결할 함수의 클래스는 자기 자신 클래스인 Bullet 클래스이므로 this 키워드로 대체합니다.

델리게이트와 함수를 연결했다면 연결할 함수 내부 로직을 구현합니다. 충돌한 대상 정보는 액터 정보로 전달 받을 것입니다. 충돌 액터 정보는 OnBulletOverlapEnemy 함수의 두 번째 매개변수 AActor* OtherActor 변수를 통해 액터 값을 받아올 수 있습니다. 총알과 충돌 대상 액터가 겹쳐져 오버랩 이벤트가 발생한 상태에서 이 액터가 적 액터라면 게임에서 제거하는 기능을 구현하였습니다.

```cpp
// Bullet.cpp

#include "Bullet.h"
#include "Components/BoxComponent.h"
#include "Components/StaticMeshComponent.h"
#include "EnemyActor.h"

void ABullet::BeginPlay()
{
	Super::BeginPlay();

	// 충돌 오버랩 이벤트에 OnBulletOverlapEnemy 함수 연결
	boxComp->OnComponentBeginOverlap.AddDynamic(this, &ABullet::OnBulletOverlapEnemy);
}

... 생략

void ABullet::OnBulletOverlapEnemy(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor,
                                UPrimitiveComponent* OtherComp, int32 OtherBodyIndex,
                                bool bFromSweep, const FHitResult& SweepResult)
{
	// 충돌한 액터를 AEnemyActor 클래스로 캐스팅(변환)
	AEnemyActor* enemy = Cast<AEnemyActor>(OtherActor);

	// 캐스팅 성공했다면 포인터 변수 enemy에
	// OtherActor 주소 값이 들어있고,
	// 캐스팅 실패했다면 아무 값도 안들어감(nullptr)
	if (enemy != nullptr)
	{
		// 충돌한 액터 제거
		enemy->Destroy();
	}

	// 어떤 대상이라도 충돌하면 총알 자신 제거
	Destroy();
}
```

<br><br>