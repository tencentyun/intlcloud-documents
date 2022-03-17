## Scenario

The Windows file system typically uses the NTFS or FAT32 format, whereas the Linux file system often uses EXT-series formats. When the operating system of a CVM is changed from Windows to Linux, the data disk of the CVM remains in the same format as that of the original operating system. As a result, after the reinstallation of the system, the CVM might be unable to access the file system of the data disk. This document describes how to read a data disk in the original Windows system after the operating system is reinstalled from Windows to Linux.

## Directions

### Enabling a Linux system to support NTFS 

1. Log in to the Linux CVM after reinstallation.
2. Run the following command to install the ntfsprogs software program to enable the Linux CVM to support access to the NTFS file system.
>? This document uses CentOS as an example. Note that different types of Linux systems require different installation commands. Therefore, always run the corresponding installation command for your operating system type.
>
```
yum install ntfsprogs
```


### Mounting a data disk from the Windows CVM to the Linux CVM

>? If the data disk in your Windows CVM has been mounted to the Linux CVM, skip this operation.
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, click **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)** to go to the Cloud Block Storage management page.
3. Select the Windows data disk to be mounted and choose **More** > **Mount**.
4. In the "Mount to CVM" window that appears, select the target Linux CVM and click **OK**.
5. Log in to the Linux CVM to which the Windows data disk has been mounted.
6. Run the following command to query the mounted data disk from the Windows CVM.
```
parted -l
```
Information similar to the following will be returned:
```
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
Number  Start   End     Size    File system  Name                          Flags
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. Run the following command to mount the data disk.
```
mount -t ntfs-3g data disk path mount target
```
For example, to mount the data disk in `/dev/vdb2` to `/mnt`, run the following command:
```
mount -t ntfs-3g /dev/vdb2 /mnt
```
As the file system can be recognized by the operating system, the Linux system can directly read data from and write data to the mounted data disk.

