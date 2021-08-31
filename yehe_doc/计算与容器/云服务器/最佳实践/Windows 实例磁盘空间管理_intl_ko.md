## 작업 시나리오
본 문서는 Windows Server 2012 R2 운영 체제의 Tencent Cloud CVM을 예로, Windows 인스턴스 디스크의 용량이 부족할 때의 용량 확보 작업 및 일상적인 디스크 점검 방법에 대해 소개합니다.

## 작업 순서

### 디스크 용량 확보
[용량이 비교적 큰 파일 삭제](#deleteLargerFiles) 또는 [불필요한 파일 삭제](#deleteObsoleteFiles)를 통해 디스크 용량이 부족한 문제를 해결할 수 있습니다. 파일을 정리해도 부족하다면 디스크 확장을 통해 용량을 확장할 수 있으며, 자세한 내용은 [확장 시나리오 소개](https://intl.cloud.tencent.com/document/product/362/31600)를 참조 바랍니다.
<span id="deleteLargerFiles"></span>
#### 용량이 비교적 큰 파일 삭제
1. [RDP 파일을 사용하여 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5435)하거나 실제 작업 스타일에 따라 [원격 데스크톱 연결을 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32498)할 수 있습니다.
2. 하단의 작업 표시줄에서 <img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px"> 모양을 클릭하고 '내 PC' 창을 엽니다.
3. '내 PC'에서 정리할 디스크를 선택하고 **Crtl + F**를 눌러 검색 툴을 엽니다.
4. 아래 이미지와 같이 [검색]>[크기]를 선택하고, 시스템에 정의된 크기를 기준으로 필요에 따라 메뉴에서 선택해 파일을 필터링합니다.
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
>?또는 '내 PC' 창 오른쪽 상단의 검색 창에서 파일 크기를 사용자 정의로 검색할 수 있습니다. 예시:
>- '크기: >500M'를 입력하면 해당 디스크에 있는 500M 이상의 파일을 검색합니다.
> - '크기: > 100M < 500M'를 입력하면 해당 디스크에 있는 100M 초과 500M 미만의 파일을 검색합니다.
>

<span id="deleteObsoleteFiles"></span>
#### 불필요한 파일 삭제
1. <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px"> 모양을 클릭하여 서버 관리자를 엽니다.
2. [역할 및 기능 추가]를 클릭하면 '역할 및 기능 추가 마법사' 창이 팝업됩니다.
3. '역할 및 기능 추가 마법사' 창에서 [다음]을 클릭합니다.
4. 아래 이미지와 같이 '설치 유형 선택' 인터페이스에서 [역할 기반 또는 기능 기반 설치]를 선택하고, [다음]을 3회 연속 클릭합니다.
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. 아래 이미지와 같이 '기능 선택' 인터페이스에서 '잉크 및 필기 서비스'와 '데스크톱 체험'을 선택하고 팝업된 대화 상자에서 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. [다음]을 선택하고 [설치]를 클릭합니다. 설치가 완료되면 인터페이스의 안내에 따라 서버를 재시작합니다.
7. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px"> 모양을 클릭하고 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px"> 모양을 클릭합니다. 검색 창에 '디스크 정리'를 입력하여 검색합니다.
8. 아래 이미지와 같이, 팝업된 '디스크 정리' 창에서 해당하는 디스크를 선택한 뒤 정리를 시작합니다.
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### 일상적인 디스크 점검
#### 정기적인 응용 프로그램 정리
아래 이미지와 같이 '제어판'의 '프로그램 삭제'에서 사용하지 않는 응용 프로그램을 삭제할 수 있습니다.
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### 콘솔에서 디스크 사용 현황 조회
Tencent Cloud에서는 CVM 생성 시 클라우드 모니터링 서비스를 활성화하도록 기본 설정되어 있습니다. 따라서 콘솔에서 CVM 디스크 사용 현황을 조회할 수 있으며, 이에 대한 과정은 아래와 같습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index)에 로그인하여 Instance List 페이지로 이동합니다.
2. 조회할 인스턴스 ID를 선택해 해당 인스턴스 상세 페이지로 이동합니다.
3. 아래 이미지와 같이 인스턴스 상세 페이지에서 [모니터링] 탭을 선택하면 해당 인스턴스의 디스크 사용 현황을 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
