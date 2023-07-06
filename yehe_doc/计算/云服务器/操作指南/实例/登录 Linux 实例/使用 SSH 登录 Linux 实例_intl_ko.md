## 작업 시나리오
본 문서는 SSH 키를 사용하여 로컬 Linux, Mac OS 또는 Windows 서버에서 Linux 인스턴스에 로그인하는 방법을 설명합니다.

## 지원 운영 체제
Linux, Mac OS 혹은 Windows(Windows 10 및 Windows Server 2019 버전)

## 인증 방식
**비밀번호** 또는 **키**

## 전제 조건
- 인스턴스에 로그인하기 위한 관리자 계정과 비밀번호(또는 키)가 이미 있습니다.
 - 기본 관리자 계정은 일반적으로 Linux 인스턴스의 경우 `root`이고 Ubuntu 시스템의 경우 `ubuntu`입니다. 실제 상황에 따라 수정할 수 있습니다.
 - 시스템 기본 비밀번호를 사용하여 인스턴스에 로그인하려면 먼저 [메시지 센터](https://console.cloud.tencent.com/message)로 이동하여 비밀번호를 받으십시오.
 - [키로 로그인](#LoginWithKey)하려면 키를 생성하여 이 CVM에 바인딩해야 합니다. 자세한 내용은 [SSH 키 관리](https://intl.cloud.tencent.com/document/product/213/16691)를 참고하십시오.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
- CVM 인스턴스를 위해 퍼블릭 IP를 구매했으며 포트 22가 열려 있습니다. 빠른 구성으로 구매한 CVM 인스턴스의 경우 기본적으로 열려 있습니다.

## 작업 단계
<dx-tabs>
::: 비밀번호로 로그인[](id:passwordLogin)
1. 다음 명령을 실행하여 Linux CVM에 연결합니다.
<dx-alert infotype="explain" title="">
- 로컬 컴퓨터가 Mac OS 시스템인 경우, 먼저 시스템과 함께 제공되는 터미널(Terminal)을 연 후에 다음의 명령을 실행해야 합니다.
- 로컬 컴퓨터가 Linux 시스템인 경우, 다음 명령을 바로 실행할 수 있습니다.
- 로컬 컴퓨터가 Windows 10 혹은 Windows Server 2019 시스템인 경우, 먼저 명령 프롬프트(CMD)를 연 후에 다음의 명령을 실행해야 합니다.
</dx-alert>
``` 
ssh <username>@<hostname or IP address>
```
 - `username`은 전제 조건에서 획득한 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 퍼블릭 IP 또는 사용자 정의 도메인 이름입니다.
2. 획득한 비밀번호를 입력하고 **Enter**를 누르면 로그인할 수 있습니다.

:::
::: 키로 로그인[](id:keyLogin)
1. 다음 명령을 실행하여 프라이빗 키 파일에 본인만 읽기 가능한 권한을 부여합니다.
 - 로컬 컴퓨터가 Mac OS 시스템인 경우, 먼저 시스템과 함께 제공되는 터미널(Terminal)을 연 후에 다음의 명령을 실행해야 합니다.
 - 로컬 컴퓨터가 Linux 시스템인 경우, 다음 명령을 바로 실행할 수 있습니다.
```
chmod 400 <CVM과 연결된 프라이빗 키의 다운로드 절대 경로>
```
 - 로컬 컴퓨터가 Windows 10 시스템인 경우, 먼저 명령 프롬프트(CMD)를 연 후에 다음의 명령을 순서대로 실행해야 합니다.
```
icacls <다운로드한 CVM과 연결된 개인키의 절대 경로> /grant <Windows 시스템 사용자 계정>:F
```
```
icacls <CVM과 연결된 프라이빗 키의 다운로드 절대 경로> /inheritancelevel:r
```
2. 다음 명령을 실행하여 원격으로 로그인합니다.
```
ssh -i <CVM과 연결된 프라이빗 키의 다운로드 절대 경로> <username>@<hostname or IP address>
```
 - `username`은 전제 조건에서 획득한 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 퍼블릭 IP 또는 사용자 정의 도메인 이름입니다.

 예를 들어, `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` 명령을 실행하여 Linux CVM에 원격 로그인합니다.
:::
</dx-tabs>

## 후속 작업

CVM에 로그인한 후 개인 웹사이트 또는 포럼을 구축하거나 기타 작업을 수행할 수 있습니다. 자세한 내용은 다음을 참고하십시오.
- [WordPress 개인사이트 매뉴얼 구축](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! 포럼 수동 구축](https://www.tencentcloud.com/document/product/213/8043)
