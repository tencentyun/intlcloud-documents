## 작업 시나리오
Linux 사용자는 일부 시나리오에서 단일 사용자 모드로 특수 작업 또는 점검 관련 작업을 진행해야 합니다. 예를 들어, 비밀번호 관리, sshd 손상 복구 또는 디스크 마운트 전에 해야하는 점검 등은 단일 사용자 모드로 진행해야 합니다. 본 문서에서는 주요 Linux 운영 체제의 단일 사용자 모드 진입 작업 순서를 소개합니다.

## 작업 순서
1. CVM 콘솔에서 VNC로 CVM에 로그인합니다. 자세한 내용은 [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참조하십시오.
2. VNC 로그인 인터페이스에서 좌측 상단의 [원격 명령어 전송]>[Ctrl-Alt-Delete]을 선택하고, 팝업창에서 [확인]을 클릭합니다.
3. 연결 실패 알림 정보가 뜨면 빠르게 페이지를 새로고침하고 위, 아래 화살표 버튼(↑↓)을 눌러 시스템이 grub 메뉴에 멈추어 있도록 합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/350187ce0a771d00e6d54e929291ebae.png)
4. **e** 를 눌러 grub 모드로 진입합니다.
5. grub 모드 진입 후 실제 사용하고 있는 운영 체제 유형에 맞는 작업 순서를 선택합니다.
<dx-tabs>
::: CentOS\s6.x
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/5abc9f57184cc74bba927513fb1c4a88.png)
2. **e** 을 눌러 커널 편집 인터페이스로 이동한 뒤 ↑↓ 버튼을 사용해 **kernel**이 있는 행을 선택하고 다시 **e**를 누릅니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/1a596a48df87d1d619e415d8d5b0cb65.png)
3. 행의 맨 끝에 **single**을 입력합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/e1f74a4ce211a34301c4f74ffcc790b8.png)
4. **Enter**를 눌러 입력을 완료한 뒤 **b**를 눌러 선택한 실행 명령어를 실행하면 단일 사용자 모드로 진입합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/b379937bfc15e93f0823ec50095d1dc6.png)
다음 그림과 같이 단일 사용자 모드로 진입하였습니다.
![](https://main.qcloudimg.com/raw/517c4d2c24864f3fc8f5002bd1e2c2a1.png)
<dx-alert infotype="explain" title="">
 `exec /sbin/init` 명령을 실행하면 단일 사용자 모드가 종료됩니다.
</dx-alert>
:::
::: CentOS\s7.x
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/2ddc7d1e4416d9fa763922e23b59d580.png)
2. **e**를 눌러 커널 편집 인터페이스로 들어간 뒤, ↑↓ 버튼으로 linux16의 첫번째 항으로 이동해 `ro`를 `rw init=/bin/bash` 또는 `/usr/bin/bash`로 바꿉니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/1b861ba0ecee1cd82da4364523e8a1c6.png)
3. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다.
다음 그림과 같이 단일 사용자 모드로 진입하였습니다.
![](https://main.qcloudimg.com/raw/fbe8cfcf43aa4c914882edc4c3ee5faf.png)
<dx-alert infotype="explain" title="">
 `exec /sbin/init` 명령을 실행하면 단일 사용자 모드가 종료됩니다.
</dx-alert>
:::
::: CentOS\s8.0
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/a6ce701e5845141929d822635bd42b9a.png)
2. **e**를 눌러 커널 편집 인터페이스로 들어간 뒤, ↑↓ 버튼으로 linux의 첫번째 항으로 이동해 `ro`를 `rw init=/sysroot/bin/bash`로 바꿉니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/d06effc3cab12d545fd7bc92f4577b14.png)
3. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다.
다음 그림과 같이 단일 사용자 모드로 진입하였습니다.
![](https://main.qcloudimg.com/raw/126dcdb5916e57815c3632e9e4b24412.png)
:::
::: Ubuntu\s또는\sDebian
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/c3c0be766481edf3f6521f7764f8d4cb.png)
2. **e**를 눌러 커널 편집 인터페이스로 들어간 뒤, ↑↓ 버튼으로 linux의 첫번째 항으로 이동해 `ro`를 `quiet splash rw init=/bin/bash`로 바꿉니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/40882cf22d755c0338ea9d7c106bc280.png)
3. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다.
다음 그림과 같이 단일 사용자 모드로 진입하였습니다.
![](https://main.qcloudimg.com/raw/df55d20b7eb087744fb6283c5124e7fc.png)
:::
::: SUSE
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/4da4d0c5c98e4f0dbe4990e920a11daf.png)
2. **e**를 눌러 커널 편집 인터페이스로 들어간 뒤, ↑↓ 버튼으로 linux의 첫번째 항으로 이동해 `splash` 매개변수 앞에는 `rw`를, 뒤에는 `1`을 추가합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/013a0099ccb5c19d04441dd60ea7558b.png)
3. **Ctrl+X**를 눌러 단일 사용자 모드를 실행 및 진입합니다.
:::
::: tlinux
1. grub 모드 인터페이스에서 커널을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/c497e63321b76e5cd1f0eea06f53cdb2.png)
2. **e** 을 눌러 커널 편집 인터페이스로 이동한 뒤 ↑↓ 버튼을 사용해 **kernel**이 있는 행을 선택하고 다시 **e**를 누릅니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/06c66e0f30163e9fc7e6aafbf9463645.png)
3. 행의 맨 끝, 즉 256M 빈칸 뒤에 `1`을 추가합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/06efb32e3a2edb39f32e13be1ab8527f.png)
4. **Enter**를 누르면 단일 사용자 모드로 진입합니다.
:::
</dx-tabs>
