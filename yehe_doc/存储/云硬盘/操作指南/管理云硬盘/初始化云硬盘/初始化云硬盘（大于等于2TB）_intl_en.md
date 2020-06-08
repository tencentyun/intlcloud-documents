## Scenario
This document takes cloud disks with a capacity greater than or equal to 2TB as an example to provide guidance on disk initialization. For more information, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
MBR supports disk with a maximum capacity of 2TB. When you partition disk with a capacity greater than 2TB, we recommend that you use the GPT partition format. When GPT is used on Linux operating system, fdisk can no longer be used and the parted tool must be used.

## Prerequisites
You have [mounted a cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to your CVM.

## Notes
- To protect important data, please see [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409) before operating on your cloud disks.
- Formatting a data disk will erase all data. Make sure that the disk does not contain data, or important data has been backed up.
- To avoid exceptions, make sure before formatting that the CVM has stopped external services.

## Directions
<span id="2TBWindows2012"></span>
### Initializing cloud disks (Windows)
>This document uses the Windows Server 2012 operating system as an example. The formatting operation varies by operating system. Below is for reference only.

1. [Log in to the Windows Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5435).
2. In the CVM desktop, click <img src="https://main.qcloudimg.com/raw/0a02193a82217974f650bbcaf4e1ed2d.png"  style="margin:0;"> to enter the **Server Manager** page.
3. In the left navigation tree, click **File and Storage Services**.
4. In the left navigation tree, select **Volumes**>**Disks**.

>If the newly added disk is in offline status (as shown in the figure above), execute [Step 5](#online) before [Step 6](#initialize) to perform initialization. Otherwise, you can directly execute [Step 6](#initialize).

<span id="online"></span>
5. Disks are listed on the right-side pane. Right click the row where 1 is located, and select **Online** to bring it online. The status of 1 changes from **Offline** to **Online**.

<span id="initialize"></span>
6. Right click the row where 1 is located, and select **Initialize** in the menu.
7. Follow instructions on the interface, and click **Yes**.
8. After initialization, the partition of 1 changes from **Unknown** to **GPT**. Right click the row where 1 is located and select **New Simple Volume** in the menu.
9. In the pop-up **New Volume Wizard** dialog box, follow instructions on the interface and click **Next**.
10. Select the server and disk, and click **Next**.
11. Specify the volume size as needed, which is the maximum value by default. Click **Next**.
12. Assign a drive letter, and click **Next**.
13. Select **Format this volume with the following settings**, configure parameters as needed, format the partition, and click **Next** to complete the partition creation.
14. Confirm the information and click **Create**.
15. Wait for the system to complete the creation of the new volume, and then click **Finish**.
 After completing initialization, enter the **My Computer** interface to view the new disk.

<span id="2TBLinux"></span>
### Initializing cloud disks (Linux)

Select the initialization method according to your actual use scenario:
- If the entire disk is presented as one independent partition (i.e., no logical disks such as vdb1 and vdb2), we strongly recommend that you not use partition, and directly [create the file system on bare devices](#CreateFileSystemOnBareDevice).
- If the entire disk is presented as multiple logical partitions (i.e., there are multiple logical disks), you need to perform the partition operation first, and then [create the file system on a partition](#CreateFileSystemOnPartition).

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
mkdir <Mount point>
```
Take creating a new mount point `/data` as an example:
```
mkdir /data
```
5. Execute the following command to mount the newly created partition to the newly created mount point.
```
mount /dev/vdb <Mount point>
```
Take the newly created mount point `/data` as an example:
```
mount /dev/vdb /data
```
6. Execute the following command to view the mount result.
```
df -TH
```
>If you do not need to configure automatic disk mounting at startup, skip the following steps.
7. Confirm the mount method and obtain the corresponding information.
Based on business needs, you can use an elastic cloud disk’s soft link, file system’s UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
<table>
 <tr>
     <th>Mount method</th>
		 <th>Pros and cons</th>
		 <th>Information acquisition method</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(recommended)</b></td>
		 <td><b>Pros:</b>The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only an elastic cloud disk can use the soft link, which operates transparently for the partition formatting operation.</td>
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
8. Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
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
13. Execute the following command to check whether the `/etc/fstab` file has been written successfully.
```
mount -a 
```
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system is launched.

<span id="CreateFileSystemOnPartition"></span>
#### Creating a file system on a partition

>This example uses the parted partition tool in the CentOS 7.5 operating system to configure data disk `/dev/vdc` as the primary partition. GPT is used as the default partition format, EXT4 format as the file system, `/data/newpart2` as the mount point, and automatic mounting at startup is configured. The formatting operation varies by operating system. Below is for reference only.

1. [Log in to the Linux Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command as the root user to view the disk name.
 ```
lsblk
 ```
If information similar to what is shown below is returned, the current CVM has two disks, where “/dev/vda” is the system disk and “/dev/vdc” is the newly added data disk.
	![](https://main.qcloudimg.com/raw/72a7a48c59c13a44958a6b1aa0407ac2.png)
3. Execute the following command to enter the parted partition tool, and execute the partition operation on the newly added data disk.
```
parted <Newly added data disk>
```
Take the newly mounted data disk `/dev/vdc` as an example:
```
parted /dev/vdc
```
The returned information is similar to what is shown below:
![](https://main.qcloudimg.com/raw/0b2c9164f9fec125a72dee8861b7327d.png)
4. Enter `p` and press Enter to view the current disk partition format.
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/af906521dd6a7f3b948cfad42745aaba.png)
 **Partition Table: unknown** indicates that the disk partition format is unknown.
5. Execute the following command to configure the disk partition format.
```
mklabel <Disk partition format>
```
If the disk capacity is larger than or equal to 2TB, only GPT partition format can be used:
```
mklabel gpt
```
6. Enter `p` and press Enter to check whether the disk partition format has been configured successfully.
 The returned information is similar to what is shown below:
	![](https://main.qcloudimg.com/raw/3dfec9aba75cd3cb6dcfb06729f5ff26.png)
 **Partition Table: gpt** indicates that the disk partition format is GPT.
7. Enter `unit s` and press Enter to configure the measurement unit of the disk as sector.
8. Take creating one partition for the entire disk as an example, enter `mkpart opt 2048s 100%` and press Enter.
 2048s indicates the initial disk capacity and 100% indicates the final disk capacity. This is for reference only. You can choose the number of disk partitions and their capacities based on business needs.
9. Enter `p` and press Enter to view information about the newly created partition.
    The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/ee406e75c689f48d59e863adc768aa36.png)
 This indicates the detailed information of the newly created partition `/dev/vdc1`.
10. Enter `q` and press Enter to exit the parted partition tool.
11. Execute the following command to view the disk name.
 ```
lsblk
 ```
The returned information is similar to what is shown below. You can now see the new partition “/dev/vdc1”.
![](https://main.qcloudimg.com/raw/f95f599f11f88b8bcb89d4f02bb41292.png)
12. Execute the following command to configure the file system of the newly created partition to that required by the system.
```
mkfs -t <File system format> /dev/vdc1
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
mkfs -t ext4 /dev/vdc1
```
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/3cd6bbd019dd9bdc85ad4ed11ba64f0b.png)
 The formatting takes a while. Please pay attention to the system’s running status and do not exit.
13. Execute the following command to create a new mount point.
```
mkdir <Mount point>
```
Take creating a new mount point `/data/newpart2` as an example:
```
mkdir /data/newpart2
```
14. Execute the following command to mount the newly created partition to the newly created mount point.
```
mount /dev/vdc1 <Mount point>
```
Take the newly created mount point `/data/newpart2` as an example:
```
mount /dev/vdc1 /data/newpart2
```
15. Execute the following command to view the mount result.
```
df -TH
```
 The returned information is similar to what is shown below:
 ![](https://main.qcloudimg.com/raw/774c2d9ff266634c4836df6456b9dd4d.png)
 This indicates that the newly created partition `/dev/vdc1` has been mounted to `/data/newpart2`.

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
         <td nowrap="nowrap">Use the soft link of the elastic cloud disk<b>(recommended)</b></td>   
	       <td><b>Pros:</b>The soft link of an elastic cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons:</b>Only an elastic cloud disk can use the soft link, which operates transparently for the partition formatting operation.</td>
	       <td nowrap="nowrap">Execute the following command to view the soft link of the elastic cloud disk.</br><pre>ls -l /dev/disk/by-id</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use the UUID of the file system</td>   
	       <td>Automatic mounting configuration may fail due to changes in a file system’s UUID.</br>For example, reformatting a file system will change its UUID.</td>
	       <td nowrap="nowrap">Execute the following command to view the UUID of the file system.</br><pre>blkid /dev/vdc1</pre></td>
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
19. Press **i** to enter the edit mode. 
20. Move the cursor to the end of the file, press **Enter**, and add the following content.
 ```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
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
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system is launched.

## Related Operations
 [Initializing cloud disks (smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597).


