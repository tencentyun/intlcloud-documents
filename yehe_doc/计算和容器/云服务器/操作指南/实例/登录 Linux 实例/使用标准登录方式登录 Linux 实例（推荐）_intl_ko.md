## 작업 시나리오
WebShell은 Tencent cloud에서 권장하는 로그인 방식입니다. 로컬 시스템이 Windows, Linux 또는 Mac OS이든 인스턴스가 공용 IP를 구매한 경우, 모두 WebShell을 통해서 로그인할 수 있습니다. 본문은 표준 로그인 방법(WebShell)을 사용하여 Linux 인스턴스에 로그인하는 방법에 대해 설명합니다.
WebShell의 장점은 다음과 같습니다.
- 일괄 복사 및 붙여 넣기를 지원합니다.
- 마우스 스크롤을 지원합니다.
- 중국어 입력을 지원합니다.
- 보안성이 높아 로그인할 때마다 비밀번호 또는 키를 입력해야 합니다.

## 인증 방식

**비밀번호** 또는 **보안키**

## 전제 조건[](id:Prerequisites)

- Linux 인스턴스에 로그인하기 위한 관리자 계정 및 비밀번호(또는 키)를 획득한 상태여야 합니다.
 - 인스턴스 생성 시 시스템에서 비밀번호 랜덤 생성을 선택했다면 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 비밀번호를 받으시기 바랍니다.
 - 로그인 비밀번호가 설정되어 있는 경우 해당 비밀번호를 사용하여 로그인하시기 바랍니다. 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
 - 인스턴스에 키가 바인딩되어 있는 경우 해당 키를 사용하여 로그인할 수 있습니다. 키에 대한 자세한 설명은 [SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)를 참고하시기 바랍니다.
- CVM 인스턴스에서 공용 IP를 구매하였고, WebShell 프록시 IP가 소스인 원격 로그인 포트(기본값: 22)가 인스턴스와 연결된 보안 그룹에서 개방되어있어야 합니다.
 - 빠른 구성을 통해 CVM을 구매하시면 기본적으로 이미 활성화되어 있습니다.
 -  사용자 정의 설정을 통해 CVM을 구매한 경우 [SSH를 통한 Linux CVM 원격 연결 허용](https://intl.cloud.tencent.com/document/product/213/32369)을 참고하여 수동으로 개방합니다.

## 작업 단계

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
<dx-tabs>
::: 리스트 뷰
다음 이미지와 같이 로그인하려는 Linux CVM 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 탭 뷰
다음 이미지와 같이 로그인하려는 Linux CVM 탭을 선택하여 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>

3. 다음 이미지와 같이 ‘표준 로그인 | Linux 인스턴스’ 창에서 실제 요구사항에 따라 **비밀번호 로그인** 또는 **키 로그인** 방식을 선택하여 로그인합니다.
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
다음 설명을 참고하여 로그인에 필요한 정보를 입력하십시오.
 -  **포트**: 기본값은 22이며 필요에 따라 입력하십시오.
 -  **사용자 이름**: Linux 인스턴스 사용자 이름은 기본적으로 root(Ubuntu 시스템 인스턴스 사용자 기본 이름은 ubuntu)이며 필요에 따라 입력하십시오.
 -  **비밀번호**: [전제 조건](#Prerequisites) 단계에서 얻은 로그인 비밀번호를 입력합니다.
 - **키**: 바인딩된 인스턴스의 키를 선택합니다.
4. **로그인**을 클릭하여 Linux 인스턴스에 로그인합니다.
다음 이미지와 같이 로그인에 성공하면, WebShell 인터페이스에 다음과 같은 안내가 표시됩니다.
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## 후속 작업

CVM에 로그인 성공하면, Tencent CVM에서 개인 사이트, 포럼을 구축할 수 있으며 다른 작업 또한 진행할 수 있습니다. 관련 작업 방법은 아래의 내용을 참고하십시오.
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! 포럼 구축](https://intl.cloud.tencent.com/document/product/213/8043)


## 관련 문서
- [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)
- [SSH 키 관리](https://intl.cloud.tencent.com/document/product/213/16691)
