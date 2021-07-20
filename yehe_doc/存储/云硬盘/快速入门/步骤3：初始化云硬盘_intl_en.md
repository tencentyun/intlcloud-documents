## Overview
This document describes how to initialize a cloud disk newly mounted to a CVM, create a file system, and write a file named `qcloud.txt`.
>?For more information on initializing cloud disks, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
>

## Notes
To prevent data loss, please see [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409#.E4.BA.91.E7.A1.AC.E7.9B.98.E4.BD.BF.E7.94.A8.E4.B8.8A.E6.9C.89.E4.BB.80.E4.B9.88.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9.EF.BC.9F) before operating on your CBS cloud disks.

## Prerequisites
- You have attached the **cbs-test** cloud disk to a CVM. For detailed directions, see [Step 2. Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/39991).

## Directions
<dx-tabs>
::: Formatting, creating a file system, and writing a file (Windows)
>?This document uses a CVM with Windows Server 2012 R2 DataCenter 64-bit Chinese installed as an example. Note that the steps may vary according to the operating system version.
>
1. Log in to the Windows CVM instance as the admin user. See [Logging in to Windows Instance Using RDP (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435). 
2. On the desktop, right click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> in the lower-left corner.
3. Select **Disk Management** in the pop-up menu to open the **Disk Management** window.
4. (Optional) Right click the empty disk you need, and select **Online**.
When the disk status changes to **Not Initialized**, it has gone online.
5. (Optional) Right click the cloud disk that has just gone online. Select **Initialize Disk** and then **Master Boot Record** in the **Initialize Disk** pop-up window, and click **OK**.
>?
>- Master Boot Record (MBR) partition format supports a maximum disk capacity of 2 TB, and GUID Partition Table (GPT) supports a maximum disk capacity of 18 EB. If you need a disk capacity larger than 2 TB, please select the GPT partition format.
>- If the disk partition format is changed after the disk is put into use, the original data on the disk will be erased. Please select the partition format carefully when initializing the disk.
>
6. Right click the disk you need, select **New Simple Volume**, and click **Next** in the pop-up window.
7. Enter the simple volume size, and click **Next**.
8. Select a drive letter or drive path, and click **Next**. In this example, E is assigned as the driver letter.
![](https://main.qcloudimg.com/raw/1f61b5dcd5c965fa3e3bc11983475d38.png)
9. Select the file system, perform a quick format, and then click **Next**.
![](https://main.qcloudimg.com/raw/608ffc67e52b53691bf64f2b2411b948.png)
10. Click **Finish**.
 The disk status goes to **Formatting**. Wait for the completion of initialization. When the volume status becomes **Healthy**, the disk initialization is successful. You can then view the newly formatted data disk in the **PC** interface.
11. Enter the newly formatted data disk, create a file named `qcloud.txt`, enter the content you need, and select **File** > **Save**.
:::
::: Formatting, creating a file system, and writing a file (Linux)
>!
>- This document uses a CVM with CentOS 7.8 installed as an example. Note that the steps may vary according to the operating system version.
>- EXT4 file system is used in this example.
>- When Linux CVM restarts or starts up, data disks will not be automatically attached. You can refer to [Step 9](#Step09) - [Step 14](#Step14) to configure disk automount at startup.
>
1. Log in to the Linux CVM instance as the root user. See [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the names of data disks attached to the instance.
 ```
fdisk -l
​``` If the returned result is as shown in the following figure, the current CVM has two disks, where `/dev/vda` is the system disk and `/dev/vdb` is the newly added data disk.
In this example, the disk attached to the instance is named `/dev/vdb`:
![](https://main.qcloudimg.com/raw/969d3ca3d95b16d47103886e11714868.png)
3. Run the following command to format the disk.
 ```
mkfs.ext4 /dev/vdb
```
4. Run the following command to mount this disk to the `/data` mount point.
```
mount /dev/vdb /data
```
5. Run the following commands to enter the disk and create a new file `qcloud.txt`.
```
cd /data
``` ```
vi qcloud.txt
```
6. Press **i** to enter the edit mode and enter **This is my first test.**
7. Press **Esc** to exit the edit mode, enter **:wq**, and press **Enter** to save and exit the file.
8. Run the `ls` command, and you can see that the `qcloud.txt` file has been written to the disk.
>? Refer to [Step 9](#Step09) - [Step 14](#Step14) to configure disk automount at startup. If you do not need disk automount at startup, skip the following steps.
>
9. [](id:Step09)Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
10. Run the following command to use VI editor to open the `/etc/fstab` file.
```
vi /etc/fstab
```
11. Press **i** to enter the edit mode.
12. Move the cursor to the end of the file, press **Enter**, and add the following content.
​```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> 
<File system check sequence at startup>
​``` Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following content:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
>?You can run the `ls -l /dev/disk/by-id` command to obtain the soft link of the elastic cloud disk.
>
13. Press **Esc**, enter `:wq`, and press **Enter**.
Save the configuration and exit the editor.
14. [](id:Step14)Run the following command to check whether the `/etc/fstab` file has been written successfully.
```
mount -a 
``` If the command runs successfully, the file has been written. The newly created file system will be mounted automatically when the operating system starts up.
:::

</dx-tabs>

## Subsequent Operations
A cloud disk is an expandable storage device on cloud. You can expand its capacity to fit your business at any time without losing any data in it. For detailed directions, see [Step 4. Expanding Cloud Disk Capacity](https://intl.cloud.tencent.com/document/product/362/31646).


```