## Overview

When you need to mount an elastic cloud disk that is a **data disk** on another CVM, you can unmount this elastic cloud disk from a CVM, and then mount it to other CVMs. **Unmounting an elastic cloud disk does not erase data on this disk.**
Currently, unmounting of elastic cloud disks that are **data disk** is supported. You cannot unmount system disks or non-elastic cloud disks. **To unmount a cloud disk, you must execute `umount` (Linux) or offline (Windows) operations. Otherwise, the elastic cloud disk may not be recognized by the CVM next time it is mounted**

## Prerequisite

Before unmounting the data disk, make sure you understand the following prerequisites:

<dx-tabs>
::: Windows
 - To prevent data loss, we recommend that you suspend read and write operations on all file systems of the disk. Otherwise, data that has not been read or written will be lost.
 - When detaching an elastic cloud disk, you must first set the disk to offline status. Otherwise, you may not be able to reattach the cloud disk unless you restart the CVM instance.

:::
::: Linux
 - You must first [log In](https://intl.cloud.tencent.com/document/product/213/5436) to the instance, and perform a `umount` operation on the elastic cloud disk you want to unmount. If you directly force unmounting without executing the `umount` operation, the problem shown in the following figure may occur during shutdown and bootup:
![](https://main.qcloudimg.com/raw/0176a1c210cf620239d51fb520cfa351.png)
 - If you create a logical volume (LV) in the CVM instance, detaching the disk directly in the console will cause part of the device data to remain in the CVM memory. If a CVM application attempts to traverse or access this device, a system error will occur. Therefore, you must first execute the following operations (this example assumes that the `/dev/test/lv1` LV is created based on `/dev/vdb1` and is attached to the `/data` directory):
 a. Execute the `umount  /data` command to detach the disk from the corresponding mount point in the CVM instance.
 b. Execute the `lvremove /dev/test/lv1` command to remove the LV. If there are multiple LVs, remove them one by one.
 c. Execute the `vgremove test` command to remove the VG.
 d. Execute the `pvremove /dev/vdb1` command to remove the PV.
 e. Modify the `/etc/fstab` file to avoid the continuous mounting of the corresponding LV on next bootup.
:::
</dx-tabs>


## Directions

<dx-tabs>
::: Detaching cloud disks in the console[](id:useConsole)
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following method to unmount a cloud disk:
    a. Detach one cloud disk: Select **More** > **Detach** on the row of the target cloud disk in **Attached** status.
    b. Batch detach cloud disks: Select multiple target cloud disks in **Attached** status and click **Detach** above the list.

3. In the **Detach cloud disk** pop-up window, confirm the warning and click **OK**.
:::
::: Detaching cloud disks via API[](id:useAPI)
You can use the `DetachDisks` API to unmount a cloud disk. For more information, see [Unmounting cloud disks](https://intl.cloud.tencent.com/document/product/362/16316).
:::
</dx-tabs>


## FAQs
If you cannot detach cloud disks from Windows CVM instances in the console, see [Unable to Detach Cloud Disks from CVM Instances for Windows](https://intl.cloud.tencent.com/document/product/362/50064) for troubleshooting.
