---
title: "터미널? 콘솔?"
excerpt: "터미널과 콘솔"

categories:
  - MyInterests
tags:
  - [터미널, 콘솔]

toc: true
toc_sticky: true

date: 2023-03-31
---

## 🤓터미널
과거 컴퓨터는 오늘날의 컴퓨터의 모습과 많이 달랐다. 과거 컴퓨터는 매우 거대했으며 구멍 뚫린 카드나 테이프를 사용하여 프로그램을 작성하고 그걸 메인프레임이라고 하는 거대한 컴퓨터에 읽혀서 계산 결과를 종이로 출력하여 봤다고 한다. 모니터, 키보드, 마우스와 같은 입출력 기기가 발명되기 전 사람들은 컴퓨터에 텔레타이프(teleprinter, teletype or TTY)라는 기기를 연결하여 사용하였다. 텔레타이프는 컴퓨터와 연결된 선의 끝에 위치해있어서 터미널(Terminal)이라고 불렸다. 매우 초창기의 터미널은 컴퓨터의 끝에 붙어있는 데이터 전사 및 입출력 기능을 하는 하드웨어 장치였다.

![teletype](/assets/images/MyInterest/teletype.jpeg){: width="250" height="250"}

<br>

하지만 기술이 발전하여 CRT(Cathode-Ray Tube)라는 비디오 디스플레이 장치(VDU)가 세상에 나와 더 이상 계산 입력이나 출력을 종이에 할 필요가 없어졌다. 따라서 텔레타이프의 기능을 하는 예뮬레이터를 만들었고 이를 VDU 터미널에서 사용하였다. 그렇게 VDU 터미널이 종이를 사용하는 하드 카피 터미널인 텔레타이프를 대체하였다. 여담으로 초창기의 텔레타이프 예뮬레이터를 'Glass TTYs'라고 불렀다고 한다.

시간이 더 흘러 컴퓨터의 성능은 훨씬 좋아졌고 크기는 더 소형화되었다. 더 나아가 컴퓨터 환경이 텍스트 기반의 CLI(Command Line Interface) 환경에서 GUI(Graphic User Interface) 환경으로 변화하였고 개인용 컴퓨터(PC)가 보급되면서 과거 하드웨어로서의 터미널이 가지는 의미가 퇴색되었다. 하지만 터미널이 사라진 것은 아니다. 오늘날 터미널은 소프트웨어로서 컴퓨터 안에 프로그램으로 들어가 있다.

![vt100](/assets/images/MyInterest/VT100.png){: width="250" height="250"}

<br>

물론 넓은 의미로 보면 컴퓨터 끝에 붙어있는 여러 하드웨어 장치들을 모두 터미널이라고 부를 수 있겠지만 오늘날의 컴퓨터 시스템에서 터미널이라는 용어는 터미널 예뮬레이터라고 하는 소프트웨어적인 의미에 더 초점을 두고 사용되고 있다. 소프트웨어로서의 터미널은 컴퓨터의 쉘을 실행할 수 있는 Wrapper 프로그램이다. 터미널은 여러 의미를 가지고 있어 쉽게 정의 내리기 어렵다. 따라서 우리는 터미널을 텍스트 입력 및 출력 인터페이스 및 환경이라고 생각하면 될 것 같다.

<br><br>

## 🤓콘솔
콘솔은 여러 가지 의미를 가지지만 일반적으로 컴퓨터의 입출력을 담당하는 물리적인 장치를 뜻한다. 간단하게 예를 들면 오늘날 우리가 사용하는 키보드나 마우스, 모니터 등에 해당하는 장치들을 말한다. 과거 키보드, 마우스, 모니터 등 오늘날의 입출력 장치들이 있기 전 콘솔은 컴퓨터 시스템 관리에 사용되는 물리적 장치였다. 메인프레임에 직접 연결되어 컴퓨터를 제어하고 관리하기 위해 만들어진 장치가 콘솔이었고 이것은 일종의 특수한 터미널이었다.

![sys_console](/assets/images/MyInterest/sysconsole.jpeg){: width="250" height="250"}

<br>

오늘날 콘솔이라는 용어는 터미널과 마찬가지로 소프트웨어를 의미하기도 한다. 소프트웨어 콘솔은 하드웨어 콘솔 기능과 유사하게 사용자가 명령을 입력하여 컴퓨터 시스템을 미리 사용할 수 있도록 만들어졌다. 콘솔이 일종의 터미널이라서 두 용어가 같은 의미로 혼용되기도 하고 터미널과 마찬가지로 콘솔이 가지는 의미가 여러 가지라 그 의미를 단번에 파악하기 어렵다. 우리는 콘솔을 사용자에 의해 입출력이 가능한 시스템에 직접 연결된 터미널이라고 생각하면 될 것 같다.

