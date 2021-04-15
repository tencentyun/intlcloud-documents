본 문서는 Linux 인스턴스에 연결할 수 없을 때의 문제 해결 및 Linux 인스턴스에 연결되지 않는 주요 원인을 소개하여 문제 진단 및 해결 방법에 대해 소개합니다.

## 가능한 원인
Linux 인스턴스에 로그인할 수 없는 주요 원인엔 아래 경우가 포함합니다.
- [SSH 문제로 인해 로그인할 수 없을 경우](#UseSSHLogin)
- [비밀번호 문제로 인해 로그인할 수 없을 경우](#CryptographicProblem)
- [대역폭 이용률이 너무 높을 경우](#BandwidthUtilization)
- [서버 고부하](#HighServerLoad)
- [보안 그룹 규칙이 적합하지 않을 경우](#SafetyGroupRule)

자가 진단 툴로 문제를 진단할 수 없다면 CVM에 [VNC 방식을 통해 로그인](#VNC)하여 장애를 진단하시길 권장합니다.

## 장애 처리
### VNC 방식을 통한 로그인
<span id="VNC"></span>
표준 방식(Webshell) 또는 원격 로그인 프로그램을 통해 Linux 인스턴스에 로그인할 수 없을 경우,  Tencent Cloud VNC 로그인 방식을 통해 로그인할 수 있으며 이를 통해 장애 원인을 진단할 수 있습니다.
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 로그인이 필요한 인스턴스를 선택하고 [로그인]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. 팝업된 “Linux 인스턴스 로그인” 창에서 [Alternative login methods(VNC)]]을 선택하고 [Log In Now]을 클릭합니다.
> 로그인 과정에서 비밀번호를 잊었을 경우, 콘솔에서 해당 인스턴스의 비밀번호를 재설정할 수 있습니다. 자세한 내용은 [인스턴스 비밀번호 리셋](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
>
4. 팝업된 창에서 사용자 이름과 비밀번호를 입력하면 바로 로그인할 수 있습니다.

<span id="UseSSHLogin"></span>
### SSH 문제로 인해 로그인할 수 없을 경우
**장애 현상**: [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)할 때, 연결할 수 없거나 연결 실패 알림이 뜨는 경우
**처리 순서**: [SSH 방식으로 Linux 인스턴스에 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32486)을 참조하여 문제를 해결합니다.

<span id="CryptographicProblem"></span>
### 비밀번호 문제로 인해 로그인할 수 없을 경우
**장애 현상**: 비밀번호를 잊었거나, 잘못된 비밀번호 입력 또는 비밀번호 재설정에 실패할 경우 로그인에 실패합니다.
**해결 방법**: [Tencent Cloud 콘솔](https://console.cloud.tencent.com/cvm/index)에서 인스턴스의 비밀번호를 재설정하고 인스턴스를 재시작하세요.
**처리 순서**: 인스턴스 비밀번호 재설정 방법은 [인스턴스 비밀번호 리셋](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.

<span id="BandwidthUtilization"></span>
### 대역폭 이용률이 너무 높을 경우
**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 대역폭 이용률이 너무 높은 것이 원인인 경우.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [높은 대역폭 점유율로 인해 로그인 불가](https://intl.cloud.tencent.com/document/product/213/32542)를 참조하여 인스턴스의 대역폭 사용 상황을 조회한 후 장애를 처리합니다.

<span id="HighServerLoad"></span>
### 서버 고부하
**장애 현상**: 자가 진단 툴 또는 클라우드 모니터링을 통해 확인한 결과, 서버 CPU의 고부하로 인해 시스템 원격 연결이 불가하거나 액세스 시 심한 렉이 발생하고 있는 경우.
**가능한 원인**: 트로이 목마 바이러스 감염, 3rd party 백신 소프트웨어및 애플리케이션 오류, 드라이버 오류 또는 소프트웨어 백그라운드의 자동 업데이트로 인해 CPU 사용량이 높아져 CVM에 로그인할 수 없거나 액세스 속도가 느려질 수 있습니다.
**처리 순서**:
1. [VNC 로그인](#VNC)을 통해 인스턴스에 로그인합니다.
2. [Linux 인스턴스: CPU 및 메모리의 높은 점유율로 인해 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32387)을 참조하여 "작업 관리자"에서 고부하 프로세스를 진단합니다.


<span id="SafetyGroupRule"></span>
### 보안 그룹 규칙이 적합하지 않을 경우
**장애 현상**: 자가 진단 툴을 통해 진단한 결과, 보안 그룹 규칙 설정이 적합하지 않아 로그인하지 못하는 경우.
**처리 순서**: [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 진단합니다.
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
보안 그룹 포트 설정에서 문제가 확인될 경우, 툴의 [Open all ports] 기능을 통해 포트를 개방할 수 있습니다.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
보안 그룹 규칙의 사용자 정의 설정이 필요한 경우, [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조하여 새로운 보안 그룹 규칙을 재설정하세요.



## 기타 솔루션
위에 서술된 방법으로도 Linux 인스턴스 연결이 되지 않을 경우, 자가 진단 결과를 저장한 후 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 피드백 바랍니다.
