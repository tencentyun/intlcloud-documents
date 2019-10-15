## Scenario
This article will help you understand how to easily use cloud disks by taking as an example initializing a cloud disk that is newly mounted to a CVM, creating a file system, and writing a file named `qcloud.txt`. For more information on initializing cloud disks, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).

## Prerequisites
You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/31594), and the cloud disk status is **Mounted**.

>The following Windows and Linux CVM OS systems are used:
>- Windows Server 2008
>- CentOS 7.5

## Formatting, creating a file system, and writing a file (Windows)
1. [Log in to the Windows CVM](https://intl.cloud.tencent.com/document/product/213/5435) as the admin.
2. Enter the disk management interface by selecting **CVM Management** > **Storage** > **Disk Management**.
3. Right click the target empty disk, and select **Online**.
 When the disk status changes to **Not Initialized**, it has gone online.
4. (Optional) Right click the newly online cloud disk. Select **Initialize Disk**, select **Master Boot Record** and click **OK**.
 >?MBR (Main Boot Record) partition format supports a maximum disk capacity of 2TB, and GPT (GUID Partition Table) partition table supports a maximum disk capacity of 18EB. If you need to use a disk capacity larger than 2TB, please use the GPT partition format.
If the disk partition format is changed after the disk is put into use, the original data in the disk will be erased. Therefore, select the disk partition format carefully when initializing the disk.
5. Right click the target disk, and select **New Simple Volume**.
6. Enter the simple volume size, and click **Next**.
7. Choose to format the partition, select file system, and then click **Next**.
 ![](https://main.qcloudimg.com/raw/463ee4c2b1f14064ec5f43dd244a29a3.jpg)
8. Click **Finish**.
 The target disk is formatting. You need to wait for the system to complete the initialization operation. When the volume status is **Healthy**, the disk initialization is successful. After the initialization is complete, you can view the newly formatted data disk in the **PC** interface.
9. Enter the newly formatted data disk, create a file named `qcloud.txt`, enter the content you need, and select **File** > **Save**.

## Formatting, creating a file system, and writing a file (Linux)
>- This article takes EXT4 file system as an example.
>- When Linux CVMs restart or starts up, data disks will not be automatically mounted. For more information, see [Formatting and mounting data disks](https://intl.cloud.tencent.com/document/product/213/17487).

1. As the root user, [log In to the Linux CVM](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command to view names of data disks linked to the instance.
 ```
fdisk -l
 ```
This article takes `/dev/vdb` as an example.
3. Execute the following command to format the disk.
```
mkfs.ext4 /dev/vdb
```
4. Execute the following command to mount this disk to the `/data` mounting point.
```
mount /dev/vdb /data
```
5. Run the following commands to enter the disk and then create a new file called `qcloud.txt`.
```
cd /data
vi qcloud.txt
```
6. In editing mode, you can input the related content. For example: “This is my first test”. Press ESC to exit the editing mode. Enter `:wq` to save and exit the file.
7. Execute the `ls` command, and you can see that the `qcloud.txt` file has been written to the disk.
