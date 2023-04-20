
## Scenario
Windows employs two major file systems, NTFS or FAT32, while EXT is the de factor file system for Linux. When an operating system is changed from Linux to Windows after reinstallation, the data disk remains in its original format. Therefore, the system might not be able to access data disk’s file system. In these cases, you will need to use a format converter to read the data disk. 

This document describes how to read a data disk when the operating system has been [reinstalled](https://intl.cloud.tencent.com/document/product/213/4933) from Linux to Windows.


## Prerequisites
- DiskInternals Linux Reader has been installed on the reinstalled Windows CVM.
Download DiskInternals Linux Reader: `http://www.diskinternals.com/download/Linux_Reader.exe `
- Suppose the data disk mounted to the Linux CVM before reinstallation has two partitions, vdb1 and vdb2, as shown below:
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## Directions
### Mounting a data disk

>! If a data disk has been mounted, skip this step.
>
1. Log in to the [Tencent Cloud CVM Console](https://console.cloud.tencent.com/cvm/).
2. Click **Cloud Block Storage** from the left sidebar to enter the Cloud Block Storage management page.
3. Locate the instance with the reinstalled system, and click **More** > **Mount** on the right as shown below:
![](https://main.qcloudimg.com/raw/a3100055adb58330591e277c4e7f72eb.png)
4. In the pop-up window, select the reinstalled Windows CVM and click **Submit**.

### Viewing data disk information 
1. Run DiskInternals Linux Reader to view the information of newly mounted data disk. `/root/mnt` and `/root/mnt1` correspond to vdb1 and vdb2 respectively, which are the 2 data disk partitions on the Linux CVM before reinstallation as shown below:
>! Note that the Linux data disk is read-only at this time. To perform read and write operations on the data disk as you do on a Windows data disk, back up your needed files and re-format the disk into a standard Windows-supported file system. For more information, please see [Data Disk Partition and Formatting of Windows CVMs](https://intl.cloud.tencent.com/document/product/213/2158).
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. Double-click to enter `/root/mnt` directory, right-click the file you want to copy, and select **Save** as shown below:
![](https://main.qcloudimg.com/raw/f36cbf32a7b423b8800e1fda6ba1c038.png)




