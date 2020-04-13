## 작업 시나리오

VNC 로그인은 사용자가 Web 브라우저를 통해 CVM에 원격으로 연결하도록 Tencent Cloud에서 제공하는 연결 방식입니다. 원격 로그인 클라이언트를 설치하지 않았거나 사용할 수 없는 경우 및 기타 방식으로도 모두 로그인할 수 없는 경우, VNC 로그인을 통해 CVM에 연결하여 CVM 상태를 모니터링하고, CVM 계정을 통해 기본적인 CVM 관리 작업을 실행할 수 있습니다.

## 사용 제한

- VNC로 로그인한 CVM은 복사 붙여넣기 기능, 중국어 입력법과 파일 업로드 및 다운로드를 현재는 지원하지 않습니다.
- VNC로 CVM에 로그인할 때는 주요 브라우저를 사용해야 합니다. 예: Chrome, Firefox, IE 10 및 이상 버전 등.
- VNC 로그인은 전용 단말입니다. 즉 동시에 한 명의 사용자만 VNC를 사용해 로그인할 수 있습니다.

## 로컬 운영 체제에 적용

Window，Linux 및 Mac OS

## 전제 조건

Windows 인스턴스에 원격 로그인할 때 사용해야 하는 인스턴스의 관리자 계정과 비밀번호를 획득한 경우.
- 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)에 이동하여 획득 바랍니다.
- 비밀번호를 잊으신 경우, [인스턴스 비밀번호 리셋](http://intl.cloud.tencent.com/document/product/213/16566)하세요.

## 작업 순서

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 로그인이 필요한 Windows CVM을 선택하고 [Log In]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods (VNC)]을 선택하고 [Log In Now]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)



