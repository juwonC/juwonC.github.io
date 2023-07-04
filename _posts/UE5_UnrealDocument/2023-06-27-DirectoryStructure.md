---
title: "[UE5]디렉터리 구조"
excerpt: "디렉터리 구조"

categories:
  - Unreal_Document
tags:
  - [UE5, 디렉터리 구조]

toc: true
toc_sticky: true

date: 2023-06-27
---

**언리얼 엔진 5 공식 문서** <https://docs.unrealengine.com/5.1/ko/>
{: .notice--info}

## 🎮디렉터리 구조
### ⚙️루트 디렉터리

* Enigne: 엔진을 이루는 모든 소스코드, 컨텐츠 등이 포함
* Templates: 사용 가능한 프로젝트 템플릿 모음
* GenerateProjectFiles.bat: 비주얼 스튜디오에서 엔진과 게임 작업시 필요한 솔루션 및 프로젝트 파일 생성시 사용
* UE4Games.uprojectdirs: 엔진이 하위 디렉터리의 프로젝트를 발견할 수 있도록 도와주는 헬퍼 파일

<br>

### ⚙️공통 디렉터리

* Binaries: 컴파일 도중 생성되는 실행 파일이나 기타 파일 포함
* Build: 엔진이나 게임을 빌드하는데 필요한 파일 포함
* Config: 엔진을 제어하는 환경설정 파일 포함
* Content: 엔진이나 게임에 대한 컨텐츠, 에셋 패키지와 맵 포함
* DerivedDataCeche: 참조된 컨텐츠에 대해 로드시 생성된 파생 데이터 파일 포함(참조된 컨텐츠에 대해 캐시 파일이 없으면 로드 시간이 길어질 수 있습니다.)
* Intermediate: 엔진이나 게임 빌드 도중 생성된 임시 파일 포함
* Saved: 자동저장, 환경설정, 로그 파일 포함
* Source: 엔진, 게임, 엔진 소스 코드, 툴, 게임플레이 클래스 등 모든 소스파일 포함
  - Engine
    + Developer: 에디터와 엔진 모두 쓰이는 파일
    + Editor: 에디터에만 쓰이는 파일
    + Programs: 엔진이나 에디터에 쓰이는 외부 툴
    + Runtime: 엔진에만 쓰이는 파일
  - Game
    + Classes: 모든 게임플레이 헤더 파일 포함
    + Private: 모든 .cpp파일과 게임플레이 클래스 구현파일, 모듈 구현파일 포함
    + Public: 모듈 헤더 파일 포함

<br>

### ⚙️엔진 전용 디렉터리

* Documentation: 엔진 문서 소스와 퍼블리시된 파일 포함
  - HTML: 퍼블리시된 HTML 문서 파일
  - Source: 소스 마크다운 문서 파일
* Extras: 헬퍼, 유틸리티 파일 포함
* Plugins: 엔진에 사용되는 플러그인
* Programs: 루트 디렉터리에 저장된 프로젝트와 기타 언리얼 프로그램용 환경설정 파일과 로그 파일 포함
* Shaders: 엔진에 대한 셰이더 소스 파일 포함

<br><br>