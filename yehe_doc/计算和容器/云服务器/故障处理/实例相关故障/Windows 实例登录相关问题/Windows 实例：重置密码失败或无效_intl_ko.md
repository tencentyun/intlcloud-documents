본문은 Windows Server 2012 운영 체제를 예로 들어, 비밀번호 재설정에 실패하거나 재설정한 비밀번호가 적용되지 않는 Window CVM 인스턴스에 대한 문제 진단 방법 및 솔루션을 소개합니다.

## 현상 설명

- CVM 비밀번호를 재설정한 후 '시스템 오류로 인스턴스 비밀번호 재설정에 실패했습니다(7617d94c)' 표시됨
- CVM 비밀번호를 재설정한 후 새로운 비밀번호가 적용되지 않아 여전히 변경 전 비밀번호로 로그인됨


## 예상 원인
다음과 같은 원인으로 CVM 비밀번호 재설정에 실패하거나 재설정한 비밀번호가 적용되지 않을 수 있습니다.
- CVM 내 `cloudbase-init` 컴포넌트의 손상, 수정, 비활성화 또는 미실행
- CVM에 360 Total Security 또는 Huorong Security와 같은 타사 보안 소프트웨어를 설치한 경우, 타사 보안 소프트웨어가 비밀번호 재설정 컴포넌트 'cloudbase-init'를 차단하여 인스턴스 비밀번호 재설정이 무효화됨


## 장애 진단 및 프로세스

비밀번호 재설정에 실패하는 문제의 예상 원인에 따라, 다음 두 가지 검사 방법을 제안합니다.

### cloudbase-init 서비스 검사

1. [표준 로그인 방식으로 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/32496)을 참고하여 타깃 Windows 인스턴스에 로그인합니다.
2. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png' style='margin: -3px 0px;'></img>을(를) 우클릭하여 [실행]을 선택하고, [실행] 창에 **services.msc**를 입력한 뒤 **Enter**를 눌러 '서비스' 창을 엽니다.
3. 아래 이미지와 같이 `cloudbase-init` 서비스가 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - 서비스가 있으면 다음 단계를 실행합니다.
 - 서비스가 없으면 `cloudbase-init` 서비스를 재설치합니다. 자세한 작업 방법은 [Windows 운영 체제에서 Cloudbase-Init 설치](https://intl.cloud.tencent.com/document/product/213/32364)를 참고하십시오.
4. 아래 이미지와 같이 더블 클릭하여 `cloudbase-init`의 속성을 엽니다.
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. [일반] 탭에서 `cloudbase-init`의 실행 유형이 [자동]으로 설정되어 있는지 확인합니다.
 - 서비스가 있으면 다음 단계를 실행합니다.
 - 자동으로 설정되어 있지 않으면 `cloudbase-init`의 실행 유형을 [자동]으로 설정합니다.
6. [로그인] 탭으로 이동해 `cloudbase-init`의 로그인 계정이 [로컬 시스템 계정]으로 설정되어 있는지 확인합니다.
 - 서비스가 있으면 다음 단계를 실행합니다.
 - 로컬 시스템 계정으로 설정되어 있지 않으면 `cloudbase-init`의 로그인 계정을 [로컬 시스템 계정]으로 설정합니다.
7. [일반] 탭으로 이동해 서비스 상태의 [실행]을 클릭하여 `cloudbase-init` 서비스를 수동 실행한 뒤 오류가 발생하는지 살펴봅니다.
 - 오류가 발생하면 [CVM에 설치된 보안 프로그램 검사](#CheckSecuritySoftware)를 진행합니다.
 - 오류가 발생하지 않으면 다음 단계를 실행합니다.
8. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png' style='margin: -3px 0px;'></img>을(를) 우클릭하여 [실행]을 선택하고, [실행] 창에 **regedit**을 입력한 뒤 **Enter**를 눌러 '레지스트리 편집기' 창을 엽니다.
9. 왼쪽의 레지스트리 사이드바에서 [HKEY_LOCAL_MACHINE]>[SOFTWARE]>[Cloudbase Solutions]>[Cloudbase-Init] 디렉터리를 순서대로 펼칩니다.
10. [ins-xxx] 아래의 모든 'LocalScriptsPlugin' 레지스트리를 찾아, LocalScriptsPlugin 값이 2인지 확인합니다.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - 2가 맞다면, 다음 단계를 실행합니다.
 - 값이 다르면 LocalScriptsPlugin의 값을 2로 설정합니다.
11. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png' style='margin: -3px 0px;'></img>을(를) 클릭하여 [내 컴퓨터]를 선택한 뒤, 아래 이미지와 같이 디바이스 및 드라이브에 CD-드라이브를 로딩했는지 확인합니다.
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - 로딩하였다면, [CVM에 설치된 보안 프로그램 검사](#CheckSecuritySoftware)를 진행합니다.
 - 로딩하지 않은 경우 장치 관리자에서 CD-ROM 디스크 드라이버를 실행합니다.

<span id='CheckSecuritySoftware'></span>
### CVM에 설치된 보안 프로그램 검사

설치된 보안 프로그램에서 전체 디스크 스캔을 선택하여, CVM의 취약점과 `cloudbase-init`의 핵심 컴포넌트 차단 여부를 검사합니다.
- CVM의 취약점을 발견했다면 복구해야 합니다.
- 핵심 컴포넌트가 차단되었다면 차단을 해제해야 합니다.

`cloudbase-init` 모듈 검사 및 설정 단계는 다음과 같습니다.
1. [표준 로그인 방식으로 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/32496)을 참고하여 타깃 Windows 인스턴스에 로그인합니다.
2. 실제 설치된 타사 보안 프로그램에 'cloudbase-init' 컴포넌트를 복원 및 설정합니다.

