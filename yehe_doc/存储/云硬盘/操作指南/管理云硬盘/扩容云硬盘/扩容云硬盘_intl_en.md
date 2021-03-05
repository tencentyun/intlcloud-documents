## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data in it.
After a cloud disk is expanded, you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition. For more information, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).
>! MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.

## Expanding Data Disks
If the cloud disk is a data disk, you can expand it using the following three methods.

### Expanding system disks via the CVM console (recommended)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. Locate the CVM on which you want to expand the data disk, and select **More** > **Resource Adjustment** > **Expand Data Disk** in the **Operation** column.
3. Select the data disk to be expanded in the **Expand Data Disk** pop-up window, and click **Next**.
4. Select a new capacity (it must be greater than or equal to the current capacity) and click **Next**.
5. Read the notes and click **Adjust Now**, as shown below:
6. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Expanding data disks via the CBS console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Locate the cloud disk to be expanded, and select **More** > **Expand** in the **Operation** column.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Expanding data disk via API
You can use the `ResizeDisk` API to expand the specified cloud disks. For more information, see [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).

## Expanding System Disks
If the cloud disk works as a system disk, you can expand it using the following two methods.

### Expanding system disks via the CVM console (recommended)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index). Locate the CVM on which you want to expand the system disk, and select **More** > **Resource Adjustment** > **Expand System Disk** in the **Operation** column.
2. Select the system disk to be expanded in the pop-up window, and click **Next**.
3. Select a new capacity (it must be greater than or equal to the current capacity) and click **Next**.
4. Read the notes, select **Agree to a forced shutdown** and click **Adjust Now**, as shown below:
5. After the expansion is completed on the console, check the cloudinit configuration for [Linux instances](#confirmLinuxConfig) or [Windows instances](#confirmwindowsConfig) depending on the operating system. Then extend partitions and file systems as needed.


### Expanding system disks by reinstalling the system
You can also expand the system disk by [reinstalling the system](https://intl.cloud.tencent.com/document/product/213/4933).


## Relevant Operations
<span id="confirmLinuxConfig"></span>
### Checking the cloudinit configuration for Linux instances
After the system disk is expanded, [log in to the Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) and check whether the `/etc/cloud/cloud.cfg` file contains the `growpart` and `resizefs` configuration items.
 - If yes, ignore other operations.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: expands the partition to the disk size.
    - **resizefs**: expands or adjusts the partition file systems to the partition size.
 - If no, assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).
<span id="confirmwindowsConfig"></span>
### Checking the cloudinit configuration for Windows instances
After the system disk is expanded, [log in to the Windows instance](https://intl.cloud.tencent.com/zh/document/product/213/5435) and check whether the `ExtendVolumesPlugin` configuration item under `plugin` exists in `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`.
 - If yes, ignore other operations.
 - If no, assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
