## 작업 시나리오

본 문서는 Linux 또는 Mac OS 시스템의 로컬 컴퓨터에서 SSH를 통해 Linux 인스턴스에 로그인하는 방법을 소개합니다.

## 로컬 운영 체제에 적용

Linux 또는 Mac OS

## 인증 방식

**비밀번호** 또는 **키**

## 전제 조건
- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 키)를 획득한 상태.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)에 이동하여 획득 바랍니다.
 - 사용자가 인스턴스에 [키를 사용하여 로그인](#LoginWithKey)할 경우, 키를 생성하고 해당 CVM에 바인딩해야 합니다. 자세한 작업 내용은 [SSH 키](http://intl.cloud.tencent.com/document/product/213/16691)를 참조 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 리셋](http://intl.cloud.tencent.com/document/product/213/16566)하세요.
- 사용자의 CVM 인스턴스가 공용 IP를 구매하였고, 해당 인스턴스가 이미 CVM 인스턴스의 22번 포트를 활성화한 상태(빠른 구성을 통해 구매한 CVM 인스턴스는 기본적으로 활성화 상태입니다).

## 작업 순서

### 비밀번호를 사용하여 로그인

1. 다음 명령어를 실행하여 Linux CVM에 연결합니다.
> 사용자의 로컬 컴퓨터가 Mac OS 시스템인 경우, 먼저 시스템 자체의 터미널(Terminal)을 열고 다음 명령어를 실행해야 합니다.
> 사용자의 로컬 컴퓨터가 Linux 시스템인 경우, 다음 명령어를 바로 실행할 수 있습니다.
>
```
ssh <username>@<hostname or IP address>
```
 - `username` 은 전제 조건에서 얻은 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 공인 IP 또는 사용자 정의 도메인 이름입니다.
2. 이미 획득한 비밀번호를 입력하고 **Enter**를 눌러 로그인을 완료합니다.

<span id="LoginWithKey"></span>
### 키를 사용하여 로그인

1. 아래 명령어를 실행하여 프라이빗 키 파일에 본인만 읽기 가능 권한을 부여합니다.
> 사용자의 로컬 컴퓨터가 Mac OS 시스템인 경우, 먼저 시스템 자체의 터미널(Terminal)을 열고 다음 명령어를 실행해야 합니다.
> 사용자의 로컬 컴퓨터가 Linux 시스템인 경우, 다음 명령어를 바로 실행할 수 있습니다.
>
```
chmod 400 <다운로드한 CVM과 연결된 프라이빗 키의 절대 경로>
```
2. 다음 명령어를 실행하여 원격 로그인합니다.
```
ssh -i <다운로드한 CVM과 연결된 프라이빗 키의 절대 경로> <username>@<hostname or IP address>
```
 - `username` 은 전제 조건에서 얻은 기본 계정입니다.
 - `hostname or IP address`는 사용자의 Linux 인스턴스 공인 IP 또는 사용자 정의 도메인 이름입니다.

 예시,  `ssh -i "Mac/Downloads/shawn_qcloud_stable" ubuntu@192.168.11.123` 명령어를 실행하여 Linux CVM에 원격 로그인합니다.
