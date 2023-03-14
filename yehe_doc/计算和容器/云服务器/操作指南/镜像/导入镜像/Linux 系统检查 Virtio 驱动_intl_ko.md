## 개요
CVM 시스템 커널에서는 Virtio 드라이버(블록 디바이스 드라이버 `virtio_blk` 및 ENI 드라이버 `virtio_net`)를 지원해야만 Tencent Cloud에서 정상적으로 실행할 수 있습니다. 사용자 정의 이미지를 가져온 후에 생성된 CVM 인스턴스를 실행할 수 없는 상황을 예방하기 위해, 이미지를 가져오기 전에 원본 서버에서 이미지가 Virtio 드라이버를 지원하는지 확인하고 복구해야 합니다. 본 문서는 CentOS 운영 체제를 예로 이미지를 가져오기 전에 이미지가 Virtio 드라이버를 지원하는지 확인 및 복구하는 방법에 대해 소개합니다.

## 작업 단계


### 1단계: 커널이 Virtio 드라이버를 지원하는지 확인[](id:CheckVirtioForKernel)
다음 명령어를 실행하여 현재 커널이 Virtio 드라이버를 지원하는지 확인합니다.
```shellsession
grep -i virtio /boot/config-$(uname -r)
```
다음과 같은 결과를 리턴합니다.
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - 반환 결과에서 `CONFIG_VIRTIO_BLK` 매개변수와 `CONFIG_VIRTIO_NET` 매개변수의 값이 `m`이라면, [2단계](#CheckVirtioForInitramfs)를 진행합니다.
 - 반환 결과에서 `CONFIG_VIRTIO_BLK` 매개변수와 `CONFIG_VIRTIO_NET` 매개변수의 값이 `y`라면, 해당 운영 체제에 Virtio 드라이버가 포함되어 있음을 의미하므로 바로 사용자 정의 이미지를 Tencent Cloud에 가져올 수 있습니다. 자세한 작업 방법은 [미러 이미지 가져오기 개요](https://intl.cloud.tencent.com/document/product/213/4945)를 참조 바랍니다.
 - 반환 결과에 `CONFIG_VIRTIO_BLK` 매개변수와 `CONFIG_VIRTIO_NET` 매개변수 정보가 없다면, 해당 운영 체제에서 Tencent Cloud에 가져오기를 **지원하지 않는 것**으로, [커널 다운로드 및 컴파일](#DownloadCompileKernel)을 진행하시기 바랍니다.


### 2단계: Virtio 드라이버가 임시 파일 시스템에 있는지 확인[](id:CheckVirtioForInitramfs)
[1단계](#CheckVirtioForKernel)를 실행한 결과 매개변수 값이 `m`이라면 한 단계 더 확인해야 합니다. 임시 파일 시스템 `initramfs` 혹은 `initrd`에 `virtio` 드라이버가 포함되어 있는지 확인합니다. 운영 체제에 맞게 관련 명령어를 실행하시기 바랍니다.
- CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7 운영 체제:
```shellsession
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- RedHat 5/CentOS 5 운영 체제:
```shellsession
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Debian/Ubuntu 운영 체제:
```shellsession
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

다음과 같은 결과를 리턴합니다.
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
여기서 <code>initramfs</code>에 <code>virtio_blk</code> 드라이버와 이에 종속된 <code>virtio.ko</code>, <code>virtio_pci.ko</code> 및 <code>virtio_ring.ko</code> 드라이버가 포함되어 있음을 알 수 있습니다. 이제 바로 사용자 정의 이미지를 Tencent Cloud에 가져올 수 있습니다. 자세한 작업 방법은 <a href="https://intl.cloud.tencent.com/document/product/213/4945">미러 이미지 가져오기 개요</a>를 참조 바랍니다.
만약에 <code>initramfs</code> 혹은 <code>initrd</code>에 <code>virtio</code> 드라이버가 없다면 [3단계](#ReconfigureInitramfs)를 진행하시기 바랍니다.


### 3단계: 임시 파일 시스템 재구성[](id:ReconfigureInitramfs)
[2단계](#CheckVirtioForInitramfs)를 실행한 결과 임시 파일 시스템 `initramfs` 혹은 `initrd`에 `virtio` 드라이버가 없다면 임시 파일 시스템 `initramfs` 혹은 `initrd`에 `virtio` 드라이버가 포함되도록 다시 설정해야 합니다. 운영 체제에 맞게 관련 작업을 선택하시기 바랍니다.
 - CentOS 8/RedHat 8 운영 체제:
```shellsession
mkinitrd -f --allow-missing --with=virtio_blk --preload=virtio_blk --with=virtio_net --preload=virtio_net --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - CentOS 6/CentOS 7/RedHat 6/RedHat 7 운영 체제:
```shellsession
mkinitrd -f --allow-missing --with=xen-blkfront --preload=xen-blkfront --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - RedHat 5/CentOS 5 운영 체제:
```shellsession
mkinitrd -f --allow-missing --with=xen-vbd  --preload=xen-vbd --with=xen-platform-pci --preload=xen-platform-pci --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initrd-$(uname -r).img $(uname -r)
```
 - Debian/Ubuntu 운영 체제:
```shellsession
echo -e 'xen-blkfront\nvirtio_blk\nvirtio_pci\nvirtio_console' >> /etc/initramfs-tools/modules
mkinitramfs -o /boot/initrd.img-$(uname -r)
```

## 부록
### 커널 다운로드 및 컴파일[](id:DownloadCompileKernel)

#### 커널 설치 패키지 다운로드
1. 다음 명령어를 실행하여 커널의 필수 컴포넌트를 설치 및 컴파일합니다.
```shellsession
yum install -y ncurses-devel gcc make wget
```
2. 다음 명령어를 실행하여 현재 시스템에서 사용 중인 커널 버전을 조회합니다.
```shellsession
uname -r
```
다음과 같은 반환 결과에 따르면, 현재 시스템에서 사용 중인 커널 버전은 `2.6.32-642.6.2.el6.x86_64`입니다.
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
3. [Linux 커널 다운로드 페이지](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ)로 이동하여 해당되거나 가장 가까운 커널 버전의 소스 코드를 다운로드합니다.
예시, `2.6.32-642.6.2.el6.x86_64` 버전의 커널은 `linux-2.6.32.tar.gz` 설치 패키지를 다운로드하며, 다운로드 경로는 `https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`입니다.
4. 다음 명령어를 실행하여 디렉터리를 변경합니다.
```shellsession
cd /usr/src/
```
5. 다음 명령어를 실행하여 설치 패키지를 다운로드합니다.
```shellsession
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. 다음 명령어를 실행하여 설치 패키지를 압축 해제합니다.
```shellsession
tar -xzf linux-2.6.32.tar.gz
```
7. 다음 명령어를 실행하여 링크를 생성합니다.
```shellsession
ln -s linux-2.6.32 linux
```
8. 다음 명령어를 실행하여 디렉터리를 변경합니다.
```shellsession
cd /usr/src/linux
```

#### 커널 컴파일

1. 다음 명령어를 순서대로 실행하여 커널을 컴파일합니다.
```shellsession
make mrproper
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
아래 이미지와 같이 'Linux Kernel vX.X.XX Configuration' 인터페이스로 이동합니다.
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
<dx-alert infotype="explain" title="">
 ‘Linux Kernel vX.X.XX Configuration’ 인터페이스로 이동하지 않았다면, [18단계](#OptionalStep)를 실행합니다.
‘Linux Kernel vX.X.XX Configuration’ 인터페이스:
 - ‘Tab’ 키 혹은 ‘↑’ ‘↓’ 방향키를 눌러 커서를 이동합니다.
 - ‘Enter’를 누르거나 커서로 항목을 선택합니다.
 - 스페이스 바를 눌러 커서로 선택한 항목을 클릭하고, ‘\*‘ 표시가 나타나면 커널이 컴파일되었음을 의미하며, ‘M’ 표시가 나타나면 모듈로 컴파일되었음을 의미합니다. 
</dx-alert>
2. '↓' 키를 눌러 커서를 'Virtualization'에 두고, 스페이스 바를 눌러 'Virtualization'을 클릭합니다.
3. 'Virtualization'에서 'Enter'를 눌러 Virtualization 상세 인터페이스로 이동합니다.
4. 아래 이미지와 같이 Virtualization 상세 인터페이스에서 Kernel-based Virtual Machine (KVM)support 옵션이 선택되어 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
선택되어 있지 않다면, 스페이스 바를 눌러 Kernel-based Virtual Machine (KVM)support 옵션을 선택합니다.
5. 'Esc'를 눌러 'Linux Kernel vX.X.XX Configuration' 메인 인터페이스로 돌아갑니다.
6. '↓' 키를 눌러 커서를 'Processor type and features'에 두고, 'Enter'를 눌러 Processor type and features 상세 인터페이스로 이동합니다.
7. '↓' 키를 눌러 커서를 'Paravirtualized guest support'에 두고, 'Enter'를 눌러 Paravirtualized guest support 상세 인터페이스로 이동합니다.
8. 아래 이미지와 같이 Paravirtualized guest support 상세 인터페이스에서 'KVM paravirtualized clock'과 'KVM Guest support' 옵션이 선택되어 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
선택되어 있지 않다면, 스페이스 바를 눌러 'KVM paravirtualized clock'과 'KVM Guest support' 옵션을 선택합니다.
9. 'Esc'를 눌러 'Linux Kernel vX.X.XX Configuration' 메인 인터페이스로 돌아갑니다.
10. '↓' 키를 눌러 커서를 'Device Drivers'에 두고, 'Enter'를 눌러 Device Drivers 상세 인터페이스로 이동합니다.
11. '↓' 키를 눌러 커서를 'Block devices'에 두고, 'Enter'를 눌러 Block devices 상세 인터페이스로 이동합니다.
12. 아래 이미지와 같이 Block devices 상세 인터페이스에서 'Virtio block driver (EXPERIMENTAL)' 옵션이 선택되어 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
선택되어 있지 않다면, 스페이스 바를 눌러 'Virtio block driver (EXPERIMENTAL)' 옵션을 선택합니다.
13. 'Esc'를 눌러 Device Drivers 인터페이스로 돌아갑니다.
14. '↓' 키를 눌러 커서를 'Network device support'에 두고, 'Enter'를 눌러 Network device support 상세 인터페이스로 이동합니다.
15. 아래 이미지와 같이 Network device support 상세 인터페이스에서 'Virtio network driver (EXPERIMENTAL)' 옵션이 선택되어 있는지 확인합니다.
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
선택되어 있지 않다면, 스페이스 바를 눌러 'Virtio network driver (EXPERIMENTAL)' 옵션을 선택합니다.
16. 'Esc'를 눌러 커널 설정 인터페이스를 종료하고, 팝업 창 안내에 따라 'YES'를 선택하여 `.config` 파일을 저장합니다.
17. [1단계: 커널이 Virtio 드라이버를 지원하는지 확인](#CheckVirtioForKernel)을 참조하여 Virtio 드라이버가 정상적으로 설정되었는지 확인합니다.
18. [](id:OptionalStep)(옵션) 다음 명령어를 실행하여 `.config` 파일을 수동으로 편집합니다.
<dx-alert infotype="explain" title="">
 다음 조건 중 하나라도 만족한다면 해당 작업을 수행하시길 권장합니다.
 - 확인한 후에도 커널에 Virtio 드라이버 관련 설정 정보가 없는 경우.
 - 커널을 컴파일할 때 커널 설정 인터페이스로 이동할 수 없거나 `.config` 파일을 저장할 수 없는 경우.
</dx-alert>
```shellsession
make oldconfig
make prepare
make scripts
make
make install
```
19. 다음 명령어를 순서대로 실행하여 Virtio 드라이버의 설치 현황을 조회합니다.
```shellsession
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
명령어의 반환 결과 중에 `virtio_blk`, `virtio_pci.virtio_console` 등의 파일 리스트가 출력된다면 Virtio 드라이버가 정상적으로 설치되었음을 의미합니다.




