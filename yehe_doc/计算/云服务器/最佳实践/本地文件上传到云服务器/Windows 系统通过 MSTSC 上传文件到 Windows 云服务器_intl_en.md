## Overview

This document describes how to upload files from a local Windows computer to a Windows CVM using Microsoft Terminal Services Client (MSTSC). 

## Prerequisites

Make sure the Windows CVM can access the public network.

## Directions
>? This document takes a Windows 7 computer as an example. The procedure may vary slightly according to the operating system version.
>
### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files.

### Uploading files
1. Press **Windows + R** on the local computer to open the **Run** window.
2. In the **Run** pop-up window, enter **mstsc**, and click **OK** to open the **Remote Desktop Connection** dialog box.
3. In the pop-up dialog box, enter the public IP address of the CVM and click **Show Options**.
4. On the **General** tab, enter the CVM public IP address and username “Administrator”.
5. Select the **Local Resources** tab and click **More**.
6. In the **Local devices and resources** pop-up window, select the **Drives** module, check the local disk where the files to upload locate, and click **OK**.
7. After the local configuration is complete, click **Connect** to log in to Windows CVM remotely.
8. Select <img src="https://main.qcloudimg.com/raw/ef8fb18be7880d8b48ce402b973f22dc.png" style="margin:-3px 0px"> and click **Computer** on the Windows CVM, and you can see the local disk attached.
>? This step uses a Tencent Cloud Windows CVM with Windows Server 2016 operating system as an example. The procedure may vary slightly according to the operating system version.
>
9. Double click to open the attached local disk. Copy desired local files to another drive of the Windows CVM.
For example, copy the file A from local disk (E) to the C drive of Windows CVM.

### Downloading files
To download files from Windows CVM to your computer, you only need to copy desired files from the CVM to the attached local disk.


