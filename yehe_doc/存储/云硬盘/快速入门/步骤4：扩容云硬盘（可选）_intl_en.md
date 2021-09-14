## Overview
You can expand a cloud disk to increase its storage space. This document describes how to expand a cloud disk via the console, and assign its expanded capacity to an existing file system.
>?For more information on expanding cloud disks, see [Expanding Cloud Disk Capacity](https://intl.cloud.tencent.com/document/product/362/5747).
>

## Notes
To protect important data, you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your cloud disk data before expanding it.

## Prerequisites
You have [initialized the `cbs-test` cloud disk](https://intl.cloud.tencent.com/document/product/362/31646).

## Directions

#### Expanding cloud disks (Windows)
### Expanding cloud disks via the console
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar. 
2. Locate the cloud disk to expand, and click **More** > **Expand** under the **Operation** column on the right.

3. In the **Expand Disk Capacity** pop-up window, select a new capacity and click **Next**.
4. Click **Adjust Now**.

### Rescanning the disk
>?This document uses a CVM with Windows Server 2012 R2 DataCenter 64-bit Chinese installed as an example. Note that the steps may vary according to the operating system version. 
>
1. Log in to the CVM as the admin. See [Logging in to Windows Instance Using RDP](https://intl.cloud.tencent.com/document/product/213/5435). 
2. On the desktop, right click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> in the lower-left corner, and select **Computer Management**.
3. Right click **Disk Management**, and select **Rescan Disk**.
4. After scanning, check whether the size of data disk has been expanded.

### Extending file systems of an existing partition
>?In this example, we will assign the expanded capacity to the existing E drive. For more information, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
>
1. Right click anywhere on the blank space of the disk, and select **Extend Volume**.
2. Follow the Extend Volume Wizard to extend the volume.
The new data disk capacity will be added to the original volume.

#### Expanding cloud disks (Linux)
### Expanding cloud disks via the console
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar. 
2. Locate the cloud disk to expand, and click **More** > **Expand** under the **Operation** column on the right.
3. In the **Expand Disk Capacity** pop-up window, select a new capacity and click **Next**.
4. Click **Adjust Now**.

### Extending a file system
>?
>- This document uses a CVM with CentOS 7.8 installed as an example. Note that the steps may vary according to the operating system version. 
>- In this example, we will assign the expanded capacity to `/dev/vdb`. For more information, see [Online Extending Partitions and File Systems](https://intl.cloud.tencent.com/document/product/362/39999).
>
1. Run the following command to extend the EXT file system.
```
resize2fs /dev/vdb
​``` 
The following information will appear:

![](https://main.qcloudimg.com/raw/181bba4f10d3d5b48e2cbf331121affd.png)
2. Run the following command to view the result.
```
df -TH
``` 
If information similar to what is shown below is returned, the file system has been extended.

![](https://main.qcloudimg.com/raw/7bb79ee4eca78a6ae77d2747967c0647.png)



## Documentation
- [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600)
- [Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638)
