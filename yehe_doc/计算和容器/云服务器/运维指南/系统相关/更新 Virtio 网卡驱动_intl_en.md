## Overview

Windows Server 2008 R2 Enterprise SP1 and Windows Server 2012 R2 Tencent Cloud CVMs use Virtio ENI drivers to optimize the network performance of virtualization hardware. Tencent Cloud will continue to improve ENIs for a better performance and easy troubleshooting. This document describes how to update the Virtio ENI driver and check the driver version.

## Prerequisites

You have logged in to a Tencent Cloud CVM.

## Directions

### Viewing system version information

Perform the following steps to view the system version.
1. Log in to a CVM and access the **System** window according to the operating system:
 - **Window Server 2008 R2 Enterprise SP1**: right-click **This PC** > **Properties** on the desktop.
 - **Windows Server 2012 R2**: open **Control Panel**, and select **System**.
2. In the **View basic information about your computer** section, you can see the system version information.   

### Updating the Virtio ENI driver
>! The CVM will be disconnected briefly during the update. Please make sure that this will not affect your service before continuing. The CVM needs to be restarted after the update.
>
1. Open the browser and enter the following address to download the Virtio ENI driver installer for Window Server 2008 R2 and Windows Server 2012 R2. 
Choose the download address based on the network environment:
 - Public network download address: `http://mirrors.tencent.com/install/windows/virtio_64_10003.msi`
 - Private network download address: `http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi`
2. After the download is completed, double-click the installer, choose the **Classic** installation mode, and click **Next**.
3. In the Windows Security pop-up window, check **Always trust the software from Tencent Technology (Shenzhen) Company Limited** and click **Install**. 
During the installation process, choose **Install this driver software anyway** when prompted.      
4. Restart the computer as prompted.


### Checking the driver version

1. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;">, type **ncpa.cpl** in the Run box, and press **Enter**.
2. In the **Network Connection** window, right-click the "Ethernet" icon and choose **Properties**.
3. In the **Ethernet Properties** window, click **Configure**.
4. In the **Tencent Virtio Ethernet Adapter Properties** window, select the **Driver** tab to see the current driver version.


