## 작업 시나리오

본 문서에서는 Linux, Mac OS 혹은 Windows 시스템의 로컬 컴퓨터에서 SSH를 통해 Linux 인스턴스에 로그인하는 방법을 소개합니다.

## 로컬 운영 체제에 적용

Linux, Mac OS 혹은 Windows(Windows 10 및 Windows Server 2019 버전)

## 인증 방식

**비밀번호** 또는 **보안키**

## 전제 조건
- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 보안키)를 보유하고 있어야 합니다.
 - Linux 인스턴스 관리자 계정의 기본 설정은 `root`, Ubuntu 시스템 기본 설정은 `ubuntu`입니다. 실제 상황에 따라 수정하십시오.
 - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
 - 인스턴스에 [키를 사용하여 로그인](#LoginWithKey)하려면 키가 생성되어 있어야 하며 해당 CVM에 바인딩된 상태여야 합니다. 자세한 작업 방식은 [SSH 키](https://intl.cloud.tencent.com/document/product/213/16691)를 참조하십시오.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하십시오.
- CVM 인스턴스가 공용 IP를 구매하였고 해당 인스턴스가 CVM 인스턴스의 22번 포트를 활성화한 상태여야 합니다(빠른 구성을 통해 구매한 클라우드 서버 인스턴스는 기본적으로 활성화 상태입니다).

## 작업 순서
<dx-tabs>
::: 비밀번호를 사용하여 로그인하기 [](id:passwordLogin)
1. 다음 명령어를 실행하여 Linux CVM에 연결합니다.
<dx-alert infotype="explain" title="">
- 로컬 컴퓨터가 Mac OS 시스템이라면 먼저 시스템 자체의 터미널(Terminal)을 연 후에 다음의 명령어를 실행해야 합니다.
- 로컬 컴퓨터가 Linux 시스템이라면 바로 다음의 명령어를 실행할 수 있습니다.
- 로컬 컴퓨터가 Windows 10 혹은 Windows Server 2019 시스템이라면 먼저 명령 프롬프트(CMD)를 연 후에 다음의 명령어를 실행해야 합니다.
</dx-alert>
```
ssh <username>@<hostname or IP address>
```
 - `username`은 전제 조건에서 획득한 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 공용 IP 또는 사용자 정의 도메인 이름입니다.
2. 획득한 비밀번호를 입력하고 **Enter**를 누르면 로그인할 수 있습니다.

:::
::: 보안키를 사용하여 로그인하기 [](id:LoginWithKey)

1. 다음 명령어를 실행하여 개인키 파일에 본인만 읽기 가능한 권한을 부여합니다.
 - 로컬 컴퓨터가 Mac OS 시스템이라면 먼저 시스템 자체의 터미널(Terminal)을 연 후에 다음의 명령어를 실행해야 합니다.
 - 로컬 컴퓨터가 Linux 시스템이라면 바로 다음의 명령어를 실행할 수 있습니다.
```
chmod 400 <CVM과 연결된 개인키의 다운로드 절대 경로>
```
 - 로컬 컴퓨터가 Windows 10 시스템이라면 먼저 명령 프롬프트(CMD)를 연 후에 다음의 명령어를 순서대로 실행해야 합니다.
```
icacls <다운로드한 CVM과 연결된 개인키의 절대 경로> /grant <Windows 시스템 사용자 계정>:F
```
```
icacls <CVM과 연결된 개인키의 다운로드 절대 경로> /inheritancelevel:r
```
2. 다음 명령어를 실행하여 원격으로 로그인합니다.
```
ssh -i <CVM과 연결된 개인키의 다운로드 절대 경로> <username>@<hostname or IP address>
```
 - `username`은 전제 조건에서 획득한 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 공용 IP 또는 사용자 정의 도메인 이름입니다.

 예를 들어, `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` 명령어를 실행하여 Linux CVM에 원격 로그인합니다.
:::
</dx-tabs>

## 후속 작업

CVM에 로그인을 성공하면, Tencent CVM에서 개인 사이트, 포럼을 구축할 수 있으며 다른 작업 또한 진행할 수 있습니다. 관련 작업 방법은 아래의 내용을 참조하십시오.
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! 포럼 구축](https://intl.cloud.tencent.com/document/product/213/8043)


