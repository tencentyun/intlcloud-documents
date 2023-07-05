## Overview
CentOS has officially discontinued support for CentOS 8 since January 1, 2022, and plans to discontinue support for CentOS 7 on June 30, 2024.

If you need to purchase a new CVM instance, you are advised to use a TencentOS Server image. If you are using a CentOS instance, replace it with TencentOS Server by referring to the directions provided in this document.


## Version Suggestions
- If you are using CentOS 7 series, migrate it to TencentOS Server 2.4 (TK4).
- If you are using CentOS 8 series, migrate it to TencentOS Server 3.1 (TK4).


## Notes
- OS migration is not supported in the following cases:
 - A GUI is installed.
 - An i686 RPM package is stalled.
- Business may fail to run properly after migration under the following conditions:
 - The business program is installed with and relies on a third-party RPM package.
 - The business program relies on a fixed kernel version or has its own kernel module compiled.
The target version after migration is TK14 based on the v5.4 kernel. This version is later than the kernel versions of CentOS 7 and CentOS 8 and may have changes in some old features.
 - The business program relies on a fixed GCC version.
Currently, TencentOS 2.4 is installed with GCC v4.8.5 by default, and TencentOS 3.1 is installed with GCC v8.5 by default.
- After migration, restart is required to enter the TencentOS kernel.
- Migration does not affect data disks. Upgrade only in the OS layer does not involve any operation on data disks.

## Resource Requirements
- The memory has a free space of over 500 MB.
- The system disk has a free space of over 10 GB.

## Directions

### Data backup
Migration is irreversible. To ensure business data security, you are advised to [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up system disk data.

### Migration execution
<dx-tabs>
::: Migrating to TencentOS 2.4 (TK4)
1. Log in to the target CVM instance. For operation details, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to install Python 3:
```shell
yum install -y python3
```
3. Run the following command to obtain the migration tool:
```shell
wget http://mirrors.tencent.com/tencentos/2.4/tlinux/x86_64/RPMS/migrate2tencentos-1.0-3.tl2.noarch.rpm
```
4. Run the following command to install the migration tool. The command will create `migrate2tencentos.py` in `/usr/sbin`.
```shell
rpm -ivh migrate2tencentos-1.0-3.tl2.noarch.rpm
```
5. Run the following command to start migration:
```shell
/usr/sbin/migrate2tencentos.py -v 2.4
```
The migration takes some time. When the script execution is completed, the following information will be displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/a5d1a2cc65970b98b51071f6c90a40f5.png)
6. Restart the instance. For operation details, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
7. Check the migration result. 
   1. Run the following command to check the OS release information:
```shell
cat /etc/ os-release
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/11ae97a1ed88d3a6e6ddfddc369b2574.png)
   2. Run the following command to check the kernel:
```shell
uname -r
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/cb34dbe478757069a4d3136a9384f711.png)
<dx-alert infotype="explain" title="">
By default, the kernel is the latest version of YUM. The actual result prevails. This document uses the version shown in the figure as an example.
</dx-alert>
  3. Run the following command to check YUM:
```shell
yum makecache
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/88b9468bed347c567223385b3df161b4.png)


:::
::: Migrating to TencentOS 3.1 (TK4)
1. Log in to the target CVM instance. For operation details, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to install Python 3:
```shell
yum install -y python3
```
3. Run the following command to obtain the migration tool:
```shell
wget http://mirrors.tencent.com/tlinux/3.1/Updates/x86_64/RPMS/migrate2tencentos-1.0-3.tl3.noarch.rpm
```
4. Run the following command to install the migration tool. The command will create `migrate2tencentos.py` in `/usr/sbin`.
```shell
rpm -ivh migrate2tencentos-1.0-3.tl3.noarch.rpm
```
5. Run the following command to start migration:
```shell
/usr/sbin/migrate2tencentos.py -v 3.1
```
The migration takes some time. When the script execution is completed, the following information will be displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/e272e5f6e5eba50a1e9bc74db536a592.png)
6. Restart the instance. For operation details, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
7. Check the migration result. 
   1. Run the following command to check the OS release information:
```shell
cat /etc/ os-release
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/eb7333c8badf5d7a4852a66084fcc190.png)
   2. Run the following command to check the kernel:
```shell
uname -r
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/9bba4c6112c4bec1482d827ad02a39d6.png)
<dx-alert infotype="explain" title="">
By default, the kernel is the latest version of YUM. The actual result prevails. This document uses the version shown in the figure as an example.
</dx-alert>
  3. Run the following command to check YUM:
```shell
yum makecache
```
The information shown in the figure below is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/83a6ec7fc69ab6bd26e9ff1cf0f443da.png)

:::
</dx-tabs>


