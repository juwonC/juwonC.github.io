---
title: "[Unity]FindObjectOfType"
excerpt: "SnowBoarding - FindObjectOfType"

categories:
  - SnowBoarding
tags:
  - [Unity, SnowBoarding]

toc: true
toc_sticky: true

date: 2024-01-16
---

## 🎮FindObjectOfType
### ⚙️FindObjectOfType
자신 이외의 다른 게임 오브젝트의 컴포넌트에 접근하기 위해 FindObjectOfType() 메서드를 사용할 수 있다. 하지만 이 방법은 대상이 여러 개 있을 경우 동작하지 않는다.

플레이어 게임 오브젝트의 컴포넌트인 PlayerController에서 레벨 스프라이트 게임 오브젝트의 SurfaceEffector2D 컴포넌트에 접근해서 SurfaceEffector2D의 속도를 수정하는 코드이다.

```cs
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [SerializeField] float boostSpeed = 40f;
    [SerializeField] float baseSpeed = 20f;

    SurfaceEffector2D surfaceEffector2D;

    // Start is called before the first frame update
    void Start()
    {
        surfaceEffector2D = FindObjectOfType<SurfaceEffector2D>();
    }

    // Update is called once per frame
    void Update()
    {
        RespondToBoost();
    }

    void RespondToBoost()
    {
        if(Input.GetKey(KeyCode.Space)) 
        {
            surfaceEffector2D.speed = boostSpeed;
        }
        else
        {
            surfaceEffector2D.speed = baseSpeed;
        }
    }
}
```

<br><br>