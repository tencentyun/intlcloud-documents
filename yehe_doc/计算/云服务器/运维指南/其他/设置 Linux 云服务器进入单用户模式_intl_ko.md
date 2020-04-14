## 작업 시나리오

Linux 사용자는 때로 단일 사용자 모드로 진입하여 몇 가지 특수 작업을 실행해야 합니다. 이는 비밀번호 관리 통제, sshd 손상 등을 예로 들 수 있습니다. 본 문서는 주요 Linux 운영 체제의 단일 사용자 모드 진입에 대한 작업 순서를 소개합니다.

## 작업 순서

### 운영 체제 유형 판단

운영 체제 유형에 맞는 작업 순서를 선택합니다.
 - CentOS 6 운영 체제는 [CentOS 6 의 순서](#configCentOS6)를 실행합니다.
 - CentOS 7 운영 체제는 [CentOS 7 의 순서](#configCentOS7)를 실행합니다.
 - Ubuntu 운영 체제는 [Ubuntu 의 순서](#configUbuntu)를 실행합니다.

<span id="configCentOS6"></span>
### CentOS 6

>? Centos 6은 GRUB를 사용하여 가이드 프로그램을 실행합니다. 다음의 작업 순서는 CentOS 6.9를 예로 들며, 운영 체제 버전에 따라 세부 작업 순서에 약간의 차이가 있습니다.
> 
1. CVM 인스턴스에 원격 로그인합니다.
2. 다음 명령어를 실행하여 `/etc/grub.conf` 파일을 엽니다.
```
vi /etc/grub.conf
```
3. **I** 를 눌러 편집 모드로 진입합니다.
4. "GRUB_TIMEOUT" 실행 항목 대기 시간의 매개변수 기본 값을 조회하고, 실제 수요에 따라 해당 값을 설정 범위 내로 수정합니다.
"GRUB_TIMEOUT" 기본 값은 5초입니다. 대기 시간이 너무 짧아 시작 인터페이스를 보지 못하는 경우를 방지하기 위해, 60초 혹은 더 긴 시간으로 조정하시기 바랍니다.
>! 해당 항목은 시스템의 실행 시간에 영향을 주므로, 설정을 완료한 후 이를 다시 기본 값으로 수정해야 합니다.
5. **Esc**를 눌러 편집 모드에서 나간 후 **:wq**를 입력하고 **Enter**를 누릅니다.
설정을 저장하고 VI 편집기에서 나갑니다.
6. 다음 명령어를 실행하여 서버를 재시작합니다.
```
reboot
```
7. 약 1분간 기다린 후 [VNC로 해당 CVM 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)합니다. 로그인 인터페이스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/82a82601e1545274c4f61c8f34f5c100.png)
8. 아무 키를 눌러 메뉴에 진입합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/6336b8fd579799108a5765b5b58e2a21.png)
9. **e**를 눌러 커널 편집 인터페이스에 진입하고 **single**을 입력합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/14168276d81a398702e80f9c83186869.png)
10. **Enter**를 누릅니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/149eeb5776329a5db1ea42ae20cd316d.png)
11. 다음 그림과 같이 인터페이스에서 **b**를 눌러 단일 사용자 모드에 진입합니다.
![](https://main.qcloudimg.com/raw/2d6d53de84cd78b3e88319b8538cec8e.png)
12. 다음 명령어를 실행하여 단일 사용자 모드에서 나갑니다.
```
exec /sbin/init
```

<span id="configCentOS7"></span>
### CentOS 7

>? CentOS 6과 달리 CentOS 7 이후 버전은 GRUB 2를 사용합니다. 다음의 작업 순서는 Centos 7.5를 예로 들며, 운영 체제 버전에 따라 세부 작업 순서에 약간의 차이가 있습니다.
> 
1. CVM 인스턴스에 원격 로그인합니다.
2. 다음 명령어를 실행하여 `/etc/default/grub` 파일을 엽니다.
```
vi /etc/default/grub
```
3. **I** 를 눌러 편집 모드로 진입합니다.
4. "GRUB_TIMEOUT" 실행 항목 대기 시간의 매개변수 기본 값을 조회하고, 실제 수요에 따라 해당 값을 설정 범위 내로 수정합니다. 아래 그림 참조
"GRUB_TIMEOUT" 기본 값은 5초입니다. 대기 시간이 너무 짧아 시작 인터페이스를 보지 못하는 경우를 방지하기 위해, 60초 혹은 더 긴 시간으로 조정하시기 바랍니다.
>! 해당 항목은 시스템의 실행 시간에 영향을 주므로, 설정을 완료한 후 이를 다시 기본 값으로 수정해야 합니다.
>
![](https://main.qcloudimg.com/raw/5ee3b8d8a4609ca846e3c1e929608b34.png)
5. **Esc**를 눌러 편집 모드에서 나간 후 **:wq**를 입력하고 **Enter**를 누릅니다.
설정을 저장하고 VI 편집기에서 나갑니다.
6. 다음 명령어를 실행하여 grub.cfg 파일을 다시 컴파일링 및 생성합니다.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
리턴 결과는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/62da54e985f2f78efce045bb2da1e5e5.png)
7. 다음 명령어를 실행하여 서버를 재시작합니다.
```
reboot
```
8. 약 1분간 기다린 후 [VNC로 해당 CVM 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)합니다. 로그인 인터페이스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/95dba957dea2da680ffca516dc2b62b3.png)
9. **e**를 눌러 커널 편집 인터페이스에 진입하고 **init=/bin/sh**를 붉은 테두리 부분에 추가합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/81173f4c723809f1b733a51a2eb002d5.png)
7. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/b9004e2a1d58a9a09316cf2a8a907399.png)
8. 다음 명령어를 실행하여 단일 사용자 모드에서 나갑니다.
```
exec /sbin/init
```

