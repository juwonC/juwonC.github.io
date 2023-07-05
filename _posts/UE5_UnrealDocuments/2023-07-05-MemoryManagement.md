---
title: "[UE5]메모리 관리"
excerpt: "메모리 관리"

categories:
  - Unreal_Documents
tags:
  - [UE5, 메모리 관리]

toc: true
toc_sticky: true

date: 2023-07-05
---

## 🎮메모리 관리
### ⚙️언리얼 오브젝트의 메모리 관리
스마트 포인터 라이브러리는 일반 C++ 객체를 위한 것이라서 언리얼 오브젝트에는 사용할 수 없습니다. 언리얼 오브젝트는 언리얼 엔진 가상 머신의 가비지 컬렉션에 의해 자동적으로 관리됩니다. 하나의 언리얼 오브젝트가 가비지 컬렉션에 의해 자동 관리되기 위해서 선언에 반드시 UPROPERY 매크로가 들어가야 합니다. 그러면 언리얼 엔진에 의해서 필요가 없어질 때 자동으로 회수됩니다.

가비지 컬렉션 시스템이 언리얼 오브젝트를 관리하는 방식은 스마트 포인터 중 공유 포인터와 거의 유사합니다. 다만 다른 점은 중앙의 GC 시스템에 의해서 모든 관리되기 때문에, 메모리에서 해지되는 타이밍을 정확히 예측할 수 없다는 점입니다.

<br>

출처
<br>
[이득우 교수님의 블로그](https://blog.naver.com/PostView.naver?blogId=destiny9720&logNo=220951194710&categoryNo=19&parentCategoryNo=&from=thumbnailList)

<br><br>