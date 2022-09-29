## Overview
This document describes how to initialize a cloud disk newly mounted to a CVM, create a file system, and write a file named `qcloud.txt`.
<dx-alert infotype="explain" title="">
For more information on cloud disk initialization, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
</dx-alert>


## Note
To protect important data, see [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409) before performing any operation on your CBS cloud disks.

## Prerequisites
- You have attached the **cbs-test** cloud disk to a CVM. For detailed directions, see [Step 2. Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/39991).

## Directions
<dx-tabs>
::: Windows CVMs

<dx-alert infotype="explain" title="">
This section uses a CVM instance with Windows Server 2012 R2 DataCenter 64-bit English installed as an example. Note that the steps may vary by operating system version.
</dx-alert>


1. Log in to the Windows CVM instance as the admin user. See [Logging in to Windows Instance Using RDP (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435). 
2. On the desktop, right click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> in the lower-left corner.
3. In the pop-up menu, select **Disk Management**.
4. (Optional) Right-click the target disk and select **Online**.
When the disk status changes to **Not Initialized**, it has gone online.
5. (Optional) Right-click an online disk and select **Initialize Disk**. In the pop-up window, select **MBR (Master Boot Record)** and click **OK**.
<dx-alert infotype="explain" title="">
- The master boot record (MBR) format supports a disk of up to 2 TB, while GUID partition table (GPT) supports a disk of up to 18 EB. If you need a larger capacity than 2 TB, adopt GPT.
- If the partition format is changed for a disk in use, the original disk data will be cleared. Therefore, select the disk partition format with caution when initializing the disk.
</dx-alert>
6. Right-click the target disk and select **New Simple Volume**. In the pop-up window, click **Next**.
7. Enter the size of the simple volume and click **Next**.
8. Select the drive letter or path and click **Next**. Here, the drive letter E is used as an example.

9. Select the file system, perform a quick format, and then click **Next**.

10. Click **Complete**.
 The disk status becomes **Formatting**. Wait for the completion of initialization. When the volume status becomes **Healthy**, the disk initialization is successful. You can then view the newly formatted data disk in the **PC** interface.
11. Go to the newly partitioned data disk, create the `qcloud.txt` file, enter the content, and select **File** > **Save**.

:::
::: Linux CVMs


<dx-alert infotype="notice" title="">
- This section uses a Linux CVM instance with CentOS 7.8 installed as an example. Note that the steps may vary by operating system version.
- This section uses the EXT4 file system as an example.
- When a Linux CVM instance restarts or starts up, data disks will not be automatically attached. You can refer to [Step 9](#Step09)–[Step 14](#Step14) to configure disk automount at startup.
</dx-alert>


1. Log in to the Linux CVM instance as the root user. See [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command to view the names of data disks attached to the instance.
```
fdisk -l
```
If the returned result is as shown in the following figure, the current CVM has two disks, where `/dev/vda` is the system disk and `/dev/vdb` is the newly added data disk,
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
```
```
vi qcloud.txt
```
6. Press **i** to enter the edit mode and enter **This is my first test.**
7. Press **Esc** to exit the edit mode, enter **:wq**, and press **Enter** to save and exit the file.
8. Run the `ls` command, and you can see that the `qcloud.txt` file has been written to the disk.
<dx-alert infotype="explain" title="">
Refer to [Step 9](#Step09)–[Step 14](#Step14) to configure disk automount at startup. If you don't need this feature, skip the following steps.
</dx-alert>
9. [](id:Step09)Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
10. Run the following command to use VI editor to open the `/etc/fstab` file.
```
vi /etc/fstab
```
11. Press **i** to enter edit mode.
12. Move the cursor to the end of the file and press **Enter**, then add the following content.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
​``` Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following content:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
<dx-alert infotype="explain" title="">
You can run the `ls -l /dev/disk/by-id` command to view the soft link of the elastic cloud disk.
</dx-alert>
13. Press **Esc**, enter `:wq`, and press **Enter**.
Save the configuration and exit the editor.
14. [](id:Step14)Run the following command to check whether the `/etc/fstab` file has been written successfully.
```
mount -a 
``` 
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system starts up.
:::

</dx-tabs>

## Subsequent Operations
A cloud disk is an expandable storage device on cloud. You can expand its capacity to fit your business at any time without losing any data in it. For detailed directions, see [Step 4. Expanding Cloud Disk Capacity](https://intl.cloud.tencent.com/document/product/362/31646).

 

