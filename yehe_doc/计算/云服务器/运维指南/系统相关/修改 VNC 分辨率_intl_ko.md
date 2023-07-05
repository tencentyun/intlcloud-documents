## 작업 시나리오
본문은 CVM 콘솔을 통해 VNC 로그인 시 인스턴스의 디스플레이 해상도를 조정하는 방법을 설명합니다.

Windows 시스템 이미지의 경우 VNC 해상도가 너무 낮으면 일부 항목의 정상적인 표시에 영향을 미치거나 일부 애플리케이션이 열리지 않을 수 있습니다. 해상도를 수정하여 이러한 문제를 방지할 수 있습니다.
일부 Linux 시스템 이미지의 VNC의 기본 디스플레이 해상도는 더 낮습니다. 예를 들어 CentOS 6의 VNC의 기본 해상도는 720 \* 400에 불과합니다. grub 매개변수를 수정하여 Linux 시스템 이미지의 VNC 해상도를 1024 \* 768로 설정할 수 있습니다.
<dx-alert infotype="explain" title="">
CentOS 7, CentOS 8, Ubuntu, Debian 9.0 등 최신 시스템 이미지와 같은 다양한 유형의 Linux 시스템 이미지가 있습니다. VNC의 기본 해상도는 1024 \* 768이며 VNC 해상도를 수정할 필요가 없습니다.
</dx-alert>












## 전제 조건
VNC를 사용하여 인스턴스에 로그인했습니다. 로그인하지 않은 경우 다음 문서를 참고하여 진행할 수 있습니다.
 - [VNC로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)
 - [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)


## 작업 단계

<dx-tabs>
::: Windows 인스턴스
<dx-alert infotype="explain" title="">
본문은 Windows Server 2012 중국어 버전 시스템 이미지를 예로 들어 Windows 인스턴스의 VNC 해상도를 수정하는 방법을 안내합니다.
</dx-alert>



1. 운영 체제 인터페이스에서 마우스 오른쪽 버튼을 클릭하여 **화면 해상도**를 선택합니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
2. 열린 화면 해상도 창에서 **해상도**의 크기를 설정하고 **적용**을 클릭합니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
3. 팝업 창에서 **보관**을 클릭합니다.
4. **확인**을 클릭하여 화면 해상도 창을 비활성화합니다.


:::
::: Linux 인스턴스

본문은 CentOS 6 및 Debian 7.8을 예시로 VNC 해상도를 변경하는 방법을 안내합니다.


#### CentOS 6

CentOS 6 시스템 이미지의 경우 VNC의 기본 해상도는 720 \* 400입니다. grub 실행 매개변수를 수정하여 VNC 해상도를 1024 \* 768로 설정할 수 있습니다. 다음과 같이 설정됩니다.
1. 운영 체제 인터페이스에서 다음 명령어를 실행하여 `grub.conf` 파일을 엽니다.
```
vim /etc/grub.conf
```
2. **i**를 눌러 편집 모드로 전환하고 `vga=792`를 `grub` 매개변수 값에 추가합니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 다음 명령어를 실행하여 CVM을 재시작합니다.
```
reboot
```



#### Debian 7.8

Debian 7.8 및 Debian 8.2 시스템 이미지의 기본 VNC 해상도는 720 \* 400입니다. grub 실행 매개변수를 수정하여 VNC 해상도를 1024 \* 768로 설정할 수 있습니다. 다음과 같이 설정됩니다.
1. 운영 체제 인터페이스에서 다음 명령어를 실행하여 grub 파일을 엽니다.
```
vim /etc/default/grub
```
2. **i**를 눌러 편집 모드로 전환하고 `GRUB_CMDLINE_LINUX_DEFAULT` 매개변수 값 뒤에 `vga=792`를 추가합니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 다음 명령어를 실행하여 `grub.cfg` 파일을 업데이트합니다.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
5. 다음 명령어를 실행하여 CVM을 재시작합니다.
```
reboot
```

:::
</dx-tabs>



## 부록

Linux 인스턴스 해상도와 VGA의 매개변수 비교표는 다음과 같습니다.
<table>
	<tr><th>해상도</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
