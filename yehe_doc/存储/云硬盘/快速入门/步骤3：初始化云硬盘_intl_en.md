## Scenario
This document takes initializing a cloud disk newly mounted to a CVM, creating a file system, and writing a file named `qcloud.txt` as an example to help you understand how to use CBS. For more information on initializing cloud disks, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).

## Prerequisites
You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/31645), and the cloud disk status is **Mounted**.

>The following Windows and Linux CVM OS systems are used:
>- Windows Server 2008
>- CentOS 7.5


## Notes
To protect important data, please see [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409) before performing any operation on your CBS cloud disks.


## Formatting, creating a file system, and writing a file (Windows)
1. [Log in to the Windows instance](https://intl.cloud.tencent.com/document/product/213/5435) as an admin.
2. Enter the disk management interface by selecting **CVM Management**>**Storage**>**Disk Management**.
3. (Optional) Right click the empty disk you need, and select **Online**.
When the disk status changes to **Not Initialized**, it has gone online.
4. (Optional) Right click the cloud disk that has just gone online. Select **Initialize Disk** and then **Master Boot Record** in the pop-up **Initialize Disk** window, and click **OK**.
 >MBR (Main Boot Record) partition format supports a maximum disk capacity of 2 TB, and GPT (GUID Partition Table) supports a maximum disk capacity of 18 EB. If you need a disk capacity larger than 2 TB, please select the GPT partition format.
If the disk partition format is changed after the disk is put into use, the original data on the disk will be erased. Please select the partition format carefully when initializing the disk.
5. Right click the disk you need, and select **New Simple Volume**.
6. Enter the simple volume size, and click **Next**.
7. Select a drive letter or drive path, and click **Next**. 
8. Select the file system, perform a quick format, and then click **Next**.
8. Click **Finish**.
 The disk you have selected is formatting. Wait for the system to complete the initialization operation. When the volume status becomes **Healthy**, the disk initialization is successful. You can then view the newly formatted data disk in the **PC** interface.
9. Enter the newly formatted data disk, create a file named `qcloud.txt`, enter the content you need, and select **File** > **Save**.

## Formatting, creating a file system, and writing a file (Linux)
>
>- This document takes EXT4 file system as an example.
>- When Linux CVM restarts or starts up, data disks will not be automatically mounted. For more information, see [Format and Mount Data Disks](https://intl.cloud.tencent.com/document/product/213/17487).

1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) as the root user.
2. Run the following command to view the names of data disks attached to the instance.
 ```
fdisk -l
 ```
If the returned result is similar to what is shown below, the current CVM has two disks, where `/dev/vda` is the system disk and `/dev/vdb` is the newly added data disk,
In this example, the disk attached to the instance is named `/dev/vdb`:
![](https://main.qcloudimg.com/raw/442e440d3871f9f66446cd75489a87fe.png)
3. Execute the following command to format the disk.
```
mkfs.ext4 /dev/vdb
```
4. Execute the following command to mount this disk to the `/data` mount point.
```
mount /dev/vdb /data
```
5. Run the following commands to enter the disk and create a new file `qcloud.txt`.
```
cd /data
```
```
vi qcloud.txt
```
6. Press **i** to enter the edit mode and enter "This is my first test." Press **ESC** to exit the edit mode, and enter **:wq** to save and exit the file.
7. Execute the `ls` command to view that the `qcloud.txt` file has been written to the disk.




