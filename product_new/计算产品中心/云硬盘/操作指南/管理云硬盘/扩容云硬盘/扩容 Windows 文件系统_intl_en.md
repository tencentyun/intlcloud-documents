## Scenario

After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign the expanded capacity to an existing partition, or format it into an independent new partition.

If you expand a cloud disk when it is mounted to a running CVM, you need to **Rescan Disk** to recognize the disk capacity after expansion.
If you expand a cloud disk when it is not yet mounted or mounted to a CVM that is shut down, the disk capacity after expansion will be automatically recognized.

## Notes

- Extending the file system may affect existing data. We strongly recommend that you manually [create a snapshot] to back up your data before performing the operation.
- To extend the file system, you need to [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928) or rescan the disk, which will lead to business interruption for a certain period. We recommend you choose an appropriate time for this operation.

## Prerequisites

- You have [expanded the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Windows CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5435) the Windows CVM on which you want to expand partitions and the file system.

## Directions
>- When you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), if the cloud disk is mounted to a CVM that is in normal operating status, you must [rescan the disk](#Scanning) to recognize the cloud disk capacity after expansion before [extending the volume](#Extending).
>- When you [expand a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), if the cloud disk is not yet mounted or mounted to a CVM that is shut down, you can proceed directly to [extending the volume](#Extending).

<span id="Scanning"></span>
### Rescanning the disk (optional)

1. Open **Computer Management**.
2. In the left sidebar, select **Storage**>**Disk Management**.
3. Right click **Disk Management**, and select **Rescan Disk**, as shown in the following figure:
4. After completing the scan, check whether the data disk has changed to the size after expansion (in this example, the scan shows that the cloud disk has expanded from 10GB to 50GB), as shown in the following figure:

<span id="Extending"></span>
### Extending Volumes

1. Right click any white area of the disk space. Select **Extend Volume**.
2. Follow the Extend Volume Wizard to extend the volume. The newly added data disk space will be merged into the original volume. This is shown in the following figure:

## Related Actions
[Expanding partitions and file systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)

