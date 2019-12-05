클라우드 서버 시스템 커널은 virtio 드라이버(블록 디바이스 드라이버 ‘virtio_blk’ 및 네트워크 카드 드라이버 'virtio_net' 포함)를 지원해야 Tencent Cloud에서 정상 작동할 수 있습니다. 컴파일되지 않은 커널의 ‘virtio_blk’ 드라이버의 경우, ‘initramfs(또는 initrd)’ 문서에 포함되어 있어야 클라우드 서버가 정상 작동할 수 있습니다. 본 문서는 미러 이미지를 가져오기 전에 어떻게 검사하고 미러 이미지에서 virtio 드라이버 지원에 대한 수정 방식을 설명합니다.

## 커널의 virtio 드라이버 검사 지원
‘Centos 7’을 예로 들어 현재 커널이 ‘virtio’ 드라이버를 지원하는지 확인하는 방법을 설명합니다.

(1) 현재 커널이 'virtio' 드라이버를 지원하는지 확인합니다.
```
grep -i virtio /boot/config-$(uname -r)
```
아래 이미지 참조: 현재 커널에는`virtio_blk` 및 `virtio_net` 드라이버가 포함되어 있으며, 모듈 형식으로 컴파일되어 있습니다(‘CONFIG_VIRTIO_BLK=m’은 커널 모듈로 컴파일된 것을 의미하여, y가 커널에 컴파일된 것을 의미함). 이 단계에서 `virtio_net` 또는 `virtio_blk` 드라이버 정보를 찾지 못하면, 미러 이미지는 Tencent Cloud에 가져오기를 *지원하지 않습니다*.
![](https://mc.qcloudimg.com/static/img/4f4c1b835ccc8a344c20fdf34183b48f/image.png)

커널이 'virtio' 드라이버('virtio_blk' 및 'virtio_net' 모두 지원)를 지원하고 'virtio_blk' 드라이버가 커널에 컴파일되는 경우(즉, `CONFIG_VIRTIO_BLK=y`), 커널은 후속 확인 없이 가져오기를 지원합니다. 'virtio_blk' 드라이버가 커널 모듈(즉, `CONFIG_VIRTIO_BLK=m`)으로 컴파일되는 경우, 후속 확인 단계를 계속하여 'virtio_blk' 드라이버가 `initramfs(또는 initrd)` 파일에 제대로 포함되어 있는지 확인해야 합니다.

(2) `initramfs`에 `virtio_blk` 드라이버가 포함되어 있는지 확인합니다.
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
아래 이미지와 같이 `initramfs`에는 `virtio_blk` 드라이버 및 해당 드라이버가 종속되는 `virtio.ko`, `virtio_pci.ko`, `virtio_ring.ko`이 있습니다. `initramfs`에 드라이버가 정상적으로 포함되어 있으면 미러 이미지를 가져올 수 있습니다.
![](https://mc.qcloudimg.com/static/img/4bac7c12a585eea3cdbd4b27c6a8caa6/image.png)

(3) `initramfs`에 관련된 'virtio' 정보가 없으면 `initramf`s 파일을 다시 생성합니다.

1) CentOS 7 작동 방법
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
![](https://mc.qcloudimg.com/static/img/559c71e11c197ea620a035b0ddd443cf/image.png)

2) Redhat5/Centos5 작동 방법
a. 다음과 같이 드라이버 정보가 initrd 파일에 포함되어 있는지 확인하십시오.
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```

b. `initrd` 파일을 다시 만들어야 하는 경우, 다음 커맨드를 실행하십시오.
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```

3) Debian/Ubuntu 작동 방법
a. virtio 드라이버 상태를 검사하십시오.
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```
b. initramfs에 포함되어 있지 않으면 다음 단계를 실행하여 수정하십시오.
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```
