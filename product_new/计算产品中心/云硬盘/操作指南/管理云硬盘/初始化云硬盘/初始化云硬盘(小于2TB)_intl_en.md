## Scenario
This article provides a guide to cloud disk initialization operations by taking cloud disk with a capacity of less than 2TB as an example. For more information, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).

## Notes
- Formatting a data disk will erase all data. Please ensure that the data disk does not contain data, or that important data has been backed up.
- To avoid service exceptions, ensure before formatting that the CVM has stopped external services.

## Prerequisites
You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/31594) to a CVM.

## Directions

<span id="Windows2008"></span>
### Initializing cloud disks (Windows)
>This article uses the Windows Server 2008 operating system as an example. The formatting operations on different operating systems may vary. This article is for reference only.

1. [Log in to the Windows Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5435).
2. In the CVM desktop, click **Start**.
3. Right click **Computer** in the start menu and select **Manage**.
4. In the left navigation tree, select **Storage**>**Disk Management** to enter the **Disk Management** page.

>If the newly added disk is in offline status (as shown in the figure above), you must execute [Step 5](#online) before executing [Step 6](#initialize) to perform initialization. In other cases, you can directly execute [Step 6](#initialize) to perform initialization.

<span id="online"></span>
5. Disk list is shown in the right-side pane. Right click the disk 1 area, and select **Online** from the menu to put it online. The status of disk 1 changes from **Offline** to **Online**.
<span id="initialize"></span>
6. Right click the disk 1 area, and select **Initialize Disk** in the menu.
7. In the **Initialize Disk** dialog box, the disk you need to initialize is displayed. Select **MBR** or **GPT** and click **OK**.
> If the disk partition format is changed after the disk is put into use, the original data on the disk will be erased. Therefore, select an appropriate partition format according to actual needs.
8. Right click the unallocated space of the disk, and select **New Simple Volume**.
9. In the pop-up **New Simple Volume Wizard** dialog box, follow instructions on the interface and click **Next**.
10. Specify the volume size according to actual circumstances. The default is the largest value. Click **Next**.
11. Assign a drive letter, and click **Next**.
12. Select **Format this volume with the following settings**, set parameters according to actual circumstances, format the partition, and click **Next** to complete partition creation.
13. Click **Complete** to complete the wizard. Wait for the system to complete the initialization operation. When the volume status becomes **Healthy**, disk initialization is successful.
    After successfully completing the initialization, enter the **Computer** interface to view the new disk.
<span id="Linux"></span>
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
> The formatting takes a while, please pay attention to the system’s running status, and do not exit.
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

> As an example, this operation uses the fdisk partition tool in the CentOS 7.5 operating system to set `/dev/vdb` data disk as the primary partition, the default partition format is MBR, the file system is set as EXT4 format, mounted under `/data/newpart`, and also set to automatically mount at startup. The formatting operations on different operating systems may vary. This article is for reference only.
>

1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
fdisk -l
 ```
 Returned information is similar to what is shown in the following figure, which indicates that the current CVM has two disks, “/dev/vda” is the system disk, and “/dev/vdb” is the newly added data disk.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute the following command to enter the fdisk partition tool and execute partitioning operations on the newly added data disk.
 ```
fdisk <Newly added data disk>
 ```
 Take the newly mounted data disk `/dev/vdb` as an example:
 ```
fdisk /dev/vdb
 ```
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/db1fe212e2559ac635c52e5e397e7531.png)
4. Enter `n` and press **Enter** to start creating the new partition.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/c89b572c0ac2af1302189f8e7e1a849e.png)
 This indicates that the disk has two partition types:
  - **p** indicates the primary partition.
  - **e** indicates the extended partition.
5. Take creating a primary partition as an example, enter `p` and press **Enter** to start creating a new primary partition.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/efb65b60631d95e9b0213e6fd6125bbb.png)
 **Partition number** indicates the number of the primary partition. You can choose 1-4.
6. Take selecting partition number 1 as an example, enter the primary partition number `1` and press **Enter**.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/e1a1a7755a3bb392ec6d623e6774c315.png)
 **First sector** indicates the start sector. You can choose 2048 - 20971519. The default value is 2048.
7. Take selecting default start sector number 2048 as an example, press **Enter**.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/58a8202531b239a73fd3182d0ea0cf34.png)
 **Last sector** indicates the end sector, you can select 2048 - 20971519. The default value is 20971519.
8. Take selecting the default end sector number 20971519 as an example, press **Enter**.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/ad3a6459a6eaf154aed578b37dfc89d0.png)
 This indicates the partitioning is complete, that is, one new partition has been created on the 60GB data disk.
9. Enter `p` and press **Enter** to view the information of the newly created partition.
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/98427c11e0a181e02eb23a95fc1e908c.png)
 This indicates the detailed information of the newly created partition `/dev/vdb1`.

>If the partitioning operation above contains an error, enter `q` to exit the fdisk partition tool, and the prior partition results will not be retained.

10. Enter `w` and press **Enter** to write the partition results into the partition table.
 Returned information is similar to what is shown in the following figure, indicating the partition has been created.
 ![](https://main.qcloudimg.com/raw/7011369be260150fcddf272b4a4ab2fa.png)
11. Execute the following command to sync the partition table to the operating system.
 ```
partprobe
 ```
12. Execute the following command to set the file system of the newly created partition to the format required by the system.
 ```
mkfs -t <File system format> /dev/vdb1
 ```
 The partition size supported by different file systems varies. Select an appropriate file system according to your actual needs. In the following example, `EXT4` is set as the file system:
 ```
mkfs -t ext4 /dev/vdb1
 ```
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/6de097cea77634f8847816dd795292a7.png)
 The formatting takes a while, please pay attention to the system’s running status, and do not exit.
13. Execute the following command to create a new mounting point.
 ```
mkdir <Mounting point>
 ```
 Take the newly created mounting point `/data/newpart` as an example:
 ```
mkdir /data/newpart
 ```
14. Execute the following command to mount the newly created partition to the newly created mounting point.
 ```
mount /dev/vdb1 <Mount point>
 ```
 Take the newly created mounting point `/data/newpart` as an example:
 ```
mount /dev/vdb1 /data/newpart
 ```
15. Execute the following command to view the mounting results.
 ```
df -TH
 ```
 Returned information is similar to what is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/b7e5501fed8d7d648b48dc66685baf94.png)
 This indicates that the newly created partition `/dev/vdb1` has been mounted to `/data/newpart`.

>If you do not need to set automatic disk mounting at startup, skip the following steps.
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
/dev/disk/by-id/virtio-disk-drkhklpe-part1 /data/newpart   ext4 defaults     0   2
 ```
 - Take automatic mounting using the UUID of the disk partition as an example. Add the following to the previous example:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data/newpart   ext4 defaults     0   2
```
 - Take automatic mounting using the device name as an example. Add the following to the previous example:
```
/dev/vdb1 /data/newpart   ext4 defaults     0   2
```
20. Press **Esc**, enter **:wq**, and press **Enter**.
 Save the configuration and exit the editor.
21. Execute the following command to check whether the `/etc/fstab` file has been written successfully.
```
 mount -a 
```
If the command runs successfully, it means the file has been written successfully, and the newly created file system will automatically mount when the operating system is launched.

## Related Actions
[Initializing cloud disks (larger than or equal to 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

