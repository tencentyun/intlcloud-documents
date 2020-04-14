## 작업 시나리오

본 문서는 Windows Server 2012 운영 체제를 예시로 Windows 패치 업데이트에 대해 안내합니다.

## 작업 순서

### 공용 네트워크를 통한 업데이트
시스템의 Windows Update 서비스를 통해 패치 프로그램을 설치할 수 있습니다. 자세한 작업 순서는 다음과 같습니다.
1. Windows CVM에 로그인합니다.
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> >[제어판]>[Windows 업데이트]를 클릭하여 Windows 업데이트 창을 엽니다.
3. [업데이트 검사]를 클릭하여 검사가 완료될 때까지 기다려 주세요.
4. 검사 완료 후, "Windows 업데이트"에서 [**n개의 필수 업데이트 사용 가능**] 또는 [**n개의 선택 업데이트 사용 가능**]를 클릭합니다.
5. "설치할 업데이트 선택" 팝업 창에서 설치할 업데이트 프로그램을 선택하고 [설치]를 클릭합니다.
업데이트 완료 후 시스템에서 시스템 재시작 메시지가 표시되면 CVM을 즉시 재시작하세요.
> 패치 업데이트를 완료하고 CVM을 재시작하면 VNC 방식을 통해 CVM에 로그인하여 모니터링 해야 합니다. 시스템에서 "업데이트 중이니 전원을 끄지 마십시오." 또는 "설정이 완료되지 않았습니다."라고 표시되면 컴퓨터를 강제 종료하지 마시기 바랍니다. 강제 종료 시, CVM이 손상될 수 있습니다.

### 내부 네트워크를 통한 업데이트
CVM이 공용 네트워크에 연결할 수 없을 경우 Tencent Cloud의 내부 네트워크 패치 서버를 사용해 업데이트할 수 있습니다. Tencent Cloud의 Windows 패치 서버에는 Windows에서 일반적으로 사용하는 패치 업데이트 프로그램이 포함되어 있습니다. 그러나 하드웨어 드라이버 패키지와 일부 자주 사용하지 않는 서버 업데이트 패키지는 포함되어 있지 않습니다. 일부 자주 사용하지 않는 서비스는 Tencent Cloud의 내부 네트워크 패치 서버에서 검색되지 않을 수 있습니다.
Tencent Cloud 내부 네트워크의 패치 서버 사용 방법은 다음과 같습니다.
1. Windows CVM에 로그인합니다.
2. IE 브라우저를 이용해 Tencent Cloud 내부 네트워크의 설정 툴(wusin.bat)에 액세스하여 다운로드합니다.
wusin.bat 다운로드 주소: `http://mirrors.tencentyun.com/install/windows/wusin.bat`
3. 다음의 이미지를 참고하여 TCCLI(CMD)을 사용해 wusin.bat를 엽니다.
> IE에서 wusin.bat 툴을 바로 실행하면 콘솔 창이 자동으로 닫혀 출력 정보를 관찰할 수 없습니다.
>

Tencent Cloud 내부 네트워크의 Windows 패치 서버를 더는 사용할 필요가 없을 경우 wusout.bat 정리 툴을 다운로드하여 정리할 수 있습니다. 자세한 방법은 다음과 같습니다.
1. Windows CVM에 로그인합니다.
2. IE 브라우저를 통해 Tencent Cloud 내부 네트워크의 정리 툴(wuout.bat)에 액세스하여 다운로드합니다.
wuout.bat 다운로드 주소: `http://mirrors.tencentyun.com/install/windows/wusout.bat`
3. 다음의 이미지를 참고하여 TCCLI(CMD)을 사용해 wusout.bat를 엽니다.
> IE에서 wusout.bat 툴을 바로 실행하면 콘솔 창이 자동으로 닫혀 출력 정보를 관찰할 수 없습니다.
>
