
## Scenario
You can adjust the storage hardware media as needed.
Tencent Cloud provides two types of block storage, i.e., [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) and [Local Storage](https://intl.cloud.tencent.com/document/product/213/5798). We currently support the change of local disks to cloud disks. This document describes how to change disk media type.
The downside of CVMs with local disks:
- The configuration cannot be customized due to the limit of host resources.
- Features such as snapshots and creation acceleration are not supported.
- Low data reliability.
- Host failures will have a longer impact.

To avoid the downside of CVMs with local disks, you can change the existing CVMs with local disks in your account to CVMs with cloud disks.

<span id="LocalDiskPrecondition"></span>
## Prerequisites
- **CVM Status**
 This operation can only be done when a CVM is in the **Shut down** state. Please shut down your CVM first.
- **CVM Type**
 - Spot CVMs do not support the change of local disks to cloud disks.
 - Dedicated CVMs do not support the change of local disks to cloud disks.
 - CVMs such as big data model D1 and D2 and high I/O model I3 and I4 do not support the change of local disks to cloud disks.
 - Bare metal instances do not support the change of local disks to cloud disks.
- **CVM Configuration**
 - You can change local disks to cloud disks only when there is at least one **regular local disk** or **SSD local disk** among the system disk and data disks of the CVM.
 - You can change local disks to cloud disks only when cloud disks are available in the availability zone of the CVM and the size of the local disks is within the range supported by cloud disks.
 - If both the system disk and the data disks of the CVM are local disks, when you change the disk media type, it will apply to **all** of the local disks of the CVM. You will also be able to configure the cloud disk type for each disk separately.
 That means when you change the disk media type for a CVM whose disks are all local disks, you cannot change only the system disk or only the data disks to cloud disks. If you make the change, it will apply to all the disks.
 - Changing the media type of a disk will not change its size. After you change the media type, you may [expand cloud disks](https://intl.cloud.tencent.com/document/product/362/5747).
 - Changing local disks to cloud disks will not change the life cycle of a CVM, instance ID, internal/external network IP, disk name, and mount point.

<span id="LocalDiskNotice"></span>
## Notes

- When you change a local disk to a cloud disk, all the data from the local disk needs to be copied to the cloud disk. Depending on the disk size and transmission speed, this could take some time. 
- You can only change local disks to cloud disks, not the other way around.
- **It is recommended to start and log in to the CVM to check if there is any data loss after the change is completed**.

## Directions
1. Log in to the CVM console and go to **Instances**.
> If the CVM has already been shut down, go to [Step 3](#step3).
2. To the right of the CVM you want to make change to, click **More** > **Instance Status** > **Shutdown** to shut down the CVM.
<span id="step3"></span>
3. To the right of the CVM you want to make change to, click **More** > **Resource Adjustment** > **Change Disk Media Type**.
4. In the pop-up window, select the cloud disk type you want to use for the system disk and the data disks, check the consent box, and click **Convert Now**.
5. Double-check the information, make a payment if applicable, and wait for the process to complete.
 
