---
title: "[Unity]에셋 추가"
excerpt: "TopDown Drive - 에셋 추가"

categories:
  - TopDownDrive
tags:
  - [Unity, TopDown Drive]

toc: true
toc_sticky: true

date: 2024-01-11
---

## 🎮에셋 추가
### ⚙️프로젝트에 에셋 추가
열려있는 프로젝트의 에셋 폴더에 컴퓨터에 저장되어 있는 이미지나 에셋을 그대로 끌어서 놓으면 프로젝트에 에셋이 추가된다.

<br>

### ⚙️에셋 크기 변경
Scene을 보면 격자가 있는데 격자 하나에 1 유니티 유닛이라고 한다. 이 단위에 특별한 의미는 없고 사용자가 표현하고자 하는 단위가 될 수 있다.(예를 들어, 미터, 킬로미터, 인치 등)

유니티는 1 유니티 단위 당 100 픽셀이 기본값이다.

![HouseAsset](/assets/images/TopDownDrive/HouseAsset.png){: width="600" height="600"}{: .align-center}

불러온 집 에셋을 Scene에 배치했을 때 너무 작은 것을 확인할 수 있다.

픽셀의 수를 수정하지 않고 유니티에서 에셋 이미지의 크기를 조정하고 싶으면 단위 당 픽셀(Pixels Per Unit)을 조절하면 된다.

불러온 에셋을 클릭하면 Inspector 창에서 Pixels Per Unit을 조정할 수 있는 부분을 확인할 수 있다.

에셋 이미지를 크게 하고 싶으면 단위 당 픽셀을 적게 조정하면 된다.
<br>
-> 격자(1 유니티 유닛) 하나에 들어가는 픽셀 수를 적게 하면 이미지가 늘려진다고 이해.

단위 당 픽셀을 많게 조정하면 에셋 이미지를 작게 할 수 있을 것이다.
<br>
-> 격자 하나에 들어가는 픽셀 수를 많게 하면 압축되니까 이미지가 작아진다고 이해.

집 에셋의 단위 당 픽셀이 기본값 100으로 설정되어 있는데 Inspector 창에서 이 값을 25로 바꾸고 apply를 눌러 이미지를 크게 만들어 보면 아래와 같아진다.

![PixelPerUnit](/assets/images/TopDownDrive/PixelPerUnit.png){: width="300" height="300"}{: .align-center}

![ChangeAssetSize](/assets/images/TopDownDrive/ChangeAssetSize.png){: width="600" height="600"}{: .align-center}

<br>

### ⚙️스프라이트 교체
전에 만들었던 캡슐 형태의 플레이어의 스프라이트를 자동차 이미지로 바꿔보자.

플레이어를 오브젝트를 선택하고 Inspector 창에서 Sprite 항목 옆에 원 아이콘을 눌러서 타겟 스프라이트를 바꿀 수 있다.

![ChangeSprite](/assets/images/TopDownDrive/ChangeSprite.png){: width="300" height="300"}{: .align-center}

<br><br>