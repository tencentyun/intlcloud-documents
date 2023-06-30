## Overview

For Tencent Cloud CVMs that using Windows Server 2008 R2, Windows Server 2012 R2, Windows Server 2016, and Windows Server 2019, Virtio ENI drivers are installed to optimize the network performance of virtualization hardware. This document describes how to update the Virtio ENI driver and check the driver version.

## Prerequisites

You have logged in to a Windows CVM.

## Directions

### Viewing system version information

Perform the following steps to view the system version.
1. Log in to the CVM, right-click <img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px">, and select **Run** in the pop-up menu.
2. Enter `cmd` in the pop-up window and press **Enter**.
3. In the pop-up window, run the `systeminfo` command to view the system information.
This document uses Windows Server 2016 Datacenter Edition 64-bit as an example. 
![](https://qcloudimg.tencent-cloud.cn/raw/8c46c9c368201575fafed26272638544.png)

### Updating the Virtio ENI driver

<dx-alert infotype="notice" title="">
The CVM will be disconnected briefly during the update. Please make sure that this will not affect your service before continuing. The CVM needs to be restarted after the update.
</dx-alert>


1. Download the Virtio ENI driver installation file for the operating system version by using the browser in the CVM. 
Choose the download address based on the network environment:
 - **Public network download address**: `http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
 - **Private network download address**: `http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
2. After the download is completed, double-click the installer and click **Next**.
3. Keep "VirtioDrivers" checked by default and click **Next**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/e77875fd9fdac5364188bc989bba0c05.png)
4. Select the installation location and click **Install**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d38b32cba76dbb2cdfad95bae3de1f58.png)
5. In the Windows Security pop-up window, check **Always trust the software from Tencent Technology (Shenzhen) Company Limited** and click **Install**.
During the installation process, choose **Install this driver software anyway** when prompted.      
6. Follow the prompt to restart the computer to complete the update.


### Checking the driver version

1. Right-click <img src="https://qcloudimg.tencent-cloud.cn/raw/67b4c8b9bac6c8f0c8a60a5ed9c6b5dd.png" style="margin:-3px 0px"> and select **Run** in the pop-up menu.
2. In the **Run** window, enter **ncpa.cpl** and press **Enter**.
2. In the **Network Connection** window, right-click the "Ethernet" icon and choose **Properties**.
4. In the **Ethernet Properties** window, click **Configure**.
4. In the **Tencent Virtio Ethernet Adapter Properties** window, select the **Driver** tab to see the current driver version.


