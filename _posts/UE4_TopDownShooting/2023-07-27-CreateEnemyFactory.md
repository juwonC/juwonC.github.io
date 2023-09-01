---
title: "[UE4]적 생성 액터 제작"
excerpt: "2D Shooting - 적 생성 액터 제작"

categories:
  - TopDown_Shooting
tags:
  - [UE4, 탑다운 2D 슈팅 게임]

toc: true
toc_sticky: true

date: 2023-07-27
---

## 🎮적 생성 액터 제작
### ⚙️적 생성 액터 클래스
앞서 만들었던 적을 바로 레벨에 배치하여 사용할 수 있겠지만 게임 월드에 위치해 있던 적이 현재 플레이하는 맵을 벗어나거나 플레이어에게 공격 당해 사라진다고 한다면 해당 적 액터는 다시 사용할 수 없을 것입니다.

게임을 플레이하는 중에 적 액터를 레벨에 손수 배치할 수 없기 때문에 적을 일정 시간마다 생성해주는 액터를 만들어 보겠습니다. 우선 'EnemyFactory'라는 이름의 C++ 액터 클래스를 새로 생성합니다.

<br><br>

### ⚙️적 생성 타이머 구현
헤더파일에 적을 생성할 시간 간격을 설정하기 위한 delayTime 변수와 현재까지 얼마나 시간이 흘렀는지 알기 위한 curTime 변수를 선언합니다.

```cpp
// EnemyFactory.h

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "EnemyFactory.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API AEnemyFactory : public AActor
{
	GENERATED_BODY()
	
public:	
	AEnemyFactory();

protected:
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	float delayTime = 2.0f;

private:
	float curTime = 0;
};
```

<br>

프레임마다 적을 생성할 시간이 됐는지 체크하기 위해 Tick 함수 안에 curTime이 적을 생성할 시점에 왔는지 체크해줍니다. 적을 생성할 시간이 아직 안되었으면 현재 프레임에 소요된 시간을 더하여 누적시킵니다. 반면에 적을 생성할 시간이 되었다면 curTime에 0을 대입시켜 시간을 다시 0으로 초기화시킵니다.

```cpp
// EnemyFactory.cpp

void AEnemyFactory::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

  // 현재까지 소요된 시간이 적 생성 시간을 초과했으면
	if (curTime > delayTime)
	{
    // 현재까지 소요된 시간을 0으로 초기화
		curTime = 0;

	}
  // 아직 적을 생성할 시간이 되지 않았다면
	else
	{
    // 프레임에 소요된 시간을 더하여 누적
		curTime += DeltaTime;
	}
}
```

<br><br>

### ⚙️적 액터 스폰
현재까지 소요된 시간이 적을 생성할 시간을 초과했을 때 블루프린트를 월드에 생성하는 코드를 구현하였습니다. 우선 헤더파일에 블루프린트 파일을 할당하기 위한 TSubClassOf<T> 변수를 선언합니다.

```cpp
// EnemyFactory.h

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "EnemyFactory.generated.h"

UCLASS()
class SHOOTINGSAMPLE_API AEnemyFactory : public AActor
{
	GENERATED_BODY()
	
public:	
	AEnemyFactory();

protected:
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

	UPROPERTY(EditAnywhere)
	float delayTime = 2.0f;

	UPROPERTY(EditAnywhere)
	TSubClassOf<class AEnemyActor> enemy;

private:
	float curTime = 0;
};
```

<br>

소스파일에서 SpawnActor<T> 함수를 사용하여 적 블루프린트를 생성하는 기능을 추가합니다.

```cpp
// EnemyFactory.cpp

#include "EnemyFactory.h"
#include "EnemyActor.h"

...생략

void AEnemyFactory::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

  // 현재까지 소요된 시간이 적 생성 시간을 초과했으면
	if (curTime > delayTime)
	{
        // 현재까지 소요된 시간을 0으로 초기화
		curTime = 0;
        
		// EnemyFactory와 동일한 위치에 적 생성
		AEnemyActor* spawnActor = GetWorld()->SpawnActor<AEnemyActor>(enemy, GetActorLocation(), GetActorRotation());

	}
  // 아직 적을 생성할 시간이 되지 않았다면
	else
	{
    // 프레임에 소요된 시간을 더하여 누적
		curTime += DeltaTime;
	}
}
```

<br>

💡트랜스폼 정보로 클래스 인스턴스 스폰

지정된 Location 과 Rotation 에 지정된 Class 인스턴스를 스폰시키는 함수 템플릿으로, 템플릿 클래스와 같은 유형의 해당 인스턴스로의 포인터 T* 를 반환합니다.

```cpp
// 사용
APawn* ResultPawn = SpawnActor<APawn>(DefaultPawnClass, StartLocation, StartRotation, NULL, Instigator);
```

자세한 내용은 
[UE4 액터 스폰하기 공식 문서](https://docs.unrealengine.com/4.27/ko/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/Spawning/)
를 참고하시기 바랍니다.

<br><br>