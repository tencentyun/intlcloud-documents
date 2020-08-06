## Overview

This document describes how to create a Linux image.

## Directions

### Preparations

Before creating and exporting a system disk image, complete the following checks.
>? If you need to prepare and export a data disk image, skip this operation.
>

#### Checking the partitioning and start mode of the operating system
1. Run the following command to check whether the OS partition is a GPT partition.
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - If the returned result is msdos, the partition is an MBR partition. In this case, go to the next step.
 - If the returned result is gpt, the partition is a GPT partition. Currently, service migration does not support GPT partitions. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
2. Run the following command to check whether the OS start mode is EFI.
```
sudo ls /sys/firmware/efi
```
 - If the EFI file exists, the operating system starts in EFI mode. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
 - If the EFI file does not exist, proceed with the next step.

#### Checking system-critical files
The system-critical files to be checked include but are not limited to:
>? Follow the standards of relevant distributions to ensure that the paths and permissions of the system-critical files are correct and the files can be read and written normally.
>
 - /etc/grub/grub.cfg: in the kernel parameter, uuid is recommended for mounting root. Other methods (such as root=/dev/sda) may cause a failure in starting the system.
 - /etc/fstab: do not mount other disks. After the migration, the system may not be started due to disk missing.
 - /etc/shadow: it has appropriate permissions and can be read and written.

#### Unmounting the software
Unmount the drivers and software (including VMWare tools, Xen tools, Virtualbox GuestAdditions and other software that comes with underlying drivers) that cause conflicts.

#### Checking the virtio driver
For more information, see [Checking Virtio Drivers in Linux](https://intl.cloud.tencent.com/document/product/213/9929).

#### Installing cloud-init
For more information, see [Installing Cloud-Init on Linux](https://intl.cloud.tencent.com/document/product/213/12587).

#### Checking other hardware configurations
After the migration to the cloud, changes in the hardware include but are not limited to:
 - The graphics card changes to Cirrus VGA.
 - The disk changes to Virtio Disk. The device name is vda or vdb.
 - ENI changes to Virtio Nic. By default, only eth0 is available.

### Querying partitions and their sizes
Run the following command to query the current OS partition format and determine the partitions to be copied and their sizes.
```
mount
```
A result similar to the following is returned:
```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=4080220k,nr_inodes=1020055,mode=755)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
/dev/sda1 on / type ext4 (rw,relatime,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
systemd-1 on /home/libin/work_doc type autofs (rw,relatime,fd=33,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12692)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12709)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
configfs on /sys/kernel/config type configfs (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=817176k,mode=700,uid=1000,gid=100)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=100)
```
From the result, you can see the root partition resides in `/dev/sda1`, no independent partitions reside in `/boot` or `/home`, sda1 contains the boot partition, and mbr is missing. Therefore, we only need to copy the entire sda.
>! The exported image should contain at least the root partition and mbr. If the exported image lacks mbr, it cannot be started.
> In the current operating system, if `/boot` and `/home` are independent partitions, the exported image also needs to include both independent partitions.
> 

### Exporting an image
You can use either of the following method to export an image.
- [Use tools](#Useplatform)
- [Run commands](#ExportImageForUsingCommand)

<span id="Useplatform"></span>
#### Exporting an image by using a platform tool
For more information on how to use image export tools including VMWare vCenter Convert, Citrix XenConvert and other virtualization platforms, see the documentation for the respective platform.
>? Tencent Cloud Service Migration supports images in qcow2, vhd, raw, and vmdk formats.
>

<span id="ExportImageForUsingCommand"></span>
#### Exporting an image by running commands
>! Manual export with commands poses a high risk (For example, the file system's metadata may be corrupted when I/O is busy). We recommend that you [check the image](#CheckMirror) to make sure that the image is intact and correct after it is exported.
>

You can use either the [qemu-img](#qemuimg) or [dd](#dd) command to export an image.
- **Use the `qemu-img` command**<span id="qemuimg"></span>
 1. Run the following command to install the package. This document uses Debian as an example. Replace the command parameters as needed. The package name might be different for distributions, such as `qemu-img` for CentOS.
```
apt-get install qemu-utils
```
 2. Run the following command to export `/dev/sda` to `/mnt/sdb/test.qcow2`.
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
In this command, `/mnt/sdb` indicates the mounted new disk or another network storage.
To convert it to other formats, change the value of the `-O` parameter to one of the following:
<span id="-OParameterValue"></span>
<table>
	<tr><th>Parameter Value</th><th>Description</th></tr>
	<tr><td>qcow2</td><td>qcow2 format</td></tr>
	<tr><td>vpc</td><td>vhd format</td></tr>
	<tr><td>vmdk</td><td>vmdk format</td></tr>
	<tr><td>raw</td><td>No format</td></tr>
</table>
- **Use the `dd` command**<span id="dd"></span>
For example, run the following command to export the image in raw format.
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
The `count` parameter specifies the number of partitions to be copied, which can be queried by running the `fdisk` command. To copy all partitions, ignore the `count` parameter.
For example, run the following command to view the number of partitions of `/dev/sda`.
```
fdisk -lu /dev/sda
```
A result similar to the following is returned:
```
Disk /dev/sda: 1495.0 GB, 1494996746240 bytes
255 heads, 63 sectors/track, 181756 cylinders, total 2919915520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk identifier: 0x0008f290

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    41945087    20971520   83  Linux
/dev/sda2        41945088    46123007     2088960   82  Linux swap / Solaris
/dev/sda3        46123008    88066047    20971520   83  Linux
/dev/sda4        88066048  2919910139  1415922046   8e  Linux LVM
```
From the returned result of the `fdisk` command, you can see that sda1 ends at 41945087 \* 512 bytes, so set `count` to 20481 MB.
>? The image exported by using the `dd` command is in raw format. We recommend that you [convert the format to qcow2, vhd, or other image formats](#ImageFormatConversion).
>

<span id="ImageFormatConversion"></span>
### Converting the image format
>? Currently, Tencent Cloud Service Migration supports images in qcow2, vpc, vmdk, and raw formats. We recommend using the compressed image format to reduce transmission and migration time.
> 
Convert the image format by using the `qemu-img` command
For example, run the following command to convert the image from the raw format to the qcow2 format.
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f` indicates the source image format.
- `-O` indicates the target image format. For the supported formats, see [`-O` Parameter Values](#-OParameterValue).

<span id="CheckMirror"></span>
### Checking the image
>? The image file system that you create may be corrupted if you create the image without stopping the service or due to other reasons. Therefore, we recommend that you check the image after creating it.
>
If the image format is supported by the current platform, you can directly open the image to check the file system. For example, the Windows platform supports VHD images, the Linux platform allows you to use qemu-nbd to open QCOW2 images, and the Xen platform allows you to directly open VHD files. This document uses the Linux platform as an example:
1. Run the following commands sequentially to check whether the nbd module exists.
```
modprobe nbd
```
```
lsmod | grep nbd
```
If the following is returned, the nbd module exists. If nothing is returned, check whether the kernel compilation option `CONFIG_BLK_DEV_NBD` is enabled. If not, enable it or change the system before compiling the kernel again.
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2. Run the following commands sequentially to check the image.
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
After you run the `qemu-nbd` command, `/dev/nbd0` maps to `xxx.qcow2`, and `/dev/nbd0p1` indicates the first partition of the virtual disk. If nbd0p1 does not exist or mount fails, the image is likely to encounter an error.
In addition, you can start the CVM to check whether the image file works before uploading the image.


