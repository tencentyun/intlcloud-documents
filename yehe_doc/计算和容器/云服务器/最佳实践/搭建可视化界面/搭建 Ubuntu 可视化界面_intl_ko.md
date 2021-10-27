## 작업 시나리오
VNC(Virtual Network Console)는 가상 네트워크 콘솔의 약자로, 유명한 AT&T의 유럽 연구소에서 개발한 우수한 원격 제어 툴 소프트웨어입니다. VNC는 UNIX와 Linux 운영 체제 기반의 오픈 소스 소프트웨어이며, Windows 및 MAC의 어떤 원격 제어 소프트웨어에도 뒤지지 않는 강력하고 효율적인 원격 제어 기능을 갖추고 있습니다. 본문은 Ubuntu 운영 체제의 CVM에 시각화 인터페이스를 구축하는 방법을 소개합니다.

## 전제 조건
Ubuntu 운영 체제 Linux CVM을 구비해야 합니다. CVM을 구매하지 않았다면, [Linux CVM 빠른 구성](https://intl.cloud.tencent.com/zh/document/product/213/10517)을 참고하시기 바랍니다.


## 작업 순서


### 인스턴스 보안 그룹 설정

VNC 서비스는 TCP 프로토콜을 사용하며 기본적으로 5901 포트가 사용됩니다. 인스턴스에 바인딩된 보안 그룹에서 5901 포트가 개방되어 있어야 합니다. 인바운드 규칙 TCP:5901을 생성하여 5901 포트를 개방합니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.


### 패키지 설치
1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 실행하여 현재 사용자를 root 사용자로 전환합니다.
```
sudo -i
```
3. 다음 명령어를 실행하여 최신 소프트웨어 및 버전 정보를 업데이트하고 획득합니다.
```
apt-get update
```
4. 다음 명령어를 실행하여 데스크톱 환경에 필요한 소프트웨어 패키지를 설치합니다. 시스템 패널, 창 관리자, 파일 브라우저 및 터미널과 같은 데스크톱 응용 프로그램을 포함합니다.
```bash
apt install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal ubuntu-desktop
```



### VNC 설정

1. 실제 상황에 따라 다음 명령어를 실행하여 VNC를 설치합니다.
<dx-tabs>
::: Ubuntu 18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
2. [](id:step02)다음 명령어를 실행하여 VNC 서비스를 시작하고 VNC의 비밀번호를 설정합니다.
```
vncserver
```
다음과 같은 결과가 반환되면 VNC가 성공적으로 실행되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
3. 다음 명령어를 실행하여 VNC 구성 파일을 엽니다.
```
vi ~/.vnc/xstartup
```
4. **i**를 눌러 편집 모드로 전환하고 구성 파일을 다음 콘텐츠와 같이 수정합니다.
```
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"
gnome-session --session=gnome-flashback-metacity --disable-acceleration-check &
```
5. **Esc**를 눌러 **:wq**를 입력하면 파일이 저장 및 반환됩니다
6. 다음 명령어를 실행하여 데스크톱 프로세스를 재시작합니다.
```
vncserver -kill :1 #기존 데스크톱 프로세스 종료 후 명령어 입력(이 중 :1은 데스크톱 번호)
```
```
vncserver -geometry 1920x1080 :1 #새로운 세션 생성
```
7. [여기](https://www.realvnc.com/en/connect/download/viewer/)를 클릭하여 VNC Viewer 공식 홈페이지로 이동한 후 로컬 컴퓨터의 운영 체제 유형에 따라 버전을 다운로드하고 설치합니다.
8. VNC Viewer 소프트웨어에서 `CVM의 IP 주소 :1`을 입력하고 **Enter**를 누릅니다.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
9. 팝업된 알림 창에서 **Continue**를 클릭합니다.
10. [2단계](#step02)에서 설정한 VNC 비밀번호를 입력하고 **OK**를 클릭하면 인스턴스에 로그인하여 그래픽 인터페이스를 사용할 수 있습니다.



