## Overview
Extundelete is an open-source data recovery tool. With powerful features, it supports the ext3 and ext4 partition recovery of data disk files that are deleted accidentally, provided the disk is not written after the accident. This document describes how to use Extundelete to quickly recover the accidentally deleted data on a CentOS 7.7 Tencent Cloud CVM.
Tencent Cloud also offers [snapshots](https://intl.cloud.tencent.com/document/product/362/5755), [custom images](https://intl.cloud.tencent.com/document/product/213/4942) and [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222) to store data. We recommend that you regularly back up data to enhance data security.

## Software
- Linux: Linux operating system. This document uses CentOS 7.7 as an example.
- Extundelete: open-source data recovery tool. This document uses Extundelete 0.2.4 as an example.


## Directions
>!Refer to [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) and [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942) to back up data before performing operations so that you can recover the instance to its initial status if a problem occurs.
>

### Installing Extundelete
1. Run the following command to install the Extundelete dependencies and libraries.
>!
>- Extundelete requires the libext2fs version 1.39 or later.
>- To support the ext4 format, install the e1fsprogs version 1.41 or later. You may use the `dumpe2fs` command to view the version. 
>
```
yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make
```
2. Download the [Extundelete](https://sourceforge.net/projects/extundelete/) installation package.
3. Run the following commands in sequence to decompress the Extundelete installation package and access its directory.
```
tar -xvjf extundelete-0.2.4.tar.bz2
```
```
cd extundelete-0.2.4 
```
4. Run the following commands in sequence to compile and install Extundelete.
```
./configure   
```
```
make && make install
```
After the installation is completed, you will be able to see the executable file “extundelete” in the `usr/local/bin` directory.

### Testing the data recovery
Recover data as needed by performing the following steps.
1. Initialize and partition the data disk by referring to [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597). Run the following command to view the existing disks and the available partitions.
```
fdisk -l
```
The following information will appear:
![](https://main.qcloudimg.com/raw/34abb1b0c7a1f6fb4ff233a42a781123.png)
2. Run the following commands in sequence to create a mount point and mount the partition. This document uses mounting the `/dev/vdb1` partition to `/test` as an example.
```
mkdir /test
```
```
mount /dev/vdb1 /test
```
3. Run the following commands in sequence to create the “hello” test file at the mount point.
```
cd /test
```
```
echo test > hello
```
4. <span id="Step4"></span>Run the following command to record the MD5 value of the “hello” file. This value can be used to compare the original and recovered files.
```
md5sum hello
```
The following information will appear:
![](https://main.qcloudimg.com/raw/230d4c9a4456df8b3623c0bd401d878a.png)
5. Run the following commands in sequence to delete the “hello” file.
```
rm -rf hello
```
```
cd ~
```
```
fuser -k /test
```
6. Run the following command to unmount the partition.
```
umount /dev/vdb1
```
7. Run the following command to search the partition for accidentally deleted files.
```
extundelete --inode 2 /dev/vdb1
```
The following information will appear:
![](https://main.qcloudimg.com/raw/97a64a2e0de658f4ed55500f162b1eb7.png)
8. Run the following command to use Extundelete to recover the file.
```
/usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1
```
After the file is recovered, you will see the `RECOVERED_FILES` folder in the same-level directory.
9. Access the `RECOVERED_FILES` folder, check the recovered file, and run the following command to obtain its MD5 value.
```
md5sum Recovered file
```
If the obtained MD5 value is the same as that of the “hello” file recorded in [Step 4](#Step4), the data has been recovered successfully.
