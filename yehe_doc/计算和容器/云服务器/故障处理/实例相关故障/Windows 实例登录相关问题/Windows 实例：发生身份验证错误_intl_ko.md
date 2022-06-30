## 문제 설명

원격 데스크톱 연결을 통해 Windows 인스턴스에 로그인할 때 다음의 오류 발생.
- ‘인증 오류입니다. 기능에 제공된 토큰이 잘못되었습니다’.
- ‘인증 오류입니다. 요청한 기능이 지원되지 않습니다’.

## 문제 분석

Microsoft에서 2018년 3월에 배포한 보안 업데이트가 CredSSP 프로토콜을 지원함과 동시에, 실명 인증의 인증 요청 방식을 업데이트하여 CredSSP의 원격 코드 실행 취약점이 수정되었습니다. 따라서 클라이언트와 서버 모두 이 업데이트를 설치해야 하며, 그렇지 않으면 문제 설명에서 서술한 상황이 발생할 수 있습니다.
원격 연결에 실패하는 이유는 다음 세 가지 경우가 있습니다.

- 경우1: 클라이언트 패치 안 함, 서버에 보안 업데이트 설치됨, 정책이 "강제 업데이트된 클라이언트"로 설정됨
- 경우2: 서버 패치 안 함, 클라이언트에 보안 업데이트 설치됨, 정책이 "강제 업데이트된 클라이언트"로 설정됨
- 경우3: 서버 패치 안 함, 클라이언트에 보안 업데이트 설치됨, 정책이 "완화"로 설정됨

## 솔루션



<dx-alert infotype="explain" title="">
클라이언트를 로컬에서만 업그레이드해야 하는 경우 [솔루션1: 보안 업데이트 설치(권장)](#step4)를 사용하십시오.
</dx-alert>


### VNC로 CVM에 로그인

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이 인스턴스 관리 페이지에서 타깃 CVM 인스턴스를 찾아 **로그인**을 클릭합니다.
![CVM 리스트 페이지](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ‘표준 로그인 | Windows 인스턴스’ 팝업 창에서 **VNC 로그인**을 선택합니다.
4. 아래 이미지와 같이 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 전송”을 선택하고 **Ctrl-Alt-Delete**를 클릭해 시스템 로그인 인터페이스에 진입합니다.
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)
5. 로그인 비밀번호를 입력하고 **Enter**를 눌러 Windows CVM에 로그인합니다.


### 솔루션1: 보안 업데이트 설치(권장)[](id:step4)

보안 업데이트를 설치하여 패치하지 않은 클라이언트/서버를 업데이트합니다. 각 시스템에 따른 업데이트 현황은 [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)을 참고 바랍니다. 본 솔루션은 Windows Server 2016을 예로 듭니다.
기타 운영 체제는 다음 작업을 참고하여 **Windows 업데이트**를 열 수 있습니다.

- Windows Server 2012: <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width: 22px;"></img> > **제어판** > **시스템 및 보안** >**Windows 업데이트**
- Windows Server 2008: **시작** > **제어판** > **시스템 및 보안** > **Windows Update**
- Windows10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img> > **설정** > **업데이트 및 보안**
- Windows 7: <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin:-3px 0px;width: 28px;"></img> > **제어판** > **시스템 및 보안** > **Windows Update**


1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img>을(를) 클릭하고 **설정**을 선택합니다.
2. ‘설정’ 창에서 **업데이트 및 보안**을 선택합니다.
3. **업데이트 및 보안** 페이지에서 **Windows 업데이트**를 선택하고 **업데이트 확인**을 클릭합니다.
4. **업데이트 설치**를 클릭합니다.
5. 설치 완료 후 인스턴스를 재시작하여 업데이트를 완료합니다.

### 솔루션2: 정책 설정 수정

보안 업데이트가 설치된 CVM에서 **암호화 Oracle 수정** 정책을 ‘취약’으로 설정합니다. 이 솔루션은 Windows Server 2016을 예시로 사용합니다. 다음 단계를 완료하십시오.


<dx-alert infotype="notice" title="">
Windows 10 Home 운영 체제에서 그룹 정책 편집기를 사용할 수 없는 경우 레지스트리에서 정책을 수정할 수 있습니다. 자세한 내용은 [솔루션3: 레지스트리 수정](#Plan3)을 참고하십시오.
</dx-alert>


1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>을(를) 클릭하고 **gpedit.msc**를 입력하고 **Enter**키를 눌러 ‘로컬 그룹 정책 편집기’를 엽니다.
<dx-alert infotype="explain" title="">
또는 ‘**Win+R**’ 키를 눌러 실행 대화 상자를 열 수도 있습니다.
</dx-alert>
2. 왼쪽 탐색 트리에서 **컴퓨터 구성** > **관리 템플릿** > **시스템** > **자격 증명 위임**을 선택하고 **암호화 Oracle 수정**을 더블 클릭합니다.
3. ‘암호화 Oracle 수정’ 창에서 **활성화됨**을 선택하고 **보호 레벨**을 **취약**으로 설정합니다.
4. **확인**을 클릭하여 구성을 마칩니다.


### 솔루션3: 레지스트리 수정[](id:Plan3)

1. 바탕 화면에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>을(를) 클릭하고 **regedit**를 입력하고 **Enter**키를 눌러 레지스트리 편집기를 엽니다.
<dx-alert infotype="explain" title="">
또는 ‘**Win+R**’ 키를 눌러 실행 대화 상자를 열 수도 있습니다.
</dx-alert>
2. 왼쪽 탐색 트리에서 **컴퓨터** > **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters**를 선택합니다.
<dx-alert infotype="explain" title="">
해당 경로가 없으면 수동으로 생성합니다.
</dx-alert>
4. **Parameters**를 마우스 우클릭 후 **새로 만들기** > **DWORD(32비트) 값**을 선택하고 파일 이름을 ‘AllowEncryptionOracle’로 지정합니다.
5. 새로 생성된 ‘AllowEncryptionOracle’ 파일을 더블 클릭하고 ‘값 데이터’를 ‘2’로 설정한 후 **확인**을 클릭합니다.
6. 인스턴스를 재시작합니다.

## 관련 문서

- [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CVE-2018-0886 의 CredSSP 업데이트](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)

