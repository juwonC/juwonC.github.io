---
title: "[Unity]사운드 효과 추가"
excerpt: "SnowBoarding - 사운드 효과 추가"

categories:
  - SnowBoarding
tags:
  - [Unity, SnowBoarding]

toc: true
toc_sticky: true

date: 2024-01-25
---

## 🎮사운드 효과
### ⚙️사운드 효과

* 오디오 리스너: 마이크 처럼 소리를 받아들이는 장치이다. Scene에서 기본값으로 카메라에 위치한다. 메인 카메라의 Inspector 창을 보면 이미 오디오 리스너가 컴포넌트로 추가되어 있는 것을 확인할 수 있다.

* 오디오 소스: 소리를 만들고 설정(볼륨 조절 등)을 조절하도록 한다.

* 오디오 클립: Scene에서 재생할 소리의 데이터(mp3, Wav, OGG)

<br>

### ⚙️사운드 효과 추가
골인 지점에 Audio Source 컴포넌트를 추가하고 Audio Clip에 원하는 소리의 데이터를 지정한다.

![AudioSource](/assets/images/SnowBoarding/AudioSource.png){: width="400" height="400"}{: .align-center}

오디오 클립 필드로 파일을 지정하게 되면 특정한 게임 오브젝트에 사운드 효과가 적용된다.

프로젝트를 실행하자마자 소리가 나는 것을 방지하기 위해 PlayOnAwake 옵션은 꺼준다.

마지막으로 골인 지점의 트리거를 지나면 소리가 나도록 스크립트를 수정한다.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class FinishLine : MonoBehaviour
{
    [SerializeField] float reloadTime = 0.5f;
    [SerializeField] ParticleSystem finishEffect;

    void OnTriggerEnter2D(Collider2D collision)
    {
        if(collision.tag == "Player")
        {
            finishEffect.Play();
            GetComponent<AudioSource>().Play();
            Invoke("ReloadScene", reloadTime);
        }
    }

    void ReloadScene()
    {
        SceneManager.LoadScene(0);
    }
}
```

### ⚙️사운드 중첩 재생

오디오 소스에 오디오 클립을 지정하는 방법도 있지만 스크립트에서 SerializeField로 오디오 클립을 저장하여 사운드 효과를 추가하는 방법도 있다. 이 방법은 여러 소리를 동시에 중첩해서 사용할 수 있다.

```cs
public class CrashDetector : MonoBehaviour
{
    [SerializeField] AudioClip crashSFX;

    void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.tag == "Ground")
        {
            GetComponent<AudioSource>().PlayOneShot(crashSFX);
        }
    }
}
```

<br><br>