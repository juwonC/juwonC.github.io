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

Input 함수에 숨겨진 문자를 설정해보고 맞고 틀림에 따라 특정 메시지를 출력하는 기능을 구현해보겠습니다.

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
Isogram은 한 단어에 같은 글자가 없는 글자를 의미합니다. 숨겨진 단어가 Isogram인지 체크하여 참 또는 거짓을 반환하는 함수를 만들어 봅시다.

함수의 원형은 bool UBullCowCartridge::IsIsogram(const FString& Word) const 로 만들어 볼 수 있습니다. 함수에 들어오는 인자의 값이 변하지 않도록 매개변수 앞에 const 키워드를 사용하였고 이 멤버함수가 멤버변수들의 값을 변하게 하지 않기 위해 const 키워드를 사용해 const 멤버함수로 만들었습니다.

문자열이 Isogram인지 체크하는 함수는 인자로 들어온 문자열의 첫 번째 문자 부터 끝 문자 앞(null문자 앞)까지 순회하면서 첫 번째 인덱스의 문자와 그 다음 인덱스의 문자들을 순차적으로 비교하여 만약 같은 문자가 있으면 거짓을 반환하고 같은 문자가 없다면 참을 반환합니다.

예를 들어, 문자열 Word의 첫 번째 인덱스 번호 0인 문자 Word[0]을 Word[1]과 비교합니다. 그리고 Word[0]과 Word[2]를 비교합니다. 이런 식으로 순차적으로 첫 번째 문자와 나머지 문자들을 비교하는 방법입니다.

```cpp
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

<br><br>