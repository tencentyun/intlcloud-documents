## 적용 시나리오
Windows에서 Window 인스턴스에 원격 연결 시, 다음 그림과 같은 알림이 표시됩니다.
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

다음 중 하나의 이유로 원격 데스크탑이 원격 컴퓨터에 연결할 수 없습니다.
1) 서버에 대한 원격 액세스가 활성화되지 않은 경우
2) 원격 컴퓨터가 꺼진 상태인 경우
3) 네트워크에서 원격 컴퓨터를 사용할 수 없는 경우

원격 컴퓨터가 전원 상태, 네트워크에 연결 여부 및 원격 액세스가 활성화 여부를 확인합니다.


## 예상 원인

위와 같은 알림이 표시되는 원인은 다음 내용이 포함됩니다(다음 상황에 국한되지 말고 실제 상황을 근거로 분석하세요).
- 인스턴스가 비정상적인 구동 상태에 있을 경우
- 공인 IP가 없거나 공용 네트워크 대역폭이 0일 경우
- 인스턴스를 바인딩한 보안 그룹이 원격 로그인 포트(기본 값 3389)를 개방하지 않았을 경우
- 원격 데스크탑 서비스를 실행하지 않았을 경우
- 원격 데스크탑 설정 문제
- Windows 방화벽 설정 문제

## 문제 해결 순서

### 인스턴스가 구동 상태인지 점검
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. "CVM" 페이지의 인스턴스 리스트에서 인스턴스가 [구동 중]인지 조회합니다. 아래 그림 참조
![CVM 리스트 페이지](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - 구동 중인 경우, [서버의 공인 IP 설정 여부를 점검](#step01)하세요.
 - 구동 중이 아닌 경우, 해당 Windows 인스턴스를 운행하세요.

<span id="step01"></span>
### 서버의 공인 IP 설정 여부 점검
CVM 콘솔에서 서버의 공인 IP 설정 여부를 점검합니다. 아래 그림 참조
![공인 IP 없음](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)
 - 설정한 경우, [공용 네트워크 대역폭의 구매 여부 점검](#step02)하세요.
 - 설정하지 않은 경우, [EIP를 신청하고 바인딩](https://intl.cloud.tencent.com/document/product/213/16586)하세요.
 
<span id="step02"></span>
###  공용 네트워크 대역폭의 구매 여부 점검
공용 네트워크 대역폭이 0Mb(최소 1Mbps)인지 점검합니다.
 - 0Mb인 겨우, [네트워크 조정](https://intl.cloud.tencent.com/document/product/213/15517)을 통해 대역폭을 1Mbps 또는 이상으로 조정하세요.
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - 0Mb이 아닌 경우, [인스턴스 원격 로그인 포트(3389)의 개방 여부를 점검](#step03)하세요.

<span id="step03"></span>
### 인스턴스 원격 로그인 포트(3389)의 개방 여부 점검
1. 콘솔에서 로그인이 필요한 인스턴스를 클릭하고 인스턴스 정보 페이지에 진입합니다.
2. "Security Group" 탭에서 인스턴스의 보안 그룹이 원격 로그인 포트(기본 원격 데스크탑 포트:3389)를 개방했는지 점검합니다. 아래 그림 참조
![보안 그룹](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - 개방한 경우, [Windows 인스턴스의 시스템 설정을 점검](#step04)하세요.
 - 개방하지 않은 경우, 대응하는 보안 그룹 규칙을 편집하여 개방하세요. 조작 방법은 [보안 그룹 조작 가이드](https://intl.cloud.tencent.com/document/product/213/18197)를 참조 바랍니다.

<span id="step04"></span>
### Windows 인스턴스의 시스템 설정 점검
1. VNC 로그인 인스턴스를 사용하여 Windows 인스턴스의 시스템 설정을 진단합니다.
>? VNC 로그인의 자세한 내용은 [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435) 중 "VNC로 로그인"을 참조 바랍니다.
2. 로그인한 인스턴스 시스템에서 [시작]을 클릭하고 [구동]에 **services.msc**를 입력한 다음 **Enter**를 눌러 “서비스” 창을 엽니다.
3. 더블 클릭으로 “Remote Desktop Services”의 속성을 열고 원격 데스크탑 서비스가 구동 중인지 점검합니다. 아래 그림 참조
![Remote Desktop Service](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - 구동 중인 경우, [4단계](#step04_4)를 실행하세요.
 - 구동 중이 아닌 경우, "구동 유형"을 "자동"으로 설정하고 "서비스 상태"를 "정상 구동"으로 설정(즉, [구동]을 클릭하여 서비스 시작)하세요.
4. <span id="step04_4">[시작]을 클릭하고 [구동]에서 **sysdm.cpl**을 입력하고 **Enter**를 눌러 “시스템 속성” 창을 엽니다.</span>
5. "원격" 탭에서 원격 데스크탑이 "이 컴퓨터(L)로 원격 연결 허용"으로 설정했는지 점검합니다. 아래 그림 참조
![원격 설정](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - 설정한 경우, [6단계](#step04_6)를 실행하세요.
 - 설정하지 않은 경우, 원격 데스크탑을 "이 컴퓨터(L)로 원격 연결 허용"으로 설정하세요.
6. <span id="step04_6">[시작]을 클릭하고 [제어판]을 선택하여 제어판을 엽니다.</span>
7. "제어판"에서 [시스템과 보안]>[Windows 방화벽]을 선택하여 "Windows 방화벽"을 엽니다.
8. "Windows 방화벽"에서 Windows 방화벽 상태를 점검합니다. 아래 그림 참조
![Windows 방화벽 상태](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - 상태 "활성화"를 위해 [9단계](#step04_9)를 실행하세요.
 - 상태 "비활성화"를 위해 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백 바랍니다.
9. <span id="step04_9">"Windows 방화벽"에서 [애플리케이션 허용 또는 Windows 방화벽 통과 가능]을 클릭하고 "허용된 애플리케이션" 창을 엽니다.</span>
10. "허용된 애플리케이션" 창에서 "허용된 애플리케이션과 기능(A)"에 "원격 데스크탑"을 체크했는지 점검합니다. 아래 그림 참조
![원격 데스크탑 체크](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - 체크한 경우, [11단계](#step04_11)를 실행하세요.
 - 체크하지 않은 경우, "원격 데스크탑"을 체크하여 "원격 데스크탑"을 개방하세요.
11. <span id="step04_11">"Windows 방화벽"에서 [Windows 방화벽 활성화 또는 비활성화]를 클릭하고 "사용자 정의 설정" 창을 엽니다.</span>
12. "사용자 정의 설정" 창에서 "전용 네트워크 설정"과 "공용 네트워크 설정"을 "Windwos 방화벽 비활성화(권장하지 않음)"로 설정합니다. 아래 그림 참조
![비활성화](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

상기 작업을 실행한 후에도 원격 데스크탑을 통해 Windows 인스턴스에 연결할 수 없다면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백 바랍니다.


