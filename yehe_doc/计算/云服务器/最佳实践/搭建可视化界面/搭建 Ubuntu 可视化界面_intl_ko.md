## 작업 시나리오
VNC(Virtual Network Console)는 가상 네트워크 콘솔의 약자입니다. 유명한 AT&T 유럽 연구소에서 개발한 우수한 원격 제어 소프트웨어입니다. VNC는 UNIX 및 Linux 운영 체제를 기반으로 하는 오픈 소스 소프트웨어로, 강력한 원격 제어 기능, 높은 효율성 및 실용성을 갖추고 있으며, 그 성능은 Windows 및 MAC의 모든 원격 제어 소프트웨어와 견줄만합니다. 본문은 Ubuntu CVM에서 시각적 인터페이스를 구축하는 방법을 안내합니다.

## 전제 조건
Ubuntu CVM을 구입 완료해야 합니다.

## 작업 단계


### 인스턴스 보안 그룹 설정

VNC 서비스는 TCP 프로토콜을 사용하며 기본적으로 5901 포트가 사용됩니다. 인스턴스에 바인딩된 보안 그룹에서 5901 포트가 개방되어 있어야 합니다. 인바운드 규칙 TCP:5901을 생성하여 5901 포트를 개방합니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.


### 패키지 설치

<dx-tabs>
::: Ubuntu 18.04
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령을 실행하여 캐시를 삭제하고 소프트웨어 패키지 리스트를 업데이트합니다.
```shellsession
sudo apt clean all && sudo apt update
```
3. 다음 명령어를 실행하여 데스크톱 환경에 필요한 소프트웨어 패키지를 설치합니다. 시스템 패널, 창 관리자, 파일 브라우저 및 터미널과 같은 데스크톱 응용 프로그램이 포함됩니다.
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. 아래의 명령어를 실행하여 VNC를 설치합니다.
```shellsession
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령을 실행하여 캐시를 삭제하고 소프트웨어 패키지 리스트를 업데이트합니다.
```shellsession
sudo apt clean all && sudo apt update
```
3. 다음 명령어를 실행하여 데스크톱 환경에 필요한 소프트웨어 패키지를 설치합니다. 시스템 패널, 창 관리자, 파일 브라우저 및 터미널과 같은 데스크톱 응용 프로그램이 포함됩니다.
```shellsession
sudo apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```
4. 아래의 명령어를 실행하여 VNC를 설치합니다.
```shellsession
apt-get install tightvncserver
```
:::
::: Ubuntu 22.04
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 캐시를 지우고 소프트웨어 패키지 목록을 업데이트합니다.
```shellsession
sudo apt clean all && sudo apt update
```
3. 데스크톱 환경을 설치합니다.
```shellsession
sudo apt install xfce4 xfce4-goodies
```
4. 아래의 명령어를 실행하여 VNC를 설치합니다.
```shellsession
sudo apt install tightvncserver
```
:::
</dx-tabs>

### VNC 설정
<dx-tabs>
::: Ubuntu 18.04
1. [](id:step02)다음 명령어를 실행하여 VNC 서비스를 시작하고 VNC의 비밀번호를 설정합니다.
```shellsession
vncserver
```
다음과 같은 결과가 반환되면 VNC가 성공적으로 실행되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2. 다음 명령어를 실행하여 VNC 구성 파일을 엽니다.
```shellsession
vi ~/.vnc/xstartup
```
3. **i**를 눌러 편집 모드로 전환하고 구성 파일을 다음 콘텐츠와 같이 수정합니다.
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4. **Esc**를 눌러 **:wq**를 입력하여 파일을 저장 및 반환합니다.
5. 다음 명령어를 실행하여 데스크톱 프로세스를 재시작합니다.
```shellsession
vncserver -kill :1 #기존 데스크톱 프로세스 종료 후 명령어 입력(이 중 :1은 데스크톱 번호)
```
```shellsession
vncserver -geometry 1920x1080 :1 #새로운 세션 생성
```
6. [여기](https://www.realvnc.com/en/connect/download/viewer/)를 클릭하여 VNC Viewer 공식 홈페이지로 이동한 후 로컬 컴퓨터의 운영 체제 유형에 따라 버전을 다운로드하고 설치합니다.
7. VNC Viewer 소프트웨어에서 `CVM의 IP 주소 :1`을 입력하고 **Enter**를 누릅니다.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. 팝업된 알림 창에서 **Continue**를 클릭합니다.
9. [2단계](#step02)에서 설정한 VNC 비밀번호를 입력하고 **OK**를 클릭하면 인스턴스에 로그인하여 그래픽 인터페이스를 사용할 수 있습니다.

:::


::: Ubuntu 20.04
1. [](id:step03)다음 명령어를 실행하여 VNC 서비스를 시작하고 VNC의 비밀번호를 설정합니다.
```shellsession
vncserver
```
다음과 같은 결과가 반환되면 VNC가 성공적으로 실행되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
2. 다음 명령어를 실행하여 VNC 구성 파일을 엽니다.
```shellsession
vi ~/.vnc/xstartup
```
3. **i**를 눌러 편집 모드로 전환하고 구성 파일을 다음 콘텐츠와 같이 수정합니다.
```shellsession
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
4. **Esc**를 눌러 **:wq**를 입력하여 파일을 저장 및 반환합니다.
5. 다음 명령어를 실행하여 데스크톱 프로세스를 재시작합니다.
```shellsession
vncserver -kill :1 #기존 데스크톱 프로세스 종료 후 명령어 입력(이 중 :1은 데스크톱 번호)
```
```shellsession
vncserver -geometry 1920x1080 :1 #새로운 세션 생성
```
6. [여기](https://www.realvnc.com/en/connect/download/viewer/)를 클릭하여 VNC Viewer 공식 홈페이지로 이동한 후 로컬 컴퓨터의 운영 체제 유형에 따라 버전을 다운로드하고 설치합니다.
7. VNC Viewer 소프트웨어에서 `CVM의 IP 주소 :1`을 입력하고 **Enter**를 누릅니다.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
8. 팝업된 알림 창에서 **Continue**를 클릭합니다.
9. [2단계](#step03)에서 설정한 VNC 비밀번호를 입력하고 **OK**를 클릭하면 인스턴스에 로그인하여 그래픽 인터페이스를 사용할 수 있습니다.

:::

::: Ubuntu 22.04
[](id:g1)
1. 다음 명령어를 실행하여 VNC 서비스를 시작하고 VNC의 비밀번호를 설정합니다.
```shellsession
vncserver
```
다음과 같은 결과가 반환되면 VNC가 성공적으로 실행되었음을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5fb63d9cc28d3a0cebd5def424051e7a.png)
2. [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) 공식 홈페이지로 이동한 후 로컬 컴퓨터의 운영 체제 유형에 따라 버전을 다운로드하고 설치합니다.
3. VNC Viewer 소프트웨어에서 `CVM의 IP 주소 :1`을 입력하고 Enter를 누릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3e7d432ce674a8587066df25f42595bf.png)
4. 팝업 창에서 **Continue**를 클릭합니다.
5. 이전 단계에서 vncserver 명령어로 생성한 비밀번호를 입력하고 OK를 클릭하면 인스턴스에 로그인하여 그래픽 인터페이스를 사용할 수 있습니다.
 <dx-alert infotype="notice" title="">
비밀번호를 잊은 경우 인스턴스에서 `vncpasswd` 명령을 실행하여 vnc 로그인 비밀번호를 다시 변경해야 합니다.
 </dx-alert>
 부록:
데스크톱 chrome 브라우저 설치:
 - 인스턴스에서 명령을 실행하여 **.deb** 패키지 파일 다운로드 
```shellsession
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
 - **.deb** 파일 설치
```shellsession
sudo apt install ./google-chrome-stable_current_amd64.deb
```
:::
</dx-tabs>
