## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its storage capacity at any time without losing any data in it.
After the capacity expansion, you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition. For more information, see [Expanding Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Expanding Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/zh/document/product/362/31602).
>!MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.

## Expanding Data Disks
To expand a cloud data disk, you can try the following three methods.
>!If there are multiple cloud disks of the same capacity and type mounted to your CVM, you can find the desired one as instructed in [Querying data disks](#distinguish). 
>

### Expanding data disks via the CVM console (recommended)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. Locate the CVM on which you want to expand the data disk, and select **More** > **Resource Adjustment** > **Expand Data Disk** in the **Operation** column.
3. Select the data disk to be expanded in the pop-up window, and click **Next**.
4. Select a new capacity (it must be greater than the current capacity.) and click **Next**.
5. Read the notes and click **Adjust Now**.

6. Assign the newly-added capacity to an existing partition or format it into an independent new partition. See [Expanding Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Expanding Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/zh/document/product/362/31602).

### Expanding data disks via the CBS console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Locate the cloud disk to be expanded, and select **More** > **Expand** in the **Operation** column.
3. Select a new capacity. It must be greater than the current capacity.
4. Complete the payment.
5. Assign its expanded capacity to an existing partition or format it into an independent new partition. See [Expanding Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Expanding Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/zh/document/product/362/31602).

### Expanding data disks via API
You can use the `ResizeDisk` API to expand the specified cloud disks. For more information, see [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).

## Expanding System Disks
To expand a cloud system disk, you can try the following two methods.

### Expanding system disks via the CVM console (recommended)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index). Locate the CVM on which you want to expand the system disk, and select **More** > **Resource Adjustment** > **Expand System Disk** in the **Operation** column.
2. Select the system disk to be expanded in the pop-up window, and click **Next**.
3. Select a new capacity (it must be greater than or equal to the current capacity.) and click **Next**.
4. Read the notes, select **Agree to forced shutdown** and click **Adjust Now**.

5. After expanding the capacity on the console, check the cloudinit configuration of the CVM as instructed in [Checking the cloudinit configuration for Linux instances](#confirmLinuxConfig) or [Checking the cloudinit configuration for Windows instances](#confirmwindowsConfig). Then expand partitions and file systems as needed.


### Expanding system disks by reinstalling the system
You can also expand the system disk by [reinstalling the system](https://intl.cloud.tencent.com/document/product/213/4933) in the CVM.

[](id:distinguish)
## Relevant Operations
### Querying data disks
You can query all the cloud disks mounted to a CVM as instructed below:

#### Linux
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command to query all mounted cloud disks.
```
ls -l /dev/disk/by-id
​```
The following information appears:
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
Note that `disk-xxxx` is the ID of a cloud disk. You can go to the [CBS console](https://console.cloud.tencent.com/cvm/cbs) to check the cloud disk.

#### Windows
1. [Log in to a Windows instance](https://intl.cloud.tencent.com/zh/document/product/213/5435).
2. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">, and select **Run**.
3. Enter `cmd` in the pop-up window and press **Enter**.
4. Execute the following command to query the cloud disks mounted to the CVM.
```
wmic diskdrive get caption,deviceid,serialnumber
```
You can also execute the following command
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
The following information appears:
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
Note that `disk-xxxx` is the ID of a cloud disk. You can go to the [CBS console](https://console.cloud.tencent.com/cvm/cbs) to check the cloud disk.


[](id:confirmLinuxConfig)
### Checking the cloudinit configuration for Linux instances
After the system disk is expanded, [log in to the Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) and check whether the `/etc/cloud/cloud.cfg` file contains the `growpart` and `resizefs` configuration items.
 - If yes (as shown below), the operation is completed.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: expands the partition to the disk size.
    - **resizefs**: expands or adjusts the `/` partition file system to the partition size.
 - If no, you need to manually assign the newly-added capacity to an existing partition, or format it into an independent new partition. See [Expanding Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/zh/document/product/362/31602).

[](id:confirmwindowsConfig)
### Checking the cloudinit configuration for Windows instances
After the system disk is expanded, [log in to the Windows instance](https://intl.cloud.tencent.com/zh/document/product/213/5435) and check whether the `ExtendVolumesPlugin` configuration item exists in the `plugin` under `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`.
 - If yes, the operation is completed.
 - If no, you need to manually assign the newly-added capacity to an existing partition, or format it into an independent new partition. See [Expanding Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
