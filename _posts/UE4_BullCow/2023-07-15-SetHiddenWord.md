---
title: "[UE4]숨겨진 문자 설정"
excerpt: "Bulls&Cows - 숨겨진 문자 설정"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-15
---

## 🎮숨겨진 문자 설정
### ⚙️숨겨진 문자 설정
BullCowCartridge의 OnInput 함수는 사용자가 문자를 입력하고 엔터 키를 누르면 호출되는 함수입니다. OnInput 함수의 내부 구현을 간단하게 알아보겠습니다.

OnInput 함수는 Cartridge 클래스에서 순수 가상 함수로 선언되어 있습니다.(Cartridge 클래스는 BullCowCartridge 클래스의 부모 클래스입니다.) 따라서 Cartridge 클래스에서는 이 함수가 정의되어 있지 않고 자식 클래스들에서 정의될 수 있습니다.

우리는 터미널이라는 곳에 문자를 입력하고 출력하는 게임을 만들고 있기 때문에 Terminal 클래스에서 OnInput 함수를 사용하는 것을 알 수 있습니다. Terminal 클래스에서 어떻게 OnInput 함수가 사용되는지 알아봅시다. Terminal 클래스의 ActivateTerminal 함수에서 키 바인딩에 의해 아무 키나 눌렀을 때 OnKeyDown 함수가 호출됩니다. 그 다음 OnKeyDown 함수에서 입력된 키가 Enter라면 AcceptInputLine 함수가 호출되고 Cartridge 클래스의 OnInput 함수가 AcceptInputLine 함수 안에서 호출됩니다.

Cartridge 클래스의 OnInput 함수는 앞에서 말했듯이 순수 가상 함수이기 때문에 오버라이딩된 자식들의 OnInput 함수가 터미널 클래스에서 호출될 수 있습니다.

Input 함수에 숨겨진 문자를 설정해보고 맞고 틀림에 따라 특정 메시지를 출력하는 기능을 구현하였습니다.

```cpp
void UBullCowCartridge::OnInput(const FString& PlayerInput)
{
    ClearScreen();

    FString HiddenWord = TEXT("dogs");

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

### ⚙️Isogram 체크
Isogram은 한 단어에 같은 글자가 없는 단어를 의미합니다. 숨겨진 단어가 Isogram인지 체크하여 참 또는 거짓을 반환하는 함수를 만들어 봅시다.

함수의 원형은 bool UBullCowCartridge::IsIsogram(const FString& Word) const 로 만들어 볼 수 있습니다. 함수에 들어오는 인자의 값이 변하지 않도록 매개변수 앞에 const 키워드를 사용하였고 이 멤버함수가 멤버변수들의 값을 변하게 하지 않기 위해 const 키워드를 사용해 const 멤버함수로 만들었습니다.

```cpp
// BullCowCartridge.h

#pragma once

#include "CoreMinimal.h"
#include "Console/Cartridge.h"
#include "BullCowCartridge.generated.h"

UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class BULLCOWGAME_API UBullCowCartridge : public UCartridge
{
	GENERATED_BODY()

public:
	virtual void BeginPlay() override;
	virtual void OnInput(const FString& PlayerInput) override;
	bool IsIsogram(const FString& Word) const;
};
```

<br>

문자열이 Isogram인지 체크하는 함수는 인자로 들어온 숨겨진 문자열의 첫 번째 문자 부터 끝 문자 앞(null문자 앞)까지 순회하면서 첫 번째 인덱스의 문자와 그 다음 인덱스의 문자들을 순차적으로 비교하여 만약 같은 문자가 있으면 거짓을 반환하고 같은 문자가 없다면 참을 반환합니다.

예를 들어, 문자열 Word의 첫 번째 인덱스 번호 0인 문자 Word[0]을 Word[1]과 비교합니다. 그리고 Word[0]과 Word[2]를 비교합니다. 이런 식으로 순차적으로 첫 번째 문자와 나머지 문자들을 비교하는 방법입니다.

```cpp
// BullCowCartridge.cpp

bool UBullCowCartridge::IsIsogram(const FString& Word) const
{
    for (int32 Index = 0, Comparison = Index + 1; Comparison < Word.Len(); ++Comparison)
    {
        if (Word[Index] == Word[Comparison])
        {
            return false;
        }
    }

    return true;
}
```

<br><br>

### ⚙️TArray에 숨겨진 문자 담아서 사용
언리얼에서 배열을 사용하고자 할 때 TArray라는 동적 배열을 사용합니다. TArray를 사용하여 숨겨진 단어들을 여러 개 넣어서 순차적으로 사용해보고자 합니다. 우선 TArray를 멤버변수로 선언해줍니다. 숨겨진 문자열을 저장해줄 멤버변수도 헤더파일에 선언해줍시다.

```cpp
// BullCowCartridge.h

#pragma once

#include "CoreMinimal.h"
#include "Console/Cartridge.h"
#include "BullCowCartridge.generated.h"

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

