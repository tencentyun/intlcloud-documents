## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data in it.
After a cloud disk is expanded, you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition. For more information, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).
>!MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and attach a new data disk and use the GPT partition format to copy data.

## Expanding Data Disks
If the cloud disk is a data disk, you can expand it using the following three methods.
>!If multiple cloud disks of the same capacity and type are attached to the CVM, you can identify them using the method shown in [Distinguishing data disks](#distinguish). Select a data disk and expand its capacity as instructed below.

[](id:useCVMConsole)

#### Expanding data disks via the CVM console (recommended)

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. Locate the CVM on which you want to expand the data disk, and select **More** > **Resource Adjustment** > **Expand Data Disk** in the **Operation** column.
3. Select the data disk to be expanded in the pop-up window, and click **Next**.
4. Select a new capacity (it must be greater than or equal to the current capacity) and click **Next**.
5. Read the notes and click **Adjust Now**.
6. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).

[](id:useCBSConsole)
#### Expanding data disks via the CBS console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Locate the cloud disk to be expanded, and select **More** > **Expand** in the **Operation** column.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).

#### Expanding data disks via API[](id:useAPI)
You can use the `ResizeDisk` API to expand the specified cloud disks. For more information, see [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).




## Expanding System Disks
If the cloud disk works as a system disk, you can expand it using the following two methods.

[](id:useCVMconsole)
#### Expanding system disks via the CVM console (recommended)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index). Locate the CVM on which you want to expand the system disk, and select **More** > **Resource Adjustment** > **Expand System Disk** in the **Operation** column.
2. Select the system disk to be expanded in the pop-up window, and click **Next**.
3. Select a new capacity (it must be greater than or equal to the current capacity) and click **Next**.
4. Read the notes, select **Agree to a forced shutdown**, and click **Adjust Now**.
5. After the expansion is completed on the console, check the cloudinit configuration for [Linux instances](#confirmLinuxConfig) or [Windows instances](#confirmwindowsConfig) according to the operating system of the CVM. Then extend partitions and file systems as needed.

[](id:reinstallSystem)
#### Expanding system disks by reinstalling the system
You can also expand the system disk by [reinstalling the operating system](https://intl.cloud.tencent.com/document/product/213/4933) of the CVM instance.



## Operations

[](id:distinguish)

### Distinguishing data disks
Check cloud disks according to the operating system of the CVM.
#### Linux
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the relationship between the elastic cloud disks and the device name.
```
ls -l /dev/disk/by-id
```
The following information will appear:
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
Note that `disk-xxxx` is the ID of a cloud disk. You can use it to view cloud disk details on the [CBS console](https://console.cloud.tencent.com/cvm/cbs).

#### Windows
1. [Log in to a Windows instance](https://intl.cloud.tencent.com/document/product/213/5435).
2. Right click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">, and select **Run**.
3. Enter `cmd` in the pop-up window and press **Enter**.
4. Run the following command to view the relationship between the elastic cloud disks and the device name.
```
wmic diskdrive get caption,deviceid,serialnumber
```
You can also run the following command.

```
wmic path win32_physicalmedia get SerialNumber,Tag
```
The following information will appear:
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
Note that `disk-xxxx` is the ID of a cloud disk. You can use it to view cloud disk details on the [CBS console](https://console.cloud.tencent.com/cvm/cbs).


### Checking the cloudinit configuration
Check cloud disks according to the operating system of the CVM.

[](id:confirmLinuxConfig)
#### Checking the cloudinit configuration for Linux instances
After the system disk is expanded, [log in to the Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) and check whether the `/etc/cloud/cloud.cfg` file contains the `growpart` and `resizefs` configuration items.
 - If yes, ignore other operations.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: extends the partition to the disk size.
    - **resizefs**: extends or adjusts the file system in the `/` partition to the partition size.
 - If no, manually [extend partitions and file systems (Linux)](https://intl.cloud.tencent.com/document/product/362/39995) according to the operating system, and assign its extended capacity to an existing partition, or format it into an independent new partition.

[](id:confirmwindowsConfig)
#### Checking the cloudinit configuration for Windows instances
After the system disk is expanded, [log in to the Windows instance](https://intl.cloud.tencent.com/document/product/213/5435) and check whether the `ExtendVolumesPlugin` configuration item exists under `plugin` in `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`.
 - If yes, ignore other operations.
 - If no, manually [extend partitions and file systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) according to the operating system, and assign its expanded capacity to an existing partition, or format it into an independent new partition.
