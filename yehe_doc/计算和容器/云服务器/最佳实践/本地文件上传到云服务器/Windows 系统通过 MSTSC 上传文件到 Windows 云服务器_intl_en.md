## Scenario

The common method for file upload to Windows CVM is to use Microsoft Terminal Services Client. This document describes how to upload files to Windows CVM using remote desktop connection on a local Windows computer.

## Prerequisites

Make sure the Windows CVM can access the public network.

## Directions
> The following takes the local computer with Windows 7 operating system as an example. The specific steps may vary by operating systems.
>
### Obtaining a public IP
Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index). On the instance list page, record the public IP of the CVM to which you want to upload files.

### Uploading a file
1. Use the shortcut key **Windows + R** on the local computer to open the **Run** window.
2. In the pop-up **Run** window, enter **mstsc**, and click **OK** to open the **Remote Desktop Connection** box.
3. In the **Remote Desktop Connection** box, enter the public IP address of the CVM and click **Show Options**.
4. On the **General** tab, enter the CVM public network IP address and user name Administrator.
5. Select the **Local Resources** tab and click **More**.
6. In the pop-up **Local devices and resources** window, select the **Drives** module, check local disks where files to be uploaded to Windows CVM are located, and click **OK**.
7. After the local configuration is complete, click **Connect** to log in to Windows CVM remotely.
8. Click **Start** > **Computer** on Windows CVM, and you can see the local disks mounted to the CVM.
9. Double-click to open the mounted local disks, and copy the local files to other hard disks of Windows CVM to complete file uploads.
For example, copy file A from local disk (E) to disk C of Windows CVM.

### Downloading a file
To download files from Windows CVM to the local computer, refer to the file upload operations above and copy the required files from Windows CVM to the mounted local disks to complete file downloads.
