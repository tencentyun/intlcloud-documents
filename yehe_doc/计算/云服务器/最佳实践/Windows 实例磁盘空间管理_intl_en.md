## Overview
This document describes how to release disk space on a Windows Server 2012 R2-based Tencent Cloud CVM when the disk space is insufficient. It also describes how to perform routine disk maintenance.

## Directions

### Releasing disk space
You can delete [large files](#deleteLargerFiles) or [obsolete files](#deleteObsoleteFiles) to free up disk space. If the disk space is still insufficient after deleting large and obsolete files, you can expand the disk space. To do this, please see [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
<span id="deleteLargerFiles"></span>
#### Deleting large files
1. Log in to a Windows instance using either [the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435) or [the remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).
2. Click <img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px"> in the bottom toolbar and open the “This PC” window.
3. Select the disk in which you want to free up space, and press **Crtl + F** to open the search tool.
4. Select **Search** -> **Size** and filter files by the system-defined size options, as shown below:
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
>?You can also enter a size in the search box in the upper-right corner of the **This PC** window. For example:
>- Enter “Size: > 500 MB” to search the disk for files larger than 500 MB.
>- Enter “Size: > 100 MB < 500 MB” to search the disk for files larger than 100 MB but less than 500 MB.
>

<span id="deleteObsoleteFiles"></span>
#### Deleting obsolete files
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px"> to open **Server Manager**.
2. Click **Add Roles and Features** under **Manage**.
3. In the pop-up window, click **Next**.
4. Select **Role-based or feature-based installation** and click **Next** twice, as shown below:
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. On the **Select features** page, check **Ink and Handwriting Services** and **Desktop Experience**, as shown below. Click **OK** in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. Click **Next** and then **Install**. Wait for the installation to complete, and restart CVM when prompted.
7. Select <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px"> and click <img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px"> in the top-right corner. Enter **Disk Management** and search.
8. In the pop-up **Disk Cleanup** window, select the target disk and start the cleanup, as shown below:
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### Routine disk maintenance
#### Removing programs regularly
Select **Control Panel** -> **Programs and Features** -> **Uninstall or change a program** to regularly remove obsolete programs, as shown below:
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### Viewing disk usage on the console
The Cloud Monitor feature is automatically enabled once a CVM instance is created. You can view the disk usage by following the steps below:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index) and access the **Instances** page.
2. Select the ID/Name of the target instance to access the details page.
3. Select the **Monitoring** tab to view the instance disk usage, as shown below:
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
