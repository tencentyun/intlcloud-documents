## 작업 시나리오

RDP는 Remote Desktop Protocol의 줄임말로 Microsoft에서 개발한 사유 프로토콜입니다. 사용자의 로컬 컴퓨터가 원격 컴퓨터에 연결되도록 도와줍니다. RDP는 Tencent Cloud가 사용자의 Windows CVM에 로그인하도록 권장하는 방식입니다. 이 문서에서는 RDP 파일을 사용하여 Windows 인스턴스에 로그인하는 방법에 대해 설명합니다.

## 로컬 운영 체제에 적용
Windows, Linux 및 Mac OS 모두 RDP 방식을 사용하여 CVM에 로그인할 수 있습니다.

## 전제 조건

 - Windows 인스턴스에 원격 로그인 할 경우 인스턴스의 관리자 계정과 비밀번호를 사용하십시오.
  - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
  - 비밀번호를 잊어버린 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
 - CVM 인스턴스가 이미 공인 IP를 구매한 경우 해당 인스턴스가 이미 CVM 인스턴스의 3389번 포트가 활성화되어 있습니다(빠른 구성을 통해 구매한 CVM 인스턴스는 기본적으로 활성화 상태입니다).

## 작업 순서

### Window 시스템에서 RDP를 사용하여 로그인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오.
2. 인스턴스의 관리 페이지에서 로그인해야하는 Windows CVM을 선택하고 [로그인]을 클릭하십시오. 아래 이미지를 참조하십시오.
3. [Windows 인스턴스 로그인] 팝업창이 뜨면 [RDP를 사용하여 파일에 로그인]을 선택하고 [RDP 파일 다운로드]를 클릭하여 RDP 파일을 로컬 컴퓨터로 다운로드하십시오.
4. 로컬 컴퓨터로 다운로드 한 RDP 파일을 더블 클릭하여 Windows CVM에 원격으로 연결하십시오.
  - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
  - 비밀번호를 잊어버린 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.

### Linux 시스템에서 RDP를 사용하여 로그인

> 사용자가 상응하는 원격 데스크탑을 설치하여 프로그램에 연결해야 하는 경우 rdesktop을 사용하여 연결을 권장합니다. 자세한 내용은 [rdesktop 홈페이지 설명](http://www.rdesktop.org/)을 참조하십시오.
>
1. 다음 명령어를 실행하여 시스템에 rdesktop이 설치되어 있는지 여부를 확인하십시오.
```
rdesktop
```
  - 만약 rdesktop이 이미 설치되어 있으면 [4단계](#step04)를 실행하십시오.
  - 만약 command not found 표시가 뜨면 rdesktop이 설치되어 있지 않다는 의미이므로 [2단계](#step02)를 실행하십시오.
2. <span id="step02"></span>단말기에서 다음 명령어를 실행하여 rdesktop 설치 패키지를 다운로드하십시오. 이 단계에서는 rdesktop 1.8.3 버전을 예로 사용합니다.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
최신 설치 패키지가 필요한 경우 [GitHub rdesktop 페이지](https://github.com/rdesktop/rdesktop/releases)로 이동하여 최신 설치 패키지를 찾아 명령어 라인에서 최신 설치 경로로 바꾸십시오.
3. rdesktop의 대기 설치 목록에서 명령어를 순서대로 실행하여 rdesktop을 압축 해제 및 설치하십시오.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.x는 다운로드한 버전 번호로 교환 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">다음 명령어를 실행하여 Windows 인스턴스에 원격 연결하십시오.</span>
> 예시의 파라미터를 사용자 본인의 파라미터로 수정하십시오.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` 는 전제 조건에서 획득하는 관리자 계정입니다.
 - `<your-password>` 는 사용자가 설정한 로그인 비밀번호입니다.
   사용자가 시스템 기본 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오. 비밀번호를 잊은 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
 - `<hostname or IP address>`는 사용자의 Windows 인스턴스 공인 IP 또는 사용자 정의 도메인 이름입니다.

### MacOS 시스템에서 RDP를 사용하여 로그인

> 다음 작업은 Microsoft Remote Desktop for Mac을 예로 사용합니다. 해당 클라이언트는 테스트 버전 클라이언트이며 Microsoft가 공식적으로 관리하므로 해당 버전의 클라이언트를 우선 사용하길 권장합니다. Microsoft 공식 홈페이지는 2017년에 Remote Desktop 클라이언트의 다운로드 연결 지원을 중단하였고, 자회사인 HockeyApp이 Beta 버전의 배포를 진행하고 있습니다.
>
1. [Microsoft Remote Desktop for Mac](https://rink.hockeyapp.net/apps/5e0c144289a51fca2d3bfa39ce7f2b06/)을 다운로드 하십시오.
2. 클라이언트 도구를 열고 [Add Deskop]을 클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/d310a22009134182def49929625e6f1d.png)
3. 팝업된 대화 상자에서 Windows 인스턴스의 공인 IP 주소를 입력하고 [Add]를 클릭하여 원격 데스크탑을 추가하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/57d7f343e8d52d9365fcd4f4ada5d090.png)
4. 새로 추가된 원격 데스크탑을 더블 클릭하여 열고 인스턴스의 관리자 계정과 비밀번호를 입력한 다음 Windows CVM에 원격으로 연결하십시오.
  - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
  - 비밀번호를 잊어버린 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
