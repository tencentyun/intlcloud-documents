## 작업 시나리오
Pagoda Panel은 사용하기 쉽고 강력하며 평생 무료로 제공되는 서버 관리 소프트웨어이며 Linux 및 Windows 시스템을 지원합니다. Pagoda Panel에서는 LAMP, LNMP, 웹 사이트, 데이터베이스, FTP, SSL을 원클릭으로 설정할 수 있으며 Web을 통해 서버를 쉽게 관리할 수 있습니다.

본 문서는 Tencent Cloud Market 이미지를 통해 Windows 운영 체제의 CVM에 Pagoda Panel을 빠르게 설치하는 방법에 대해 설명합니다.


## 작업 단계

### CVM 생성 시 Pagoda Panel 설치


<dx-alert infotype="notice" title="">
구매한 CVM 부서를 이용하여 Pagoda Panel을 설치하고자 하는 경우 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 통해 해당 이미지를 어워드 마켓에서 선택하여 환경 구축을 완료할 수 있습니다. 현재 중국 외 일부 리전의 CVM은 이미지 마켓을 통한 시스템 재설치를 지원하지 않으니 타 리전의 클라우드 서버를 이용하여 구축하거나 [Pagoda Panel 공식 홈페이지](https://www.bt.cn/)  에서 자세한 설치 정보를 확인하시기 바랍니다.
</dx-alert>

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인 한 후 인스턴스 관리 페이지에서 **생성**을 클릭합니다.
2. 페이지의 프롬프트에 따라 모델을 선택하고 ‘이미지’에서 **이미지 마켓** > **이미지 마켓에서 선택**을 아래 이미지와 같이 선택합니다.
<dx-alert infotype="notice" title="">
- 현재 일부 중국 외 리전은 이미지 마켓을 통한 CVM 생성을 지원하지 않습니다. 선택한 리전에 **이미지 마켓**이 없는 경우 이미지 마켓을 지원하는 다른 리전을 선택하십시오.
- 메모리가 2GB 이상이고 시스템 디스크 용량이 40GB 이상인 인스턴스 설정을 선택하는 것이 좋습니다.
3. ‘이미지 Market’ 창의 검색 창에서 **유지보수 툴**을 선택하고 ‘pagoda’를 입력한 후 <img src="https://main.qcloudimg.com/raw/70c20e0ff30f88eef20d6b540d6ef804.png" style="margin:-3px 0px">을(를) 클릭합니다.
4. 필요에 따라 이미지를 선택합니다. 본 문서는 **Pagoda Windows Panel Official Version (WAMP/WNMP/Tomcat/Node.js)**을 예로 듭니다. 클릭 **무료 사용 **.
5. 인스턴스와 연결된 보안 그룹에서 포트 8888을 개방하는 인바운드 규칙을 추가해야 합니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.
실제 필요에 따라 스토리지 미디어 및 대역폭과 같은 기타 설정을 구성하고 구매를 선택하여 Pagoda Panel 구축을 완료합니다.


### 패널 로그인 정보 가져오기
1. CVM에 로그인합니다. 자세한 내용은 [표준 방식으로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
2. 운영 체제 인터페이스에서 왼쪽 하단의 <img src="https://qcloudimg.tencent-cloud.cn/raw/c6e9910fc4f983d45729b4f6924e8273.png" style="margin:-3px 0px">을(를) 우클릭하고 팝업 메뉴에서 **실행**을 클릭합니다.
3. cmd 창에서 다음 명령을 실행하여 로그인 정보를 가져옵니다.
```
bt default
```
결과가 반환되면 탑 패널의 주소와 로그인 정보를 기록합니다.


### Pagoda Panel에 로그인
1. 로컬 컴퓨터에서 브라우저를 열고 가져온 Pagoda Panel 주소에 액세스합니다.
```shell
http://CVM 공용 IP:8888/xxxx
```
2. 기록된 사용자 이름과 암호를 입력하고 로그인을 클릭합니다.
3. ‘<이용약관>에 동의합니다’를 선택하고 **패널로 이동하기**를 클릭합니다.
4. 실제 필요에 따라 패널에서 관련 패키지 설치 및 배포 웹 사이트를 선택하십시오.
