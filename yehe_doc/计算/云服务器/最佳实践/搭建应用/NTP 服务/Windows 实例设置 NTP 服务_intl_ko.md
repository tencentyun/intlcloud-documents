## 작업 시나리오

Windows 타임 서비스(Windows Time service, W32Time)는 로컬 시스템과 클럭 소스 서버 간의 시간 동기화에 사용됩니다. 네트워크 타임 프로토콜(NTP)을 사용하여 네트워크상의 컴퓨터 시계를 동기화합니다. 본 문서는 Windows Server 2012 운영 체제의 CVM을 예로 NTP 서비스 실행 및 클럭 소스 서버 주소 수정 방법에 관해 설명합니다.

## 작업 순서

1. Windows CVM에 로그인합니다.
2. 시작에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > [관리 도구]>[서비스]를 클릭하여 서비스 창을 엽니다.
3. 아래 이미지와 같이 "서비스" 창에서 [Windows Time]을 더블 클릭하여 창을 엽니다.
![](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
4. 아래 이미지와 같이 열린 "Windows Time 속성(로컬 컴퓨터)" 창에서 [시작 유형]을 [자동]으로 설정하고, [서비스 상태]를 [시작]으로 설정한 다음 [확인]을 누릅니다.
![](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
5. 아래 이미지와 같이 운영 체제 인터페이스 작업 표시란에서, 우측 하단의 시간 >[날짜 및 시간 설정]을 클릭합니다.
![](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)
6. 아래 이미지와 같이 팝업된 “날짜 및 시간” 창에서 [인터넷 시간] 탭을 선택하고 [설정 변경]을 클릭합니다.
![](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)
7. 아래 이미지와 같이 팝업된 "인터넷 시간 설정" 창에서 [서버]를 타깃 클럭 소스 서버의 도메인 또는 IP 주소로 설정하고, [확인]을 눌러 설정을 완료합니다.
![](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)



