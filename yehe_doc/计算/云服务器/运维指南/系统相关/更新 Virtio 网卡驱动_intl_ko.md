## 작업 시나리오

Tencent Cloud CVM의 Window Server 2008 R2 기업용 SP1 및 Windows Server 2012 R2는 Virtio ENI 드라이버 설치를 통해 가상화 하드웨어의 네트워크 성능을 최적화합니다. Tencent Cloud는 ENI 드라이버를 계속 업데이트하여 성능 업그레이드 및 장애 해결에 사용하고자 합니다. 본 문서에서는 Virtio ENI 드라이버 업데이트 방법 및 드라이버 버전 조회 방법에 대해 설명합니다.

## 전제 조건

Tencent Cloud의 CVM에 로그인.

## 작업 순서

### 시스템 버전 정보 조회

시스템 버전은 다음과 같은 방법으로 조회할 수 있습니다.
1. CVM에 접속하여 바탕화면에서 [컴퓨터]>[속성]을 우클릭하여 "시스템" 창을 엽니다.
2. “시스템”의 [컴퓨터 관련 기본 정보 보기]에서 시스템 버전 정보를 조회할 수 있습니다. 다음 이미지 참고
![](//mccdn.qcloud.com/static/img/5cd57bbbd48668cca57efdaba7e5ae84/image.png)   

### Virtio ENI 드라이버 업데이트 방법
>! 업데이트 과정에 네트워크가 일시적으로 끊길 수 있어 업데이트 전에 비즈니스에 영향이 없는지 확인 바랍니다. 업데이트 후에 컴퓨터를 재시작합니다.
>

1. CVM 내의 브라우저를 통해 Window Server 2008 R2 및 Windows Server 2012 R2에 해당하는 VirtIO ENI 드라이버 설치 파일을 다운로드합니다. 
VirtIO ENI 드라이버 다운로드 주소: http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi
2. 다운로드 완료 후 설치 프로그램을 더블 클릭하여 실행합니다. [일반] 설치 모드를 선택한 후 [다음 단계]를 클릭합니다. 다음 이미지 참고
![](//mccdn.qcloud.com/static/img/0d596e42ae299cfa295a0493dc68bc4d/image.png)
3. 보안 메시지 팝업창에서 ["Tencent Technology(Shenzhen) Company Limited”의 소프트웨어를 항상 신뢰]를 체크한 다음 [설치]를 클릭합니다. 다음 이미지 참고
![](//mccdn.qcloud.com/static/img/f2f5aea8ed1aa8814e69fa9142254537/image.png) 
설치 과정에 다음과 같은 팝업 창이 뜨면 [해당 드라이버를 항상 설치] 옵션을 선택합니다.
![](//mccdn.qcloud.com/static/img/ca48d6e37f5deb2f4575bc608f5c49d6/image.png)      
4. 안내 메시지에 따라 컴퓨터를 재시작하면 업데이트가 완료됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

### 드라이버 버전 보기

1. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;"> 를 클릭하고 "실행"창에서 **ncpa.cpl**을 입력하고 **Enter**를 누르면 다음 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/958e5f143dfabe5c63d5dec63ㄴ0d1292.png)
2. 열려진 "네트워크 연결"창에서 "이더넷" 아이콘을 우클릭하고 [속성]을 선택합니다. 다음 이미지 참고
![](https://main.qcloudimg.com/raw/47a14b72bd71150eb126bcdca3d6157c.png)
3. "이더넷 속성" 창에서 [설정]을 클릭합니다. 다음 이미지 참고
![](https://main.qcloudimg.com/raw/f9e00988e840d775c6ff5f9f789c5172.png)
4. "Tencent VirtIO Ethernet Adapter 속성"창에서 [드라이버] 탭을 선택하면 현재 드라이버 버전을 조회할 수 있습니다. 다음 이미지 참고
![](https://main.qcloudimg.com/raw/ce1be9c37b22e945a11e530c39be41d9.png)


