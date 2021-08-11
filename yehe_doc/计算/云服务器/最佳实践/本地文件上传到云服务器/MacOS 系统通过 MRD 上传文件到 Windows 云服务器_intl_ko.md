## 작업 시나리오
Microsoft Remote Desktop(이하 MRD)은 Microsoft가 Mac 디바이스용으로 출시한 원격 데스크톱 응용 프로그램입니다. 본 문서에서는 Mac 디바이스에서 MRD을 통해 Windows Server 2012 R2로 빠르게 파일을 업로드할 수 있는 운영 체제인 Cloud Virtual Machine(CVM)에 대해 소개합니다. 

## 전제 조건
- 로컬 컴퓨터에 MRD이 다운로드 및 설치되어 있어야 합니다. 본 문서에서는 Microsoft Remote Desktop for Mac를 예로 들어 설명합니다. Microsoft는 2017년 Remote Desktop 클라이언트의 다운로드 링크 제공을 중단하였고, 자회사인 HockeyApp에서 Beta 버전을 배포하고 있습니다. [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)에서 Beta 버전을 다운로드 받으실 수 있습니다.
- MRD는 Mac OS 10.10 이상의 버전을 지원하므로 지원하는 운영 체제를 사용해 주십시오.
- Windows CVM을 구매해야 합니다.

## 작업 순서
### 공용 IP 획득
[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후, 인스턴스 리스트 페이지에서 파일을 업로드할 CVM의 공용 IP를 다음 이미지와 같이 기록합니다.
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### 파일 업로드
1. 아래 이미지와 같이 MRD를 실행하고 [Add Desktop]을 클릭합니다.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. 아래 이미지와 같이 ‘Add Desktop’ 팝업창에서 아래의 순서대로 업로드할 폴더를 선택하고 링크를 생성합니다.
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. ‘PC name’에 획득한 CVM의 공용 IP를 입력합니다.
  2. [Folders]를 클릭하여 선택한 폴더 리스트로 전환합니다.
  3. 왼쪽 하단의 <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px">를 클릭하고 팝업창에서 업로드할 폴더를 선택합니다.
  4. 선택 완료 후, 업로드할 폴더 리스트를 조회할 수 있으며, [Add]를 클릭하여 생성을 확인합니다.
  5. 나머지 옵션은 기본 설정을 유지하고 링크 생성을 완료합니다.
생성된 링크는 다음과 같이 창에서 바로 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 신규 생성한 링크를 더블 클릭하여 열고, 팝업창에서 뜨는 메시지에 따라 CVM 계정 및 비밀번호를 입력 후 [Continue]를 클릭합니다.
>?
>- CVM 계정은 `Administrator`로 기본 설정되어 있습니다.
>- 시스템 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
>- 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
>
5. 아래 이미지와 같이 팝업창에서 [Continue]를 클릭하여 연결합니다.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
아래 이미지와 같이 연결 성공 후, Windows CVM 인터페이스가 열립니다.
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
6. 왼쪽 하단의 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">>[내 PC]를 클릭하면 공유 중인 폴더를 확인할 수 있습니다.
8. 더블 클릭으로 공유 폴더를 열고, 업로드하려는 로컬 파일을 Windows CVM의 다른 디스크에 복사해 넣으면 파일 업로드가 완료됩니다.
폴더 안의 A 파일을 Windows CVM의 C 드라이브로 복사하는 것을 예로 들 수 있습니다.

### 파일 다운로드
Windows CVM의 파일을 로컬 컴퓨터로 다운로드하려는 경우, 파일 업로드 작업을 참조하여 필요한 파일을 Windows CVM에서 공유 폴더로 복사해 파일을 다운로드할 수 있습니다.


