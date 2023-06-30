## 작업 시나리오

VNC 로그인은 사용자가 Web 브라우저를 통해 CVM에 원격으로 연결하도록 Tencent Cloud에서 제공하는 연결 방식입니다. 원격 로그인 클라이언트를 설치하지 않았거나 사용할 수 없는 경우 및 기타 방식으로도 모두 로그인할 수 없는 경우, VNC 로그인을 통해 CVM에 연결하여 CVM 상태를 모니터링하고, CVM 계정을 통해 기본적인 CVM 관리 작업을 실행할 수 있습니다.


## 사용 제한

- VNC로 로그인한 CVM은 복사 붙여넣기 기능, 중국어 입력기 및 파일 업로드/다운로드가 지원되지 않습니다.
- VNC로 CVM에 로그인할 때는 주요 브라우저를 사용해야 합니다. 예: Chrome, Firefox, IE 10 및 이후 버전 등.
- VNC 로그인은 전용 단말입니다. 즉 동시에 한 명의 사용자만 VNC를 사용해 로그인할 수 있습니다.

## 전제 조건
인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호를 보유하고 있어야 합니다.
- 인스턴스 생성 시 시스템에서 비밀번호 랜덤 생성을 선택했다면 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 비밀번호를 받으시기 바랍니다.
- 로그인 비밀번호가 설정되어 있는 경우 해당 비밀번호를 사용하여 로그인하시기 바랍니다. 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.


## 작업 단계

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
<dx-tabs>
::: 리스트 뷰
아래 이미지와 같이 로그인하려는 Linux CVM 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 탭 뷰
아래 이미지와 같이 로그인하려는 Linux CVM 탭을 선택하여 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. 아래 이미지와 같이 ‘표준 로그인 | Linux 인스턴스’ 창에서 **VNC 로그인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/1bd4877abc15d06adb8c54fc7ed1318e.png)
4. 창에서 ‘login’ 뒤에 사용자 이름을 입력한 후 **Enter**키를 누릅니다.
Linux 인스턴스의 기본 사용자 이름은 'root'이고 Ubuntu 시스템 인스턴스의 기본 사용자 이름은 'ubuntu'입니다. 필요에 따라 입력하십시오.
5. ‘Password’에 비밀번호를 입력한 후 **Enter**키를 누릅니다.
입력한 비밀번호는 기본적으로 표시되지 않으며, 로그인이 완료되면 아래 이미지와 같이 명령 프롬프트 왼쪽에 현재 CVM에 로그인한 정보가 표시됩니다.
![](https://main.qcloudimg.com/raw/03a8492f66e8342221858709b6068669.png)


## 후속 작업


CVM에 로그인 성공하면, Tencent CVM에서 개인 사이트, 포럼을 구축할 수 있으며 다른 작업 또한 진행할 수 있습니다. 관련 작업 방법은 아래의 내용을 참고하십시오.
-  [Linux 일상 작업 및 명령어](https://intl.cloud.tencent.com/document/product/213/2150) 
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/zh/document/product/213/8044)
- [Discuz! 포럼 구축](https://intl.cloud.tencent.com/zh/document/product/213/8043)

