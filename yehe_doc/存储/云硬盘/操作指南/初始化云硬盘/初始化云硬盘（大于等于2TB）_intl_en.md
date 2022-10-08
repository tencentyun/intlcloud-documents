## Overview
This document describes how to initialize a cloud disk with a capacity greater than or equal to 2 TB. For more cases, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
MBR supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you use the GPT partition format. When GPT is used on Linux operating system, fdisk can no longer be used and the parted tool must be used.

## Prerequisite
You have [attached the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to your CVM.

## Notes
- Read [FAQs about cloud disk usage](https://intl.cloud.tencent.com/document/product/362/32409) before working with cloud disks.
- Formatting a data disk will erase all data. Make sure that the disk does not contain data, or important data has been backed up.
- To prevent service exceptions, ensure that the CVM has stopped providing external services before formatting.


## Directions[](id:Steps)

<dx-tabs>
::: Initializing cloud disks (Windows)[](id:Windows)

<dx-alert infotype="explain" title="">
This document uses a CVM instance with Windows Server 2012 installed as an example. Note that the steps may vary by operating system version.
</dx-alert>



1. [Log in to the Windows CVM instance](https://intl.cloud.tencent.com/document/product/213/5435).
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/0a02193a82217974f650bbcaf4e1ed2d.png"  style="margin:-5px 0px"/>.
3. Go to the **Server Manager** page and click **File and Storage Services** on the left sidebar.
4. On the left sidebar, select **Volume** > **Disk**.

<dx-alert infotype="explain" title="">
If the newly added disk is in offline status, execute [Step 5](#online) before [Step 6](#initialize) to perform initialization. Otherwise, you can directly execute [Step 6](#initialize).
</dx-alert>
5. [](id:online)Disks are listed on the right pane. Right-click the row where 1 is located, and select **Online** to bring it online. Then its status becomes **Online**.

6. [](id:initialize)Right-click the row where 1 is located, and select **Initialize** in the menu.

7. Click **Yes** as prompted.

8. After the initialization, 1 changes from the **Unknown** to **GPT** partition. Click the row where 1 is located and select **New Simple volume** in the menu.

9. In the welcome page of **New Volume Wizard** pop-up window, click **Next**.

10. Select the server and disk and click **Next**.

11. Specify the volume size as needed, which is the maximum value by default. Click **Next**.

12. Assign a drive letter and click **Next**.

13. Configure parameters as needed, format the partition, and click **Next** to complete the partition creation.

14. After confirming that everything is correct, click **Create**.

15. Wait for the completion of the volume creation and click **Close**.
 After the initialization is completed, go to **My Computer** to view the new disk.


:::
::: Initializing cloud disks (Linux)[](id:Linux)

Select the initialization method according to your actual use cases:
- If the entire disk is presented as one independent partition (there is no logical disks such as vdb1 and vdb2), we strongly recommend that you not use partition, and directly [create the file system on bare devices](#CreateFileSystemOnBareDevice).
- If the entire disk needs to be presented as multiple logical partitions (there are multiple logical disks), you need to first partition the disk, and then [create the file system on a partition](#CreateFileSystemOnPartition).


### Creating file systems on bare devices[](id:CreateFileSystemOnBareDevice)

1. [Log in to the Linux CVM instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command as the root user to view the disk name.
```
fdisk -l
```
If information similar to what is shown below is returned, the current CVM has two disks, where "/dev/vda" is the system disk and "/dev/vdb" is the newly added data disk.
![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Run the following command to create a file system on the `/dev/vdb` bare device.
``` 
mkfs -t <File system format> /dev/vdb
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
mkfs -t ext4 /dev/vdb
```
<dx-alert infotype="notice" title="">
The formatting takes a while. Pay attention to the system's running status and do not exit.
</dx-alert>
4. Run the following command to create a new mount point.
```
mkdir <Mount point>
```
Take creating a new mount point `/data` as an example:
```
mkdir /data
```
5. Run the following command to mount the new partition to the newly created mount point.
```
mount /dev/vdb <Mount point>
```
Take creating a new mount point `/data` as an example:
```
mount /dev/vdb /data
```
6. Run the following command to view the mount result.
```
df -TH
```
<dx-alert infotype="explain" title="">
If you don't need to configure disk automount at startup, skip the following steps.
</dx-alert>
7. Confirm the mount method and obtain the corresponding information.
Based on business needs, you can use an elastic cloud disk's soft link, file system's UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
<table>
 <tr>
     <th>Mounting method</th>
		 <th>Pros and cons</th>
		 <th>	Information acquisition method</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the soft link of the elastic cloud disk <b>(recommended)</b></td>
		 <td><b>Pros</b>: The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons</b>: Only an elastic cloud disk can use the soft link, which operates imperceptibly for the partition formatting operation.</td>
		 <td nowrap="nowrap">Run the following command to obtain the soft link of the elastic cloud disk.</br><pre style="color:white;">ls -l /dev/disk/by-id</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the UUID of the file system</td>
		 <td>Auto-mounting configuration may fail due to changes in a file system's UUID.</br>For example, reformatting a file system will change its UUID.</td>
		 <td nowrap="nowrap">Run the following command to obtain the UUID of the file system.</br><pre style="color:white;">blkid /dev/vdb</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use device name</td>
		 <td>Automatic mounting configuration may fail due to changes in device name.</br>For example, if an elastic cloud disk on the CVM is unmounted and then remounted, the device name may change when the operating system recognizes the file system again.</td>
		 <td nowrap="nowrap">Run the following command to obtain the device name.</br><pre style="color:white;">fdisk -l</pre></td>
	</tr>
</table>
8. Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
9. Execute the following command to use VI editor to open the `/etc/fstab` file.
```
vi /etc/fstab
```
10. Press **i** to enter edit mode.
11. Move the cursor to the end of the file, press **Enter**, and add the following content.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
  - **(Recommended)** Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following content:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
  - Take automatic mounting using the UUID of the disk partition as an example. Add the following content:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
  - Take automatic mounting using the device name as an example. Add the following content:
```
/dev/vdb /data   ext4 defaults     0   0
```
12. Press **Esc**, enter **:wq**, and press **Enter**.
Save the configuration and exit the editor.
13. Execute the following command to check whether the `/etc/fstab` file has been written successfully.
```
mount -a 
```
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system starts up.


### Creating a file system on a partition[](id:CreateFileSystemOnPartition)



<dx-alert infotype="explain" title="">
This document uses the parted partition tool in the CentOS 7.5 operating system to configure the `/dev/vdc` data disk as the primary partition. GPT is used as the default partition format, EXT4 format as the file system, and `/data/newpart2` as the mount point. Disk automount at startup is configured. Note that the formatting operation may vary according to the operating system.
</dx-alert>



1. [Log in to the Linux CVM instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command as the root user to view the disk name.
 ```
lsblk
``` If the returned result is as shown below, the current CVM instance has two disks, where `/dev/vda` is the system disk and `/dev/vdc` is the newly added data disk.
![](https://main.qcloudimg.com/raw/72a7a48c59c13a44958a6b1aa0407ac2.png)
3. Run the following command to use the parted tool to partition the newly added data disk.
 ```
parted <Newly added data disk>
```
Take the newly mounted data disk `/dev/vdc` as an example:
```
parted /dev/vdc
```
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/0b2c9164f9fec125a72dee8861b7327d.png)
4. Enter `p` and press **Enter** to view the current disk partition format.
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/af906521dd6a7f3b948cfad42745aaba.png)
**Partition Table: unknown** indicates that the disk partition format is unknown.
5. Run the following command to configure the disk partition format.
```
mklabel <Disk partition format>
```
If the disk capacity is larger than or equal to 2TB, only GPT partition format can be used:
```
mklabel gpt
```
6. Enter `p` and press **Enter** to check whether the disk partition format has been configured successfully.
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/3dfec9aba75cd3cb6dcfb06729f5ff26.png)
**Partition Table: gpt** indicates that the disk partition format is GPT.
7. Enter `unit s` and press **Enter** to set the unit of the disk to sector.
8. Take creating one partition for the entire disk as an example, enter `mkpart opt 2048s 100%` and press **Enter**.
Where, 2048s indicates the initial disk capacity and 100% indicates the final disk capacity. This is for reference only. You can choose the number of disk partitions and their capacities based on business needs.
9. Enter `p` and press **Enter** to view information about the newly created partition.
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/ee406e75c689f48d59e863adc768aa36.png)
This indicates the detailed information of the newly created partition `/dev/vdc1`.
10. Enter `q` and press **Enter** to exit the parted partition tool.
11. Run the following command to view the disk name.
```
lsblk
```
The returned information is similar to what is shown below. You can now see the new partition `/dev/vdc1`.
![](https://main.qcloudimg.com/raw/f95f599f11f88b8bcb89d4f02bb41292.png)
12. Run the following command to configure the file system of the newly created partition to that required by the system.
```
mkfs -t <File system format> /dev/vdc1
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
mkfs -t ext4 /dev/vdc1
```
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/3cd6bbd019dd9bdc85ad4ed11ba64f0b.png)
The formatting takes a while. Pay attention to the system's running status and do not exit.
13. Run the following command to create a new mount point.
```
mkdir <Mount point>
``` Take creating a new mount point `/data/newpart2` as an example:
```
mkdir /data/newpart2
```
14. Run the following command to mount the new partition to the newly created mount point.
```
mount /dev/vdc1 <Mount point>
```
Take creating the `/data/newpart2` mount point as an example:
```
mount /dev/vdc1 /data/newpart2
```
15. Run the following command to view the mount results.
```
df -TH
```
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/774c2d9ff266634c4836df6456b9dd4d.png)
This indicates that the newly created partition `/dev/vdc1` has been mounted to `/data/newpart2`.
<dx-alert infotype="explain" title="">
If you don't need to configure disk automount at startup, skip the following steps.
</dx-alert>
16. [](id:step16)Confirm the mounting method and get the corresponding information.
 Based on business needs, you can use an elastic cloud disk's soft link, file system's UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
 <table>
     <tr>
         <th>Mounting method</th>  
         <th>Pros and cons</th>  
         <th>Information acquisition method</th>  
     </tr>
	   <tr>      
         <td nowrap="nowrap">Use the soft link of the elastic cloud disk <b>(recommended)</b></td>   
	       <td><b>Pros</b>: The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.<br><b>Cons</b>: Only an elastic cloud disk can use the soft link, which operates imperceptibly for the partition formatting operation.</td>
	       <td nowrap="nowrap">Run the following command to obtain the soft link of the elastic cloud disk.</br><pre style="color:white;">ls -l /dev/disk/by-id</pre></td>
     </tr> 
     <tr>      
         <td nowrap="nowrap">Use the UUID of the file system</td>   
         <td>Auto-mounting configuration may fail due to changes in a file system's UUID.</br>For example, reformatting a file system will change its UUID.</td>
         <td nowrap="nowrap">Run the following command to obtain the UUID of the file system.</br><pre style="color:white;"> blkid /dev/vdc1</pre></td>
     </tr> 
     <tr>      
         <td nowrap="nowrap">Use device name</td>   
	       <td>Automatic mounting configuration may fail due to changes in device name.</br>For example, if an elastic cloud disk on the CVM is unmounted and then remounted, the device name may change when the operating system recognizes the file system again.</td>
	       <td>Run the following command to obtain the device name.</br><pre style="color:white;">fdisk -l</pre></td>
     </tr> 
</table>
17. Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
cp -r /etc/fstab /home
```
18. Run the following command to use VI editor to open the `/etc/fstab` file.
 ```
vi /etc/fstab
 ```
19. Press <b>i</b> to enter edit mode. 
20. Move the cursor to the end of the file, press <b>Enter</b>, and add the following content.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
  - <b>(Recommended)</b> Take automatic mounting using the soft link of an elastic cloud disk as an example. Add the following content:
 ```
/dev/disk/by-id/virtio-disk-bm42ztpm-part1 /data/newpart2   ext4 defaults     0   2
 ```
  - Take automatic mounting using the UUID of the disk partition as an example. Add the following content:
```
UUID=fc3f42cc-2093-49c7-b4fd-c616ba6165f4 /data/newpart2   ext4 defaults     0   2
```
  - Take automatic mounting using the device name as an example. Add the following content:
```
/dev/vdc1 /data/newpart2   ext4 defaults     0   2
```

20. Press <b>Esc</b>, enter <b>:wq</b>, and press <b>Enter</b>.
Save the configuration and exit the editor.
21. Run the following command to check whether the `/etc/fstab` file has been written successfully.
```
mount -a 
```
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system starts up.

:::
</dx-tabs>


## Related Operations
 [Initializing Cloud Disks (<2 TB)](https://intl.cloud.tencent.com/document/product/362/31597).
