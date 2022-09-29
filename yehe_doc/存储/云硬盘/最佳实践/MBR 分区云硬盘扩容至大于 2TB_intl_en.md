## Overview
When your cloud disk has an MBR partition with a created file system and has been expanded to greater than 2 TB, the file system cannot be expanded to greater than 2 TB. This document describes how to convert the MBR partition to the GPT partition to implement the expansion.

## Notes
- To convert the partition format, you need to replace the original partition. The original partition data will not be deleted in normal cases. However, as the original partition needs to be unmounted, online businesses will be affected.
- Maloperation may cause data losses or exceptions. Proceed with caution. Create a snapshot of the cloud disk for data backup. For detailed directions, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755). If data is lost due to maloperation, you can roll back the data for restoration.


## Directions
1. [Log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to check whether the partition format is MBR.
```shellsession
fdisk -l
```
If the following result is shown (which may vary by operation system), the partition format is MBR.
![](https://qcloudimg.tencent-cloud.cn/raw/294dcfd8c0e243f30ae9d50430ba2cc3.png)
3. Run the following command to unmount the partition.
```shellsession
umount <Mount point>
```
Taking the `/data` mount point as an example, run the following command:
```shellsession
umount /data
```
4. Run the following command to view the unmount result.
```shellsession
lsblk
```
If the `MOUNTPOINT` of the original partition is empty, the unmount is successful. This document takes the `/dev/vdb1` partition as an example. Below is the returned result. ![](https://qcloudimg.tencent-cloud.cn/raw/67123caf1eb7052b07c4c4c186d6c232.png)
5. Run the following command to use the parted partition tool.
```shellsession
parted <Disk path>
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```shellsession
parted /dev/vdb
```
6. Enter `p` and press **Enter** to view the current partition information. Below is the returned information:
![](https://qcloudimg.tencent-cloud.cn/raw/f58f03bf910e52647645e9730c9f0307.png)
7. Enter `rm partition number` and press **Enter** to delete the last partition to be replaced.
In this example, there is only one partition, so you can enter `rm 1` and press **Enter** to delete partition 1.
8. Enter `p` and press **Enter** to view the current partition information. Check whether the last partition has been deleted.
9. Enter `mklabel GPT` and press **Enter** to create a partition in GPT format.
10. Enter `Yes` and press **Enter**.
![](https://qcloudimg.tencent-cloud.cn/raw/b8d89b8f1fc358e2e3c357aa04b1f02c.png)
11. Enter `mkpart primary 2048s 100%` and press **Enter** to create the partition.
Here, `2048s` indicates the initial disk capacity, and `100%` indicates the maximum disk capacity. This is for reference only. You can choose the number of disk partitions and their capacities based on your business needs.
<dx-alert infotype="notice" title="">
Data may be lost in the following cases:
- The configured initial capacity differs from the original partition capacity.
- The configured maximum capacity is smaller than the original partition capacity before the expansion.
</dx-alert> 
12. Enter `p` and press **Enter** to check whether the partition has been replaced successfully. If the following result is shown, the replacement is successful:
![](https://qcloudimg.tencent-cloud.cn/raw/a48c842ae52e696d7ad03cca217638f3.png)
13. Enter `q` and press **Enter** to exit the parted partition tool.
14. Run the following command to mount the partition.
```shellsession
mount <Partition path> <Mount point>
```
Taking the `/dev/vdb1` partition path and `/data` mount point as an example, run the following command:
```shellsession
mount /dev/vdb1 /data
```
15. Run the command to extend the file system.
<dx-tabs>
::: Extending the EXT file system
Run the following command to extend the EXT file system.
```shellsession
 resize2fs /dev/corresponding partition
```
Taking the `/dev/vdb1`partition path as an example, run the following command:
```shellsession
 resize2fs /dev/vdb1
```
:::
::: Extending the XFS file system
Run the following command to extend the XFS file system.
```shellsession
xfs_growfs /dev/corresponding partition
```
Taking the `/dev/vdb1`partition path as an example, run the following command:
```shellsession
xfs_growfs /dev/vdb1

```
:::
</dx-tabs>
14. Set partition auto-mounting as instructed in [Initializing Cloud Disks (≥2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).

At this point, you have converted the MBR partition to the GPT partition. You can run the `df -h` command to view the partition information.
