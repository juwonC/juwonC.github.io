---
title: "[UE4]레벨 설정"
excerpt: "Bulls&Cows - 레벨 설정"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-25
---

## 🎮레벨 설정
### ⚙️레벨 설정
비밀 단어를 맞추면 레벨이 올라가고 레벨에 따라 비밀 단어의 수가 늘어나는 방식으로 레벨업 시스템을 간단하게 만들어 보았습니다.

현재 레벨과 최대 레벨을 저장하는 정수형 변수를 멤버변수로 선언하고 각각 1과 5로 초기화하였습니다. 그리고 Isogram을 담은 배열을 매개변수로 하는 레벨 설정 함수를 헤더파일에 선언합니다.

void LevelSetting(const TArray<FString>& IsogramArray); 와 같이 함수의 원형을 선언하였습니다.

```cpp
// BullCowCartridge.h

#include "CoreMinimal.h"
#include "Console/Cartridge.h"
#include "BullCowCartridge.generated.h"

struct FBullCowCount
{
	int32 Bulls = 0;
	int32 Cows = 0;
};

UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class BULLCOWGAME_API UBullCowCartridge : public UCartridge
{
	GENERATED_BODY()

public:
	virtual void BeginPlay() override;
	virtual void OnInput(const FString& PlayerInput) override;
	bool IsIsogram(const FString& Word) const;
	TArray<FString> Words;
	TArray<FString> GetValidWords(const TArray<FString>& WordList) const;
	FBullCowCount GetBullCows(const FString& Guess) const;
	void LevelSetting(const TArray<FString>& IsogramArray);

private:
	FString HiddenWord;
	int32 CurrentLevel = 1;
	int32 MaxLevel = 5;
	TArray<FString> Isograms;
};
```

<br>

소스파일로 가서 LevelSetting 함수를 정의해줍니다. 비밀 단어를 담은 배열을 처음 부터 끝까지 순회하고 현재 레벨에 맞는 길이의 단어를 함수 내부에 임시로 만든 LevelWords 배열에 넣어 줍니다.

그리고 LevelWords에 담긴 단어들을 FMath::RnadRange 함수를 사용하여 멤버변수 HiddenWord에 저장합니다.

```cpp
// BullCowCartridge.cpp

void UBullCowCartridge::LevelSetting(const TArray<FString>& IsogramArray)
{
    TArray<FString> LevelWords;

    for (FString Element : IsogramArray)
    {
        // 단어 맞춘 뒤 레벨업하면 히든단어 한 글자씩 늘어남
        if ((CurrentLevel + 1) < Element.Len() && Element.Len() <= (CurrentLevel + 2))
        {
            LevelWords.Emplace(Element);
        }
    }

    HiddenWord = LevelWords[FMath::RandRange(0, LevelWords.Num() - 1)];
}
```

<br>

레벨 설정 함수의 구현을 마무리하고 OnInput 함수에서 플레이어가 비밀 단어를 맞추면 레벨이 올라가고 LevelSetting 함수를 호출하여 레벨에 맞게 단어를 설정하도록 해주었습니다.

다만, 현재 레벨이 계속 올라가는 것을 방지하기 위해 현재 레벨이 최대 레벨 이상이 될 때 현재 레벨에 최대 레벨을 대입하여 현재 레벨이 최대 레벨을 넘지 못하게 하였습니다.

```cpp
// BullCowCartridge.cpp

void UBullCowCartridge::BeginPlay()
{
    Super::BeginPlay();

    Words = {TEXT("trust"), TEXT("coffee"), TEXT("bee"), TEXT("responsible"), TEXT("jazz")};

    Isograms = GetValidWords(Words);
}

void UBullCowCartridge::OnInput(const FString& PlayerInput)
{
    ClearScreen();

    FBullCowCount Score = GetBullCows(PlayerInput);

    PrintLine(TEXT("You have %i Bulls and %i Cows."), Score.Bulls, Score.Cows);

    if(PlayerInput == HiddenWord)
    {
      PrintLine(TEXT("You Win!"));
      ++CurrentLevel;
      LevelSetting(Isograms);

      // 현재 레벨이 최대 레벨을 넘지 못하게 함
      if (CurrentLevel >= MaxLevel)
      {
          CurrentLevel = MaxLevel;
      }
    }
    else
    {
      PrintLine(TEXT("Game Over!"));
    }
}
```

<br><br>