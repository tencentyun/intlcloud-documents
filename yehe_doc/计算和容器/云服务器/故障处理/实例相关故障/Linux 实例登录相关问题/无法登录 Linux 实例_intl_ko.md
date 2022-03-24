본 문서는 Linux 인스턴스에 연결할 수 없을 때의 문제 해결 및 Linux 인스턴스에 연결되지 않는 주요 원인을 소개하여 문제 진단 및 해결 방법에 대해 소개합니다.


## 문제 추적
### 자가 진단 툴 사용
Tencent Cloud는 대역폭, 방화벽 및 보안 그룹 설정 등의 문제로 인한 것인지 판단할 수 있는 자가 진단 툴을 제공합니다. 70%의 장애는 툴에 의해 위치가 측정되며, 점검된 원인에 따라 로그인 실패를 일으키는 장애 문제의 위치를 측정할 수 있습니다.
1. [자가 진단](https://console.intl.cloud.tencent.com/workorder/check)을 클릭하여 자가 진단 툴을 엽니다.
2. 아래 이미지와 같이 툴 인터페이스 안내에 따라 진단할 CVM를 선택하고 **점검 시작**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/1956fb3b3a0f0d93da0edf1fed51f2f7.png)


## 예상 원인
Linux 인스턴스에 로그인할 수 없는 주요 원인엔 아래 경우가 포함합니다.
- [SSH 문제로 인해 로그인할 수 없을 경우](#UseSSHLogin)
- [비밀번호 문제로 로그인할 수 없을 경우](#CryptographicProblem)
- [대역폭 이용률이 지나치게 높을 경우](#BandwidthUtilization)
- [서버 고부하](#HighServerLoad)
- [보안 그룹 규칙이 적합하지 않을 경우](#SafetyGroupRule)

## 장애 처리
### VNC 방식을 통해 로그인[](id:VNC)

표준 방식(Webshell) 또는 원격 로그인 프로그램을 통해 Linux 인스턴스에 로그인할 수 없을 경우,  Tencent Cloud VNC 로그인 방식을 통해 로그인할 수 있으며 이를 통해 장애 원인을 진단할 수 있습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이 인스턴스의 관리 페이지에서 로그인하려는 인스턴스를 선택하고 **로그인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. ‘표준 로그인 | Linux 인스턴스’ 팝업 창에서 **VNC 로그인**을 선택합니다.
<dx-alert infotype="explain" title="">
 로그인 과정에서 비밀번호를 잊은 경우, 콘솔에서 해당 인스턴스의 비밀번호를 재설정할 수 있습니다. 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하시기 바랍니다.
</dx-alert>
4. 사용자 이름과 비밀번호를 입력하여 로그인합니다.


### SSH 문제로 인해 로그인할 수 없을 경우[](id:UseSSHLogin)
**장애 현상**: [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)할 때, 연결할 수 없거나 연결 실패 알림이 발생합니다.
**처리 단계**: [SSH 방식으로 Linux 인스턴스에 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32486)을 참고하여 문제를 해결합니다.

<span id="CryptographicProblem"></span>
### 비밀번호 문제로 로그인할 수 없을 경우
**장애 현상**: 비밀번호를 잊었거나, 잘못된 비밀번호 입력 또는 비밀번호 재설정에 실패해 로그인할 수 없는 경우입니다.
**해결 방법**: [Tencent Cloud 콘솔](https://console.cloud.tencent.com/cvm/index)에서 인스턴스의 비밀번호를 재설정하고 인스턴스를 재시작합니다.
**처리 순서**: 인스턴스 비밀번호 재설정 방법은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고 하시기 바랍니다.


### 대역폭 이용률이 지나치게 높을 경우[](id:BandwidthUtilization)
**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 대역폭 이용률이 너무 높은 것이 원인인 경우입니다.
**해결 절차**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [높은 대역폭 이용률로 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32542)를 참고하여 인스턴스의 대역폭 소모 현황과 장애 처리 방법을 조회할 수 있습니다.


### 서버 고부하[](id:HighServerLoad)
**장애 현상**: 자가 진단 툴 또는 클라우드 모니터링을 통해 확인한 결과, 서버 CPU의 고부하로 인해 시스템 원격 연결이 불가하거나 액세스 시 심한 랙이 발생하고 있는 경우입니다.
**예상 원인**: 트로이 목마 바이러스 감염, 3rd party 백신 소프트웨어 및 애플리케이션 오류, 드라이버 오류 또는 소프트웨어 백그라운드의 자동 업데이트로 인해 CPU 이용률이 높아져 CVM에 로그인할 수 없거나 액세스 속도가 느려질 수 있습니다.
**해결 절차**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [Linux 인스턴스: CPU 및 메모리의 높은 점유율로 인해 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32387)을 참고하여 ‘작업 관리자’에서 고부하 프로세스를 진단합니다.


### 보안 그룹 규칙이 적합하지 않을 경우[](id:SafetyGroupRule)
**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 보안 그룹 규칙 설정이 적합하지 않아 로그인하지 못하는 경우입니다.
**처리 순서**: [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 진단합니다.
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
보안 그룹 포트 설정 문제로 확인될 경우, 툴의 **원클릭 오픈**를 통해 포트를 개방할 수 있습니다.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
보안 그룹 규칙의 사용자 정의 설정이 필요한 경우, [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하여 새로운 보안 그룹 규칙을 재설정합니다.



## 기타 솔루션
위에 서술된 방법으로도 Linux 인스턴스 연결이 되지 않을 경우, 자가 진단 결과를 저장한 후 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category
)을 통해 문의해주시기 바랍니다.
