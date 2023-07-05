## 작업 시나리오

WebShell은 Tencent cloud에서 권장하는 로그인 방식입니다. 로컬 시스템이 Windows, Linux 또는 Mac OS이든 인스턴스가 공용 네트워크 IP를 구매한 경우, 모두 WebShell을 통해서 로그인할 수 있습니다. 본 문서는 표준 로그인 방법(WebShell)을 사용하여 Linux 인스턴스에 로그인하는 방법에 대해 설명합니다.
WebShell의 장점은 다음과 같습니다.
- 일괄 복사 및 붙여 넣기를 지원합니다.
- 마우스 스크롤을 지원합니다.
- 중국어 입력을 지원합니다.
- 보안성이 높아 로그인할 때마다 비밀번호 또는 키를 입력해야 합니다.

## 로컬 작업 시스템에 적용

Window，Linux 또는 Mac OS

## 인증 방식

**비밀번호**또는**키**

## 전제 조건

- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 키)를 얻으십시오.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)에 이동하여 획득하십시오.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하십시오.
- 클라우드 서버 인스턴스가 이미 공용 IP를 구매한 경우 해당 인스턴스가 이미 클라우드 서버 인스턴스의 22번 포트가 활성화되어 있습니다(빠른 구성을 통해 구매한 클라우드 서버 인스턴스는 기본적으로 활성화 상태입니다).

## 작업 순서

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오.
2. 인스턴스 관리페이지에서 로그인해야하는 Linux CVM을 선택하고 [로그인]을 클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3.[Linux 인스턴스 로그인]창에서 [표준 로그인 방식]을 선택하고,[즉시 로그인]을 클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
4. Webshell 로그인 페이지에서, 실제 요구사항에 따라 [비밀번호 로그인] 또는 [키 로그인] 방식을 선택하여 로그인하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/87ba7e511f8d0ffe48f220cecaa7b057.png)
로그인에 성공하면, WebShell 인터페이스에 Socket connection established가 표시됩니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)
## 후속 작업

클라우드 서버에 로그인 성공하면, Tencent 클라우드 서버에서 개인 사이트, 포럼을 구축할 수 있고, 다른 작업을 사용할 수 있습니다. 관련 작업 방법은 아래의 내용을 참조하십시오.
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/document/product/213/8044)

