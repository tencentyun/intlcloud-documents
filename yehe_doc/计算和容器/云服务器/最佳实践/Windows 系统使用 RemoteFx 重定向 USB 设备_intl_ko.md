## 작업 시나리오

RemoteFx는 Windows RDP 데스크톱 프로토콜의 업그레이드 버전으로, RDP 8.0 버전부터는 RemoteFx를 사용한 USB 리디렉션이 가능합니다. RDP의 데이터 채널을 통해 로컬 USB 장치를 원격 데스크톱으로 리디렉션하면, 클라우드 기기에서 USB 장치를 사용할 수 없는 문제를 해결할 수 있습니다.

본 문서는 다음과 같은 환경을 예로 들어, RDP의 RemoteFx USB Redirection 기능을 활성화하고 CVM에 리디렉션하는 방법을 소개합니다.
- 클라이언트: Windows 10 운영 체제
- 서버: Windows Server 2016 운영 체제

## 사용 제한

RDP 8.0 이상의 버전은 모두 RemoteFX USB Redirection 기능을 지원하며, Windows 8, Windows 10, Windows Server 2016 및 Windows Server 2019 도 모두 RemoteFX USB Redirection 기능을 지원합니다. 만약 로컬 컴퓨터의 운영 체제가 상기 버전이라면, RDP 8.0 Update 패치는 설치할 필요 없습니다. 만약 로컬 컴퓨터의 운영 체제가 Windows 7 이나 Windows Vista 라면, [Microsoft 공식 홈페이지](https://support.microsoft.com/en-us)에서 RDP 8.0 Update 패치를 설치하시기 바랍니다.


## 작업 순서

### 서버 설정

1. [RDP 파일을 사용하여 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5435)합니다.
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/ab9a3a22baf69f63a90a43476f12db94.png" style="margin: 0;"></img>를 클릭한 뒤, [서버 관리자]를 선택해 서버 관리자 창을 엽니다.
3. 아래 이미지와 같이, '서버 관리자' 창에서 [역할 및 기능 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/518287dced9ccc1de01cbf73315f70d1.png)
4. 팝업된 '역할 및 기능 추가 마법사' 창에서 [다음]을 클릭하여 '설치 유형 선택' 인터페이스로 이동합니다.
5. '설치 유형 선택' 인터페이스에서 [역할 기반 또는 기능 기반 설치]를 선택하고, [다음]을 클릭합니다.
6. '대상 서버 선택' 인터페이스에서 기본 설정을 유지한 채 [다음]을 클릭합니다.
7. 아래 이미지와 같이, '서버 역할 선택' 인터페이스에서 [원격 데스크톱 서비스]를 선택하고 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/05868c877afe2e6043e34e54c023408e.png)
8. 기본 설정을 유지한 채 [다음]을 2번 연속 클릭합니다.
9. 아래 이미지와 같이, '역할 서비스 선택' 인터페이스에서 [원격 데스크톱 세션 호스트], [원격 데스크톱 연결 브로커], [원격 데스크톱 라이선싱]을 선택한 뒤, 팝업 창에서 [기능 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/efc41c3d8c5b54d27664772587261460.png)
10. [다음]을 클릭합니다.
11. [설치]를 클릭합니다.
13. 설치가 완료되면 CVM을 재시작합니다.
14. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>를 클릭하고, **gpedit.msc**를 입력한 뒤 **Enter**를 눌러 '로컬 그룹 정책 편집기'를 엽니다.
15. 아래 이미지와 같이 왼쪽 디렉터리 트리에서 [컴퓨터 구성]>[관리 템플릿]>[Windows 구성 요소]>[원격 데스크톱 서비스]>[원격 데스크톱 세션 호스트]>[장치 및 리소스 리디렉션]을 선택한 뒤, [지원되는 플러그 앤 플레이 장치 리디렉션 허용 안 함]을 더블 클릭하여 엽니다.
![](https://main.qcloudimg.com/raw/a812e4da0f4435b2ca351b286e283b2e.png)
16. 아래 이미지와 같이, 팝업 창에서 [사용 안 함]을 선택한 뒤 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/e9f02b468e39d2b78365514f91cb13d1.png)
17. CVM을 재시작합니다.


