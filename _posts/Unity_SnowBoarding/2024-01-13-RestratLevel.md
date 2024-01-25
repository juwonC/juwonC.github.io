---
title: "[Unity]레벨 재시작"
excerpt: "SnowBoarding - 레벨 재시작"

categories:
  - SnowBoarding
tags:
  - [Unity, SnowBoarding]

toc: true
toc_sticky: true

date: 2024-01-13
---

## 🎮레벨 재시작
### ⚙️도착점 만들기
우선 빈 게임 오브젝트를 만들고 오브젝트의 자식으로 사각형과 원 스프라이트를 붙여서 골인 지점을 만들었다.

FinishLine 이라는 C# 스크립트를 만들고 골인 지점에 해당하는 오브젝트에 추가한다.

FinishLine C# 스크립트에 OnTriggerEnter2D() 메서드를 사용해 골인 지점에 무엇인가 지나가면 콘솔에 로그 메세지를 출력하도록 테스트한다.

플레이어만 골인 지점을 지나가면 로그 메세지를 출력하도록 하겠다. 우선 플레이어 오브젝트의 태그를 Player로 설정한다.

그 다음 OnTriggerEnter2D() 메서드를 이용해서 충돌하는 오브젝트의 태그가 플레이어인지 검사하고 로그 메세지를 출력하도록 한다.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class FinishLine : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D collision)
    {
        if(collision.tag == "Player")
        {
            Debug.Log("You finished!");
        }
    }
}
```

<br>

### ⚙️SceneManager
화면 전환을 위해 SceneManagement 네임스페이스 안에 있는 SceneManager 클래스를 사용해야 한다.

[https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html)

현재 Scene을 저장하고 빌드 세팅에서 새로 만들었던 Scene을 불러와야 한다.

![BuildSetting](/assets/images/SnowBoarding/BuildSetting.png){: width="400" height="400"}{: .align-center}

그 다음 스크립트에서 플레이어가 골인 지점과 충돌할 때 SceneManager가 0번 Scene을 로드하도록 만들면 된다.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class FinishLine : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D collision)
    {
        if(collision.tag == "Player")
        {
            // Debug.Log("You finished!");
            SceneManager.LoadScene(0);
        }
    }
}
```

플레이어가 골인 지점과 충돌하면 처음 Scene으로 돌아가는 것을 확인할 수 있다.

<br>

💡Ctrl + .

Visual Studio에서 SceneManager. 까지만 타이핑하고 Ctrl + .을 입력하면 아래와 같이 자동완성 기능을 제공해준다.

![Namespace](/assets/images/SnowBoarding/Namespace.png){: width="500" height="500"}{: .align-center}

<br><br>