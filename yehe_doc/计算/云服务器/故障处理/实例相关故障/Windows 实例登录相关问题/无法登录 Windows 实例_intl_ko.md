

본 문서에서는 Windows 인스턴스 로그인 실패의 가능한 원인과 문제 해결 방법에 대해 설명합니다. 지침에 따라 문제의 원인을 식별하고 해결 방법을 배울 수 있습니다.

## 예상 원인
Windows 인스턴스에 로그인할 수 없는 주요 원인은 다음과 같습니다.
- [비밀번호 문제](#CryptographicProblem)
- [높은 대역폭 이용률](#BandwidthUtilization)
- [서버 고부하](#HighServerLoad)
- [부적절한 원격 포트 설정](#RemotePortConfiguration)
- [부적절한 보안 그룹 규칙](#SafetyGroupRule)
- [방화벽 또는 보안 소프트웨어로 인한 예외](#LoginSecuritySoftware)
- [원격 데스크톱을 통한 액세스 중 인증 오류](#AuthenticationError)

## 자가 진단 툴 사용

Tencent Cloud는 대역폭, 방화벽 및 보안 그룹 설정 등의 문제로 인해 Windows 인스턴스 연결이 불가능한 것인지 판단할 수 있는 자가 진단 툴을 제공합니다. 70%의 장애는 툴에 의해 위치가 측정되며, 점검된 원인에 따라 로그인 실패를 일으키는 장애 문제의 위치를 측정할 수 있습니다.
1. [자가 진단](https://console.cloud.tencent.com/workorder/check)을 클릭하여 자가 진단 툴을 여십시오.
2. 툴 인터페이스 안내에 따라 진단할 CVM를 선택하고 **점검 시작**을 클릭합니다.

자가 진단 툴로 문제를 진단할 수 없다면 CVM에 [VNC 방식을 통해 로그인](#VNC)하여 장애를 진단하시길 권장합니다.


## 장애 처리[](id:TroubleshootingIdeas)


### VNC 방식을 통해 로그인[](id:VNC)

RDP 또는 원격 액세스 소프트웨어를 통해 Windows 인스턴스에 로그인할 수 없는 경우 대신 VNC를 통해 로그인하면 문제의 원인을 식별하는 데 도움이 됩니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이 인스턴스 관리 페이지에서 액세스할 인스턴스를 선택하고 **로그인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ‘표준 로그인 | Windows 인스턴스’ 팝업 창에서 대체 방법(VNC)을 선택하고 **지금 로그인**을 클릭합니다.
<dx-alert infotype="explain" title="">
인스턴스의 비밀번호를 잊어버린 경우 콘솔에서 재설정할 수 있습니다. 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.
</dx-alert>
4. 로그인 팝업 창에서 왼쪽 상단 모서리에 있는 Send CtrlAltDel을 선택하고 Ctrl-Alt-Delete를 눌러 다음 그림과 같이 시스템 로그인 창을 엽니다.
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)



### 비밀번호 문제[](id:CryptographicProblem)

**장애 현상**: 비밀번호를 잊었거나, 잘못된 비밀번호 입력 또는 비밀번호 재설정에 실패해 로그인할 수 없는 경우입니다.
**처리 순서**: [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에서 이 인스턴스의 비밀번호를 재설정하고 인스턴스를 다시 시작하십시오. 자세한 내용은 [인스턴스 암호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.



### 높은 대역폭 이용률[](id:BandwidthUtilization)

**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 대역폭 이용률이 너무 높은 것이 원인인 경우입니다.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [높은 대역폭 점유율로 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32542)를 참고하여 인스턴스의 대역폭 사용률을 확인하고 그에 따라 문제를 해결합니다.


### 서버 고부하[](id:HighServerLoad)

**장애 현상**: 자가 진단 툴 또는 TCOP 통해 확인한 결과, 서버 CPU의 고부하로 인해 시스템 원격 연결이 불가하거나 액세스 시 심한 랙이 발생하고 있는 경우입니다.
**예상 원인**: 바이러스, 트로이 목마, 타사 바이러스 백신 소프트웨어, 응용 프로그램 예외, 드라이버 예외 및 백엔드의 소프트웨어 자동 업데이트로 인해 CPU 사용률이 높아져 CVM 로그인 실패 또는 액세스 속도 저하가 발생할 수 있습니다.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [Windows 인스턴스: CPU 혹은 메모리 점유율이 높아 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32405)를 참고하여 ‘작업 관리자’에서 높은 부하를 일으키는 프로세스를 찾습니다.


### 부적절한 원격 포트 설정[](id:RemotePortConfiguration)

**장애 현상**: 인스턴스에 대한 원격 액세스 시도가 실패했거나, 원격 액세스 포트가 기본 포트가 아니거나, 수정되었거나, 포트 3389가 열려 있지 않습니다.
**문제 진단**: 인스턴스의 공용 IP 주소를 ping하여 네트워크 연결을 확인하고 telnet을 실행하여 포트가 열려 있는지 확인합니다.
**처리 순서**: 자세한 절차는 [포트 문제로 원격 로그인을 할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32540)를 참고하십시오.


### 부적절한 보안 그룹 규칙[](id:SafetyGroupRule)

**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 보안 그룹 규칙 설정이 적합하지 않아 로그인하지 못하는 경우입니다.
**처리 순서**: [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 문제를 해결합니다.
<dx-alert infotype="notice" title="">
원격으로 로그인한 Windows 인스턴스의 경우 포트 3389를 개방해야 합니다.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/bd91ec53dfd0df6bd1127a7f4f9db35c.png"/><br>
보안 그룹에 대한 사용자 정의 규칙을 사용자 정의하려면 <a href="https://intl.cloud.tencent.com/document/product/213/34272">보안 그룹 규칙 추가</a>를 참고하십시오.



### 방화벽 또는 보안 소프트웨어로 인한 예외[](id:LoginSecuritySoftware)

**장애 현상**: CVM 방화벽 또는 보안 소프트웨어로 인해 로그인 시도가 실패했습니다.
**문제 진단**: VNC를 통해 Windows 인스턴스에 로그인하여 방화벽이 활성화되어 있는지, 360 Total Security 또는 보안 동글(dongles)과 같은 보안 소프트웨어가 서버에 설치되어 있는지 확인하십시오.
<dx-alert infotype="notice" title="">
이 작업에는 CVM 방화벽을 종료하는 작업이 포함됩니다. 이를 수행하려면 해당 권한이 있는지 확인하십시오.
</dx-alert>

**처리 순서**: 방화벽 또는 설치된 보안 소프트웨어를 종료한 후 원격으로 다시 액세스를 시도하십시오. 예를 들어 다음과 같이 Windows Server 2016의 방화벽을 종료할 수 있습니다.
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. 운영 체제의 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;">을(를) 클릭하고 **제어판**을 선택합니다.
3. 제어판 창에서 **Windows 방화벽**을 클릭합니다.
4. Windows 방화벽 창에서 왼쪽에 있는 **Windows 방화벽 활성화 또는 비활성화**를 클릭하여 ‘사용자 정의 설정’을 엽니다.
5. **개인 네트워크 설정** 및 **공용 네트워크 설정**을 **Windows 방화벽 비활성화**로 설정하고 **확인**을 클릭합니다.
6. 인스턴스를 재시작하고 원격으로 다시 액세스를 시도하십시오.


### 원격 데스크톱을 통한 액세스 중 인증 오류[](id:AuthenticationError)

**장애 현상**: 원격 데스크톱을 통해 Windows 인스턴스에 로그인하려고 하면 ‘인증 오류입니다. 함수에 잘못된 플래그가 제공되었습니다.’라는 메시지가 표시됩니다. 또는 ‘인증 오류입니다. 필요한 기능이 지원되지 않습니다.’가 나타납니다.
**문제 원인**: Microsoft는 2018년 3월에 보안 업데이트를 출시했습니다. 이 업데이트는 자격 증명 보안 지원 프로그램(CredSSP)이 인증 프로세스 중 요청의 유효성을 검사하는 방식을 수정하여 CredSSP의 원격 코드 실행 취약점을 수정합니다. 클라이언트와 서버를 모두 업데이트해야 하며 그렇지 않으면 이전 오류가 발생할 수 있습니다.
**처리 순서**: 보안 업데이트를 설치합니다(권장). 자세한 내용은 [Windows 인스턴스: 신분 인증 오류가 발생할 경우](https://intl.cloud.tencent.com/document/product/213/32421)를 참고하십시오.

## 기타 솔루션
상기 방법을 시도한 후에도 여전히 Window 인스턴스에 로그인할 수 없으면 자가 진단 결과를 저장하고, 지원을 위해 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 피드백을 보내주십시오.