### 클라이언트 설정

1. 로컬 컴퓨터에서 <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img>를 우클릭하고 [실행]을 선택하여 실행 대화 상자를 엽니다.
2. 실행 대화 상자에 **gpedit.msc**를 입력한 뒤 [확인]을 클릭하여 '로컬 그룹 정책 편집기'를 엽니다.
3. 아래 이미지와 같이 왼쪽 디렉터리 트리에서 [컴퓨터 구성]>[관리 템플릿]>[Windows 구성 요소]>[원격 데스크톱 서비스]>[원격 데스크톱 연결 클라이언트]>[RemoteFx USB 장치 리디렉션]을 선택한 뒤, [이 컴퓨터에서 지원되는 기타 RemoteFx USB 장치의 RDP 리디렉션 허용]을 더블 클릭하여 엽니다.
![](https://main.qcloudimg.com/raw/760b413ec2fb3aec917716556875a99f.png)
4. 아래 이미지와 같이, 팝업 창에서 [사용]을 선택한 뒤 RemoteFx USB 리디렉션 액세스 권한을 [관리자 및 사용자]로 설정합니다.
![](https://main.qcloudimg.com/raw/a34da80ec13c8c041662b2c1142c931e.png)
5. [확인]을 클릭합니다.
6. 로컬 컴퓨터를 재시작합니다.

### 설정 효과 검증

1. 로컬 컴퓨터에 USB 장치를 삽입한 뒤, <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img>를 우클릭하고 [실행]을 선택하여 대화 상자를 엽니다.
2. 아래 이미지와 같이, 실행 대화 상자에 **mstsc**를 입력한 뒤 **Enter**를 눌러 원격 데스크톱 연결 대화 상자를 엽니다.
![](https://main.qcloudimg.com/raw/107284ef6b3548585f0598f419ec7b98.png)
3. [컴퓨터] 오른쪽 입력란에 Windows 서버의 공인 IP를 입력한 후 [옵션 표시]를 클릭합니다.
4. 아래 이미지와 같이, [로컬 리소스] 탭을 선택한 뒤 '로컬 장치 및 리소스' 메뉴의 [더 보기]를 클릭하면 로컬 장치 및 리소스 창이 팝업됩니다.
![](https://main.qcloudimg.com/raw/ab14993dae9d7c7bf22b9443c5badc13.png)
5. 팝업된 로컬 장치 및 리소스 창에서 [지원되는 다른 RemoteFx USB 장치]를 펼치고, 연결할 USB 장치를 선택한 다음 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/9c86c1ad14906f4e2566a26eceaf91de.png)
6. [연결]을 클릭합니다.
7. 아래 이미지와 같이, 팝업된 'Windows 보안' 창에서 인스턴스의 사용자 이름 및 암호를 입력합니다.
![](https://main.qcloudimg.com/raw/0a0ffbf1f09c8bac278d97adb9e5ac96.png)
8. [확인]을 클릭하고 Windows 인스턴스에 로그인합니다.
Windows 인스턴스의 작업 인터페이스 상단에 <img src="https://main.qcloudimg.com/raw/73fe2b3cfa740517e44e4596a222840a.png" style="margin: 0;"></img>가 나타난다면 설정 성공입니다.
![](https://main.qcloudimg.com/raw/751a4e2204cc38a0769116732c464789.png)


## 관련 작업

Windows RDP 프로토콜은 자주 사용하는 USB 장치에 더 최적화된 연결 기능을 제공하므로, RemoteFx 기능을 활성화하지 않아도 디스크 드라이버, 카메라 등의 디바이스를 바로 매핑할 수 있습니다. 자주 사용하지 않는 USB 장치의 경우 RemoteFX USB Redirection 기능을 사용해야 하며, 아래의 내용을 참조하여 해당하는 리디렉션 방법을 선택하시기 바랍니다.
![](https://main.qcloudimg.com/raw/715de06c08753eefe6e4ff5cc3bca270.png)

