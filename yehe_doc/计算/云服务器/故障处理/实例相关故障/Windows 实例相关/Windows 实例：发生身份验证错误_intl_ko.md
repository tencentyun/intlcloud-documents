## 문제 설명

원격 데스크탑 연결을 통해 Windows 인스턴스에 로그인 시 다음과 같은 오류 메시지가 뜹니다.
- "인증 오류가 발생했습니다. 요청한 함수가 지원되지 않습니다."라고 뜹니다. 
- "인증 오류가 발생했습니다.요청한 함수가 지원되지 않습니다." 라고 오류 메시지가 뜹니다. 

## 문제 분석

Microsoft에서 2018년 3월 보안 업데이트를 배포했습니다. 해당 업데이트는 redential Security Support Provider protocol(CredSSP)의 인증 프로세스 중 인증 요청 방식을 수정하여 CredSSP에 존재하는 원격 코드 실행 취약점을 수정했습니다. 클라이언트와 서버 모두 이 업데이트를 받아야 하며, 그렇지 않을 경우 언급된 문제들이 발생할 수 있습니다.

위의 이미지와 같이 다음의 3가지 상황이 모두 원격 연결 실패를 일으킵니다.
- 상황 1: 클라이언트 패치를 하지 않고 서버에 보안 업데이트를 설치하였으며 정책을 "클라이언트 강제 업데이트"로 설정했을 경우
- 상황 2: 서버 패치를 하지 않고 클라이언트에 보안 업데이트를 설치하였으며 정책을 "클라이언트 강제 업데이트"로 설정했을 경우
- 상황 3: 서버 패치를 하지 않고 클라이언트에 보안 업데이트를 설치하였으며 정책을 "완화"로 설정했을 경우

## 솔루션

>? 클라이언트 로컬에 대해서만 업데이트를 하려면 [방안 1: 보안 업데이트 설치(권장)](#step4)를 바로 실행하면 됩니다.
>
### VNC를 통해 CVM에 로그인

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. "Instances" 페이지에서 목표 CVM 인스턴스를 찾고 [Log In]을 클릭합니다. 아래 이미지 참조
![CVM 리스트 페이지](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

<span id="step4"></span>
### 방안 1: 보안 업데이트 설치(권장)

보안 업데이트를 설치하면 패치되지 않은 클라이언트/서버를 업데이트할 수 있습니다. 각 시스템에 대응되는 업데이트 상황은 [CVE-2018-0886 | CredSSP의 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)을 참조하십시오. 본 방안은 Windows Server 2016을 예로 듭니다.
기타 운영 체제는 다음의 작업 순서를 참조하여 [Windows 업데이트]를 할 수 있습니다.
- Windows Server 2012：<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> >[제어판]>[시스템 및 보안]>[Windows 업데이트]
- Windows Server 2008: [시작]>[제어판]>[시스템 및 보안]>[Windows Update]
- Windows10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> >[설정]>[업데이트 및 보안]
- Windows 7：<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> >[제어판]>[시스템 및 보안]>[Windows Update]


1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> 클릭한 후 [설정]을 선택합니다. 
2. 열린 "설정" 창에서 [업데이트 및 보안]을 선택합니다. 
3. "업데이트 및 보안"에서 [Windows 업데이트]를 선택하고 [업데이트 확인]을 클릭합니다. 
4. 인터페이스 알림에 따라 [설치 시작]을 클릭합니다.
5. 설치 완료 후 인스턴스를 재시작하고 업데이트를 완료합니다.

### 방안 2: 정책 설정 수정

보안 업데이트 설치를 완료한 디바이스에서 [암호화 Oracle 수정] 정책을 "취약"으로 설정합니다. 본 방안은 Windows Server 2016을 예로 들며, 작업 순서는 다음과 같습니다.
>! Windows 10 홈버전 운영 체제에 그룹 정책 에디터가 없으면 레지스트리 수정을 통해 구현할 수 있습니다. 작업 순서는 [방안 3: 레지스트리 수정](#Plan3)을 참조하십시오.
>
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img> 클릭하고 **gpedit.msc**를 입력한 후 **Enter**를 눌러 "로컬 그룹 정책 에디터"를 엽니다.
>? 사용자는 단축 키 "Win+R"을 통해서도 실행 인터페이스를 열 수 있습니다
>
3. 왼쪽 메뉴에서 [컴퓨터 설정]>[관리 템플릿]>[시스템]>[자격 증명 위임]을 선택하고 [암호화 Oracle 수정]을 더블 클릭합니다. 
3. 열린 "암호화 Oracle 수정" 창에서 [활성화]를 선택하고 [보호 수준]을 [취약]으로 설정합니다. 
4. [확인]을 클릭하여 설정을 완료합니다.

<span id="Plan3"></span>
### 방안 3: 레지스트리 수정

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>를 클릭하고 **regedit**를 입력한 후 **Enter**를 눌러 레지스트리 편집기를 엽니다.
>? 사용자는 단축 키 "Win+R"을 통해서도 실행 인터페이스를 열 수 있습니다
> 
2. 왼쪽 메뉴에서 차례대로 [컴퓨터]>[HKEY_LOCAL_MACHINE]>[SOFTWARE]>[Microsoft]>[Windows]>[CurrentVersion]>[Policies]>[System]>[CredSSP]>[Parameters] 디렉터리를 펼칩니다. 
>? 해당 디렉터리 경로가 존재하지 않으면 수동으로 생성하십시오.
>

4. [Parameters]를 우클릭하고 [생성]>[DWORD(32비트)값]을 선택하여 파일 이름을 "AllowEncryptionOracle"로 합니다.
5. 생성한 "AllowEncryptionOracle" 파일을 더블 클릭하고 "값 데이터"를 "2"로 설정한 후 [확인]을 클릭합니다. 
6. 인스턴스를 재시작합니다.

## 관련 문서

- [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CVE-2018-0886의 CredSSP 업데이트](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