private:
  FString HiddenWord;
};
```

<br>

배열에 넣어 줄 단어들은 BeginPlay 함수에다가 간단하게 몇 개 넣어보도록 하겠습니다.

```cpp
void UBullCowCartridge::BeginPlay() // When the game starts
{
    Super::BeginPlay();
    
    Words = {TEXT("trust"), TEXT("coffee"), TEXT("bee"), TEXT("responsible"), TEXT("jazz")};
}
```

<br>

다음으로 TArray에 들어있는 단어들이 사용하기에 적합한 단어인지 체크하고 사용 가능한 단어들이 들어있는 배열을 반환하는 함수를 구현해봅시다. 헤더 파일에 함수 원형을 선언해주고 소스파일에 함수에 대한 정의를 해줍니다.

먼저 GetValidWords 함수 안에 사용 가능한 단어들을 담을 임시 배열을 선언해줍니다. 그 다음 배열의 첫 번째 원소 부터 끝 원소까지 순회하면서 원소의 길이가 3이상 8이하인 문자열을 찾고 그 문자열이 Isogram인지 IsIsogram 함수를 이용하여 확인합니다. 해당 문자열이 Isogram이 맞으면 함수 안에 임시로 만들었던 배열의 끝에 삽입(Emplace)합니다.

```cpp
// BullCowCartridge.cpp

TArray<FString> UBullCowCartridge::GetValidWords(const TArray<FString>& WordList) const
{    
    TArray<FString> ValidWords;
    
    //for (int32 i = 0; i < WordList.Num(); ++i)
    //{
    //    if (4 <= WordList[i].Len() && WordList[i].Len() <= 8)
    //    {
    //        if (IsIsogram(WordList[i]))
    //        {
    //            ValidWords.Emplace(WordList[i]);
    //        }
    //    }
    //}

    // Range based for loop
    for (FString Element : WordList)
    {
		    if (3 <= Element.Len() && Element.Len() <= 8)
		    {
			    if (IsIsogram(Element))
			    {
                ValidWords.Emplace(Element);
			    }
		    }
    }

    return ValidWords;
}
```

<br>

💡**Emplace** vs **Add**
<br>
TArray 끝에 원소를 삽입할 때 Emplace와 Add 함수를 사용할 수 있습니다. 두 함수가 배열 끝에 원소를 삽입한다는 기능은 거의 같지만 둘 사이에 살짝 다른 점이 있습니다.

배열에 문자열을 삽입한다고 했을 때, Add는 스트링 리터럴에서 임시 FString 을 생성한 다음, 그 임시 내용물을 컨테이너 안의 새로운 FString으로 복사합니다. 반면 Emplace는 스트링 리터럴을 사용해서 FString을 직접 만듭니다. 결과는 같지만, Emplace는 임시 변수 생성을 하지 않는다는 점에서 차이가 있습니다.

일반적으로 Emplace가 호출되는 곳에 인스턴스를 임시 생성 후 컨테이너에 복사 내지 이동하는 불필요한 절차를 피할 수 있기 때문에 Add 보다 좋습니다.

<br><br>

### ⚙️배열에 담긴 문자열 램덤하게 사용

배열에 담긴 문자열을 무작위로 사용하려면 배열의 인덱스를 랜덤하게 설정할 수 있으면 됩니다. 배열의 인덱스를 랜덤하게 설정하기 위해 FMath::RandRange 함수를 사용합니다. FMath::RandRange(int32 Min, int32 Max) 함수는 최소값과 최대값 사이의 수를 무작위로 반환하는 함수입니다. 공식 문서를 보면 이 함수는 Math/UnrealMathUtility.h를 포함하여 사용할 수 있습니다.

BullCowCartridge.h를 보면 CoreMinimal.h를 포함시켰는데 여기에 Math/UnrealMathUtility.h가 포함되어 있어 따로 헤더 파일을 포함시켜줄 필요가 없습니다. 이제 소스파일의 BeginPlay() 함수에 FMath::RandRange를 사용하여 배열에 담긴 문자열 램덤하게 사용해보겠습니다.

```cpp
// BullCowCartridge.h

#pragma once

#include "CoreMinimal.h"
#include "Console/Cartridge.h"
#include "BullCowCartridge.generated.h"

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

private:
  FString HiddenWord;
};
```

```cpp
// BullCowCartridge.cpp

#include "BullCowCartridge.h"

void UBullCowCartridge::BeginPlay() // When the game starts
{
    Super::BeginPlay();

    Words = {TEXT("trust"), TEXT("coffee"), TEXT("bee"), TEXT("responsible"), TEXT("jazz")};
    
    // 배열 첫 번째 인덱스 0이 최소값
    // 배열 마지막 인덱스인 (배열 길이 - 1)이 최대값
    HiddenWord = GetValidWord(Words)[FMath::RandRange(0, Words.Num() - 1)];
}
```

<br><br>