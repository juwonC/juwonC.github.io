---
title: "[UE4]문자열 입출력 분석"
excerpt: "Bulls&Cows - 문자열 입출력 분석"

categories:
  - BullCow_Game
tags:
  - [UE4, Bulls&Cows]

toc: true
toc_sticky: true

date: 2023-07-12
---

## 🎮문자열 입출력 분석
### ⚙️터미널 액터
게임 월드안에서 문자열을 입력하고 출력하는 기능은 강의에서 미리 만들어 놓은 기능이라 간단하게 분석을 해보려고 한다.

Terminal이라는 액터에 Static Mesh 컴포넌트와 Text Render 컴포넌트가 붙어 있는 것으로 보아 큐브 모양의 스태틱 메쉬 위에 텍스트 렌더를 띄어서 문자열을 나타낸 것 같다.

![TerminalActor](\assets\images\BullCow\Terminal.png)

<br>

### ⚙️문자열 입력과 출력

터미널 블루프린트 클래스에서 Event Graph를 살펴보려고 한다.

Tab키를 누르면 터미널이 활성화 되어 키보드 입력이 가능하고 다시 Tab키를 누르면 터미널이 비활성화 되는 기능이 만들어져 있다. 그리고 텍스트가 업데이트되면 텍스트 렌더에 텍스트가 세팅되는 것처럼 보인다.

![TerminalBlueprint](\assets\images\BullCow\TerminalBlueprint.png)

<br>

이제 Terminal의 내부가 어떻게 구현되었는지 간단하게 알아보려고 한다. Terminal 클래스의 헤더파일을 보면 아래와 같이 만들어져 있다.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "Components/ActorComponent.h"
#include "GameFramework/Actor.h"
#include "Terminal.generated.h"

DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FTextUpdateSignature, FString, Text);

struct FKey;

UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )
class BULLCOWGAME_API UTerminal : public UActorComponent
{
	GENERATED_BODY()

public:
	UPROPERTY(BlueprintAssignable, Category = "Terminal")
	FTextUpdateSignature TextUpdated;

	UFUNCTION(BlueprintCallable, BlueprintPure)
	FString GetScreenText() const;

	UFUNCTION(BlueprintCallable)
	void ActivateTerminal();

	UFUNCTION(BlueprintCallable)
	void DeactivateTerminal() const;

	void PrintLine(const FString& Line);
	void ClearScreen();

protected:
	// Called when the game starts
	virtual void BeginPlay() override;

private:
	void OnKeyDown(FKey Key);
	TArray<FString> WrapLines(const TArray<FString>&  Lines) const;
	void Truncate(TArray<FString>& Lines) const;
	FString JoinWithNewline(const TArray<FString>& Lines) const;
	void AcceptInputLine();
	void Backspace();
	FString GetKeyString(FKey Key) const;
	void UpdateText();


	UPROPERTY(EditAnywhere)
	int32 MaxLines = 10;

	UPROPERTY(EditAnywhere)
	int32 MaxColumns = 70;

	TArray<FString> Buffer;
	FString InputLine;

	int32 PressedBindingIndex;
	int32 RepeatBindingIndex;
};
```

<br>

* void ActivateTerminal();

OnKeyDown() 함수(Enter와 BackSpace 키)가 바인딩되어 키보드로 부터 입력을 받는다.

<br>

* void PrintLine(const FString& Line);

이 함수는 문자열을 출력하는 기능을 한다. 멤버변수인 Buffer 배열에 문자열을 넣고 UpdateText() 함수를 호출한다.

<br>

* void ClearScreen();

Buffer 배열을 비우고 UpdateText() 함수를 호출한다.

<br>

* void OnKeyDown(FKey Key);

Enter, BackSpace 키 입력을 통해 문자열 입력과 지우기 기능을 구현하였고 각각 void AcceptInputLine();, void Backspace(); 함수를 호출한다. Shift 키와 CapsLock키 입력에 따른 대소문자 입력 기능도 구현되어 있다. InputLine에 문자열을 추가한다.

<br>

* TArray<FString> WrapLines(const TArray<FString>&  Lines) const;

입력 문자열이 터미널의 가로 크기를 벗어나서(MaxColumns) 다음 줄로 넘어가도 문자열이 잘리지 않고 모든 내용을 볼 수 있게 하는 기능을 한다.

<br>

* void Truncate(TArray<FString>& Lines) const;

문자열을 담은 배열 Lines의 수가 MaxLines 보다 크거나 같으면 Lines의 첫번째 원소를 제거한다. 이는 문자열을 계속 입력하여 터미널의 세로 크기를 벗어나면 첫번째 줄을 지우는 기능이다.

<br>

* FString GetKeyString(FKey Key) const;

키보드로부터 입력을 받아 문자열을 반환하는 함수이다. FInputKeyManager::GetCodesFromKey(const FKey Key, const uint32*& KeyCode, const uint32*& CharCode); 함수가 사용된다.

<br>

* void AcceptInputLine();

Buffer에 InputLine 문자열과 프롬프트(constexpr TCHAR GPrompt[4] = TEXT("$> ");)를 넣는다. InputLine을 인자로 하여 카트리지 클래스의 OnInput() 함수를 호출한다.

이 게임은 카트리지 클래스가 있고 여러 게임들이 카트리지 클래스를 상속받는 형태로 제작되었다. 그리고 터미널 액터에 카트리지 컴포넌트를 붙인 형태로 게임이 제작되었다. 따라서 과거 콘솔 패키지를 교체하는 식의 형태로 여러 게임들을 클래스 별로 나눌 수 있게 만들었다.

<br>

* void Backspace();

InputLine의 뒷자리 부터 제거한다.

<br>

* FString GetScreenText() const;

문자열을 담는 배열에 InputLine 문자열과 프롬프트(constexpr TCHAR GPrompt[4] = TEXT("$> ");)를 넣고 WrapLines와 Truncate 함수를 호출하여 자동 줄 바꿈을 수행한다. 마지막으로 JoinWithNewline 함수를 호출하여 그 결과값을 반환한다.

<br>

* void UpdateText();

GetScreenText()의 반환값을 인자로 받는 Broadcast()함수를 호출한다. 델리게이트 기능이다.

<br><br>