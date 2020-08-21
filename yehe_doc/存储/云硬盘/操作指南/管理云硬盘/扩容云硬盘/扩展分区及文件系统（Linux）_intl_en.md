## Introduction
Cloud disks are expandable storage devices on the cloud. After creating a cloud disk, you can expand its capacity at any time to increase its storage space without losing any original data.
After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition.



## Prerequisites
>!Expanding the file system may affect existing data. We strongly recommend that you manually [create a snapshot](https://cloud.tencent.com/document/product/362/5755) to back up your data before the operation.
To protect your existing data, we have added two options to umount existing partitions and run fsck for a filesystem check during the expansion process. You can choose to use them as needed.
- You have [expanded the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Linux CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5436) the Linux CVM on which you want to expand partitions and the file system.

## Directions
### Confirming the expansion method
<span id="fdisk"></span>
1. Run the following command as the root user to view the partition format of the cloud disk.
```
fdisk -l
```
 - If the result indicates that the device has no partition (for example, it only shows /dev/vdb), see [extending the file system](#ExpandTheFileSystem).
 - If the result similar to the following two figures (which may vary according to the operating system) is returned, GPT partition format is used.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - If the result similar to the following two figures (which may vary according to the operating system) is returned, MBR partition format is used.
 >! The maximum disk capacity supported by MBR partition format is 2 TB. If your disk partition is in MBR format, and you need to expand its capacity to more than 2 TB, we recommend that you create and mount a new data disk, and copy the data to the new disk using GPT partition format. For Linux operating system, if the disk partition format is GPT, the fdisk partition tool can no longer be used, and parted tool must be used.
 
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2. Follow [Step 1](#fdisk) to view the cloud disk partition format, and select the corresponding operations guide.
<table>
     <tr>
         <th nowrap="nowrap">Partition format</th>  
         <th>Operations guide</th>  
         <th>Description</th>  
     </tr>
		 	 <tr>      
         <td>-</td>   
	     <td nowrap="nowrap"><a href="#ExpandTheFileSystem">Extend the file system</a></td>
	     <td>Applicable to scenarios where a file system is created directly on a bare device and no partition is created.</td>
     </tr>
	 <tr>      
         <td rowspan="2">GPT</td>   
	     <td nowrap="nowrap"><a href="#AddToTheExistingGPTPart">Assign the expanded capacity to an existing partition (GPT)</a></td>
	     <td>Also applicable to scenarios of direct formatting when no partition is created.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewGPTPart">Format the expanded capacity into an independent new partition (GPT)</a></td> 
	     <td>The original partition can be retained without changes.</td>
     </tr> 
	 <tr>
         <td rowspan="2">MBR</td>   
	     <td><a href="#AddToTheExistingMBRPart">Assign the expanded capacity to an existing partition (MBR)</a></td> 
	     <td>Also applicable to scenarios of direct formatting when no partition is created.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewMBRPart">Format the expanded capacity into an independent new partition (MBR)</a></td> 
	     <td>The original partition can be retained without changes.</td>
     </tr> 
</table>

<span id="ExpandTheFileSystem"></span>
### Extending the file system

1. Use different commands to extend the file system, depending on the file system type:
 - For an EXT file system, run the `resize2fs` command to extend the file system.
 - For an XFS file system, run the `xfs_growfs` command to extend the file system.
Taking `/dev/vdb` as an example, run the following command to extend an EXT file system:
```
resize2fs /dev/vdb
```
Taking `/dev/vdb` as an example, run the following command to extend an XFS file system:
```
xfs_growfs /dev/vdb
```
2. Run the following command to view the new partition:
```
df -h
```

<span id="AddToTheExistingGPTPart"></span>
### Assigning the expanded capacity to an existing partition (GPT)
1. Run the following command as the root user to confirm changes in cloud disk capacity:
 ```
parted <Disk path> print
 ```
Taking the disk path `/dev/vdb` as an example, run the following command:
```
parted /dev/vdb print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the following figure, the cloud disk capacity is 107 GB after expansion and the existing partition capacity is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)

2. Run the following command to check whether the cloud disk has partitions mounted:
```
mount | grep '<Disk path>' 
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Run the following command to unmount the data disk:
```
umount <mount point>
```
Taking the mount point `/data`mount point as an example, run the following command:
```
umount /data
```
>?Unmount the file systems from all partitions on the cloud disk, and execute the operations in [Step 4](#step4) again. You can run the following command again to confirm that the unmounting is successful.
```
mount | grep '/dev/vdb'
```
The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9242efdec1aab382ae74f975ca68d68a.png)
4. <span id="step4"></span>Run the following command to access the parted tool.
```
parted '<Disk path>'
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```
parted '/dev/vdb'
```
5. Run the following command to change the unit from the default “GB” to “sector” for display and operation:
```
unit s
```
6. Run the following command to view partitions and record their `Start` values:
>! After a partition is deleted and a new one is created, the `Start` value must remain unchanged. Otherwise, it may cause data loss.
>
```
print
```
Take the `Start` value `2048s` as an example:
![](//mccdn.qcloud.com/static/img/67ba54c1d9d63c307d4b8a157b70c722/image.png)

7. Run the following command to delete the existing partition:
```
rm <Partition Number>
```
For example, run the following command to delete the partition “1” from the CVM:
```
 rm 1
```
The following figure shows the command output.
![](//mccdn.qcloud.com/static/img/3384eeada87ce75695e0e55125109eff/image.png)
8. Run the following command to create a new primary partition:
```
mkpart primary <Start sector of the original partition> 100%
```
The 100% in the command indicates this partition goes to the end of the disk.
Assume that the primary partition starts from sector 2048 (it must be the same as that of the previously deleted partition, that is, the `Start` value must be 2048s), run the following command:
```
mkpart primary 2048s 100%
```
If a status as shown in the following figure appears, enter `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
6. Run the following command to check whether the new partition has been created successfully:
```
print
```
If the result as shown in the following figure is returned, the new partition has been created successfully.
![](//mccdn.qcloud.com/static/img/cb1af5adaf6c89d066077c43fd428a38/image.png)
7. Run the following command to exit the parted tool:
```
quit
```
11. Run the following command to check the extended partition:
```
e2fsck -f <Partition path>
```
Taking the newly created partition “1” (that is, the partition path is `/dev/vdb1`) as an example, run the following command:
```
e2fsck -f /dev/vdb1
```
The following figure shows the command output.
![](//mccdn.qcloud.com/static/img/307f7a0c98eea05ca1d4560fe4e96f57/image.png)
Extend your file system depending on the type:
	- For an **EXT file system**:
		1. Run the following command to extend the EXT file system in the new partition:
```
resize2fs <Partition path>
```
Taking the partition path `/dev/vdb1` as an example, run the following command:
```
resize2fs /dev/vdb1
```
If the result as shown in the following figure is returned, the expansion is successful.
![](//mccdn.qcloud.com/static/img/57d66da9b5020324703498dbef0b12f9/image.png)
		2. Run the following command to manually mount the new partition:
```
mount <Partition path> <Mount point>
```
Taking the partition path `/dev/vdb1` and the mount point `/data` as an example, run the following command:
```
mount /dev/vdb1 /data
```
 - For an **XFS file system**:
	  1. Run the following command to manually mount the partition:
```
mount <Partition path> <Mount point>
```
Taking the partition path `/dev/vdb1` and the mount point `/data` as an example, run the following command:
```
mount /dev/vdb1 /data
```
	  2. Run the following command to extend the XFS file system in the new partition:
```
xfs_growfs <Partition path>
```
Taking the partition path `/dev/vdb1` as an example, run the following command:
```
xfs_growfs /dev/vdb1
```
12. Run the following command to view the new partition:
```
df -h
```
If the result as shown in the following figure is returned, the mount is successful and you can see the data disk.
![](//mccdn.qcloud.com/static/img/a2bd04c79e8383745689e19033a0daaa/image.png)

<span id="CreateANewGPTPart"></span>
### Formatting the expanded capacity into an independent new partition (GPT)

1. Run the following command as the root user to confirm changes in cloud disk capacity:
 ```
parted <Disk path> print
 ```
Taking the partition path `/dev/vdb` as an example, run the following command:
```
parted /dev/vdb print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the following figure, the cloud disk capacity is 107 GB after expansion and the existing partition capacity is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)
2. Run the following command to check whether the cloud disk has partitions mounted:
```
mount | grep '<Disk path>' 
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Run the following command to unmount the data disk:
```
umount <mount point>
```
Taking the mount point `/data` as an example, run the following command:
```
umount /data
```
>?Unmount the file systems from all partitions on the cloud disk, and execute the operations in [Step 4](#Step4) again. You can run the following command again to confirm that the unmounting is successful.
```
mount | grep '/dev/vdb'
```
The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d1a9a33f0d4e3725aed677f2403c91ae.png)
<span id="Step4"></span>
4. Run the following command to access the parted partition tool:
```
parted '<Disk path>'
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```
parted '/dev/vdb'
```
5. Run the following command to view partitions and record their `End` values, which will be used as the start offset of the next partition:
```
print
```
![](//mccdn.qcloud.com/static/img/788ce125bba952f204ed6ee36dfb644d/image.png)
6. Run the following command to create a new primary partition. This partition starts from the end of the existing partition, and covers all the newly added space on the disk.
```
mkpart primary start end
```
Taking the `End` value “10.7 GB” as an example, run the following command:
```
mkpart primary 10.7GB 100%
```
7. Run the following command to check whether the new partition has been created successfully:
```
print
```
![](//mccdn.qcloud.com/static/img/fc54fd4c05102ee91c648526d77d1b42/image.png)
8. Run the following command to exit the parted tool:
```
quit
```
9. Run the following command to format the newly created partition:
```
mkfs.<fstype> <Partition path> 
```
Select a file system format such as EXT2 or EXT3 as needed.
Taking the EXT3 file system as an example, run the following command: 
```
mkfs.ext3 /dev/vdb2
```

<span id="AddToTheExistingMBRPart"></span>
### Assigning the expanded capacity to an existing partition (MBR)
You can use the fdisk/e2fsck/resize2fs automatic expansion tools to add the newly expanded disk space to the existing file system on a Linux CVM. For a successful expansion, the following four requirements must be met:
- The file system is EXT2, EXT3, EXT4, or XFS.
- The current file system does not have any error.
- The disk size after expansion does not exceed 2 TB.
- The current tools only support Python version 2, not Python version 3.


1. Run the following command as the root user to unmount the partition:
```
umount <Mount point>
```
Taking the mount point `/data` as an example, run the following command:
```
umount /data
```
![](//mccdn.qcloud.com/static/img/c0acc05057941681627a5fd34979d194/image.jpg)
2. Run the following command to download a tool:
```
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. Run the following command to use the expansion tool for expansion:
```
python /tmp/devresize.py <Disk path>
```
Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
```
python /tmp/devresize.py /dev/vdb
```
![](//mccdn.qcloud.com/static/img/c7617b90578192d64d19f02325f00ffb/image.jpg)
 - If “The filesystem on /dev/vdb1 is now XXXXX blocks long.” is returned, the expansion is successful. Execute [Step 4](#step4MBR).
 - If “[ERROR] - e2fsck failed!!” is returned, execute the following steps:
   a. Run the following command to fix the partition where the file system resides:
```
fsck -a <Partition path>
```
Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
```
fsck -a /dev/vdb1
```
    b. Run the following command again after the fix to use the expansion tool for expansion:
```
python /tmp/devresize.py /dev/vdb
```
<span id="step4MBR"></span>
4. Run the following command to manually mount the extended partition:
```
mount <Partition path> <Mount point>
```
Take the mount point `/data` as an example.
 - If there is a partition before expansion and the partition path is `/dev/vdb1`, run the following command:
```
mount /dev/vdb1 /data
```
 - If there is no partition before expansion, run the following command:
```
mount /dev/vdb /data
```
5. Run the following command to view the partition capacity after expansion:
```
df -h
```
The result similar to to what is shown below is returned, the mount is successful, and you can see the data disk.
![](//mccdn.qcloud.com/static/img/2367f3e70cd0c3c1bef665cc47c1c3bc/image.jpg)
6. Run the following command to view the data of the original partition after expansion and check whether the new storage space has been added to the file system.
```
ll /data
```

<span id="CreateANewMBRPart"></span>
### Formatting the expanded capacity into an independent new partition (MBR)
1. Run the following command as the root user to view the partitions of the mounted data disk:
```
df -h
```
![](//mccdn.qcloud.com/static/img/0a450dfaa9cfc7b2c7fdc04861f0e754/image.png)
2. Run the following command to view the data disk after expansion without partitions:
```
fdisk -l
```
![](//mccdn.qcloud.com/static/img/594671a1215dee3036b7940892438f62/image.png)
3. Run the following command to unmount all mounted partitions:
```
umount <mount point>
```
Taking the mount point `/data` as an example, run the following command:
```
umount /data
```
>? Unmount the file systems from all partitions on the cloud disk, and execute the operations in [Step 4](#Step4MBR) again. You can run the following command again to confirm that unmounting is successful.
```
mount | grep '<Disk path>'
```
If it returns null, all file systems have been unmounted from partitions on the cloud disk.
4. <span id="Step4MBR"></span>Run the following command to create a partition.
```
fdisk <Disk path>
```
Taking the disk path `/dev/xvdc` as an example, run the following command:
```
fdisk /dev/xvdc
```
When prompted, sequentially enter `p` (check existing partitions), `n` (create a partition), `p` (create a primary partition), `2`(create a second primary partition), press **Enter** twice (keep default configurations), enter `w` (save the partition table), and start the partition, as shown in the following figure:
![](//mccdn.qcloud.com/static/img/8c35d6f4dfb367e74edc27ce6822c317/image.png)
>? This document uses creating one partition as an example. You can also create multiple partitions as needed.
5. Run the following command to view the new partition:
```
fdisk -l
```
As shown in the following figure, the new partition “xvdc2” has been created.
![](//mccdn.qcloud.com/static/img/e04e924d62317bc2c605c8abaac394f5/image.png)
6. Run the following command to format the new partition and create a file system:
```
mkfs.<fstype> <Partition path> 
```
Select a file system format such as EXT2 or EXT3 as needed.
Taking the EXT3 file system as an example, run the following command:
```
mkfs.ext3 /dev/xvdc2
```
![](//mccdn.qcloud.com/static/img/074e23eaa580495f96fb532b688d2d68/image.png)
7. Run the following command to create a mount point:
```
mkdir <New mount point>
```
This example taking `/data1` as the new mount point, run the following command:
```
mkdir /data1
```
8. Run the following command to manually mount the new partition:
```
mount <New partition path> <New mount point>
```
This example taking `/dev/xvdc2` as the new partition path and `/data1` as the new mount point, run the following command:
```
mount /dev/xvdc2 /data1
```
9. Run the following command to view the new partition:
```
df -h
```
If the result as shown in the following figure is returned, the mount is successful, and you can see the data disk.
![](//mccdn.qcloud.com/static/img/7b749a4bb6e7c8267c9354e1590c35d4/image.png)
>? To allow the CVM to automatically mount a data disk at restart or startup, perform [Step 10](#AddNewPartINFOstep10) and [Step 11](#AddNewPartINFOstep11) to add the new partition information to `/etc/fstab`.
10. <span id="AddNewPartINFOstep10"></span>Run the following command to add information:
```
echo '/dev/xvdc2 /data1 ext3 defaults 0 0' >> /etc/fstab
```
11. <span id="AddNewPartINFOstep11"></span>Run the following command to view information:
```
cat /etc/fstab
```
If the result as shown in the following figure is returned, the partition information is successfully added.
![](//mccdn.qcloud.com/static/img/f0b5c14bf08fd3629ddf6d9b1ae01ffc/image.png)

## Related Operations
[Extending partitions and file systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## FAQs
If you encounter any problem when using a cloud disk, refer to the following documents for troubleshooting based on your actual situation.
- [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409)
- [Features FAQs](https://intl.cloud.tencent.com/document/product/362/32408)
