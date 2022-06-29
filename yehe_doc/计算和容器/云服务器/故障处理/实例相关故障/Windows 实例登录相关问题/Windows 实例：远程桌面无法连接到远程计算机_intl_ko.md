## 현상 설명
Windows에서 Windows 인스턴스에 원격으로 연결하려고 하면 다음 이미지와 같은 메시지가 표시됩니다.
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

다음 이유 중 하나로 인해 원격 데스크톱을 사용하여 원격 컴퓨터에 연결할 수 없습니다.
1) 서버에 대한 원격 액세스가 활성화되어 있지 않습니다.
2) 원격 컴퓨터가 꺼져 있습니다.
3) 네트워크에서 원격 컴퓨터를 사용할 수 없습니다.

원격 컴퓨터가 켜져 있고 네트워크에 연결되어 있고 원격 액세스가 활성화되어 있는지 확인하십시오.


## 가능한 원인

이 문제의 가능한 원인에는 다음이 포함되지만 이에 국한되지는 않습니다. 실제 상황에 따라 문제를 해결하십시오.
- 인스턴스가 비정상 상태입니다.
- CVM에 공용 IP 주소가 없거나 공중망 대역폭이 0입니다.
- 인스턴스와 바인딩된 보안 그룹에서 원격 로그인 포트(기본적으로 포트 3389)가 인터넷에 개방되어 있지 않습니다.
- 원격 데스크톱 서비스가 시작되지 않았습니다.
- 원격 데스크톱 설정이 올바르지 않습니다.
- Windows 방화벽 설정이 올바르지 않습니다.

## 문제 해결 단계


