## Introduction

After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition.
- If you expand a cloud disk that is mounted to a running CVM, you need to **Rescan Disk** to recognize the disk capacity after expansion.
- If you expand a cloud disk that is unmounted or mounted to an inactive CVM, the disk capacity after expansion will be automatically recognized.

>
>- Extending the file system may affect the existing data. We strongly recommend you to manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before the operation.
>- To extend the file system, you need to [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928) or rescan the disk, which will lead to business interruption for a certain period. We recommend that you choose an appropriate time for this operation.
>- After extending the file system, we strongly recommend you to [rescan disks](#Scanning) to recognize the capacity. If you **Refresh** the system or do other operations, the expanded capacity may not be recognized.
>


## Prerequisites

- You have [expanded the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Windows CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5435) the Windows CVM on which you want to extend partitions and the file system.
>This document describes how to expand a disk mounted to a CVM on Windows Server 2012 R2. The expansion may slightly vary with operating systems, so this document is for reference only.
>

## Directions
>
>- If you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747) that is mounted to a running CVM, you must [rescan disk](#Scanning) to recognize the expanded cloud disk capacity before [extending volumes](#Extending).
>- If you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747) that is unmounted or amounted to an inactive CVM, you can proceed directly to [extending the volume](#Extending).

<span id="Scanning"></span>
### Rescan the disk
1. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, and select **Computer Management**.
2. In the left sidebar of the **Computer Management** window, select **Storage** -> **Disk Management**.
3. Right click **Disk Management**, and select **Rescan Disks**, as shown below:
4. After the scan is complete, check whether the data disk has the size after the expansion. (In this example, the scan shows that the cloud disk is expanded from 10GB to 50GB). 

<span id="Extending"></span>
### Extend volumes

1. Right click any white area of the disk space. Select **Extend Volume**.
2. Follow the Extend Volume Wizard to extend the volume.
The new data disk capacity will be added to the original volume.

## Related Actions
‏[Extending Linux file systems](https://intl.cloud.tencent.com/document/product/362/31602)
