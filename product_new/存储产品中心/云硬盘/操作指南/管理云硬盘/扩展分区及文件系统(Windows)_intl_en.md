## Scenario

After [Expanding a Cloud Disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either categorize the expanded capacity to an existing partition, or format it into a new, independent partition.

If the expanded cloud disk is mounted to a running CVM, you need to **Rescan Disk** to recognize the expanded cloud disk capacity.
If the expanded cloud disk is not mounted, or is mounted to a CVM that is shut down, the expanded capacity will be automatically recognized.

## Prerequisites
>- Extending the file system may affect the existing data. We strongly recommend that you manually [Create a Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before performing the operation.
>- To extend the file system, you need to restart the instance or rescan the disk. This will cause business interruptions, so please perform this operation at a suitable time.
>
>- You have [Expanded the Capacity of the Cloud Disk](https://cloud.tencent.com/document/product/362/5747).
- You have [Mounted the Cloud Disk](https://intl.cloud.tencent.com/document/product/362/5745) to a Windows CVM, and have created a file system.
- You are logged in to the Windows CVM for the partition and the file system to be extended.

## Directions
>- If, when you [Expand a Cloud Disk](https://intl.cloud.tencent.com/document/product/362/5747), the CVM to which the cloud disk is mounted is in normal operating status, you must [Rescan the Disk](#Scanning) to recognize the expanded cloud disk space before [Extending the Volume](#Extending).
>- If, when you [Expand a Cloud Disk](https://intl.cloud.tencent.com/document/product/362/5747), the cloud disk is not yet mounted, or the CVM to which the disk is mounted is shut down, you can proceed directly to [Extending the Volume](#Extending).
>- This article uses the Windows Server 2012 operating system as an example. The expansion operations on different operating systems may be different. This article is for reference only.

<span id="Scanning"></span>
### (Optional) Rescanning the Disk

1. Open **Computer Management**.
2. In the left sidebar, select **Storage** > **Disk Management**.
3. Right click **Disk Management**, and select **Rescan Disks**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/4dcdd9f42a942cba2352c730090ba049.png)
4. After the scan is complete, check whether the data disk has changed to the size after expansion. (In this example, the scan shows that the cloud disk expanded from 10GB to 20GB). This is shown in the following figure:
![](https://main.qcloudimg.com/raw/6cbf3575b9ee5fd1a3620ddf87105789.jpg)

<span id="Extending"></span>
### Extending Volume

1. Right click anywhere in the white area of the disk space. Select **Extend Volume**.
2. Follow the Extend Volume Wizard to extend the volume. The newly added data disk space will be merged into the original volume. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a561eba48c0fb8e903981f2ea82ae6be.png)

## Related Actions
[Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/6734)
