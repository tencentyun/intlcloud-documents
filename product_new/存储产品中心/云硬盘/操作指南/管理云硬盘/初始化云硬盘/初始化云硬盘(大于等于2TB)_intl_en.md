## Scenario
This article provides a guide to cloud disk initialization operations by taking cloud disk with a capacity greater than or equal to 2TB as an example. For more information, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
MBR supports disk with a maximum capacity of 2TB. When you partition disk with a capacity greater than 2TB, we recommend you use GPT as the partition format. For Linux operating systems, when GPT is chosen as the partition format, fdisk partition tools can no longer be used, instead parted tools must be used.

## Notes
- Formatting a data disk will erase all data. Please ensure that the data disk does not contain data, or that important data has been backed up.
- To avoid service exceptions, ensure before formatting that the CVM has stopped external services.

## Prerequisites
You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/31594) to a CVM.

## Directions
<span id="2TBWindows2012"></span>

### Initializing cloud disks (Windows)
>This article uses the Windows Server 2012 operating system as an example. The formatting operations on different operating systems may vary. This article is for reference only.

1. [Log in to the Windows Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5435).
2. In the CVM desktop, click <img src="https://main.qcloudimg.com/raw/0a02193a82217974f650bbcaf4e1ed2d.png"  style="margin:0;"> to enter the **Server Manager** page.
3. In the left navigation tree, click **File and Storage Services**.
4. In the left navigation tree, select **Volume**>**Disk**.
 ![](https://main.qcloudimg.com/raw/e21c6ae7dbd7b41a3bfe9c5e2fd25c50.png)

>If the newly added disk is in offline status (as shown in the figure above), you must execute [Step 5](#online) before executing [Step 6](#initialize) to perform initialization. In other cases, you can directly execute [Step 6](#initialize) to perform initialization.

<span id="online"></span>
5. Disk list is shown in the right-side pane. Right click the row where 1 is located, and select **Online** in the menu to put it online. The status of 1 changes from **Offline** to **Online**.
 ![](https://main.qcloudimg.com/raw/e8bf6970a2b203a3fc926a35322680c2.png)
<span id="initialize"></span>
6. Right click the row where 1 is located, and select **Initialize** in the menu.
 ![](https://main.qcloudimg.com/raw/9cb41b9ea7d29115035e15924e65a86f.png)
7. Follow instructions on the interface, and click **Yes**.
 ![](https://main.qcloudimg.com/raw/4bd1346cb8f15bda39fb6ab399a3b2e2.png)
8. After initialization, the partition of 1 changes from **Unknown** to **GPT**. Right click the row where 1 is located and select **New Simple Volume** in the menu.
 ![](https://main.qcloudimg.com/raw/d9dbae385dee6e92534db02b3a1cf443.png)
9. In the pop-up **New Volume Wizard** dialog box, follow instructions on the interface and click **Next**.
 ![](https://main.qcloudimg.com/raw/896583a11d0004c9172c0d1a31f0ff74.png)
10. Select the server and disk, and click **Next**.
 ![](https://main.qcloudimg.com/raw/368ee2e2a5b858504a931d0aa0888915.png)
11. Specify the volume size according to actual circumstances. The default is the largest value. Click **Next**.
 ![](https://main.qcloudimg.com/raw/4a6b81ca6a0034fd409289fee70374a1.png)
12. Assign a drive letter, and click **Next**.
 ![](https://main.qcloudimg.com/raw/4c6f82f8e0027ffbbf20869ed4df5dfb.png)
13. Select **Format this volume with the following settings**, set parameters according to actual circumstances, format the partition, and click **Next** to complete partition creation.
 ![](https://main.qcloudimg.com/raw/952b5425be9d7b3c44730801b3563d6b.png)
14. After confirming the information contains no errors, click **Create**.
 ![](https://main.qcloudimg.com/raw/61f81b09d6244962379dda362e07b660.png)
15. Wait for the system to complete the creation of the new volume, and then click **Close**.
 After completing initialization, enter the **My Computer** interface to view the new disk.
 ![](https://main.qcloudimg.com/raw/1053f9ea5f3ab8cf85f7c81ba1bf53b8.png)

<span id="2TBLinux"></span>
### Initializing cloud disks (Linux)

Select the initialization method according to your actual use scenario:
- If the entire disk is presented as one independent partition (that is, there are not multiple logical disks such as vdb1 and vdb2), we strongly recommend you not use partitions, and directly [create the file system on bare devices](#CreateFileSystemOnBareDevice).
- If the entire disk needs to be presented as multiple logical partitions (that is, there are multiple logical disks), you need to perform the partitioning first, then [create the file system on a partition](#CreateFileSystemOnPartition).

<span id="CreateFileSystemOnBareDevice"></span>
#### Creating file systems on bare devices

1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
fdisk -l
 ```
 Returned information is similar to what is shown in the following figure, which indicates that the current CVM has two disks, “/dev/vda” is the system disk, and “/dev/vdb” is the newly created data disk.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute the following command to create a file system on the “/dev/vdb” bare device.
```
mkfs -t <File system format> /dev/vdb
```
The partition size supported by different file systems varies. Select an appropriate file system according to your actual needs. In the following example, `EXT4` is set as the file system:
```
mkfs -t ext4 /dev/vdb
```
>! The formatting takes a while, please pay attention to the system’s running status, and do not exit.
4. Execute the following command to create a new mounting point.
```
mkdir <Mounting point>
```
Take the newly created mounting point `/data` as an example:
```
mkdir /data
```
5. Execute the following command to mount the newly created partition to the newly created mounting point.
```
mount /dev/vdb <Mounting point>
```
Take the newly created mounting point `/data` as an example:
```
mount /dev/vdb /data
```
6. Execute the following command to view the mounting results.
```
df -TH
```
>If you do not need to set automatic disk mounting at startup, skip the following steps.
7. Confirm the mounting method and obtain the corresponding information.
You can choose to use an elastic cloud disk’s soft link, file system’s UUID (universally unique identifier) or device name to automatically mount a disk, according to your business needs. The related description and information acquisition methods are as follows:
<table>
 <tr>
     <th>Mounting method</th>
		 <th>Pros and cons</th>
		 <th>Information acquisition method</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(Recommended)</b></td>
		 <td><b>Pros:</b>The soft link of each elastic cloud disk is fixed and unique, and will not change along with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only elastic cloud disks can use soft links. They cannot sense the formatting operation of the partition.</td>
		 <td nowrap="nowrap">Execute the following command to view the soft link of the elastic cloud disk.</br><pre>ls -l /dev/disk/by-id</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use a file system’s UUID</td>
		 <td>Automatic mounting configuration may become invalid due to changes in a file system’s UUID.</br>For example, reformatting a file system will change the UUID of the file system.</td>
		 <td nowrap="nowrap">Execute the following command to view the UUID of the file system.</br><pre>blkid /dev/vdb</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use device name</td>
		 <td>Automatic mounting configuration may become invalid due to changes in device name.</br>For example, during data migration, the elastic cloud disk on the CVM is unmounted and then remounted. When the operating system recognizes the file system again, the device name may change.</td>
		 <td nowrap="nowrap">Execute the following command to view the device name.</br><pre>fdisk -l</pre></td>
	</tr>
</table>
8. Backup the `/etc/fstab` file.
9. Execute the following command to use VI editor to open the `/etc/fstab` file.
```
vi /etc/fstab
```
10. Press **i** to enter editing mode.
11. Move the cursor to the end of the file and press **Enter**, then add the following content.
```
<Device information> <Mounting point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
 - **(Recommended)** Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following to the previous example:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
 - Take automatic mounting using the UUID of the disk partition as an example. Add the following to the previous example:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
 - Take automatic mounting using the device name as an example. Add the following to the previous example:
```
/dev/vdb /data   ext4 defaults     0   0
```
12. Press **Esc**, enter **:wq**, and press **Enter**.
Save the configuration and exit the editor.
13. Execute the following command to check whether the **/etc/fstab** file has been written successfully.
```
mount -a 
```
If the command runs successfully, it means the file has been written successfully, and the newly created file system will automatically mount when the operating system is launched.

<span id="CreateFileSystemOnPartition"></span>
#### Creating a file system on a partition

>As an example, this article uses the parted partition tool in the CentOS 7.5 operating system to set `/dev/vdc` data disk as the primary partition, the default partition format is GPT, the file system is set as EXT4 format, mounted under `/data/newpart2`, and also set to automatically mount at startup. The formatting operations on different operating systems may vary. This article is for reference only.

1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
lsblk
 ```
Returned information is similar to what is shown in the following figure, which indicates that the current CVM has two disks, “/dev/vda” is the system disk, and “/dev/vdc” is the newly created data disk.
	![](https://main.qcloudimg.com/raw/72a7a48c59c13a44958a6b1aa0407ac2.png)
3. Execute the following command to enter the parted partition tool and execute partitioning operations on the newly added data disk.
```
parted <Newly added data disk>
```
Take the newly mounted data disk `/dev/vdc` as an example:
```
parted /dev/vdc
```
Returned information is similar to what is shown in the following figure:
![](https://main.qcloudimg.com/raw/0b2c9164f9fec125a72dee8861b7327d.png)
4. Enter `p`, and press Enter to view the current disk partition format.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/af906521dd6a7f3b948cfad42745aaba.png)
 **Partition Table: unknown** indicates the disk partition format is unknown.
5. Execute the following command to set the disk partition format.
```
mklabel <Disk partition format>
```
If disk capacity is larger than or equal to 2TB, only GPT partition format can be used:
```
mklabel gpt
```
6. Enter `p`, and press Enter to view whether the disk partition format has been set successfully.
 Returned information is similar to what is shown in the following figure:
	![](https://main.qcloudimg.com/raw/3dfec9aba75cd3cb6dcfb06729f5ff26.png)
 **Partition Table: gpt** indicates that the disk partition format is GPT.
7. Enter `unit s` and press Enter to set the measurement unit of the disk as sector.
8. Take creating one partition for the entire disk as an example, enter `mkpart opt 2048s 100%`, and press Enter.
 2048s indicates the initial disk capacity. 100% indicates the ending disk capacity. This is for reference only. You can plan the number of disk partitions and their capacities according to your business needs.
9. Enter `p` and press Enter to view the information of the newly created partitions.
    Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/ee406e75c689f48d59e863adc768aa36.png)
 This indicates the detailed information of the newly created partition `/dev/vdc1`.
10. Enter `q` and press Enter to exit the parted partition tool.
11. Execute the following command to view the disk name.
 ```
lsblk
 ```
Returned information is similar to what is shown in the following figure, you can now see the new partition “/dev/vdc1”.
![](https://main.qcloudimg.com/raw/f95f599f11f88b8bcb89d4f02bb41292.png)
12. Execute the following command to set the file system of the newly created partition to the format required by the system.
```
mkfs -t <File system format> /dev/vdc1
```
The partition size supported by different file systems varies. Select an appropriate file system according to your actual needs. In the following example, `EXT4` is set as the file system:
```
mkfs -t ext4 /dev/vdc1
```
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/3cd6bbd019dd9bdc85ad4ed11ba64f0b.png)
 The formatting takes a while, please pay attention to the system’s running status, and do not exit.
13. Execute the following command to create a new mounting point.
```
mkdir <Mounting point>
```
Take the newly created mounting point `/data/newpart2` as an example:
```
mkdir /data/newpart2
```
14. Execute the following command to mount the newly created partition to the newly created mounting point.
```
mount /dev/vdc1 <Mounting point>
```
Take the newly created mounting point `/data/newpart2` as an example:
```
mount /dev/vdc1 /data/newpart2
```
15. Execute the following command to view the mounting results.
```
df -TH
```
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/774c2d9ff266634c4836df6456b9dd4d.png)
 This indicates that the newly created partition `/dev/vdc1` has been mounted to `/data/newpart2`.

>?If you do not need to set automatic disk mounting at startup, skip the following steps.
>
16. Confirm the mounting method and obtain the corresponding information.
 You can choose to use an elastic cloud disk’s soft link, file system’s UUID (universally unique identifier) or device name to automatically mount a disk, according to your business needs. The related description and information acquisition methods are as follows:
 <table>
     <tr>
         <th>Mounting method</th>  
         <th>Pros and cons</th>  
         <th>Information acquisition method</th>  
     </tr>
	   <tr>      
         <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(Recommended)</b></td>   
	       <td><b>Pros:</b>The soft link of each elastic cloud disk is fixed and unique, and will not change along with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only elastic cloud disks can use soft links. They cannot sense the formatting operation of the partition.</td>
	       <td nowrap="nowrap">Execute the following command to view the soft link of the elastic cloud disk.</br><pre>ls -l /dev/disk/by-id</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use a file system’s UUID</td>   
	       <td>Automatic mounting configuration may become invalid due to changes in a file system’s UUID.</br>For example, reformatting a file system will change the UUID of the file system.</td>
	       <td nowrap="nowrap">Execute the following command to view the UUID of the file system.</br><pre>blkid /dev/vdc1</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use device name</td>   
	       <td>Automatic mounting configuration may become invalid due to changes in device name.</br>For example, during data migration, the elastic cloud disk on the CVM is unmounted and then remounted. When the operating system recognizes the file system again, the device name may change.</td>
	       <td>Execute the following command to view the device name.</br><pre>fdisk -l</pre></td>
     </tr> 
</table>
17. Backup the `/etc/fstab` file.
18. Execute the following command to use VI editor to open the `/etc/fstab` file.
 ```
vi /etc/fstab
 ```
19. Press **i** to enter editing mode. 
20. Move the cursor to the end of the file and press **Enter**, then add the following content.
 ```
<Device information> <Mounting point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
 ```
 - **(Recommended)** Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following to the previous example:
 ```
/dev/disk/by-id/virtio-disk-bm42ztpm-part1 /data/newpart2   ext4 defaults     0   2
 ```
 - Take automatic mounting using the UUID of the disk partition as an example. Add the following to the previous example:
```
UUID=fc3f42cc-2093-49c7-b4fd-c616ba6165f4 /data/newpart2   ext4 defaults     0   2
```
 - Take automatic mounting using the device name as an example. Add the following to the previous example:
```
/dev/vdc1 /data/newpart2   ext4 defaults     0   2
```
20. Press **Esc**, enter **:wq**, and press **Enter**.
 Save the configuration and exit the editor.
21. Execute the following command to check whether the `/etc/fstab` file has been written successfully.
```
 mount -a 
```
If the command runs successfully, it means the file has been written successfully, and the newly created file system will automatically mount when the operating system is launched.

## Related Actions
[Initializing cloud disks (smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597).