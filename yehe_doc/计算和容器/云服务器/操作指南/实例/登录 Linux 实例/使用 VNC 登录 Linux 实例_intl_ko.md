## 작업 시나리오


VNC 로그인은 사용자가 Web 브라우저를 통해 CVM에 원격으로 연결하도록 Tencent Cloud에서 제공하는 연결 방식입니다. 원격 로그인 클라이언트를 설치하지 않았거나 사용할 수 없는 경우 및 기타 방식으로도 모두 로그인할 수 없는 경우, VNC 로그인을 통해 CVM에 연결하여 CVM 상태를 모니터링하고, CVM 계정을 통해 기본적인 CVM 관리 작업을 실행할 수 있습니다.

## 로컬 운영 체제에 적용

Windows, Linux 및 Mac OS 시스템

## 사용 제한

- VNC로 로그인한 CVM은 복사 붙여넣기 기능, 중국어 입력법과 파일 업로드 및 다운로드를 현재는 지원하지 않습니다.
- VNC로 CVM에 로그인할 때는 주요 브라우저를 사용해야 합니다. 예: Chrome, Firefox, IE 10 및 이상 버전 등.
- VNC 로그인은 전용 단말입니다. 즉 동시에 한 명의 사용자만 VNC를 사용해 로그인할 수 있습니다.

## 전제 조건
인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 키)를 획득한 경우.
- 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)에 이동하여 획득 바랍니다.
- 비밀번호를 잊으신 경우, [인스턴스 비밀번호 리셋](http://intl.cloud.tencent.com/document/product/213/16566)하세요.

## 작업 순서

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 로그인이 필요한 Linux CVM을 선택하고 [로그인]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. 팝업된 [Linux 인스턴스 로그인] 창에서 [Alternative login methods(VNC)]을 선택하고 [Log In Now]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/1bd4877abc15d06adb8c54fc7ed1318e.png)
4. 팝업된 대화창에서 사용자 이름과 비밀번호를 입력하면 바로 로그인할 수 있습니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/03a8492f66e8342221858709b6068669.png)

