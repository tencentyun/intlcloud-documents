## 작업 시나리오

일부 Linux 시스템 이미지의 경우 VNC 기본 디스플레이 해상도가 낮습니다(예: CentOS 6의 경우 VNC 기본 해상도가 720 \* 400에 불과). grub 매개변수를 수정하여 Linux 시스템 이미지의 VNC 해상도를 1024 \* 768로 설정할 수 있습니다.
Window 시스템 이미지의 경우, VNC 해상도가 너무 낮으면 일부 프로젝트가 정상적으로 표시되지 않거나 일부 애플리케이션을 열 수 없게 됩니다. 해상도를 변경하여 이러한 문제를 해결할 수 있습니다.

본 문서는 CVM의 VNC 디스플레이 해상도를 변경하는 방법을 소개합니다.

## 작업 순서

### Windows 인스턴스의 VNC 해상도 변경

> 아래는 Windows Server 2012 중국어 버전의 운영 체제 이미지를 예로 들어, 인스턴스의 VNC 해상도를 변경하는 방법에 대해 안내합니다.
>

1. [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)합니다.
2. 아래 이미지와 같이 운영 체제 인터페이스에서 우클릭 후, [디스플레이 해상도]를 선택합니다.
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. 아래 이미지와 같이 열린 디스플레이 해상도 창에서 [해상도]의 크기를 설정하고 [적용]을 클릭합니다.
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. 팝업된 대화 상자에서 [변경 유지]를 클릭합니다.
5. [확인]을 클릭하고 디스플레이 해상도 창을 닫습니다.

### Linux 인스턴스의 VNC 해상도 변경

Linux 시스템 이미지는 다양한 유형이 있으며, 그중에서도 CentOS 7, CentOS 8, Ubuntu, Debian 9.0 등 비교적 최신 버전의 시스템 이미지의 경우 VNC 기본 해상도가 1024 \* 768이므로, VNC 해상도를 변경하지 않아도 됩니다. 아래는 CentOS 6, Debian 7.8을 예로 들어 VNC 해상도를 변경하는 방법에 대해 안내합니다.

#### CentOS 6

CentOS 6 시스템 이미지의 VNC 기본 디스플레이 해상도는 720 \* 400입니다. grub 시작 매개변수를 수정하여 VNC 해상도를 1024 \* 768로 설정할 수 있으며, 설정 방법은 아래와 같습니다.
1. [표준 방식으로 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수 있습니다.
 - [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
 - [SSH를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
 - [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)
2. 운영 체제 인터페이스에서 다음 명령어를 실행하여 `grub.conf` 파일을 엽니다.
```
vim /etc/grub.conf
```
3. 아래 이미지와 같이 **i** 를 눌러 편집 모드로 전환한 후 `grub` 매개변수 값 뒤에 에서 `vga=792`를 추가합니다.
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 후 돌아갑니다.
5. 다음 명령어를 실행하여 CVM을 재시작합니다.
```
reboot
```

#### Debian 7.8

Debian 7.8과 Debian 8.2 시스템 이미지의 VNC 기본 해상도는 720 \* 400입니다. grub 시작 매개변수를 수정하여 VNC 해상도를 1024 \* 768로 설정할 수 있으며, 설정 방법은 아래와 같습니다.
1. [표준 방식으로 Linux 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436). 실제 작업 스타일에 따라 다른 로그인 방식을 선택할 수 있습니다.
 - [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
 - [SSH를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
 - [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)
2. 운영 체제 인터페이스에서 다음 명령어를 실행하여 grub 파일을 엽니다.
```
vim /etc/default/grub
```
3. 아래 이미지와 같이 **i** 를 눌러 편집 모드로 전환한 후 `GRUB_CMDLINE_LINUX_DEFAULT` 매개변수 값 뒤에 `vga=792`를 추가합니다.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 후 돌아갑니다.
5. 다음 명령어를 실행하여 `grub.cfg` 파일을 업데이트합니다.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. 다음 명령어를 실행하여 CVM을 재시작합니다.
```
reboot
```


## 부록

해상도와 VGA의 매개변수 대조표는 아래와 같습니다.
<table>
	<tr><th>해상도</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
