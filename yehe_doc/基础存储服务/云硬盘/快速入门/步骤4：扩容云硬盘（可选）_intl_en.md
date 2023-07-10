## Overview
You can expand a cloud disk to increase its storage space. This document describes how to expand a cloud disk via the console, and assign its expanded capacity to an existing file system.

<dx-alert infotype="explain" title="">
For more information on cloud disk expansion, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5747).
</dx-alert>



## Note
To protect important data, you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your cloud disk data before expanding it.

## Prerequisites
You have [initialized the `cbs-test` cloud disk](https://intl.cloud.tencent.com/document/product/362/31645).

## Directions
<dx-tabs>
::: Expanding cloud disks (Windows CVMs)[](id:windows)
### Expanding cloud disks via the console
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar. 
2. Select **More** > **Expand** on the right of the target cloud disk.

3. In the **Expand Disk Capacity** pop-up window, select the new capacity and click **Next**.
4. Click **Adjust Now**.

### Rescanning the disk

<dx-alert infotype="explain" title="">
This section uses a CVM instance with Windows Server 2012 R2 DataCenter 64-bit English installed as an example. Note that the steps may vary by operating system version.
</dx-alert>


1. Log in to the Windows CVM instance as the admin user. See [Logging in to Windows Instance Using RDP (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435). 
2. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> in the lower-left corner, and select **Computer Management**.
3. Right-click **Disk Management** and select **Rescan Disks**.
4. After the scan is complete, check whether the data disk has the size after the expansion.

### Extending file systems of an existing partition

<dx-alert infotype="explain" title="">
This document takes extending file systems of the existing partition as an example, that is, assigning the expanded capacity to the existing E drive. For more information, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
</dx-alert>


1. Right-click the blank space of the disk and select **Extend Volume**.

2. Follow the **Extend Volume Wizard** to extend the volume.
The new data disk capacity will be added to the original volume.
:::
::: Expanding cloud disks (Linux)[](id:linux)
### Expanding cloud disks via the console
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar. 
2. Select **More** > **Expand** on the right of the target cloud disk.

3. In the **Expand Disk Capacity** pop-up window, select the new capacity and click **Next**.
4. Click **Adjust Now**.

### Extending a file system (Linux CVMs)


<dx-alert infotype="explain" title="">
- This section uses a Linux CVM instance with CentOS 7.8 installed as an example. Note that the steps may vary by operating system version.
- This section takes extending file systems of the existing partition as an example, that is, assigning the expanded capacity to `/dev/vdb`. For more information, see [Online Extending Partitions and File Systems](https://www.tencentcloud.com/document/product/362/39993).
</dx-alert>


1. Run the following command to extend the EXT file system.
```shellsession
resize2fs /dev/vdb
​``` The returned result is as shown below:
![](https://main.qcloudimg.com/raw/181bba4f10d3d5b48e2cbf331121affd.png)
2. Run the following command to view the result.
​```shellsession
df -TH
``` If information similar to what is shown below is returned, the file system has been extended successfully.
![](https://main.qcloudimg.com/raw/7bb79ee4eca78a6ae77d2747967c0647.png)
:::
</dx-tabs>

## References
- [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600)
- [Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638)

