## Overview

Microsoft Terminal Services Client (MSTSC) is commonly used for file upload to a Windows CVM. This document describes how to upload files from a Windows computer to a Windows CVM using MSTSC.

## Prerequisites

Make sure the Windows CVM can access the public network.

## Directions
<dx-alert infotype="explain" title="">
This document uses a Windows 7 computer as an example. The procedure may vary slightly according to the operating system version.
</dx-alert>


### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/43f0fa221ab8a5483f1aa7a2698e4cf1.png)

### Uploading files
1. On your local computer, use the **Windows+R** shortcut to open the **Run** window.
2. In the **Run** window, enter **mstsc** and click **OK** to open the **Remote Desktop Connection** window.
3. In the pop-up dialog box, enter the public IP address of the CVM and click **Show Options**.
4. On the **General** tab, enter the CVM public IP address and username "Administrator".
5. Select the **Local Resources** tab and click **More**.
6. In the **Local devices and resources** pop-up window, select the **Drives** module, select the local disk where the file to be uploaded to the Windows CVM instance is located, and click **OK** as shown below:
7. After completing the local configuration, click **Connect** and enter the Windows CVM instance's login password in the **Windows Security** pop-up window to log in to the instance remotely.
8. Select <img src="https://main.qcloudimg.com/raw/ef8fb18be7880d8b48ce402b973f22dc.png" style="margin:-3px 0px"> and click **Computer** on the Windows CVM, and you can see the local disk attached.
9. Double click to open the attached local disk. Copy desired local files to another drive of the Windows CVM.
For example, copy the file A from local disk (E) to the C drive of Windows CVM.

### Downloading files
To download files from Windows CVM to your computer, you only need to copy desired files from the CVM to the attached local disk.

