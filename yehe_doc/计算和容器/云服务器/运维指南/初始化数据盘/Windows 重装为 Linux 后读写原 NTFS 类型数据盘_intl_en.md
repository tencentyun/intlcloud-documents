## Overview

Windows file system typically uses NTFS or FAT32 format, while Linux file system often uses EXT series format. When the operating system of a CVM is reinstalled from Windows to Linux, the data disk of the CVM remains in the format of the original operating system. As a result, after the system reinstallation, the CVM might be unable to access the data disk file system. This document describes how to read a data disk in the original Windows system after the operating system is reinsalled from Windows to Linux.

## Directions

### Installing NTFS software on a Linux CVM

1. Log in to the Linux CVM after reinstallation.
2. Run the following command to install the ntfsprogs software to enable the Linux CVM to support access to the NTFS file system.
<dx-alert infotype="explain" title="">
This document takes CentOS as an example. Different types of Linux systems have different installation commands. Please use the corresponding installation commands.
</dx-alert>
```shellsession
yum install  -y ntfsprogs
```


### Attaching a data disk from the Windows CVM to the Linux CVM



>?
>- If the data disk in your Windows CVM has been attached to the Linux CVM, skip this operation.
>- If you want to attach a new data disk to the reinstalled Linux CVM, please [Initialize Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31597).


1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, click **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)** to enter the Cloud Block Storage management page.
3. Select the target Windows data disk. Click **More** > **Attach**.
![](https://qcloudimg.tencent-cloud.cn/raw/6acf53df9c1df0518502402d8bcadb6b.png)
4. In the pop-up window, choose the target Linux CVM, and click **OK**.
5. Log in to the Linux CVM to which the Windows data disk has been attached.
6. Run the following command to query the data disk attached from the Windows CVM.
```shellsession
parted -l
```
A message similar to the one below is returned:
```shellsession
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
Number  Start   End     Size    File system  Name                          Flags
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. Run the following command to attach the data disk.
```shellsession
mount -t ntfs-3g Data disk path Mount point
```
For example, if you need to attach the data disk in `/dev/vdb2` to `/mnt`, run the following command:
```shellsession
mount -t ntfs-3g /dev/vdb2 /mnt
```
Since the file system is identifiable, Linux system can directly perform read and write operations on the attached data disk.




