## 작업 시나리오
VNC(Virtual Network Console)는 가상 네트워크 콘솔의 약자로, 유명한 AT&T의 유럽 연구소에서 개발한 훌륭한 원격 제어 툴 소프트웨어입니다. VNC는 UNIX와 Linux 운영 체제 기반의 오픈 소스 소프트웨어이며, Windows 및 MAC의 어떤 원격 제어 소프트웨어에도 뒤지지 않는 강력하고 효율적인 원격 제어 기능을 갖추고 있습니다. 본 문서는 Ubuntu 운영 체제의 CVM에 시각화 인터페이스를 구축하는 방법을 소개합니다.

## 전제 조건
운영 체제가 Ubuntu인 Linux CVM을 구매해야 합니다. CVM을 아직 구매하지 않았다면 [Linux CVM 사용자 정의 설정](https://intl.cloud.tencent.com/document/product/213/10517)을 참고하십시오.


- 작업 순서

1. [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 실행하여 현재 사용자를 root 사용자로 전환합니다.
```
sudo su root
```
3. 다음 명령어를 실행하여 최신 소프트웨어 및 버전 정보를 업데이트하고 획득합니다.
```
apt-get update
```
4. 실제 상황에 따라 다음 명령어를 실행하여 VNC를 설치합니다.
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu\s20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
5. <span id="step05"></span>다음 명령어를 실행하여 VNC 서비스를 시작하고 VNC의 비밀번호를 설정합니다.
```
vncserver
```
다음과 같은 결과가 반환되면 VNC가 성공적으로 실행되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
6. 다음 명령어를 실행하여 기본적인 X-windows를 설치합니다.
```
sudo apt-get install x-window-system-core
```
7. 실제 상황에 따라 다음 명령어를 실행하여 로그인 관리자를 설치합니다.
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
sudo apt-get install gdm
```
:::
::: Ubuntu\s20.04
```
sudo apt-get install gdm3
```
:::
</dx-tabs>
8. 다음 명령어를 실행하여 Ubuntu의 데스크톱을 설치합니다.
```
sudo apt-get install ubuntu-desktop
```
설치 중 `Default display manager:`는 'gdm3'을 선택합니다.
9. 다음 명령어를 실행하여 Gnome 관련 패키지 소프트웨어를 설치합니다.
```
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
10. 다음 명령어를 실행하여 VNC 구성 파일을 엽니다.
```
vi ~/.vnc/xstartup
```
11. **i**를 눌러 편집 모드로 전환하고 구성 파일을 다음과 콘텐츠와 같이 수정합니다.
```
#!/bin/sh
# Uncomment the following two lines for normal desktop:
export XKL_XMODMAP_DISABLE=1
 unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```
12. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 반환합니다.
13. 다음 명령어를 실행하여 데스크톱 프로세스를 재시작합니다.
```
vncserver -kill :1 #기존 데스크톱 프로세스 종료 후 명령어 입력(이 중 :1은 데스크톱 번호)
```
```
vncserver :1 #새로운 세션 생성
```
14. [여기](https://www.realvnc.com/en/connect/download/viewer/)를 클릭하여 VNC Viewer 공식 홈페이지로 이동한 후 로컬 컴퓨터의 운영 체제 유형에 따라 버전을 다운로드하고 설치합니다.
15. VNC Viewer 소프트웨어에서 `CVM의 IP 주소 :1`을 입력하고 **Enter**를 누릅니다.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
16. 팝업된 알림 창에서 [Continue]를 클릭합니다.
17. [5단계](#step05)에서 설정한 VNC의 비밀번호를 입력하고 [OK]를 클릭합니다.
>?연결 시간 초과의 오류 보고 정보가 발생한 경우, 네트워크의 연결 여부 및 보안 그룹 개방 여부를 확인하십시오. 보안 그룹은 VNC Server가 수신하는 5901 포트가 개방되어 있어야 합니다. 즉, '인바운드 규칙'에 개방 프로토콜 포트를 `TCP:5901`로 하는 규칙이 추가되어야 합니다. 구체적인 작업은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조하십시오.









