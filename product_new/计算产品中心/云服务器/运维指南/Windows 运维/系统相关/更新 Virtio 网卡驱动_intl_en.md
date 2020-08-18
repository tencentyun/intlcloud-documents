## Scenario

Tencent Cloud's Windows Server 2008 R2 Enterprise SP1 and Windows Server 2012 R2 use Virtio ENI drivers to optimize the network performance of virtualization hardware. Tencent Cloud will continue to improve ENIs for performance improvement and troubleshooting. This document describes how to upgrade the Virtio ENI driver and check the driver version.

## Prerequisites

You have logged in to a Tencent Cloud CVM.

## Directions

### Checking system version information

You can view the system version information in the following steps:
1. Log in to CVM and perform the following operations depending on the operating system you use:
 - **Window Server 2008 R2 SP1**: right-click **Computer** -> **Property** on the desktop.
 - **Windows Server 2012 R2**:  open **Control Panel**, and select **System**.
2. In the **View basic information about your computer** section, you can see the system version information as shown below:
   

### Updating the Virtio ENI driver
> The CVM will be disconnected from the network briefly during the update. Please make sure that this will not affect your service before updating. The CVM needs to be restarted after the update.
>

1. Use the browser of the CVM to download the Virtio ENI driver installer for Window Server 2008 R2 and Windows Server 2012 R2. 
Download the Virtio ENI driver: http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi
2. After the download is completed, double-click the installer, choose the **Classic** installation mode, and click **Next**.

3. In the Windows Security pop-up window, check **Always trust the software from Tencent Technology (Shenzhen) Company Limited** and click **Install** as shown below:
 
During the installation process, if the following box pops up, choose **Install this driver software anyway**.
      
4. Follow the prompt to restart the computer to complete the update.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

### Checking the driver version

1. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;">, type **ncpa.cpl** in the Run box, and press **Enter** as shown below:

2. In the "Network Connections" window, right-click the "Ethernet" icon and choose **Properties**.

3. In the "Ethernet Properties" window, click **Configure**.

4. In the "Tencent Virtio Ethernet Adapter Properties" window, go to the **Driver** tab to see the current driver version as shown below:



