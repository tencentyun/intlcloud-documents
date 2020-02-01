## Scenario
A CVM must have a kernel supporting virtio drivers (including the block device driver `virtio_blk` and NIC driver `virtio_net`) in order to run on Tencent Cloud. CVMs whose kernels do not have the `virtio_blk` driver must include this driver in the file `initramfs (or initrd)` for normal operation. This document describes how to check and repair the support for virtio drivers before importing images.

## Directions

<span id="CheckVirtioForKernel"></span>
### Step 1: Checking Whether Virtio Drivers are Supported in the Kernel
Check whether `virtio` drivers are support in the kernel
```
grep -i virtio /boot/config-$(uname -r)
```
You will get a result like below:
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - If `CONFIG_VIRTIO_BLK`  and `CONFIG_VIRTIO_NET` = `m`，please do [Step 2](#CheckVirtioForInitramfs).
 - If `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` = `y`, which means the OS has Virtio, you can import the image to Tencent Cloud. For details, see [Overview of Import Images](https://intl.cloud.tencent.com/document/product/213/4945)。
 - If there are no `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` shown, which means the OS can not be imported to Tencent Cloud. Please go to [Download and Compile Kernel](#DownloadCompileKernel).

<span id="CheckVirtioForInitramfs"></span>
### Step 2: Checking Whether Virtio Drivers are in the Temporary File System
If [Step 1](#CheckVirtioForKernel) has result to be `m`, you need to confirm whether `virtio` is in `initramfs` or `initrd`.
- CentOS 6/CentOS 7/RedHat 6/RedHat 7:
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- RedHat 5/CentOS 5:
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Debian/Ubuntu:
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```
As shown in the figure below:
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
 `initramfs` contains the `virtio_blk` driver and the dependent `virtio.ko`, `virtio_pci.ko`, and `virtio_ring.ko`, which means all the neccesary components are included in `initramfs`. In this case, the image can be imported. Otherwise, please go to [Step 3](#ReconfigureInitramfs)

<span id="ReconfigureInitramfs"></span>
### Step 3: Recreate the Temporary File  System
 - CentOS 6/CentOS 7/RedHat 6/RedHat 7:
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
 - RedHat 5/CentOS 5:
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```
 - Debian/Ubuntu:
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```


## Appendix
<span id="DownloadCompileKernel"></span>
### Download and Compile Kernel
#### Download the install package
```
yum install -y ncurses-devel gcc make wget
```
Check the current version of kernel
```
uname -r
```

Get a result like below, kernel version to be `2.6.32-642.6.2.el6.x86_64`.
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)

3. Go to  [Linux Kernel Download Page](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ)
For example, for the version `2.6.32-642.6.2.el6.x86_64`, you should download `linux-2.6.32.tar.gz` ：`https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`.
4. Switch directory.
```
cd /usr/src/
```
5. Download the install package
```
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. Unzip
```
tar -xzf linux-2.6.32.tar.gz
```
7. Make connection
```
ln -s linux-2.6.32 linux
```
8. Go to the directory
```
cd /usr/src/linux
```

#### Compile the kernel

1. Compile the kernel
```
make mrproper
symvers_path=$(find /usr/src/ -name "Module.symvers")
test -f $symvers_path && cp $symvers_path .
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
“Linux Kernel vX.X.XX Configuration”:
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)