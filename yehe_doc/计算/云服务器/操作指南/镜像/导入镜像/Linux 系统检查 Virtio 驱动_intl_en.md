## Overview
To run in Tencent Cloud, a CVM instance must have a kernel supporting virtio drivers, including the block device driver `virtio_blk` and the ENI driver `virtio_net`. To ensure that a CVM instance created with a custom image can start up properly, check whether your image supports virtio drivers in the source server before importing the image. This document uses CentOS as an example to describe how to check whether an image supports virtio drivers.

## Directions


### Step 1. Check whether the kernel supports virtio drivers[](id:CheckVirtioForKernel)
Execute the following command to check whether the current kernel supports virtio drivers:
```shellsession
grep -i virtio /boot/config-$(uname -r)
```
A result similar to the following is returned:
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - If the value of `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` is `m` in the response，please go to [Step 2](#CheckVirtioForInitramfs).
 - If the value of `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` is `y` in the response, which means the operating system contains the virtio drivers, you can import the custom image to Tencent Cloud. For detailed directions, see [Overview](https://intl.cloud.tencent.com/document/product/213/4945).
 - If you cannot find `CONFIG_VIRTIO_BLK` and `CONFIG_VIRTIO_NET` in the response, it means that images with the OS **cannot** be imported to Tencent Cloud. Please [download and compile kernel](#DownloadCompileKernel).


### Step 2. Check whether the temporary file system contains virtio drivers[](id:CheckVirtioForInitramfs)
If the value of the parameters is `m` in [Step 1](#CheckVirtioForKernel), you need to check whether `initramfs` or `initrd` contains the `virtio` drivers. Please execute the corresponding command according to the operating system:
- For CentOS 6/CentOS 7/CentOS 8/Red Hat 6/Red Hat 7:
```shellsession
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- For RedHat 5/CentOS 5:
```shellsession
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- For Debian/Ubuntu:
```shellsession
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

A result similar to the following is returned:
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
It means that <code>initramfs</code> contains the <code>virtio_blk</code> driver and <code>virtio.ko</code>, <code>virtio_pci.ko</code>, and <code>virtio_ring.ko</code> on which the driver depends. In this case, you can import the custom image to Tencent Cloud. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/4945">Import Images > Overview</a>.
If <code>initramfs</code> or <code>initrd</code> does not contain the <code>virtio</code> drivers, please go to [Step 3](#ReconfigureInitramfs).


### Step 3. Reconfigure the temporary file system[](id:ReconfigureInitramfs)
If you find that `initramfs` or `initrd` does not contain the `virtio` drivers in [Step 2](#CheckVirtioForInitramfs), you will need to reconfigure the temporary file system to ensure that `initramfs` or `initrd` contains the `virtio` drivers. Run the corresponding command according to the operating system:
 - For CentOS 8/Red Hat 8:
```shellsession
mkinitrd -f --allow-missing --with=virtio_blk --preload=virtio_blk --with=virtio_net --preload=virtio_net --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - For CentOS 6/CentOS 7/RedHat 6/RedHat 7:
```shellsession
mkinitrd -f --allow-missing --with=xen-blkfront --preload=xen-blkfront --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - For RedHat 5/CentOS 5:
```shellsession
mkinitrd -f --allow-missing --with=xen-vbd  --preload=xen-vbd --with=xen-platform-pci --preload=xen-platform-pci --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initrd-$(uname -r).img $(uname -r)
```
 - For Debian/Ubuntu:
```shellsession
echo -e 'xen-blkfront\nvirtio_blk\nvirtio_pci\nvirtio_console' >> /etc/initramfs-tools/modules
mkinitramfs -o /boot/initrd.img-$(uname -r)
```

## Appendix
### Downloading and compiling the kernel[](id:DownloadCompileKernel)

#### Downloading the kernel installation package
1. Execute the following command to install the components necessary for kernel compilation.
```shellsession
yum install -y ncurses-devel gcc make wget
```
2. Execute the following command to view the current version of the kernel.
```shellsession
uname -r
```
A response similar to the following will be returned, indicating the current kernel version is 2.6.32-642.6.2.el6.x86_64.
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
3. Download the source code of the corresponding or closest kernel version [here](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ).
For example, for the `2.6.32-642.6.2.el6.x86_64` version, you should download `linux-2.6.32.tar.gz` at `https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`.
4. Execute the following command to switch directory.
```shellsession
cd /usr/src/
```
5. Execute the following command to download the installation package.
```shellsession
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. Execute the following command to decompress the installation package.
```shellsession
tar -xzf linux-2.6.32.tar.gz
```
7. Execute the following command to make connection.
```shellsession
ln -s linux-2.6.32 linux
```
8. Execute the following command to switch directory.
```shellsession
cd /usr/src/linux
```

#### Compiling the kernel

1. Execute the following commands to compile the kernel.
```shellsession
make mrproper
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
Enter the “Linux Kernel vX.X.XX Configuration” interface as shown below:
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
<dx-alert infotype="explain" title="">
 If you are not taken to the "Linux Kernel vX.X.XX Configuration" interface, perform [Step 18](#OptionalStep).
"Linux Kernel vX.X.XX Configuration" interface:
 - Press "Tab" or the "↑"/"↓" key to move the cursor.
 - Press "Enter" to select or execute the item selected by the cursor.
 - Press the space bar to select the item selected by the cursor. "\*" means compiling to the kernel, and "M" means compiling to a module. 
</dx-alert>

2. Press the "↓" key to move the cursor to "Virtualization" and press the space bar to select "Virtualization".
3. Press "Enter" to enter the Virtualization details interface.
4. In the Virtualization details interface, check whether the Kernel-based Virtual Machine (KVM) support option is selected as shown below:
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
If it is not selected, press the space bar to select the “Kernel-based Virtual Machine (KVM) support” option.
5. Press "Esc" to return to the "Linux Kernel vX.X.XX Configuration" main interface.
6. Press the "↓" key to move the cursor to "Processor type and features" and press "Enter" to enter the Processor type and features details interface.
7. Press the "↓" key to move the cursor to "Paravirtualized guest support" and press "Enter" to enter the detailed interface of Paravirtualized guest support.
8. In the Paravirtualized guest support details interface, check whether "KVM paravirtualized clock" and "KVM Guest support" are selected as shown below:
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
If they are not selected, press the space bar to select the "KVM paravirtualized clock" and "KVM Guest support" options.
9. Press "Esc" to return to the "Linux Kernel vX.X.XX Configuration" main interface.
10. Press the "↓" key to move the cursor to "Device Drivers" and press "Enter" to enter the Device Drivers details interface.
11. Press the "↓" key to move the cursor to "Block devices" and press "Enter" to enter the Block devices details interface.
12. In the Block devices details interface, check whether "Virtio block driver (EXPERIMENTAL)" is selected as shown below:
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
If it is not selected, press the space bar to select the "Virtio block driver (EXPERIMENTAL)" option.
13. Press “Esc” to return to the Device Drivers details interface.
14. Press the "↓" key to move the cursor to "Network device support" and press "Enter" to enter the Network device support details interface.
15. In the Network device support details interface, check whether "Virtio network driver (EXPERIMENTAL)" is selected as shown below:
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
If it is not selected, press the space bar to select the "Virtio network driver (EXPERIMENTAL)" option.
16. Press "Esc" to exit the kernel configuration interface, and select "YES" to save the `.config` file.
17. Take [Step 1: Checking whether the kernel supports the virtio drivers](#CheckVirtioForKernel) to verify whether the virtio drivers have been configured correctly.
18. [](id:OptionalStep)(Optional) Run the following command to manually edit the `.config` file.
<dx-alert infotype="explain" title="">
 This step is recommended if either of the following is true:
 - The kernel still contains no configuration information of the virtio drivers.
 - When compiling the kernel, you cannot enter the kernel configuration interface or save the `.config` file.
</dx-alert>
```shellsession
make oldconfig
make prepare
make scripts
make
make install
```
19. Execute the following commands to check the installation of the virtio drivers.
```shellsession
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
If any of the commands returns a list of files such as `virtio_blk`,` virtio_pci.virtio_console`, it indicates that you have installed the virtio drivers correctly.




