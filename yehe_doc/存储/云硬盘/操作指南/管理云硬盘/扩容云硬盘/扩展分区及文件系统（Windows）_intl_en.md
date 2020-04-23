## Scenario

After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign the expanded capacity to an existing partition, or format it into an independent new partition.
If you expand a cloud disk when it is mounted to a running CVM, you need to **Rescan Disk** to recognize the disk capacity after expansion.
If you expand a cloud disk when it is not yet mounted or mounted to a CVM that is shut down, the disk capacity after expansion will be automatically recognized.

>
>- Extending the file system may affect the existing data. We strongly recommend that you manually [Create a Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before performing the operation.
>- To extend the file system, you need to [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928) or rescan the disk, which will lead to business interruption for a certain period. We recommend you choose an appropriate time for this operation.
>


## Prerequisites

- You have [expanded the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Windows CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5435) the Windows CVM on which you want to expand partitions and the file system.
>This document uses the CVM running on Windows Server 2012 R2 as an example. The expansion operations on different operating systems may be different. This document is for reference only.
>

## Directions
>
>- If, when you [Expand a Cloud Disk](https://intl.cloud.tencent.com/document/product/362/5747), the CVM to which the cloud disk is mounted is in normal operating status, you must [Rescan the Disk](#Scanning) to recognize the expanded cloud disk space before [Extending the Volume](#Extending).
>- When you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), if the cloud disk is not yet mounted or mounted to a CVM that is shut down, you can proceed directly to [extending the volume](#Extending).

<span id="Scanning"></span>
### Rescanning the disk (optional)
1. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, and select **My Computer**.
2. In the left sidebar of the "My Computer" window, select **Storage**>**Disk Management**.
3. Right click **Disk Management**, and select **Rescan Disk**.

4. After the scan is complete, check whether the data disk has changed to the size after expansion. (In this example, the scan shows that the cloud disk expanded from 10GB to 20GB).

<span id="Extending"></span>
### Extending Volumes

1. Right click any white area of the disk space. Select **Extend Volume**.
2. Complete the expansion according to the on-screen instructions,
and the new data disk capacity will be added to the origin volume.

## Related Actions
[Expanding partitions and file systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)
