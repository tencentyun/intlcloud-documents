
본 문서에서는 Linux 인스턴스 로그인 실패의 가능한 원인과 문제 해결 방법에 대해 설명합니다. 지침에 따라 문제의 원인을 식별하고 해결 방법을 배울 수 있습니다.


## 문제 파악
### 자가 진단 툴 사용
Tencent Cloud는 대역폭, 방화벽 및 보안 그룹 설정 등의 문제로 인한 것인지 판단할 수 있는 자가 진단 툴을 제공합니다. 70%의 장애는 툴에 의해 위치가 측정되며, 점검된 원인에 따라 로그인 실패를 일으키는 장애 문제의 위치를 측정할 수 있습니다.
1. [자가 진단](https://console.cloud.tencent.com/workorder/check)을 클릭하여 자가 진단 툴을 엽니다.
2. 메시지가 표시되면 타깃 CVM 인스턴스를 선택하고 **점검 시작**을 클릭합니다.


### TAT(TencentCloud Automation Tools)를 사용하여 명령 전송
TAT를 사용하여 문제 해결 및 문제 찾기를 위해 인스턴스에 명령을 보낼 수 있습니다. 순서는 다음과 같습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인 한 후 인스턴스 리스트에서 타깃 인스턴스 ID를 클릭합니다.
2. 인스턴스 세부 정보 페이지에서 **명령 실행** 탭을 선택하고 **명령 실행**을 클릭합니다.
3. ‘실행 명령’ 팝업 창에서 필요에 따라 명령을 선택합니다. **명령 실행**을 클릭하고 결과를 확인합니다.
예를 들어 'df -TH'를 입력하고 **명령 실행**을 클릭하면 로그인하지 않고도 인스턴스의 결과를 볼 수 있습니다.
자세한 내용은 [Tencent Cloud Automation Tools](https://intl.cloud.tencent.com/document/product/1147)를 참고하십시오.


<dx-alert infotype="explain" title="">
자가 진단 툴로 문제를 진단할 수 없다면 CVM에 [VNC 방식을 통해 로그인](#VNC)하여 장애를 진단하시길 권장합니다.
</dx-alert>




## 가능한 원인
Linux 인스턴스 로그인 실패의 주요 원인은 다음과 같습니다.
- [SSH 키 문제](#UseSSHLogin)
- [비밀번호 문제](#CryptographicProblem)
- [높은 대역폭 이용률](#BandwidthUtilization)
- [서버 고부하](#HighServerLoad)
- [부적절한 보안 그룹 규칙](#SafetyGroupRule)

## 장애 처리
### VNC 방식을 통해 로그인[](id:VNC)

표준 방법(Orcaterm) 또는 원격 로그인 소프트웨어를 사용하여 Linux 인스턴스에 로그인할 수 없는 경우 Tencent Cloud VNC를 사용하여 로그인하고 문제 원인을 찾을 수 있습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스 관리 페이지에서 아래 이미지와 같이 액세스하려는 인스턴스를 찾고 **로그인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. ‘표준 로그인 | Linux 인스턴스’ 팝업 창에서 **VNC 로그인**을 선택합니다.
<dx-alert infotype="explain" title="">
 인스턴스의 비밀번호를 잊어버린 경우 콘솔에서 재설정할 수 있습니다. 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.
</dx-alert>
4. 사용자 이름과 비밀번호를 입력하여 로그인 프로세스를 완료합니다.


### SSH 키 문제[](id:UseSSHLogin)
**장애 현상**: [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)하는 동안 연결을 사용할 수 없거나 실패했음을 나타내는 메시지가 나타납니다.
**처리 순서**: [SSH 방식으로 Linux 인스턴스에 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32486)를 참고하여 문제를 해결합니다.


### 비밀번호 문제[](id:CryptographicProblem)
**장애 현상**: 비밀번호를 잊었거나, 잘못된 비밀번호 입력 또는 비밀번호 재설정에 실패해 로그인할 수 없는 경우입니다.
**솔루션**: [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에서 인스턴스의 비밀번호를 재설정하고 인스턴스를 재시작합니다.
**처리 순서**: 자세한 절차는 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.


### 높은 대역폭 이용률[](id:BandwidthUtilization)
**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 대역폭 이용률이 너무 높은 것이 원인인 경우입니다.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [높은 대역폭 점유율로 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32542)를 참고하여 인스턴스의 대역폭 사용률을 확인하고 그에 따라 문제 해결을 수행합니다.


### 서버 고부하[](id:HighServerLoad)
**장애 현상**: 자가 진단 툴 또는 Tencent Cloud Observability Platform에 서버 CPU 워크로드가 너무 높고 시스템이 원격 연결을 수행할 수 없거나 액세스가 느린 것으로 표시됩니다.
**예상 원인**: 바이러스, 트로이 목마, 3rd party 바이러스 백신 소프트웨어, 응용 프로그램 예외, 드라이버 예외 및 백엔드의 소프트웨어 자동 업데이트로 인해 CPU 이용률이 높아져 CVM 로그인 실패 또는 액세스 속도 저하가 발생할 수 있습니다.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [Linux 인스턴스: CPU 혹은 메모리 점유율이 높아 로그인 할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32387)를 참고하여 ‘작업 관리자’에서 부하가 높은 프로세스를 찾습니다.


### 부적절한 보안 그룹 규칙[](id:SafetyGroupRule)
**장애 현상**: 자가 진단 툴은 보안 그룹 규칙 구성이 부적절하여 로그인 실패로 이어짐을 보여줍니다.
**처리 순서**: [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 문제를 해결하십시오.
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
보안 그룹의 포트 문제로 인해 문제가 발생한 경우 **모든 포트 열기** 기능을 사용하여 모든 포트를 열 수 있습니다.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
보안 그룹에 대한 사용자 정의 규칙을 정의하려면 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고십시오.



## 기타 솔루션
앞의 문제 해결 방법을 사용하여도 여전히 Linux 인스턴스에 로그인할 수 없으면 자가 진단 결과를 저장하고 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 지원을 받으십시오.
