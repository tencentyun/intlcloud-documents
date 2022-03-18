## 문제 설명

원격 데스크톱 연결을 통해 Windows 인스턴스에 로그인할 때 다음의 오류 발생.
- "인증 오류가 발생했습니다. 함수에 제공한 플래그가 유효하지 않습니다.", 아래 이미지 참조:
![함수에 제공한 플래그가 유효하지 않음](https://main.qcloudimg.com/raw/cbb3b5ea89ed9d3a65af8b303880b7c8.png)
-  “인증 오류가 발생했습니다. 요청한 함수가 지원되지 않습니다.”, 아래 이미지 참조:
![요청한 함수가 지원되지 않음](https://main.qcloudimg.com/raw/09ff95a4f2e46e93a75d0e6ec38c1954.png)

## 문제 분석

Microsoft에서 2018년 3월에 배포한 보안 업데이트가 CredSSP 프로토콜을 지원함과 동시에, 실명 인증의 인증 요청 방식을 업데이트하여 CredSSP의 원격 코드 실행 취약점이 수정되었습니다. 따라서 클라이언트와 서버 모두 이 업데이트를 설치해야 하며, 그렇지 않으면 문제 설명에서 서술한 상황이 발생할 수 있습니다.
![클라이언트와 서버 상황](https://main.qcloudimg.com/raw/2734e664e7d72b083c37db3a4dc13647.png)
위 이미지와 같이 원격 연결에 실패하는 이유는 다음 세 가지 경우가 있습니다.
- 경우1: 클라이언트 패치 안 함, 서버에 보안 업데이트 설치됨, 정책이 "강제 업데이트된 클라이언트"로 설정됨
- 경우2: 서버 패치 안 함, 클라이언트에 보안 업데이트 설치됨, 정책이 "강제 업데이트된 클라이언트"로 설정됨
- 경우3: 서버 패치 안 함, 클라이언트에 보안 업데이트 설치됨, 정책이 "완화"로 설정됨

## 솔루션

> 클라이언트 로컬에서만 업데이트 작업을 한다면 바로 [방안1: 보안 업데이트 설치(권장)](#step4)를 실행하세요.
>
### VNC로 CVM에 로그인

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이 인스턴스 관리 페이지에서 타깃 CVM 인스턴스를 찾아 [Log In]을 클릭합니다.
![CVM 리스트 화면](https://main.qcloudimg.com/raw/038fce530c6c6827796e51d896306a93.png)
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]]를 선택하고 [Log In Now]를 클릭하여 CVM에 로그인합니다.
4. 아래 이미지와 같이 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 전송”을 선택하고 **Ctrl-Alt-Delete**를 클릭해 시스템 로그인 인터페이스에 진입합니다.
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)

<span id="step4"></span>
### 방안1: 보안 업데이트 설치(권장)

보안 업데이트를 설치하여 패치하지 않은 클라이언트/서버를 업데이트합니다. 각 시스템에 따른 업데이트 현황은 [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)을 참조 바랍니다. 본 방안은 Windows Server 2016을 예로 듭니다.
기타 운영 체제는 다음 조작을 참조하여 [Windows 업데이트]를 열 수 있습니다.
- Windows Server 2012：<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> >[제어판]>[시스템 보안]>[Windows 업데이트]
- Windows Server 2008: [시작]>[제어판]>[시스템 보안]>[Windows Update]
- Windows10：<img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> >[설정]>[업데이트 및 보안]
- Windows 7：<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> >[제어판]>[시스템 보안]>[Windows Update]


1. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> 클릭 후, [설정]을 선택합니다.
![설정](https://main.qcloudimg.com/raw/c5add12cacd642aad479bc356cec04f1.png)
2. 아래 이미지와 같이 "설정" 창에서 [업데이트 및 보안]을 선택합니다.
![업데이트 및 보안](https://main.qcloudimg.com/raw/59c7b0c52eee2c5572b73b062edd3ce9.png)
3. 아래 이미지와 같이 “업데이트 및 보안”에서 [Windows 업데이트]를 선택하고 [업데이트 확인]을 클릭합니다.
![업데이트 확인](https://main.qcloudimg.com/raw/0aefedca7c90bcad7b39de781e9521df.png)
4. 인터페이스 안내에 따라 [설치 시작]을 클릭합니다.
5. 설치 완료 후 인스턴스를 재시작하여 업데이트를 완료합니다.

### 방안2: 정책 설정 수정

보안 업데이트를 설치한 컴퓨터에서 [암호화 Oracle 수정] 정책을 "취약"으로 설정합니다. 본 방안은 Windows Server 2016을 예로 들며, 작업 순서를 다음과 같습니다.
> Windows 10 홈 버전 운영 체제에 정책 편집기가 없다면 regedit를 통해 수정할 수 있습니다. 작업 순서는 [방안3: regedit 수정](#Plan3)을 참조 바랍니다.
>
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>를 클릭하고,  **gpedit.msc** 입력 후 **Enter**를 눌러 "로컬 그룹 정책 편집기"를 엽니다
> 또는 “**Win+R**” 키를 사용하여 실행 인터페이스를 열 수 있습니다.
>
3. 아래 이미지와 같이 왼쪽 트리에서 [컴퓨터 구성]>[관리 템플릿]>[시스템]>[자격 증명 위임]을 선택하고 [암호화 Oracle 수정]을 더블 클릭합니다.
![암호화 Oracle 수정](https://main.qcloudimg.com/raw/ae699fa2e997b10eab3477b6c9baf544.png)
3. 아래 이미지와 같이 열린 "암호화 Oracle 수정" 창에서 [사용]을 클릭하고 [보호 수준]을 [취약]으로 설정합니다.
![취약](https://main.qcloudimg.com/raw/65135ad1ea484655953de40fa0882d06.png)
4. [확인]을 클릭하여 설정을 완료합니다.

<span id="Plan3"></span>
### 방안3: regedit 수정

1. 운영 체제의 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>를 우클릭하여 **regedit**를 입력하고 **Enter**를 눌러 레지스트리 편집기를 엽니다.
> 또는 “**Win+R**” 키를 사용하여 실행 인터페이스를 열 수 있습니다.
> 
2. 아래 이미지와 같이 왼쪽 트리에서 차례대로 [컴퓨터]>[HKEY_LOCAL_MACHINE]>[SOFTWARE]>[Microsoft]>[Windows]>[CurrentVersion]>[Policies]>[System]>[CredSSP]>[Parameters] 디렉터리를 펼칩니다.
> 해당 디렉터리의 경로가 없으면 수동으로 생성합니다.
>
![Parameters](https://main.qcloudimg.com/raw/fa4c9fecefb5fc42b9055f7e6d7d36d7.png)
4. [Parameters] 우클릭 후 [새로 만들기]>[DWORD(32비트) 값]을 선택하고 파일 이름을 “AllowEncryptionOracle”로 설정합니다.
5. 아래 이미지와 같이 생성된 “AllowEncryptionOracle” 파일을 더블 클릭하고 “값 데이터”에 “2”를 입력하여 설정한 다음 [확인]을 클릭합니다.
![AllowEncryptionOracle](https://main.qcloudimg.com/raw/2355ea7ef57d01075da6d54987b6f498.png)
6. 인스턴스를 재시작합니다.

## 관련 문서

 [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CVE-2018-0886 의 CredSSP 업데이트](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
