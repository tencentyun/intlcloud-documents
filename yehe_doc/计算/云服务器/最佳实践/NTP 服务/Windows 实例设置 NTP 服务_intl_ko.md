## 작업 시나리오

본 문은 Windows Server에서 어떻게 NTP 서비스를 실행하고 시계 원본 서버 주소를 수정하는 지를 소개합니다.

Windows 타임 서비스(Windows Time service, W32Time)는 로컬 시스템과 시계 원본 서버 간의 시간 동기화에 사용됩니다. 네트워크 타임 프로토콜(NTP)을 사용하여 네트워크상의 컴퓨터 시계를 동기화합니다. 다음은 Windows Server 2016을 예로 들어 클라이언트와 명령줄의 방식을 통해 NTP 서비스를 실행하고 시계 원본 서버 주소를 수정하는 방법을 설명합니다.

## 작업 순서

1. [Windows 인스턴스에 원격 로그인](https://intl.cloud.tencent.com/document/product/213/5435)。
2. “관리 툴 > 서비스 > Windows Time”을 클릭합니다.
![Windows Time](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
3. 시작 유형을 “자동”으로 설정하고 서비스가 실행되지 않을 경우 “실행”을 클릭합니다.
![w32time](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
4. 작업창의 공지 구역에서 시간을 클릭하고 “날짜와 시간 설정 변경”을 클릭합니다.
![시간 설정](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)	
5. “Internet 시간” 태그로 전환하여 설정 변경을 클릭합니다.
![Internet 시간](https://main.qcloudimg.com/raw/acc52fce975638cef4e39f9f821d66bc.png)
6. Internet 시간 설정 팝업창에서 목표 원본 서버 도메인 또는 IP 주소를 입력하고 “확인”을 클릭합니다.
![Internet 시간 설정](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)
7. 설정 완료 후 “날짜와 시간”을 다시 열면 시계 원본 서버가 변경 완료되었음을 확인할 수 있습니다.
![확인](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)


