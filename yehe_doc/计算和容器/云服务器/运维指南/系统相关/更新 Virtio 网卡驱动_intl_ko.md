## 작업 시나리오

Tencent Cloud CVM의 Windows Server 2008 R2, Windows Server 2012 R2, Windows Server 2016 및 Windows Server 2019 R2는 Virtio ENI 드라이버 설치를 통해 가상화 하드웨어의 네트워크 성능을 최적화합니다. Tencent Cloud는 ENI 드라이버를 계속 업데이트하여 성능 업그레이드 및 장애 해결에 사용하고자 합니다. 본 문서에서는 Virtio ENI 드라이버 업데이트 방법 및 드라이버 버전 조회 방법에 대해 설명합니다.

## 전제 조건

Windows CVM에 로그인합니다.

## 작업 단계

### 시스템 버전 정보 조회

시스템 버전은 다음과 같은 방법으로 조회할 수 있습니다.
1. CVM에 로그인하여 <img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px"> 우클릭 후, 팝업 메뉴에서 **실행**을 선택합니다.
2. 열린 "실행" 창에 **cmd**를 입력하고 **Enter**를 누릅니다.
3. 열린 "cmd" 창에 `systeminfo` 명령어를 실행하여 시스템 정보를 확인합니다.
본문의 시스템 버전은 "Windows Server 2016 데이터센터 버전의 64비트 영어 버전"을 예시로 들며 가져온 정보는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8c46c9c368201575fafed26272638544.png)

### Virtio ENI 드라이버 업데이트 방법

<dx-alert infotype="notice" title="">
업데이트 과정에 네트워크가 일시적으로 끊길 수 있어 업데이트 전에 비즈니스에 영향이 없는지 확인 바랍니다. 업데이트 후에 컴퓨터를 재시작합니다.
</dx-alert>


1. CVM의 브라우저를 통해 운영체제 버전에 맞는 VirtIO ENI 드라이버 설치 파일을 다운로드 합니다. 
VirtIO ENI 드라이버 다운로드 주소는 다음과 같으며 실제 네트워크 환경에 따라 다운로드하십시오.
 -  **공용 네트워크 다운로드 주소**: `http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
 -  **내부 네트워크 다운로드 주소**: `http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
2. 다운로드가 완료되면 더블 클릭하여 설치 프로그램을 실행하고 **Next**를 클릭합니다.
3. 기본적으로 "VirtioDrivers"가 선택된 상태로 유지하고 **Next**를 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e77875fd9fdac5364188bc989bba0c05.png)
4. 설치 위치를 선택하고 **Install**을 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d38b32cba76dbb2cdfad95bae3de1f58.png)
5. 보안 메시지 팝업창에서 “‘Tencent Technology(Shenzhen) Company Limited’의 소프트웨어를 항상 신뢰”를 체크한 다음 **설치**를 클릭합니다. 
설치 과정에 다음과 같은 팝업 창이 뜨면 **해당 드라이버를 항상 설치** 옵션을 선택합니다.      
6. 안내 메시지에 따라 컴퓨터를 재시작하면 업데이트가 완료됩니다.


### 드라이버 버전 보기

1. <img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px"> 우클릭 후, 팝업 메뉴에서 **실행**을 선택합니다.
2. 열린 "실행" 창에서 **ncpa.cpl**을 입력하고 **Enter**를 누릅니다. 
2. 열린 "네트워크 연결"창에서 "이더넷" 아이콘을 우클릭하고 **속성**을 선택합니다.
4. "이더넷 속성" 창에서 **설정**을 클릭합니다. 
5. "Tencent VirtIO Ethernet Adapter 속성"창에서 **드라이버** 탭을 선택하면 현재 드라이버 버전을 조회할 수 있습니다. 

