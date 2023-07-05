## Overview
This document describes how to initialize a data disk in the Lighthouse console. After creating a cloud disk and attaching it to the Lighthouse instance as a data disk, you need to initialize the disk to use it.


## Prerequisites
Attach a cloud disk to your Lighthouse instance. See [Attaching a Cloud Disk](https://intl.cloud.tencent.com/document/product/1103/46568).

## Considerations
- Read [FAQs about cloud disk usage](https://intl.cloud.tencent.com/document/product/362/32409) before working with cloud disks.
- Formatting a data disk will erase all data. Make sure that the disk does not contain data, or important data has been backed up.
- To prevent service exceptions, ensure that the Lighthouse instance 


## Directions

<dx-tabs>
::: Linux instance
Select the initialization method according to your actual use cases:

- If the entire disk is presented as one independent partition (there is no logical disks such as vdb1 and vdb2), we strongly recommend that you not use partition, and directly [create the file system on bare devices](#CreateFileSystemOnBareDevice).
- If the entire disk needs to be presented as multiple logical partitions (there are multiple logical disks), you need to first partition the disk, and then [create the file system on a partition](#CreateFileSystemOnPartition).


### Creating file systems on bare devices[](id:CreateFileSystemOnBareDevice)

<dx-alert infotype="explain" title="">
This example uses a Lighthouse instance using CentOS 8.0 operating system. Note that the steps may vary according to the operating system version.
</dx-alert>


1. Log in to the Lighthouse instance. For details, see [Logging in to a Linux instance via WebShell](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Run the following command to view the disk name.
```
sudo fdisk -l
```
If the returned result is similar to what is shown below, the current Lighthouse instance has two disks, where `/dev/vda` is the system disk (40 GB) and `/dev/vdb` is the new data disk (20 GB).
![](https://qcloudimg.tencent-cloud.cn/raw/022f33a4fcaced081b1fff2c1b45f68a.png)
3. Run the following command to create a file system on the `/dev/vdb` bare device.
```
sudo mkfs -t <File system format> /dev/vdb
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
sudo mkfs -t ext4 /dev/vdb
```
<dx-alert infotype="notice" title="">
The formatting takes a while. Please pay attention to the system’s running status and do not exit.
</dx-alert>
4. Run the following command to create a new mount point. The following example uses `/data` as the new mount point:
```
sudo mkdir /data
```
5. Run the following command to mount the device to a new mount point. The following example uses `/data` as the new mount point:
```
sudo mount /dev/vdb /data
```
6. Run the following command to view the mount result.
```
sudo df -TH
```
If the returned result is similar to what is shown below, `/dev/vdb` is mounted to `/data` successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/10208dbb148a2aad70043553d7406f19.png)
The disk needs to be mounted to the instance every time the instance starts up. To set the disk to be automatically mounted upon instance start-up, see [Auto-Mounting Disk upon Linux Instance Start-up](#autoMount).


### Creating a file system on a partition[](id:CreateFileSystemOnPartition)


<dx-alert infotype="explain" title="">
This example uses the parted partition tool in the CentOS 8.0 operating system to configure data disk `/dev/vdc` as the primary partition. MBR is used as the default partition format, EXT4 format as the file system, and `/data/newpart` as the mount point. Disk automount at startup is configured. Note that the formatting operation may vary according to the operating system.
</dx-alert>


1. Log in to the Lighthouse instance. For details, see [Logging In to a Linux instance via WebShell](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Run the following command to view the disk name.
```
sudo fdisk -l
```
If the returned result is similar to what is shown below, the current Lighthouse instance has two disks, where `/dev/vda` is the system disk (40 GB) and `/dev/vdb` is the new data disk (20 GB).
![](https://qcloudimg.tencent-cloud.cn/raw/022f33a4fcaced081b1fff2c1b45f68a.png)
3. Run the following command to enter the fdisk partition tool and start partitioning the new data disk. The following example uses `/dev/vdb` as the newly attached data disk:
```
sudo fdisk /dev/vdb
```
The returned information is similar to what is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/103bc99653d402383bb41c39302ad0e0.png)
4. Enter **n** and press **Enter** to start creating a partition. The following information is returned:
![](https://qcloudimg.tencent-cloud.cn/raw/58443424e28a2964a2219be36b19638f.png)
This indicates that the disk has two partition types:
 - *p*: Primary partition.
 - *e*: Extended partition.
5. Take creating a primary partition as an example. Enter `p` and press **Enter** to start creating a primary partition. The following information is returned:
![](https://qcloudimg.tencent-cloud.cn/raw/580d430456b9073dc208eea001acc53b.png)
**Partition number** indicates the number of the primary partition. Valid range: 1-4.
6. Take partition 1 as an example. Enter the primary partition number **1** and press **Enter**. The following information is returned:
![](https://qcloudimg.tencent-cloud.cn/raw/7e7b409c4619769db5d7037f0a11571b.png)
**First sector** indicates the start sector. Valid range: 2048 (default value) - 41943039.
7. Take selecting the default start sector number 2048 as an example. Press **Enter**. The following information is returned:
![](https://qcloudimg.tencent-cloud.cn/raw/6a2cbd16dc7824164c9c5a1423c68a0b.png)
**Last sector** indicates the end sector. Valid range: 2048 - 41943039 (default value).
8. Take selecting the default end sector number 41943039 as an example. Press **Enter**. The following information is returned:
![](https://qcloudimg.tencent-cloud.cn/raw/9cf97b38aa9ccebf3bd1d651ca69ddf9.png)
9. The partitioning is complete. A new partition has been created on the 20 GB data disk.
10. Enter **p** and press **Enter** to view the details of the new partition `/dev/vdb1`.
![](https://qcloudimg.tencent-cloud.cn/raw/2229afc79775ba6b9d5b70f39f66c64f.png)
<dx-alert infotype="explain" title="">
If an error occurs during the partitioning operation, enter **q** to exit the fdisk tool and the prior partition result will not be retained.
</dx-alert>
11. Enter **w** and press **Enter** to write the partition result to the partition table. The returned result is shown below, indicating that the partition creation is complete.
![](https://qcloudimg.tencent-cloud.cn/raw/d9dd755906477a7eb73b2fe83b0ca8e9.png)
12. Run the following command to sync the partition table to the operating system.
```
partprobe
```
13. Run the following command to set the file system of the new partition to the format required by the system.
```
sudo mkfs -t <File system format> /dev/vdb1
```
The partition size supported by different file systems varies. Select an appropriate file system as needed. The following example takes `EXT4` as the file system:
```
sudo mkfs -t ext4 /dev/vdb1
```
<dx-alert infotype="notice" title="">
The formatting takes a while. Please pay attention to the system’s running status and do not exit.
</dx-alert>
14. Run the following command to create a new mount point. The following example uses `/data/newpart` as the new mount point:
```
sudo mkdir /data/newpart
```
15. Run the following command to mount the new partition to a new mount point. The following example uses `/data/newpart` as the new mount point:
```
sudo mount /dev/vdb1 /data/newpart
```
16. Run the following command to view the mounting results.
```
sudo df -TH
```
The returned information is similar to what is shown below. This indicates that the partition `/dev/vdb1` has been mounted to `/data/newpart`.
![](https://qcloudimg.tencent-cloud.cn/raw/2fd33e9978b0cea3df6f5e6df917e95a.png)
The disk needs to be mounted to the instance every time the instance starts up. To set the disk partition to be automatically mounted upon instance start-up, see [Auto-Mounting Disk upon Linux Instance Start-up](#autoMount).

:::
::: Windows instances

<dx-alert infotype="explain" title="">
This example uses a Lighthouse instance using Windows Server 2016 R2 operating system. Note that the steps may vary according to the operating system version.
</dx-alert>

1. Log in to the Lighthouse instance. For more information, see [Logging in to a Windows Instance via VNC](https://intl.cloud.tencent.com/document/product/1103/46399).
2. On the desktop, right-click <img src="https://qcloudimg.tencent-cloud.cn/raw/d31f2d1c79409188f9465a041455b5cf.png" style="margin:-4px 0px"> in the lower-left corner and click **Disk management** in the pop-up menu.
Open the **Disk management** window to view the data disk information. 
![](https://qcloudimg.tencent-cloud.cn/raw/e9faf9beb760e47a4732a1d81ee4dc69.png)
<dx-alert infotype="notice" title="">
If the new disk is offline (as shown above), continue to [Step 3](#step3) to make it online. If it’s already online, go to [Step 4](#step4).
</dx-alert>
3. [](id:step3) Right-click in the Disk 1 area, and click **Online**.
![](https://qcloudimg.tencent-cloud.cn/raw/0f695c2a297f0e7283dace9b76bd02f6.png)
4. [](id:step4)Disk 1 changes from **Offline** to **Not Initialized**. Right-click in the Disk 1 area and select **Initialize Disk**.
![](https://qcloudimg.tencent-cloud.cn/raw/2e0449e401ff18bfbfc86da743846677.png)
5. In the **Initialize Disk** window, select the target disk and the disk partition format, and click **OK**. In this example, **MBR (Master Boot Record)** is used.
<dx-alert infotype="notice" title="">
If the disk partition format is changed after the disk is put into use, the original data on the disk will be erased. Please select an appropriate partition format based on actual needs.
</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/f20e82296e93672bfc946cea02e841f5.png)
6. Right-click the free space of Disk 1, and select **New Simple Volume**.
![](https://qcloudimg.tencent-cloud.cn/raw/5d887bbbeb457f9b8a7ff01f39988729.png)
7. In the welcome page of **New Simple Volume Wizard** pop-up window, click **Next**.
8. Specify the volume size as needed, which is the maximum value by default. Click **Next**.
9. Assign a drive letter, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a011638a9a65411a448afa11228d89a3.png)
10. Select **Format this volume with the following settings**. Configure the parameters as needed, format the new partition, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/64ca489770db96b0dc2bb4ef14a7045e.png)
11. Click **Complete**. Wait for a while for the system to complete the initialization. When the volume status becomes "Healthy", the disk initialization is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/c1d704e331ff7a9ae693edc15ff3b197.png)
After the initialization is complete, enter the **PC** interface to view the new disk.
![](https://qcloudimg.tencent-cloud.cn/raw/0998e5d0858d706126578af12b23ab89.png)

:::
</dx-tabs>




## Related Operations

### Auto-mounting disks upon Linux instance start-up[](id:autoMount)
1. Confirm the mounting method and obtain the corresponding information.
Based on business needs, you can use a cloud disk's soft link, file system's UUID (universally unique identifier), or device name to automatically mount a disk. The descriptions and information acquisition methods are as follows:
<table>
 <tr>
      <th>Mounting method</th>
      <th>Pros and cons</th>
      <th>Information acquisition method</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use the soft link of the cloud disk <br><b>(recommended)</b></td>
     <td><b>Pros</b>: The soft link of a cloud disk is fixed and unique. It does not change with operations such as mounting, unmounting, and formatting partitions.</br><b>Cons</b>: Only a cloud disk can use the soft link, which operates imperceptibly for the partition formatting operation.</td>
		 <td nowrap="nowrap">Run the following command to obtain the soft link of the cloud disk.</br><pre style="color:white;">sudo ls -l /dev/disk/by-id</pre></td>
	</tr>
	<tr>
	   <td nowrap="nowrap">Use the UUID of the file system</td>
		 <td>Auto-mounting configuration may fail due to changes in a file system's UUID.</br>For example, reformatting a file system will change its UUID.</td>
		 <td nowrap="nowrap">Run the following command to obtain the UUID of the file system.</br><pre style="color:white;">sudo blkid /dev/vdb</pre></td>
  </tr>
	<tr>
	   <td nowrap="nowrap">Use device name</td>     
		 <td>Auto-mounting configuration may fail due to changes in device name.</td>
		 <td nowrap="nowrap">Run the following command to obtain the device name.</br><pre style="color:white;">sudo fdisk -l</pre></td>
 </tr>
</table>
2. Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```
sudo cp -r /etc/fstab /home
```
3. Run the following command to use VI editor to open the `/etc/fstab` file.
```
sudo vi /etc/fstab
```
4. Press **i** to enter edit mode.
5. Move the cursor to the end of the file and press **Enter**, then add the following content.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
 - (Recommended) Assume that you need to automatically mount a cloud disk by using a soft link:
```
/dev/disk/by-id/virtio-disk-xxxxx /data ext4 defaults 0 0
```
For mounting the partition, add the following content:
```
/dev/disk/by-id/virtio-disk-xxxxx-part1 /data/newpart ext4 defaults 0 2
```
<dx-alert infotype="explain" title="">
If you have multiple cloud disks, you can distinguish them by comparing the `xxxxx` in `virtio-disk-xxxxx` with the cloud disk ID `lhdisk-xxxxxx` in the console. The cloud disk ID in the console is shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5176eb65bfab2987663561471e5ef251.png)
</dx-alert>
 - Take automatic mounting using the UUID of the disk partition as an example. Add the following content:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
For mounting the partition, add the following content:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data/newpart   ext4 defaults     0   2
```
 - Take automatic mounting using the device name as an example. Add the following content:
```
/dev/vdb /data   ext4 defaults     0   0
```
For mounting the partition, add the following content:
```
/dev/vdb1 /data/newpart /data/newpart ext4 defaults 0 2
```
6. Press **Esc**, enter **:wq**, and press **Enter** to save the configuration and exit the editor.
7. Run the following command to check whether the **/etc/fstab** file has been written successfully.
```
sudo mount -a 
```
If the command runs successfully, the file has been written. The newly created file system will automatically mount when the operating system starts up.
