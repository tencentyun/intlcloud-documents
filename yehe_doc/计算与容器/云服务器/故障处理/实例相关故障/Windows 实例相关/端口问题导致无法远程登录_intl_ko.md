본 문서는 CVM이 포트 문제로 인해 원격 로그인할 수 없는 경우의 문제 해결 및 솔루션에 대해 소개합니다.
> 다음 작업은 Windows Server 2012 시스템의 CVM을 예로 듭니다.
>

## 점검 툴
Tencent Cloud가 제공하는 아래의 툴을 통해 로그인할 수 없는 이유가 포트 및 보안 그룹 설정과 연관되어 있는지 판단할 수 있습니다.
- [자가 진단](https://console.cloud.tencent.com/workorder/check) 
- [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper) 

점검 결과 보안 그룹의 설정 문제로 진단할 경우, [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper) 의 [원클릭 오픈] 기능을 통해 관련 포트를 오픈하고 로그인을 다시 시도할 수 있습니다. 포트 오픈 후에도 로그인에 실패할 경우 아래 내용을 참조하여 단계적으로 원인을 조사할 수 있습니다.

## 문제 해결

### 네트워크 연결성 점검

로컬 Ping 명령어를 통해 네트워크의 연결성을 테스트할 수 있습니다. 이와 동시에 서로 다른 네트워크 환경(다른 IP 대역 또는 다른 통신사)의 컴퓨터로 테스트하여 로컬 네트워크 문제인지 서버 문제인지 판단합니다.

1. 로컬 컴퓨터의 각 운영 체제에 따라 명령 툴의 여는 방식을 선택합니다.
 - Windows 시스템: [시작]>[운행]을 클릭하고 **cmd**을 입력하면 명령 창이 팝업됩니다.
 - Mac OS 시스템: Terminal 툴을 엽니다.
2. 다음 명령어를 실행하여 네트워크 연결을 테스트합니다.
```
ping + CVM 인스턴스 공인 IP 주소
```
예시,  `ping 139.199.XXX.XXX` 명령어를 실행합니다.
 - 네트워크가 정상이면 아래와 같은 결과를 출력합니다. [원격 데스크톱 서비스 설정을 점검](#F2)하세요.
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - 네트워크가 비정상이면 [요청 시간 초과] 알림이 표시됩니다. [인스턴스 IP 주소 Ping block](https://cloud.tencent.com/document/product/213/14639)을 참조하여 문제를 해결하세요.
3. 다음 명령어를 실행하고 **Enter**를 눌러 원격 포트의 오픈 상황을 테스트하여, 포트 액세스 가능 여부를 판단합니다.
```
telnet + CVM 인스턴스 공인 IP 주소 + 포트 번호
```
예시, `telnet 139.199.XXX.XXX 3389` 명령어를 실행합니다. 아래 이미지 참조
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - 정상 상황: 블랙 스크린에 커서만 나타납니다. 원격 포트(3389) 액세스 가능함을 뜻하므로 [인스턴스 원격 데스크톱 서비스 오픈 여부를 점검](#F2)하세요.
 - 비정상 상황: 연결 실패, 네트워크에 문제 발생했음을 뜻하므로 문제 네트워크의 관련 부분을 점검하세요. 아래 이미지 참조
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### 원격 데스크톱 서비스 설정 점검

#### VNC 방식으로 CVM에 로그인

> VNC 방식은 사용자가 표준 방식으로 서버에 로그인할 수 없는 경우 권장하는 로그인 방식입니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인합니다.
2. 점검 예정인 CVM을 선택하여 [Log In]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### CVM의 원격 데스크톱 설정 활성화 여부 점검

1. CVM에서 [이 컴퓨터]>[속성]을 우클릭하여 “시스템” 창을 엽니다.
2. “시스템” 창에서 [고급 시스템 설정]을 선택하여 “시스템 속성” 창을 엽니다.
3. "시스템 속성" 창에서 [원격] 탭을 선택하여 "원격 데스크톱" 기능 표시줄에서 [이 컴퓨터로의 원격 연결 허용]을 체크했는지 점검합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - 네, 원격 연결 설정 활성화이므로 [원격 액세스 포트 오픈 여부를 점검](#F3)하세요.
 - 아니요, [이 컴퓨터로의 원격 연결 허용]을 체크하고 인스턴스에 다시 원격 연결하여 연결에 성공했는지 조회하세요.

<span id = "F3"></span>
### 원격 액세스 포트 오픈 여부 점검

1. CVM에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img>을 클릭하여 “Windows PowerShell” 창을 엽니다.
2. “Windows PowerShell” 창에서 아래 명령어를 실행하여 원격 데스크톱 운행 상황(기본 상황에서 원격 데스크톱 서비스 포트 번호는 3389)을 점검합니다.
```
netstat -ant | findstr 3389
```
 - 아래와 같은 결과를 출력하면 정상 상황입니다. [원격 데스크톱을 다시 시작](#F4)하고 인스턴스에 다시 원격 연결하여 연결에 성공했는지 조회하세요.
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - 아무 연결도 나타나지 않으면 비정상입니다. [레지스트리 원격 포트 일치 여부를 점검](#F5)하세요.

<span id = "F5"></span>
### 레지스트리 원격 포트 일치 여부 점검

> 해당 단계에서는 **TCP PortNumber** 와 **RDP Tcp PortNumer** 두 곳의 포트 번호를 점검하며, 두 포트 번호가 반드시 일치해야 합니다.
>
1. CVM에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>을 클릭하고, <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>을 선택하여 **regedit**를 입력한 다음 **Enter**를 눌러 “레지스트리 편집기” 창을 엽니다.
2. 왼쪽 메뉴에서 차례대로 [HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[Terminal Server]>[Wds]>[rdpwd]>[Tds]>[tcp] 디렉터리를 엽니다.
3. [tcp] 중에서 PortNumber를 찾아 PortNumber 의 데이터(즉 포트 번호, 기본값 3389)를 기록합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/c412f3d3d1b7e46d175b49fa418e2048.png)
4. 왼쪽 메뉴에서 차례대로 [HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[Terminal Server]>[WinStations]>[RDP-Tcp] 디렉터리를 엽니다.
5. [RDP-Tcp] 중에서 PortNumber를 찾고, [RDP-Tcp] 중의 PortNumber 데이터(포트 번호)와 [tcp] 중의 PortNumber 데이터(포트 번호)가 일치하는지 확인합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/8240dd43dcb3ca246caf3397e4a1e84f.png)
 - 일치하지 않을 경우 [6단계](#F5_step6)를 실행하세요.
 - 일치할 경우 [원격 로그인 서비스 재시작](#F4)하세요.
6. [RDP-Tcp] 중에서 PortNumber를 더블 클릭합니다.
7. 팝업된 창에서 "값 데이터"를 0 - 65535 사이의 사용 중이 아닌 포트로 수정하여 **TCP PortNumber** 와 **RDP Tcp PortNumer** 포트 번호가 일치하도록 한 후 [확인]을 클릭합니다.
7. 수정 완료 후 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 해당 인스턴스를 재시작하고 인스턴스 원격 연결을 다시 진행하여 연결 여부를 조회합니다.


<span id = "F4"></span>
### 원격 로그인 서비스 재시작

1. CVM에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>을 클릭하고, <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>을 선택하여 **services.msc**를 입력한 다음 **Enter**를 눌러 "서비스" 창을 엽니다.
2. "서비스" 창에서 [Remote Desktop Services]를 찾아 [Remote Desktop Services]를 우클릭하고 [재시작]을 선택하여 원격 로그인 서비스를 재시작합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## 기타 작업

상기 작업을 실행해도 원격 로그인할 수 없는 문제를 해결하지 못할 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백 바랍니다.
