---
title: "[UE4]Bull, Cow 카운트 세기"
excerpt: "Bulls&Cows - Bull, Cow 카운트 세기"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-21
---

## 🎮Bull, Cow 카운트 세기
### ⚙️Bull, Cow 카운트 세기
Bull과 Cow의 카운트를 세기 위해 저장할 정수형 변수는 멤버변수에 선언하지 않고 struct을 사용해보겠습니다.

언리얼 작명 규칙에 따라 struct의 이름은 FBullCowCount로 짓고 안에 정수형 변수들을 선언하고 초기화 해줍니다.

인자로 받은 문자열을 멤버변수 HiddenWord에 저장되어 있는 문자열과 비교하여 Bull과 Cow 카운트를 세는 함수를 만들어 줍니다. 헤더파일에 FBullCowCount GetBullCows(const FString& Guess) const; 와 같이 함수의 원형을 선언하고 소스파일에 함수를 정의해보겠습니다.

```cpp
// BullCowCartridge.h
#pragma once

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

private:
	FString HiddenWord;
	TArray<FString> Isograms;
};
```

<br>

소스파일에 GetBullCows 함수를 정의합니다.

```cpp
// BullCowCartridge.cpp

FBullCowCount UBullCowCartridge::GetBullCows(const FString& Guess) const
{
    FBullCowCount Count;

    for (int32 GuessIndex = 0; GuessIndex < Guess.Len(); ++GuessIndex)
    {
        // 추측한 단어와 비밀 단어의 자릿수가 같고
        // 일치하는 문자가 있다면 BullCount 증가하고,
        // 다시 반복문 실행
        if (Guess[GuessIndex] == HiddenWord[GuessIndex])
        {
            ++Count.Bulls;
            continue;
        }

        // 자릿수가 같고 일치하는 문자가 없다면 BullCount는 증가하지 않고 다음 반복문 실행,
        // 자릿수는 다르지만 비밀 단어에 포함된 문자를 찾으면 CowCount 증가,
        // 그 뒤로 더이상 문자를 찾을 필요가 없으므로 반복문 탈출
        for (int32 HiddenIndex = 0; HiddenIndex < HiddenWord.Len(); ++HiddenIndex)
        {
            if (Guess[GuessIndex] == HiddenWord[HiddenIndex]) 
            {
                ++Count.Cows;
                break;
            }
        }
    }

    return Count;
}
```

<br>

OnInput 함수에서 GetBullCows 함수를 사용하여 BullCount와 CowCount를 터미널에 출력하는 기능을 만들었습니다.

```cpp
void UBullCowCartridge::OnInput(const FString& PlayerInput)
{
    ClearScreen();

    FBullCowCount Score = GetBullCows(PlayerInput);

    PrintLine(TEXT("You have %i Bulls and %i Cows."), Score.Bulls, Score.Cows);

    if(PlayerInput == HiddenWord)
    {
      PrintLine(TEXT("You Win!"));
    }
    else
    {
      PrintLine(TEXT("Game Over!"));
    }
}
```

<br><br>