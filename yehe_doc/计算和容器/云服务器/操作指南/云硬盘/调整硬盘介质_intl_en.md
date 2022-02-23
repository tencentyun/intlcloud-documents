
## Overview
Tencent Cloud CVM supports adjusting the storage hardware media, which enables you to flexibly respond to diversified storage needs of different businesses.
Tencent Cloud provides two types of storage media: [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) and [Local Storage](https://intl.cloud.tencent.com/zh/document/product/213/5798). A local disk can be converted to a cloud disk. This document describes how to change the disk media type.
The downsides of CVMs with local disks are as follows:
- The configuration cannot be customized due to the limit of host resources.
- Features such as snapshots and creation acceleration are not supported.
- Low data reliability.
- Host failures will have a longer impact.

To avoid these downsides, you can convert the local disks attached to your CVMs to cloud disks.

<span id="LocalDiskPrecondition"></span>
## Prerequisites
- **CVM Status**
 Make sure that the related CVM is shut down.
- **Unsupported CVM Types**
 - Spot instances
 - Big data and high I/O models 
 - Bare metal instances
- **CVM Configuration**
 - At least one of the CVM’s system disk and data disks must be **HDD** or **SSD local disk**.
 - There are available cloud disks that have matched size with local disks in the availability zone where the CVM resides.
 - The adjustment will convert **all** of the local disks to cloud disks if both the system disk and data disks of the CVM are local disks. You will also be able to configure the cloud disk type for each disk separately.
 In other words, the disk media change of a CVM whose disks are all local disks applies to all of its disks, rather than only system disk or data disks.
 - Changing the cloud disk media will not resize the disk. You can [expand the cloud disk](https://intl.cloud.tencent.com/document/product/362/5747) after changing the media type.
 - This operation will not change the lifecycle of a CVM, instance ID, private/public IP, disk name, and mount point.

<span id="LocalDiskNotice"></span>
## Notes

- This conversion needs to copy all the data from the local disk to the cloud disk. Depending on the disk size and transmission speed, this could take some time.
- You can only convert local disks to cloud disks. The conversion CANNOT be reverted.
- **After the adjustment, we recommend you to start up and log in to the CVM to check the data integrity**.

## Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and access the **Instances** page.
>? If the CVM has already been shut down, go to [Step 3](#step3).
2. (Optional) Locate the target CVM, and click **More** > **Instance Status** > **Shutdown** under the **Operation** column to shut it down.
<span id="step3"></span>
3. Under the **Operation** column, click **More** > **Resource Adjustment** > **Change Disk Media Type** .
4. In the pop-up window, select the target cloud disk type, check **I have read and agreed to Rules for Changing Disk Media Type**, and click **Change Now**.
5. Double-check the information, make a payment if applicable, and wait for the process to complete.
 
