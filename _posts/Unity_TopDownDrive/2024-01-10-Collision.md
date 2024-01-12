---
title: "[Unity]충돌"
excerpt: "TopDown Drive - 충돌"

categories:
  - TopDownDrive
tags:
  - [Unity, TopDown Drive]

toc: true
toc_sticky: true

date: 2024-01-10
---

## 🎮충돌
### ⚙️Collider
두 오브젝트 사이에 충돌이 일어나게끔 하려면 Collider를 추가해야 한다.

전에 만들었던 차 오브젝트를 선택해 Inspector 창 가장 아래에서 Add Component를 눌러 Capsule Collider 2D를 추가해준다.(2D가 붙지 않은 콜라이더들은 3D 오브젝트에 적용)

Collider를 추가하고 Sprite Renderer를 잠시 끄고 확인해보면 초록색 영역으로 충돌 영역이 만들어진 것을 확인할 수 있다.

![CapsuleCollider2D](/assets/images/TopDownDrive/CapsuleCollider2D.png){: width="300" height="300"}{: .align-center}

차와 충돌할 장애물에도 콜라이더를 똑같이 적용해준다.

프로젝트를 실행시켜 차와 장애물을 충돌시켜 보면 장애물이 움직이지 않는다는 것을 확인할 수 있다.

차가 장애물과 충돌했을 때 장애물이 움직이려면 둘 중 하나에 리지드 바디라는 것을 적용시켜야 한다.

<br>

### ⚙️Rigidbody
리지드 바디는 물리적인 작용을 가능하게 하는 것이다.

플레이어의 차를 클릭하고 Rigidbody 2D라는 컴포넌트를 추가한다. Rigidbody 2D 컴포넌트를 추가함으로써 플레이어는 이제 유니티 물리 시스템 안에서 상호작용할 수 있게 되었다.

Rigidbody를 추가하면 중력이 작용하는데 탑다운 게임을 만들 것이기 때문에 중력은 0으로 설정한다.

장애물에 Rigidbody를 추가하지 않으면 플레이어와 충돌은 하는데 움직이지는 않을 것이다. 플레이어와 충돌했을 때 장애물도 움직이게 하려면 Rigidbody 2D 컴포넌트를 추가하면 된다.

<br>

### ⚙️OnCollisionEnter2D()
충돌이 일어났을 때 콘솔에 메세지를 출력하는 작업을 해보자.

C# 스크립트 파일을 하나 더 만들고 아래와 같이 작성한다.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Collision : MonoBehaviour
{
    void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("Bump!");
    }
}
```

충돌이 일어날 때 메세지가 출력되는 것을 확인하려면 스크립트를 플레이어의 컴포넌트로 추가한다.

![CollisionScript](/assets/images/TopDownDrive/CollisionScript.png){: width="300" height="300"}{: .align-center}

프로젝트를 실행해서 장애물과 플레이어를 충돌시키면 콘솔 창에 메세지가 출력되는 것을 확인할 수 있다.

![CollisionLog](/assets/images/TopDownDrive/CollisionLog.png){: width="700" height="700"}{: .align-center}

<br>

### ⚙️OnTriggerEnter2D()
어떤 영역을 지나면 콘솔에 메세지를 출력하는 작업을 해보자.

우선 원 오브젝트를 하나 추가하고 Collider 컴포넌트를 추가한다. 원을 지난다는 것을 알기 위해 영역을 설정해 줘야 하기 때문에 Collider가 필요하다.

원 형태의 오브젝트를 타원형으로 만들었고 거기에 Capsule Collider 2D를 추가했다. 추가한 오브젝트에 Collider만 추가하면 해당 오브젝트와 플레이어 차가 충돌했을 때 오브젝트가 움직이지 않고 플레이어는 오브젝트를 뚫고 가지 못하는 것을 확인할 수 있다.

플레이어 차가 오브젝트를 지나가기 위해 Capsule Collider 2D 컴포넌트에서 Is Trigger 옵션을 켜야 한다.

플레이어 차가 오브젝트를 지나갈 때 아래로 간다면 Order in Layer를 바꿔준다. 플레이어가 위로 가게 하려면 플레이어의 Order in Layer를 높여야 한다.

이제 타원 오브젝트를 지나면 콘솔에 메세지를 출력하도록 해야 한다.

위에서 작업했던 Collision 스크립트에서 OnTriggerEnter2D() 메서드를 추가해준다.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Collision : MonoBehaviour
{
    void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("Bump!");
    }

    void OnTriggerEnter2D(Collider2D collision)
    {
        Debug.Log("Pass!");
    }
}
```

* OnTriggerExit2D()

OnTriggerExit2D()이라는 메서드를 사용하면 특정 영역을 벗어났을 때 무엇인가를 할 수도 있다.

<br><br>