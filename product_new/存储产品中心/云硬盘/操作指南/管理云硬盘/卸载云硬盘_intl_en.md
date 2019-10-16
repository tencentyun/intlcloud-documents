## Scenario

When you need to mount an elastic cloud disk that is a **data disk** on another CVM, you can unmount this elastic cloud disk from a CVM, and then mount it to other CVMs. **Unmounting an elastic cloud disk does not erase data on this disk.**
Currently, unmounting of elastic cloud disks that are **data disk** is supported. You cannot unmount system disks or non-elastic cloud disks. **To unmount a cloud disk, you must execute `umount` (Linux) or offline (Windows) operations. Otherwise, the elastic cloud disk may not be recognized by the CVM next time it is mounted**

## Prerequisites

Before unmounting the data disk, make sure you understand the following prerequisites:
- In Windows operating systems:
 - To prevent data loss, we recommend that you suspend read and write operations on all file systems of the disk. Otherwise, data that has not been read or written will be lost.
 - When unmounting an elastic cloud disk, you must first set the disk to offline state. Otherwise, you may not be able to remount the elastic cloud disk unless you restart the CVM. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/47bf28a34b3a4c23c7ac376a36db85eb.png)
- In Linux operating systems:
 - You must first [log In](https://intl.cloud.tencent.com/document/product/213/5436) to the instance, and perform a `umount` operation on the elastic cloud disk you want to unmount. If you directly force unmounting without executing the `umount` operation, the problem shown in the following figure may occur during shutdown and bootup:
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
- If you create a LVM logical volume on the CVM, unmounting the disk directly from the console will cause part of the device data to remain in the CVM memory. If a CVM application attempts to traverse or access this device, a system error will occur. As a result, you must first execute the following operations (this example assumes that logical volume /dev/test/lv1 is created based on /dev/vdb1, and is mounted under the /data directory):
 a. Execute the `umount  /data` command to unmount the disk from the corresponding mounting point in the CVM.
 b. Execute the `lvremove /dev/test/lv1` command to remove the LV. If there are multiple LVs, remove all LVs one by one.
 c. Execute the `vgremove test` command to remove the VG.
 d. Execute the `pvremove /dev/vdb1` command to remove the PV.
 e. Modify the `/etc/fstab` file to avoid the continuous mounting of the corresponding LV on next bootup.

## Directions

### Using the condole to unmount cloud disks

1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. You can use the following method to unmount a cloud disk:
    a. Single unmount: In the row of the target cloud disk with the status **Mounted**, click **More**>**Unmount**.
    b. Batch unmount: Select multiple target cloud disks with the status **Mounted** and click **Unmount** at the top of the list.
![](https://main.qcloudimg.com/raw/4f62d6eeb85839f0762044db68da15be.png)
3. In the **Unmount Cloud Disk** prompt box that pops up, confirm the warning and click **Confirm** to unmount.

### Using the API to unmount cloud disks

You can use the `DetachDisks` API to unmount a cloud disk. For more information, see [Unmounting cloud disks](https://intl.cloud.tencent.com/document/product/362/16316).