<br><br>

## 🤓쉘
쉘은 명령을 처리하고 결과를 출력하는 프로그램이다. 사용자가 입력한 명령어를 운영 체제(OS)로 전달하는 명령어 해석기(인터프리터)이다. 쉘은 커널 위에 있는 레이어로서 OS의 가장 바깥쪽 계층에 있기 때문에 껍질, 껍데기를 의미하는 쉘이라는 이름이 붙었다. 쉘은 역할과 작업에 따라 CLI(명령줄 인터페이스) 또는 GUI(그래픽 사용자 인터페이스)를 사용한다.

![shell](/assets/images/MyInterest/shell.png){: width="250" height="250"}

<br><br>

## 🤓명령 프롬프트
명령 프롬프트 또는 프롬프트는 CLI환경의 터미널 예뮬레이터에서 명령을 수락할 준비가 되었음을 알려주는 문자 시퀀스이고 명령줄 대기 모드이다. prompt의 말 그대로 유저가 행동(입력)을 취하도록 재촉하는 것이다.

프롬프트는 보통 `$`, %, #, :, >, -의 문자 중에 하나로 끝난다. 그리고 현재 작업 디렉터리의 경로나 호스트명 같은 다른 정보를 포함하고 있을 수 있다. 많은 유닉스 시스템과 그 파생 시스템(Mac OS)들에서 프롬프트는 일반 사용자의 경우 주로 `$` 나 %로 끝난다. 하지만 유저가 슈퍼유저(유닉스 용어: Root) 일 경우 #으로 끝난다.

![powershell](/assets/images/MyInterest/powershell.png){: width="450" height="450"}

<br>

![mac_terminal](/assets/images/MyInterest/macterminal.png){: width="450" height="450"}

<br>

다른 의미의 명령 프롬프트는 cmd.exe와 같은 말이다. 명령 프롬프트는 Windows 운영체제에 기본으로 제공되는 명령줄 인터프리터이다. 이 것은 CLI를 사용하는 여러 명령줄 쉘 중 하나인 것이다.

![cmd](/assets/images/MyInterest/cmd.png){: width="450" height="450"}

<br>

참고자료

[https://en.wikipedia.org/wiki/Computer_terminal](https://en.wikipedia.org/wiki/Computer_terminal)

[https://ko.wikipedia.org/wiki/터미널_(macOS)](https://ko.wikipedia.org/wiki/터미널_(macOS))

[https://ko.wikipedia.org/wiki/단말_에뮬레이터](https://ko.wikipedia.org/wiki/단말_에뮬레이터)

[https://ko.wikipedia.org/wiki/윈도_콘솔](https://ko.wikipedia.org/wiki/윈도_콘솔)

[https://ko.wikipedia.org/wiki/Cmd.exe](https://ko.wikipedia.org/wiki/Cmd.exe)

[https://www.techopedia.com/definition/1906/console-con](https://www.techopedia.com/definition/1906/console-con)

[https://ko.wikipedia.org/wiki/컴퓨터](https://ko.wikipedia.org/wiki/컴퓨터)

[https://www.baeldung.com/linux/terminal-shell-tty-vs-console](https://www.baeldung.com/linux/terminal-shell-tty-vs-console)

[https://www.geeksforgeeks.org/what-is-terminal-console-shell-and-kernel/?ref=gcse](https://www.geeksforgeeks.org/what-is-terminal-console-shell-and-kernel/?ref=gcse)

[https://www.geeksforgeeks.org/difference-between-terminal-console-shell-and-command-line/](https://www.geeksforgeeks.org/difference-between-terminal-console-shell-and-command-line/)

[https://en.wikipedia.org/wiki/System_console](https://en.wikipedia.org/wiki/System_console)

[https://jaguhiremath62.medium.com/difference-between-kernel-and-shell-718b3de15be6](https://jaguhiremath62.medium.com/difference-between-kernel-and-shell-718b3de15be6)

[https://en.wikipedia.org/wiki/Command-line_interface#Command_prompt](https://en.wikipedia.org/wiki/Command-line_interface#Command_prompt)

<br><br>