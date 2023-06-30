본 문서는 CVM이 포트 문제로 인해 원격 로그인이 불가능한 경우의 진단 방법과 솔루션을 소개합니다.
>?아래 작업은 CentOS 7.8 시스템의 CVM을 예로 듭니다.
>

## 점검 툴
Tencent Cloud가 제공한 아래의 툴을 통해 로그인이 불가능한 문제가 포트 및 보안 그룹 설정과 관련이 있는지 판단할 수 있습니다. 
- [자가 진단](https://console.cloud.tencent.com/workorder/check)
- [인스턴스 포트 진단 툴](https://console.cloud.tencent.com/vpc/helper)

보안 그룹 설정 문제로 진단된 경우, [인스턴스 포트 진단 툴](https://console.cloud.tencent.com/vpc/helper)의 [원클릭 오픈] 기능을 통해 관련 포트를 개방한 후 다시 로그인을 시도하십시오. 포트를 개방한 후에도 로그인에 실패한다면 다음 내용을 참조하여 원인을 진단할 수 있습니다.

## 문제 진단
### 네트워크 연결성 점검
로컬 Ping 명령어를 통해 네트워크 연결성을 테스트할 수 있습니다. 서로 다른 네트워크 환경(IP 대역 또는 ISP)의 컴퓨터를 동시에 사용한 테스트로 로컬 네트워크 문제인지, 서버 문제인지 판단합니다.
1. 로컬 컴퓨터의 운영 체제에 따라 TCCLI를 여는 방식을 선택합니다.
	- **Windows 시스템**: [시작]>[실행]을 클릭하고 cmd를 입력하면 명령 라인 대화 상자가 팝업됩니다.
	- **Mac OS 시스템**: Terminal 툴을 엽니다.
2. 아래의 명령어를 실행하여 네트워크 연결을 테스트합니다.
```
ping + CVM 인스턴스 공용 IP 주소
```
[공용 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17940)을 참조하여 CVM 인스턴스 공용 IP를 획득할 수 있습니다(예: `ping 81.71.XXX.XXX` 실행).

 - 네트워크가 정상인 경우 다음과 유사한 결과를 반환합니다.
![](https://main.qcloudimg.com/raw/cb15a53fec87466a2a48f88bb4542df4.png)
 - 네트워크가 비정상인 경우 [요청 시간 초과] 알림이 뜹니다. [인스턴스 IP주소 Ping 연결 불가](https://intl.cloud.tencent.com/document/product/213/14639)를 참조하여 진단하십시오.

### 인스턴스 포트 연결성 점검
1. VNC로 CVM에 로그인합니다. 자세한 내용은 [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참조하십시오.
2. 아래의 명령어를 실행하고 **Enter**를 누릅니다. 원격 포트의 활성화 상태를 테스트하여 포트에 액세스가 가능한지 판단합니다.
```
telnet + CVM 인스턴스 공용 IP 주소 + 포트 번호
```
예: `telnet 119.XX.XXX.67 22` 명령어를 실행하여 22 포트의 연결성을 테스트합니다.
 - 정상 상태: 아래 이미지와 같은 정보를 반환할 경우 22 포트에 액세스할 수 있습니다.
![](https://main.qcloudimg.com/raw/246134de6829323457dc1d51f85589b8.png)
 - 비정상 상태: 아래 이미지와 같은 정보를 반환할 경우 22 포트에 액세스할 수 없습니다. 문제가 발생한 네트워크에 해당하는 부분을 점검하십시오(예: 인스턴스의 방화벽 또는 보안 그룹의 22 포트 개방 여부).
 ![](https://main.qcloudimg.com/raw/d6eadfe7638046f0b0c1f15261ea74ab.png)


### sshd 서비스 점검
[SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)할 때 연결 불가 또는 연결 실패 알림이 뜹니다. sshd 포트가 수신되지 않았거나 sshd 서비스가 실행되지 않은 것이 원인일 수 있습니다. [SSH 방식으로 Linux 인스턴스에 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32486)를 참조하여 진단하십시오.