### 인스턴스가 실행 중인지 확인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스 관리 페이지에서 다음 이미지와 같이 인스턴스가 ‘실행 중’인지 확인합니다.
![CVM 리스트 페이지](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - Yes, [CVM에 공용 IP 주소가 있는지 확인](#step01)하십시오.
 - No, Windows 인스턴스를 시작합니다.


### CVM에 공용 IP 주소가 있는지 확인[](id:step01)
다음 이미지와 같이 CVM 콘솔에서 CVM에 공용 IP 주소가 있는지 확인합니다.
![공용 IP 없음](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)

 - Yes, [공중망 대역폭을 구입했는지 확인](#step02)하십시오.
 - No, [EIP 신청 및 바인딩](https://intl.cloud.tencent.com/document/product/213/16586)합니다.


###  공중망 대역폭 구입 여부 확인[](id:step02)
공중망 대역폭이 0Mbps인지 확인합니다. 최소 1Mbps의 공중망 대역폭을 확보해야 합니다.
 - Yes, [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)을 참고하여 대역폭을 5Mbps 이상으로 늘리십시오.
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - No, [인스턴스의 원격 로그인 포트(3389)가 인터넷에 개방되었는지 확인](#step03)합니다.


### 인스턴스의 원격 로그인 포트(3389)가 인터넷에 개방되었는지 확인[](id:step03)
1. CVM 콘솔의 인스턴스 관리 페이지에서 로그인할 인스턴스의 ID 또는 이름을 클릭하여 인스턴스 세부 정보 페이지로 이동합니다.
2. **보안 그룹** 탭 페이지에서 다음 이미지와 같이 인스턴스와 바인딩된 보안 그룹의 인터넷에 원격 로그인 포트(기본적으로 포트 3389)가 개방되어 있는지 확인합니다.
![보안 그룹](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - Yes, [원격 데스크톱 서비스를 확인](#step04)하십시오.
 - No, 해당 보안 그룹 규칙을 편집하여 인터넷에 포트를 개방합니다. [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.

### 원격 데스크톱 서비스 확인[](id:step04)
1. [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)하고 Windows 인스턴스용 원격 데스크톱 서비스가 활성화되어 있는지 확인합니다.
<dx-alert infotype="explain" title="">
 다음 작업은 Windows Server 2016을 예로 들어 설명합니다.
</dx-alert>
2. <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">를 우클릭하고 팝업 메뉴에서 **시스템**을 선택합니다.
3. ‘시스템’ 팝업 창에서 **고급 시스템 설정**을 선택합니다.
4. ‘시스템 속성’ 팝업 창에서 **원격** 탭을 선택하고 ‘이 컴퓨터에 대한 원격 연결 허용’이 선택되었는지 확인합니다.
 - Yes, [5단계](#step04_5)를 실행합니다.
 - No, 선택하고 **확인**을 클릭합니다.
5. [](id:step04_5) <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">을(를) 우클릭하고 팝업 메뉴에서 **컴퓨터 관리**를 선택합니다.
6. ‘컴퓨터 관리’ 창의 왼쪽 사이드바에서 **서비스 및 애플리케이션** > **서비스**를 선택합니다.
7. 오른쪽의 서비스 목록에서 **Remote Desktop Services**가 시작되었는지 확인합니다.
 - Yes, [8단계](#step04_8)를 실행합니다.
 - No, 서비스를 시작합니다.
8. [](id:step04_8) <img src="https://main.qcloudimg.com/raw/6191c3ad8f212e7f8f6dddbbabd43f12.png" style="margin: -5px 0px;">를 우클릭하고 팝업 메뉴에서 **실행**을 선택합니다.
9. ‘실행’ 팝업 창에서 **msconfig**를 입력하고 **확인**을 클릭합니다.
10. ‘시스템 구성’ 팝업 창에서 **정상 시작**이 선택되어 있는지 확인합니다.
 - Yes, [Windows 인스턴스의 시스템 설정 확인](#step05)하십시오.
 - No, 선택하고 **확인**을 클릭합니다.


### Windows 인스턴스의 시스템 설정 확인[](id:step05)
1. [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)하고 인스턴스의 시스템 설정을 확인합니다.
<dx-alert infotype="explain" title="">
다음 작업에서는 Windows Server 2012의 인스턴스를 예로 사용합니다.
</dx-alert>
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>을(를) 우클릭하고 팝업 메뉴에서 **실행**을 선택합니다.
3. ‘실행’ 팝업 창에서 **services.msc**를 입력하고 **Enter**를 눌러 ‘서비스’ 창을 엽니다.
4. ‘Remote Desktop Services’를 더블 클릭하여 열고 원격 데스크톱 서비스가 아래와 같이 실행되고 있는지 확인합니다.
![Remote Desktop Service](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - Yes, [5단계](#step05_5)를 실행합니다.
 - No, ‘시작 유형’을 ‘자동’으로, ‘서비스 상태’를 ‘실행 중’으로 설정합니다(즉, **시작** 클릭).
5. [](id:step05_5)<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>을(를) 우클릭하고 팝업 메뉴에서 **실행**을 선택합니다.
6. ‘실행’ 팝업 창에서 **sysdm.cpl**을 입력하고 **Enter** 키를 눌러 ‘시스템 속성’ 창을 엽니다.
7. ‘원격’ 탭에서 아래와 같이 원격 데스크톱이 ‘이 컴퓨터에 대한 원격 연결 허용(L)’으로 설정되어 있는지 확인합니다.
![원격 설정](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - Yes, [8단계](#step05_8)를 실행합니다.
 - No, 원격 데스크톱을 ‘이 컴퓨터에 대한 원격 연결 허용(L)’으로 설정합니다.
8. [](id:step05_8) <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px;"></img>을 클릭하고 팝업 메뉴에서 **제어판**을 선택합니다.
9. ‘제어판’에서 **시스템 및 보안** > **Windows Defender 방화벽**을 선택하여 ‘Windows Defender 방화벽’을 엽니다.
10. "Windows Defender 방화벽"에서 아래와 같이 Windows Defender 방화벽의 상태를 확인합니다.
![Windows Defender 방화벽 상태](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - 상태가 ‘On’인 경우 [11단계](#step05_11)로 진행합니다.
 - 상태가 ‘Off’인 경우 [온라인 지원](https://console.intl.cloud.tencent.com/workorder/category)을 통해 문의해주시기 바랍니다.
11. [](id:step05_11) ‘Windows Defender 방화벽’에서 **Windows 방화벽을 통해 앱 또는 기능 허용**을 클릭하여 ‘허용된 앱’ 창을 엽니다.
12. ‘허용된 앱’ 창에서 아래와 같이 ‘허용된 앱 및 기능’에서 ‘원격 데스크톱’이 선택되어 있는지 확인합니다.
![원격 데스크톱 선택](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - Yes, [13단계](#step05_13)를 실행합니다.
 - No, ‘원격 데스크톱’을 선택하여 Windows Defender 방화벽을 통한 ‘원격 데스크톱’을 허용합니다.
13. [](id:step05_13)’Windows Defender 방화벽’에서 **Windows 방화벽 켜기 또는 끄기**를 선택하여 ‘설정 사용자 지정’ 창을 엽니다.
14. ‘설정 사용자 지정’ 창에서 아래와 같이 ‘사설망 설정’ 및 ‘공중망 설정’을 ‘Windows Defender 방화벽 끄기(권장하지 않음)’로 설정합니다.
![비활성화](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

여전히 원격 데스크톱에서 Windows 인스턴스에 연결할 수 없으면 [온라인 지원](https://console.intl.cloud.tencent.com/workorder/category)을 통해 문의해주시기 바랍니다.