<span id="configUbuntu"></span>
### Ubuntu 

>? 다음 작업 순서는 Ubuntu 16.04를 예로 들며, 운영 체제 버전에 따라 세부 작업 순서에 약간의 차이가 있습니다.
>
1. CVM 인스턴스에 원격 로그인합니다.
2. 다음 명령어를 실행하여 `/etc/default/grub` 파일을 엽니다.
```
sudo vi /etc/default/grub
```
3. **I** 를 눌러 편집 모드로 진입합니다.
4. "GRUB_TIMEOUT" 실행 항목 대기 시간의 매개변수 기본 값을 조회하고, 실제 수요에 따라 해당 값을 설정 범위 내로 수정합니다. 아래 그림 참조
"GRUB_TIMEOUT" 기본 값은 5초입니다. 대기 시간이 너무 짧아 시작 인터페이스를 보지 못하는 경우를 방지하기 위해, 60초 혹은 더 긴 시간으로 조정하시기 바랍니다.
>! 
> - 해당 항목은 시스템의 실행 시간에 영향을 주므로, 설정을 완료한 후 이를 다시 기본 값으로 수정해야 합니다.
> - Ubuntu의 계정 기본 값은 비root입니다. sudo 명령어 사용에 유의하세요.
> 
```
sudo vi /etc/default/grub
```
![](https://main.qcloudimg.com/raw/65553c2d5a01113e33b93caa93485dae.png)
3. 다음 명령어를 실행하여 grub.cfg 파일을 다시 컴파일링 및 생성합니다.
```
sudo update-grub
```
리턴 결과는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/9e685185ef67e7129ce34b11b5a16061.png)
4. 다음 명령어를 실행하여 서버를 재시작합니다.
```
sudo reboot
```
5. 약 1분간 대기한 후 [VNC로 해당 CVM 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436#.E4.BD.BF.E7.94.A8-vnc-.E7.99.BB.E5.BD.95.E5.AE.9E.E4.BE.8B)합니다. 로그인 인터페이스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/4893e2a2ed32bbe4241b33b468bdb8cf.png)
6. **e**를 눌러 커널 편집 인터페이스에 진입하고 **rw single init=/bin/bash**를 붉은 테두리 부분에 추가합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/0879dd0c8c7a720542352a0722f9b9a7.png)
7. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/ffc6c3cf07a9254fdcb4f6326c3daf75.png)

