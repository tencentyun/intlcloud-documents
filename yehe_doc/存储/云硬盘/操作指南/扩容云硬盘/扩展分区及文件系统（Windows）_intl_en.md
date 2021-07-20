## Overview

After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747) in the console, you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition.
- If you expand a cloud disk that is attached to a running CVM, you need to [rescan the disk](#Scaning) to recognize the disk capacity after expansion.
- If the cloud disk to be expanding is not attached to a CVM or the attached CVM is shut down, the disk capacity after expansion will be automatically recognized.

>!
>- Extending the file system may affect the existing data. We strongly recommend you to manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before the operation.
>- To extend the file system, you need to [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928) or rescan the disk, which will lead to business interruption for a certain period. We recommend that you choose an appropriate time for this operation.
>- After extension of the file system, we strongly recommend you to [rescan the disk](#Scaning) to recognize the capacity. If you **refresh** the system or do other operations, the expanded capacity may not be recognized.
>


## Prerequisites
- You have [expanded the cloud disk via the console](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [attached the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Windows CVM via the console and created a file system.
- You have logged in to a Windows CVM instance on which you want to extend partitions and the file system. See [Logging in to Windows Instance Using RDP (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435).
>?This document describes how to expand a disk attached to a CVM with Windows Server 2012 R2 installed. Note that the steps may vary according to the operating system version.
>

## Directions
>!
>- If you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747) that is attached to a running CVM, you must [rescan the disk](#Scaning) to recognize the capacity before [extending the file system of an existing partition or creating a partition](#Extending).
>- If the cloud disk to be expanded is not attached to a CVM or the attached CVM is shut down, you can directly proceed with [extending the file system of an existing partition or creating a partition](#Expanding).
>- If the Virtio driver of the CVM is earlier than version 58003, please [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928) before performing the operation. You can first [check the Virtio driver version](#VirtioVersion). 


### Rescanning the disk[](id:Scaning)
1. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, and select **Computer Management**.
2. In the left sidebar of the **Computer Management** window, select **Storage** > **Disk Management**.
3. Right click **Disk Management**, and select **Rescan Disks**.
![](https://main.qcloudimg.com/raw/e86a6974b7a49108a4d12a300ffc4c87.png)
4. After the scan is complete, check whether the data disk has the size after the expansion. (In this example, the scan shows that the cloud disk is expanded from 10 GB to 50 GB).
![](https://main.qcloudimg.com/raw/9612c8f95826b401d3a7c111fe632b05.png)


### Extending the file system of an existing partition or creating a partition[](id:Extending)
You can extend the file system of an existing partition or create a partition as instructed below:
<dx-tabs>
::: Extending the file system of an existing partition
1. Right click anywhere on the blank space of the disk, and select **Extend Volume**.
![](https://main.qcloudimg.com/raw/6b19804749d997c9aa008dfa1d37b5cd.png)
2. Follow the **Extend Volume Wizard** to extend the volume.
The new data disk capacity will be added to the original volume.
:::
::: Creating a partition
1. Right click the unallocated space of the disk, and select **New Simple Volume**.
![](https://main.qcloudimg.com/raw/bf0c7eb05e2658d5b426e85112bbaf0a.png)
2. Follow the **New Simple Volume Wizard** to create a simple volume with default settings.
The new data disk capacity will be formatted into a new partition.
:::
</dx-tabs>


## Relevant Operations
### Checking the Virtio driver version[](id:VirtioVersion)
1. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, and select **Device Manager**.
2. Unfold **Storage Controller** items and double click **Tencent VirtIO SCSI controller**.
3. Select the **Driver** tab to check the current version. The version 58005 is used, as shown below.
![](https://main.qcloudimg.com/raw/d6df197dfc47a719edc42a9b7ed0d4f2.png)


## Reference
- [Expanding Cloud Disk Capacity](https://intl.cloud.tencent.com/document/product/362/5747)
- [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


