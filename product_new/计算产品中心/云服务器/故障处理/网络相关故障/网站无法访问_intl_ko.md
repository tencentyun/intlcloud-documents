본 문서는 웹 사이트가 액세스하지 못하는 문제에 대해 점검 방법과 문제 위치 확인 방법을 설명합니다.

## 예상 원인

웹 사이트 문제, 방화벽 설치, 서버 과부하 등 원인이 웹 사이트에 액세스하지 못하게 합니다.

## 장애 처리
<span id="TroubleshootServer"></span>
### 서버 관련 문제 점검
서버 종료, 하드웨어 고장, CPU/메모리/대역폭 사용률이 너무 높으면 웹 사이트에 액세스하지 못할 수 있으므로 서버의 작동 상태, CPU/메모리/대역폭 사용을 차례로 조사하는 것을 권장합니다.

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 인스턴스 관리 페이지에서 인스턴스의 정상 실행 여부를 확인하십시오. 아래 이미지를 참조하십시오.
 - 해당되는 경우 [2단계](#Server_step02)를 실행하십시오.
 - 해당되지 않는 경우 CVM 인스턴스를 재시작하십시오.
2. <span id="Server_step02">인스턴스의 ID/인스턴스 이름을 클릭해 인스턴스 상세 페이지로 진입하십시오.</span>
3. [모니터링]탭을 선택하여 CPU/메모리/대역폭 사용 현황을 조회하십시오. 아래 이미지를 참조하십시오.
 - CPU/메모리가 사용량이 너무 많은 경우 [Windows 인스턴스: CPU와 메모리의 높은 점유율로 인한 로그인 불가](https://cloud.tencent.com/document/product/213/10233)와 [Linux 인스턴스: CPU와 메모리의 높은 점유율로 인한 검색 불가](https://cloud.tencent.com/document/product/213/10310)를 참조하십시오.
 - 대역폭이 사용량이 너무 많은 경우 [대역폭의 높은 점유율로 인한 로그인 불가](https://cloud.tencent.com/document/product/213/10334)를 참조하십시오.
 - CPU/메모리/대역폭 사용 현황이 정상이라면 [4단계](#Server_step04)를 수행하십시오.
4. <span id="Server_step04">다음 명령어를 실행하여 웹서비스에 대응하는 포트가 제대로 모니터링되는지 점검합니다.</span>
> 다음 작업은 HTTP 서버에 자주 사용하는 80 포트를 예시로 합니다.
>
 - Linux 인스턴스: `netstat -ntulp |grep 80` 명령어를 실행하십시오. 아래 이미지를 참조하십시오.
 ![](https://mc.qcloudimg.com/static/img/ab5fa663197c3fa0738b2ceb3f559fd3/image.png)
 - Windows 인스턴스: CLI Tool을 열어 `netstat -ano|findstr :80` 명령어를 실행하십시오. 아래 이미지를 참조하십시오.
 ![](https://mc.qcloudimg.com/static/img/c9c32a2e9f12235ad3d2a5aca313f298/image.png)
 - 포트가 정상적으로 모니터링될 경우 [5단계](#Server_step05)를 실행하십시오.
 - 포트가 정상적으로 모니터링되지 않을 경우 웹서비스 프로세스가 시작하거나 제대로 설정되었는지 점검하십시오.
5. <span id="Server_step05">방화벽 설치를 점검하여 웹서비스 프로세스가 대응하는 포트를 내보내는지 확인하십시오.</span>
 - Linux 인스턴스: `iptables -vnL` 명령어를 실행하여 iptables가 80 포트를 열 수 있는지 조회하십시오.
    - 80 포트가 이미 열려있는 경우 [네트워크 관련 문제 점검](#TroubleshootNetwork) 하십시오.
    - 80 포트가 열리지 않은 경우 `iptables -I INPUT 5 -p tcp  --dport 80 -j ACCEPT` 명령어를 실행하여 80 포트를 여십시오.
 - Windows 인스턴스: 운영 체제 인터페이스에서 [시작]>[제어판]>[방화벽 설치]를 클릭하여 Windows 방화벽이 해제되어 있는지 조회하십시오.
		- 해제 상태인 경우 [네트워크 관련 문제 점검](#TroubleshootNetwork) 하십시오.
		- 미해제 상태인 경우 방화벽 상태를 해제하십시오.

<span id="TroubleshootNetwork"></span>
### 네트워크 관련 문제 점검
네트워크 관련 문제가 웹사이트를 액세스하지 못하게 할 수도 있으므로, 다음 명령어를 실행하여 네트워크가 패킷을 손실하거나 딜레이된 경우가 없는지 점검하십시오.
```
ping 타깃 서버의 공인 IP
```
- 다음과 유사한 결과로 리턴하면 패킷이 손실되거나 딜레이가 있는 경우가 있음을 나타내므로 MTR을 사용하여 추가적인 점검을 수행하십시오. 자세한 내용은 [CVM 네트워크 딜레이와 패킷 손실](https://intl.cloud.tencent.com/document/product/213/14638)을 참조하십시오.
![](https://mc.qcloudimg.com/static/img/30d9946522f43cfc1c6731b9035ae9e9/image.png)
- 패킷이 손실되거나 딜레이된 경우가 없을 때, [보안 그룹 설치 관련 문제 점검](#TroubleshootSecurityGroup)을 진행하십시오.

<span id="TroubleshootSecurityGroup"></span>
### 보안 그룹 설정 관련 문제 점검
보안 그룹은 가상 방화벽으로, 연결된 인스턴스의 인바운드 트래픽과 아웃바운드 트래픽을 제어할 수 있습니다. 보안 그룹의 규칙은 프로토콜, 포트, 정책 등을 지정할 수 있습니다. Web 프로세스와 관련된 포트를 열지 않은 경우에도 웹 사이트에 액세스하지 못하게 할 수 있습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오. "인스턴스 리스트" 페이지에서 인스턴스의 ID/인스턴스 이름을 클릭하여 인스턴스 상세 페이지로 진입하십시오.
2. [보안 그룹] 탭을 선택하여 바인딩된 보안 그룹 및 대응 보안 그룹의 아웃바운드와 인바운드 규칙을 조회하고 Web 프로세스와 관련된 포트가 열려 있는지 확인하십시오. 아래 이미지를 참조하십시오.
 - 포트가 열린 경우 [도메인, ICP비안 및 분석 관련 문제 점검](#TroubleshootDomainFilingOrAnalysis)하십시오.
 - 포트가 닫힌 경우 보안 그룹 설치를 수정하여 Web 프로세스와 관련된 포트를 여십시오.

<span id="TroubleshootDomainFilingOrAnalysis"></span>
### 도메인, ICP비안과 분석 관련 문제 점검
[서버 관련 문제](#TroubleshootServer), [네트워크 관련 문제](#TroubleshootNetwork) 및 [보안 그룹 설치 관련 문제](#TroubleshootSer)를 조회한 뒤, CVM의 공인 IP 주소를 사용하여 액세스를 시도할 수 있습니다. IP 주소를 사용하여 액세스가 가능하지만 도메인 액세스에 실패하면 도메인 ICP비안 또는 분석 관련 문제로 인해 웹 사이트에 액세스하지 못한 것일 수 있습니다.

1. 국가 공업정보부는 허가를 받지 않았거나 ICP비안 절차를 밟지 않은 네트워크에 대해 인터넷 정보 서비스를 제공할 경우 위법 행위로 간주합니다. 네트워크의 정상적인 실행을 위해 먼저 ICP비안을 실행하고 네트워크를 구축하는 것을 권장합니다. ICP비안을 성공적으로 실행한 후 통신관리국에서 전달한 ICP비안 번호를 획득해야 액세스를 활성화할 수 있습니다.
 - 도메인에 ICP비안이 없을 경우 [도메인 ICP비안](https://console.cloud.tencent.com/beian)을 실행하십시오.
 - Tencent Cloud의 도메인 서비스를 사용할 경우 [도메인 관리 콘솔](https://console.cloud.tencent.com/domain)에 로그인하여 해당하는 도메인 이름 상황을 조회할 수 있습니다.
 - 도메인이 이미 ICP비안에 등록된 경우 [2단계](#Analysis_step02)를 실행하십시오.
2. <span id="Analysis_step02">[분석 효과 관련](https://cloud.tencent.com/document/product/302/30597)을 참조하여 분석 관련 문제를 점검하십시오.</span>
 - 웹 사이트 액세스 문제를 해결한 경우 작업을 완료합니다.
 - 여전히 웹 사이트 액세스 문제를 해결할 수 없을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=497&radio_title=%E7%BD%91%E7%AB%99%E6%97%A0%E6%B3%95%E8%AE%BF%E9%97%AE&queue=15&scene_code=14550&step=2)을 통해 피드백하십시오.


