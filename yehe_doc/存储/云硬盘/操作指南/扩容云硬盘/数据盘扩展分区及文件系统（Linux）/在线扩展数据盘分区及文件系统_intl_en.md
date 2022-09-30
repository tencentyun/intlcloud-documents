## Overview
Expanding a data disk via the console only increases its storage space. You need to extend the partition or file system of the cloud disk to the larger size. This document describes how to extend partitions and file systems online.

## Prerequisite
- Before extending partition or file system, create a snapshot of the cloud disk to back up data. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
This practice helps you roll back snapshot to recover data in case of data loss due to maloperation.
- The cloud disk has been expanded and attached to a CVM via the console. For more information, see [Expanding Cloud Disk Capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- The Linux CVM kernel should be version 3.6.0 or later. You can use the `uname -a` command to check the kernel version.
If the kernel version is earlier than 3.6.0, see [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).

## Operating Environment
<table>
<tr>
<th>Resource</th><th>Description</th>
</tr>
<tr>
<td>Operating system</td>
<td>CentOS 8.0 64-bit</td>
</tr>
<tr>
<td>Cloud disk (data disk)</td>
<td>
<ul style="margin-bottom:0px">
<li><code>/dev/vdb</code>: Uses the MBR partition and the EXT4 file system, and expands from 50 GB to 60 GB via the console.</li>
<li><code>/dev/vdc</code>: Uses the GPT partition and the XFS file system, and expands from 50 GB to 60 GB via the console.</li>
</ul>
</td>
</tr>
</table>

## Directions
### Viewing partitions of the cloud disk
1. [Log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to query partitions of the cloud disk.
```shellsession
fdisk -l
```
The following information appears:
![](https://main.qcloudimg.com/raw/19d4f0ab6be5e332022efe9247069f35.png)
As shown in the figure,
 - The 60 GB `/dev/vdb` data disk contains a 50 GB MBR partition `/dev/vdb1`.
 - The 60 GB `/dev/vdc` data disk contains a 50 GB GPT partition `/dev/vdc1`.
3. [](id:Step3)Run the following command to determine the file system type of existing partitions.
```shellsession
df -TH
```
The following information appears:
![](https://main.qcloudimg.com/raw/384bd9556f09e973504ab93dbb6aa900.png)
As shown in the figure,
 - The `/dev/vdb1` partition is on an EXT4 file system that has been attached to `/mnt/disk1`.
 - The `/dev/vdc1` partition is on an XFS file system that has been attached to `/mnt/disk2`.

### Extending a partition
1. Use the command as needed to install the gdisk tool.
 - For a MBR partition, skip this step.
 - For a GPT partition, run the following command according to the operating system of the CVM.
<dx-tabs>
::: CentOS
```shellsession
yum install gdisk -y
```
:::
::: Ubuntu or Debian
```shellsession
apt-get install gdisk -y
```
:::
</dx-tabs>
2. Run the following command to install the growpart tool according to the operating system of the CVM.
<dx-tabs>
::: CentOS
```shellsession
yum install -y cloud-utils-growpart
```
:::
::: Ubuntu or Debian
```shellsession
apt-get install -y cloud-guest-utils
```
:::
</dx-tabs>
3. Run the following command to extend partitions using growpart.
Take extending the `/dev/vdb1` partition as an example. Note that there is a space between `/dev/vdb` and `1` in the command. Replace with your actual values.
```shellsession
growpart /dev/vdb 1
```
If information similar to what is shown below is returned, the partition has been extended.
![](https://main.qcloudimg.com/raw/bc67dd4e8116510ea2cea5484529cdf1.png)

### Extending a file system
1. Use the file system-specific command to resize a file system based on the type obtained in [step 3](#Step3).
<dx-tabs>
::: Extending an EXT file system
Run the following command to extend the EXT file system.
```shellsession
resize2fs /dev/vdb1 
```The following information will appear:
![](https://main.qcloudimg.com/raw/5bd3a9bba754bf21256e792860c6d799.png)
:::
::: Extending an XFS file system
Run the following command to extend the XFS file system.
```shellsession
xfs_growfs <Mount point>
```Take mounting the `/dev/vdc1` file system to`/mnt/disk2` as an example, then run the following command:
```shellsession
xfs_growfs /mnt/disk2
```The following information will appear:
![](https://main.qcloudimg.com/raw/6e76842b419bb054c9cae9f96fa0250b.png)
:::
</dx-tabs>
2. Run the following command to view the result.
```shellsession
df -TH
```
If information similar to what is shown below is returned, the file system has been extended.
![](https://main.qcloudimg.com/raw/45bc319770858880a6b3cf35505bce46.png)
3. Check data integrity and CVM running status after expansion.
You can roll back the snapshot to recover data in case of exceptions. For more information, see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).


