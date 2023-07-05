## 작업 시나리오

Remote Desktop Protocol(RDP)은 Microsoft에서 개발한 멀티 터널 프로토콜로 사용자의 로컬 컴퓨터가 원격 컴퓨터에 연결하도록 도와줍니다. RDP는 Tencent Cloud가 권장하는 Windows CVM 로그인 방식입니다. 본 문서는 RDP 파일을 사용하여 Windows 인스턴스에 로그인하는 방법을 소개합니다.

## 로컬 운영 체제에 적용
Windows, Linux 및 Mac OS 모두 RDP 방식을 사용하여 CVM에 로그인할 수 있습니다.

## 전제 조건

- Windows 인스턴스에 원격 로그인할 때 사용할 인스턴스의 관리자 계정과 비밀번호 획득.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득합니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)합니다.
- CVM 인스턴스가 공인 IP를 구매하였고 해당 인스턴스가 CVM 인스턴스의 3389번 포트를 활성화한 경우(빠른 구성을 통해 구매한 CVM 인스턴스는 활성화 상태로 기본 설정되어 있습니다).

## 작업 순서

### Window 시스템에서 RDP를 사용하여 로그인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이 인스턴스의 관리 페이지에서 로그인할 Windows CVM을 선택하고 [Log In]을 클릭합니다.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. [Log into Windows instance] 팝업 창이 뜨면 [Log in with RDF file]을 선택하고, [Download RDP file]를 클릭하여 RDP 파일을 로컬 컴퓨터로 다운로드합니다.
>?이미 원격 로그인 포트를 변경했다면, RDP 파일을 수정하고 IP 주소 뒤에 ':포트'를 추가해야 합니다.
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. 로컬 컴퓨터로 다운로드 한 RDP 파일을 더블 클릭하여 Windows CVM에 원격 연결합니다.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득합니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)합니다.

### Linux 시스템에서 RDP를 사용하여 로그인

> 사용자가 상응하는 원격 데스크톱을 설치하여 프로그램에 연결해야 한다면 rdesktop을 사용하여 연결하도록 권장합니다. 자세한 내용은 [rdesktop 공식 홈페이지 설명](http://www.rdesktop.org/)을 참조 바랍니다.
>
1. 다음 명령어를 실행하여 시스템에 rdesktop이 설치되어 있는지 확인합니다.
```
rdesktop
```
 - rdesktop이 이미 설치되어 있다면 [4단계](#step04)를 실행합니다.
 - command not found라는 메시지가 뜨면 rdesktop이 설치되어 있지 않다는 의미이므로 [2단계](#step02)를 실행합니다.
2. <span id="step02"></span>단말에서 다음 명령어를 실행하여 rdesktop 설치 패키지를 다운로드합니다. 이 단계에서는 rdesktop 1.8.3 버전을 예시로 사용합니다.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
최신 설치 패키지가 필요하다면 [GitHub rdesktop 페이지](https://github.com/rdesktop/rdesktop/releases)로 이동하여 최신 설치 패키지를 찾아 명령어 라인에서 최신 설치 경로로 바꿉니다.
3. rdesktop의 설치 대기 목록에서 명령어를 차례대로 실행하여 rdesktop을 압축 해제 및 설치합니다.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##는 x.x.x를 다운로드한 버전 번호로 바꿉니다. 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">다음 명령어를 실행하여 Windows 인스턴스에 원격 연결합니다.</span>
> 예시의 매개변수를 사용자 본인의 매개변수로 수정합니다.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator`는 전제 조건에서 획득하는 관리자 계정입니다.
 - `<your-password>`는 사용자가 설정한 로그인 비밀번호입니다.
   사용자가 시스템 기본 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득 바랍니다. 비밀번호를 잊으신 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고 바랍니다.
 - `<hostname or IP address>`는 사용자의 Windows 인스턴스 공인 IP 또는 사용자 정의 도메인 이름입니다.
 
### MacOS 시스템에서 RDP를 사용하여 로그인

>
>- 다음 작업은 Microsoft Remote Desktop for Mac을 예시로 사용합니다. Microsoft에서는 2017년 Remote Desktop 클라이언트의 다운로드 링크 제공을 중단하였고, 그 자회사인 HockeyApp 에서 Beta 버전을 배포하고 있습니다.
>- 다음 작업은 Windows Server 2012 R2 운영 체제의 CVM을 예시로 사용합니다.
>
1. Microsoft Remote Desktop for Mac 을 다운로드하고 로컬에서 설치합니다.
2. 아래 이미지와 같이 MRD를 실행하고 [Add Desktop]을 클릭합니다.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 아래 이미지와 같이 "Add Desktop" 팝업 창에서 아래의 순서대로 링크를 생성합니다.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. "PC name"에 CVM의 공인 IP를 입력합니다.
    2. [Add]를 클릭하여 생성합니다.
    3. 나머지 옵션은 기본 설정을 유지하고 링크 생성을 완료합니다.
    생성된 링크는 아래 이미지와 같이 바로 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 신규 생성한 링크를 더블 클릭하여 열고, 팝업 창의 메시지에 따라 CVM 계정 및 비밀번호를 입력한 후 [Continue]를 클릭합니다.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득합니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)합니다.
5. 아래 이미지와 같이 팝업 창에서 [Continue]를 클릭하여 연결합니다.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
아래 이미지와 같이 연결 성공 후 Windows CVM 인터페이스가 열립니다.
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
