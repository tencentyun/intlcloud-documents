## Scenario
This document will help you understand how to easily use cloud disks by taking as an example initializing a cloud disk that is newly mounted to a CVM, creating a file system, and writing a file named `qcloud.txt`. For more information on initializing cloud disks, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).

## Prerequisites
You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/31645), and the cloud disk status is **Mounted**.

>The following Windows and Linux CVM OS systems are used:
>- Windows Server 2008
>- CentOS 7.5


## Notes
To protect your important data, you may want to look at [CBS Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409) before performing any operation on your CBS cloud disk.


## Formatting, Creating a File System, and Writing a File (Windows)
1. [Log in to the Windows instance](https://intl.cloud.tencent.com/document/product/213/5435) as an admin.
2. Enter the disk management interface by selecting **CVM Management**>**Storage**>**Disk Management**.
3. (Optional) Right click the empty destination disk, and select **Online**.
When the disk status changes to **Not Initialized**, it has gone online.
4. (Optional) Right click the newly online cloud disk. First, select **Initialize Disk**, and then **Master Boot Record** in the **Initialize Disk** popup window, and click **OK**.
 >MBR (Main Boot Record) partition format supports a maximum disk capacity of 2 TB, and GPT (GUID Partition Table) partition table supports a maximum disk capacity of 18 EB. If you need to use a disk capacity larger than 2 TB, please use the GPT partition format.
If the disk partition format is changed after the disk is put into use, the original data in the disk will be erased. Therefore, select the disk partition format carefully when initializing the disk.
5. Right click the target disk, and select **New Simple Volume**.
6. Enter the simple volume size, and click **Next**.
7. Select a drive letter or drive path, and click **Next**. 
8. Choose to format the partition, select file system, and then click **Next**.
8. Click **Finish**.
 The target disk is formatting. You need to wait for the system to complete the initialization operation. When the volume status is **Healthy**, the disk initialization is successful. After the initialization is complete, you can view the newly formatted data disk in the **PC** interface.
9. Enter the newly formatted data disk, create a file named `qcloud.txt`, enter the content you need, and select **File** > **Save**.

## Formatting, Creating a File System, and Writing a File (Linux)
>
>- This document takes EXT4 file system as an example.
>- When Linux CVMs restart or starts up, data disks will not be automatically mounted. For more information, see [Formatting and mounting data disks](https://intl.cloud.tencent.com/document/product/213/17487).

1. [log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) as root user.
2. Run the following command to view names of the data disks attached to the instance.
 ```
fdisk -l
 ```
The resulting response is similar to what is shown in the figure below, which indicates that the current CVM has two disks, `/dev/vda`, the system disk, and `/dev/vdb`, the newly added data disk,
i.e., the disk attached the instance in this example.
![](https://main.qcloudimg.com/raw/442e440d3871f9f66446cd75489a87fe.png)
3. Execute the following command to format the disk.
```
mkfs.ext4 /dev/vdb
```
4. Execute the following command to mount this disk to the `/data` mounting target.
```
mount /dev/vdb /data
```
5. Run the following commands to enter the disk and then create a new file called `qcloud.txt`.
```
cd /data
```
```
vi qcloud.txt
```
6. Press **i** to enter "This is my first test." in Edit Mode. Press **ESC** to exit Edit Mode, and enter **:wq** to save and exit the file.
7. Execute the `ls` command, and you can see that the `qcloud.txt` file has been written to the disk.




