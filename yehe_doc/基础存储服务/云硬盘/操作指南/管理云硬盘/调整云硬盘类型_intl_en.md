## Overview
Tencent Cloud CBS supports the adjustment of storage hardware types when business is in operating state. You can upgrade the type without business interruption to satisfy your business requirements for higher performance. The cloud disk type takes effect immediately after fee payment. For information on fees for adjusting cloud disk types, see [Fees for adjusting cloud disk types](https://intl.cloud.tencent.com/document/product/362/31651).
Currently, only upgrading is supported for adjusting cloud disk types. Downgrading is not supported. Details are as follows:
- A HDD cloud disk can be adjusted to premium cloud storage or SSD cloud disk.
- A premium cloud storage can only be adjusted to SSD cloud disk.
- A SSD cloud disk cannot be upgraded currently.

## Prerequisite
- **CVM Status**
For a cloud disk that has been attached to a CVM instance, you can adjust the cloud disk type only when the CVM instance is in **Running** or **Shutdown** status.
- **Cloud disk status**
- Adjustment of cloud disk types is currently not supported for system disks and non-elastic data disks.
- The adjustment of cloud disk types is not supported in Guangzhou Zone 1.
- The current availability zone has available cloud disk upgrade types. Adjustment of the cloud disk type is only supported when the current disk size is in the range supported by the cloud disk.
- Adjusting the cloud disk type does not change the size of the disk. After adjusting the disk type, you can refer to [Expanding cloud disks](https://intl.cloud.tencent.com/document/product/362/5747) to adjust the disk size.
- Adjusting the cloud disk type does not change the lifecycle, disk ID, disk device name, or mounting point of the cloud disk.

## Notes
- Adjusting the cloud disk type uses the data copying method to copy data of the source cloud disk to the target cloud disk. This operation is limited by the data size and data transfer speed, and may take a while.
- Currently, downgrading of the cloud disk type is not supported. The details are as follows:
 - A HDD cloud disk can be adjusted to premium cloud storage or SSD cloud disk.
 - A premium cloud storage can only be adjusted to SSD cloud disk.
 - A SSD cloud disk cannot be upgraded currently.
- **After the adjustment, we recommend you to start up and log in to the CVM to check the data integrity**.

## Directions

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs), and go to the cloud disk list.
2. On the row of the target cloud disk, select **More** > **Change Disk Media Type**.
3. In the **Change Disk Media Type** pop-up window, select the target cloud disk type, indicate your consent, and click **Change Now**.
4. Make necessary payment if applicable, and wait for the operation to complete.


