## Overview
This document takes cloud disks with a capacity less than 2 TB as an example to provide guidance on disk initialization. For more information, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).


## Prerequisites
You have [mounted a cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to your CVM.

## Notes
- To protect important data, please see [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409) before operating on your cloud disks.
- Formatting a data disk will erase all data. Make sure that the disk does not contain data, or important data has been backed up.
- To avoid exceptions, make sure before formatting that the CVM has stopped external services.

## Directions

<span id="Windows2008"></span>
### Initializing cloud disks (Windows)
>This article uses the Windows Server 2012 R2 operating system as an example. The formatting operation varies by operating system. Below is for reference only.
>
1. [Log in to the Windows Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5435).
2. On the CVM desktop, right click the lower-right icon <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px">.
3. Select **Disk Management** in the pop-up menu to open the **Disk Management** window.
>If the newly added disk is in offline status (as shown in the figure above), execute [Step 4](#online) before [Step 5](#initialize) to perform initialization. Otherwise, you can directly execute Step 5](#initialize).
4. <span id="online"></span>Disks are listed on the right-side pane. Right click disk 1 area, and select **Online** to bring it online. The status of disk 1 changes from **Offline** to **Not Initialized**.

5. <span id="initialize"></span>Right click disk 1 area, and select **Initialize Disk** in the menu.

6. In the **Initialize Disk** dialog box, the disk you need to initialize is displayed. Select **MBR** or **GPT** and click **OK**.
>If the disk partition format is changed after the disk is put into use, the original data on the disk will be erased. Please select an appropriate partition format based on actual needs.

7. Right click the unallocated space of the disk, and select **New Simple Volume**.
8. In the pop-up **New Simple Volume Wizard** dialog box, follow instructions on the interface and click **Next**.
9. Specify the volume size as needed, which is the maximum value by default. Click **Next**.
10. Assign a drive letter, and click **Next**.
11. Select **Format this volume with the following settings**, configure parameters as needed, format the partition, and click **Next** to complete the partition creation.
12. Click **Complete** to complete the wizard. Wait for the system to complete the initialization operation. When the volume status becomes **Healthy**, disk initialization is successful.
    After successfully completing the initialization, enter the **Computer** interface to view the new disk.

<span id="Linux"></span>
### Initializing cloud disks (Linux)

Select the initialization method according to your actual use cases:
- If the entire disk is presented as one independent partition (there is no logical disk such as vdb1 and vdb2), we strongly recommend that you not use partition, and directly [create the file system on bare devices](#CreateFileSystemOnBareDevice).
- If the entire disk needs to be presented as multiple logical partitions (there are multiple logical disks), you need to perform the partition operation first, and then [create the file system on a partition](#CreateFileSystemOnPartition).

<span id="CreateFileSystemOnBareDevice"></span>
#### Creating file systems on bare devices

1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
fdisk -l
 ```
 If information similar to what is shown below is returned, the current CVM has two disks, where “/dev/vda” is the system disk and “/dev/vdb” is the newly added data disk.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute the following command to create a file system on the “/dev/vdb” bare device.
```
mkfs -t <File system format> /dev/vdb
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
mkfs -t ext4 /dev/vdb
```
> The formatting takes a while. Please pay attention to the system’s running status and do not exit.
4. Execute the following command to create a new mount point.
```
mkdir <mount point>
```
Take creating a new mount point `/data` as an example:
```
mkdir /data
```
5. Execute the following command to mount the newly created partition to the newly created mount point.
```
mount /dev/vdb <mount point>
```
Take creating a new mount point `/data` as an example:
```
mount /dev/vdb /data
```
6. Execute the following command to view the mount result.
```
df -TH
```
> If you do not need to configure automatic disk mounting at startup, skip the following steps.
7.Confirm the mount method and obtain the corresponding information.
Based on business needs, you can use an elastic cloud disk’s soft link, file system’s UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
<table>
 <tr>
      <th>Mount method</th>
      <th>Pros and cons</th>
      <th>Information acquisition method</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(Recommended)</b></td>
     <td><b>Pros:</b>The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only an elastic cloud disk can use the soft link, which operates imperceptibly for the partition formatting operation.</td>
		 <td nowrap="nowrap">Execute the following command to view the soft link of the elastic cloud disk.</br><pre>ls -l /dev/disk/by-id</pre></td>
	</tr>
	<tr>
	   <td nowrap="nowrap">Use the UUID of the file system</td>
		 <td>Automatic mounting configuration may fail due to changes in a file system’s UUID.</br>For example, reformatting a file system will change its UUID.</td>
		 <td nowrap="nowrap">Execute the following command to view the UUID of the file system.</br><pre>blkid /dev/vdb</pre></td>
  </tr>
	<tr>
	   <td nowrap="nowrap">Use device name</td>     
		 <td>Automatic mounting configuration may fail due to changes in device name.</br>For example, if an elastic cloud disk on the CVM is unmounted and then remounted, the device name may change when the operating system recognizes the file system again.</td>
		 <td nowrap="nowrap">Execute the following command to view the device name.</br><pre>fdisk -l</pre></td>
 </tr>
</table>
8. Execute the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
9. Execute the following command to use VI editor to open the `/etc/fstab` file.
```
vi /etc/fstab
```
10. Press **i** to enter the edit mode.
11. Move the cursor to the end of the file, press **Enter**, and add the following content.
```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
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
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system is launched.

<span id="CreateFileSystemOnPartition"></span>
#### Creating a file system on a partition

>This example uses the fdisk partition tool in the CentOS 7.5 operating system to configure data disk `/dev/vdc` as the primary partition. MBR is used as the default partition format, EXT4 format as the file system, `/data/newpart` as the mount point, and automatic mounting at startup is configured. The formatting operation varies by operating system. Below is for reference only.


1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
fdisk -l
 ```
 If information similar to what is shown below is returned, the current CVM has two disks, where `/dev/vda` is the system disk and `/dev/vdb` is the newly added data disk.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute the following command to enter the fdisk partition tool and execute partitioning operations on the newly added data disk.
 ```
fdisk <Newly added data disk>
 ```
 Take the newly mounted data disk `/dev/vdb` as an example:
 ```
fdisk /dev/vdb
 ```
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/db1fe212e2559ac635c52e5e397e7531.png)
4. Enter `n` and press **Enter** to start creating the new partition.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/c89b572c0ac2af1302189f8e7e1a849e.png)
 This indicates that the disk has two partition types:
  - **p** indicates the primary partition.
  - **e** indicates the extended partition.
5. Take creating a primary partition as an example. Enter `p` and press **Enter** to start creating a new primary partition.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/efb65b60631d95e9b0213e6fd6125bbb.png)
 **Partition number** indicates the number of the primary partition. You can choose from 1-4.
6. Take selecting partition number 1 as an example. Enter the primary partition number `1` and press **Enter**.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/e1a1a7755a3bb392ec6d623e6774c315.png)
 **First sector** indicates the start sector. You can choose from 2048 - 20971519. The default value is 2048.
7. Take selecting default start sector number 2048 as an example. Press **Enter**.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/58a8202531b239a73fd3182d0ea0cf34.png)
 **Last sector** indicates the end sector. You can choose from 2048 - 20971519. The default value is 20971519.
8. Take selecting the default end sector number 20971519 as an example. Press **Enter**.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/ad3a6459a6eaf154aed578b37dfc89d0.png)
 This indicates that partitioning is completed. A new partition has been created on the 60 GB data disk.
9. Enter `p` and press **Enter** to view information about the newly created partition.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/98427c11e0a181e02eb23a95fc1e908c.png)
 This indicates the detailed information of the newly created partition `/dev/vdb1`.

>If the partitioning operation above has an error, enter `q` to exit the fdisk partition tool, and the prior partition result will not be retained.

10. Enter `w` and press **Enter** to write the partition result into the partition table.
 If the returned information is similar to what is shown below, the partition has been created.
 ![](https://main.qcloudimg.com/raw/7011369be260150fcddf272b4a4ab2fa.png)
11. Execute the following command to sync the partition table to the operating system.
 ```
partprobe
 ```
12. Execute the following command to configure the file system of the newly created partition to that required by the system.
 ```
mkfs -t <File system format> /dev/vdb1
 ```
 The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
 ```
mkfs -t ext4 /dev/vdb1
 ```
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/6de097cea77634f8847816dd795292a7.png)
 The formatting takes a while. Please pay attention to the system’s running status and do not exit.
13. Execute the following command to create a new mount point.
 ```
mkdir <mount point>
 ```
 Take creating a new mount point `/data/newpart` as an example:
 ```
mkdir /data/newpart
 ```
14. Execute the following command to mount the newly created partition to the newly created mount point.
 ```
mount /dev/vdb1 <Mount point>
 ```
 Take creating a new mount point `/data/newpart` as an example:
 ```
mount /dev/vdb1 /data/newpart
 ```
15. Execute the following command to view the mount result.
 ```
df -TH
 ```
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/b7e5501fed8d7d648b48dc66685baf94.png)
 This indicates that the newly created partition `/dev/vdb1` has been mounted to `/data/newpart`.

>If you do not need to configure automatic disk mounting at startup, skip the following steps.
>
16. Confirm the mount method and obtain the corresponding information.
 Based on business needs, you can use an elastic cloud disk’s soft link, file system’s UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
 <table>
     <tr>
         <th>Mount method</th>  
         <th>Pros and cons</th>  
         <th>Information acquisition method</th>  
     </tr>
	   <tr>      
         <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(Recommended)</b></td>   
	       <td><b>Pros:</b>The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only an elastic cloud disk can use the soft link, which operates imperceptibly for the partition formatting operation.</td>
	       <td nowrap="nowrap">Execute the following command to view the soft link of the elastic cloud disk.</br><pre>ls -l /dev/disk/by-id</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use the UUID of the file system</td>   
	       <td>Automatic mounting configuration may fail due to changes in a file system’s UUID.</br>For example, reformatting a file system will change its UUID.</td>
	       <td nowrap="nowrap">Execute the following command to view the UUID of the file system.</br><pre>blkid /dev/vdb1</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use device name</td>   
	       <td>Automatic mounting configuration may fail due to changes in device name.</br>For example, if an elastic cloud disk on the CVM is unmounted and then remounted, the device name may change when the operating system recognizes the file system again.</td>
	       <td>Execute the following command to view the device name.</br><pre>fdisk -l</pre></td>
     </tr> 
</table>
17. Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
18. Execute the following command to use VI editor to open the `/etc/fstab` file.
 ```
vi /etc/fstab
 ```
19. Press **i** to enter editing mode. 
20. Move the cursor to the end of the file, press **Enter**, and add the following content.
 ```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
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
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system is launched.

## Related Operations
[Initializing cloud disks (larger than or equal to 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).


