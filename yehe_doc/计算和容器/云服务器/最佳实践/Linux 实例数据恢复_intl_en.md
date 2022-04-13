## Overview
This document uses a CVM instance on CentOS 8.0 as an example to describe how to use the open-source tool [Extundelete](https://sourceforge.net/projects/extundelete/) to recover accidentally deleted data.
Extundelete can recover accidentally deleted files in EXT3 and EXT4 file systems, but the specific level of recovery is subject to various factors such as whether files are overwritten by writes after deletion and whether metadata is stored in the journal. If the file system to be recovered is on the system disk, and there are always business or system processes writing files, the possibility of recovery is low.

<dx-alert infotype="explain" title="">
Tencent Cloud also offers [snapshots](https://intl.cloud.tencent.com/document/product/362/5755), [custom images](https://intl.cloud.tencent.com/document/product/213/4942) and [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222) to store data. We recommend that you regularly back up data to enhance data security.
</dx-alert>




## Preparations
Before recovering the data, complete the following preparations:
- Back up your data by referring to [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) and [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
- Stop writing data to the file system. If you need to recover a data disk, run `umount` to detach the disk from the CVM instance first.


## Directions

1. Install Extundelete in the following two ways:
<dx-tabs>
::: Download (recommended)
1. Run the following command to directly download the compiled binary program.
```
wget https://github.com/curu/extundelete/releases/download/v1.0/extundelete
```
2. Run the following command to grant file permissions.
```
chmod a+x extundelete
```
:::
::: Manual set-up

<dx-alert infotype="explain" title="">
The steps below are for CentOS 7 as an example. Note that the steps vary by the operating system.
</dx-alert>



1. Run the following command to install the Extundelete dependencies and libraries.
```shell
yum install libcom_err e2fsprogs-devel
```
```shell
yum install gcc gcc-c++ 
```
2. Run the following command to download the Extundelete source code.
```
wget https://github.com/curu/extundelete/archive/refs/tags/v1.0.tar.gz
```
3. Run the following command to decompress the `v1.0.tar.gz` file.
```
tar  xf v1.0.tar.gz
```
4. Run the following commands in sequence to compile and install.
```
cd extundelete-1.0
```
```
./configure
```
```
make
```
5. Run the following command to enter the `src` directory to view the compiled Extundelete file.
```
cd ./src
```
:::
</dx-tabs>
2. Run the following command to try recovering the data.
```
./extundelete  --restore-all  /dev/corresponding disk
```
The recovered files are located in the `RECOVERED_FILES` folder at the same directory level. Check whether there are the needed files.


