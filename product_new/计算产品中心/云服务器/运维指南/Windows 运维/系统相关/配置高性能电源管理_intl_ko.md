## 작업 시나리오

Windows Server 운영 체제에서 고성능 전원관리를 구성하여 인스턴스 소프트 리부팅을 지원할 수 있습니다. 그렇지 않으면 CVM 콘솔에서 하드 셧다운 방식으로만 인스턴스를 종료할 수 있습니다. 본 문서에서는 Windows Server 2012 운영 체제를 예로 들어 전원관리를 구성하는 방법에 대해 설명합니다.

## 작업 설명

전원 관리를 수정하기 위해 컴퓨터를 재시작할 필요가 없습니다.

## 작업 순서

1. Windows CVM에 로그인하십시오.
2. IE 브라우저를 통해 Tencent Cloud 내부 네트워크를 액세스하고 Tencent Cloud 전원 수정 및 구성 툴을 다운로드합니다.
다운로드 주소: `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`
예를 들어 Tencent Cloud 전원 수정 및 구성 툴(power-set-win.bat)을 C: 디스크에 다운로드합니다.
3. 관리자의 CLI Tool을 사용하여 power-set-win.bat 를 여십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/65cb9654bcc9978a12ada6aabecb7de3.png)
4. 현재 전원 관리솔루션을 조회하기 위해 다음 명령어를 실행합니다.
```
powercfg -L
```
다음과 같은 결과를 리턴합니다.
4. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> >[제어판]>[시스템 및 보안]>[전원 선택항목]을 클릭하고 전원 선택항목 창을 여십시오.
5. 전원 선택항목 창에서 [계획 설정 변경]을 클릭하십시오. 아래 이미지를 참조하십시오.
6. 열린 "계획 설정 변경"창에서 모니터 및 디스크의 유휴 종료 시간을 수정하십시오. 아래 이미지를 참조하십시오.



