## Introduction
Cloud disks are expandable storage devices on the cloud. After creating a cloud disk, you can expand its capacity at any time to increase its storage space without losing any original data.
After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign the expanded capacity to an existing partition, or format it into an independent new partition.



##  Prerequisites
> Extending the file system may affect existing data. We strongly recommend that you manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before performing the operation.
>
- You have [expanded the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/5745) to a Linux CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5436) the Linux CVM on which you want to expand partitions and the file system.

### Directions
### Confirming the expansion method
<span id="fdisk"></span>
1. Run the following command as the root user to view the partition format of the cloud disk.
```
fdisk -l
```
 - If the result indicates that the device has no partition (for example, it only shows /dev/vdb), see [Extending the file system](#ExtendTheFileSystem).
 - If the result is as shown in the following two figures (which may vary according to the operating system), the GPT partition format is used.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - If the result is as shown in the following figure (which may vary according to the operating system), the MBR partition format is used.
 > The maximum disk capacity supported by MBR partition format is 2 TB. If your disk partition is in MBR format, and you need to expand its capacity to more than 2 TB, we recommend that you create and mount a new data disk, select the GPT partition style, and copy the data from the MBR disk to the new disk. For Linux operating system, if the disk partition format is GPT, the fdisk partition tool can no longer be used, and the parted tool must be used.
 >
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
	     <td nowrap="nowrap"><a href="#ExtendTheFileSystem">Extend the file system</a></td>
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

<span id="ExtendTheFileSystem"></span>
### Extending the file system

1. Different commands are used for extending file systems, depending on the file system type. 
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
1. Run the following command as the root user to confirm changes in cloud disk capacity.
 ```
parted <Disk path> print
```
If the disk path is `/dev/vdb`, run the following command:
```
parted /dev/vdb print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the following figure, the cloud disk size is 107 GB after expansion and the size of existing partitions is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)

2. Run the following command to check whether the cloud disk has partitions mounted:
```
mount | grep '<Disk path>' 
```
If the disk path is `/dev/vdb`, run the following command:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Run the following command to unmount the data disk:
```
umount <Mounting point>
```
If the mounting point is `/data`, run the following command:
```
umount /data
```
> Unmount the file systems from all partitions on the cloud disk, and perform the operations in [Step 4](#step4) again. You can run the following command again to confirm that the file systems have been unmounted from all partitions on the cloud disk:
```
mount | grep '/dev/vdb'
```
The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9242efdec1aab382ae74f975ca68d68a.png)
4. <span id="step4"></span>Run the following command to access the parted tool.
```
parted '<Disk path>'
```
If the disk path is `/dev/vdb`, run the following command:
```
parted '/dev/vdb'
```
5. Run the following command to change the display and operational unit to sector (GB by default).
```
unit s
```
6. Run the following command to view the partition information and record the `Start` value of the existing partition:
> After a partition is deleted and a new one is created, the `Start` value must remain unchanged. Otherwise, data may be lost.
>
```
print
```
The `Start` value in this document is `2048s`, as shown in the following figure.
![](//mccdn.qcloud.com/static/img/67ba54c1d9d63c307d4b8a157b70c722/image.png)

7. Run the following command to delete the existing partition.
```
rm <Partition Number>
```
For example, from the figure above, we see that the cloud disk has one partition whose number is 1. In this case, run the following command:
```
 rm 1
```
The following figure shows the command output.
![](//mccdn.qcloud.com/static/img/3384eeada87ce75695e0e55125109eff/image.png)
8. Run the following command to create a new primary partition:
```
mkpart primary <Start sector of the original partition> 100%
```
Here, 100% indicates this partition goes to the end of the disk.
If the primary partition starts from sector 2048 (it must be the same as that of the previously deleted partition, that is, the `Start` value must be 2048s), run the following command:
```
mkpart primary 2048s 100%
```
If a status appears as shown in the following figure, enter `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
6. Run the following command to check whether the new partition has been created successfully:
```
print
```
If the command output is as shown in the following figure, it indicates that the new partition has been created successfully.
![](//mccdn.qcloud.com/static/img/cb1af5adaf6c89d066077c43fd428a38/image.png)
7. Run the following command to exit the parted tool:
```
quit
```
11. Run the following command to check the extended partition:
```
e2fsck -f <Partition path>
```
If the newly created partition is 1 (that is, the partition path is `/dev/vdb1`), run the following command:
```
e2fsck -f /dev/vdb1
```
The following figure shows the command output.
![](//mccdn.qcloud.com/static/img/307f7a0c98eea05ca1d4560fe4e96f57/image.png)
12. Run the following command to extend the EXT file system in the new partition:
```
resize2fs <Partition path>
```
If the partition path is `/dev/vdb1`, run the following command:
```
resize2fs /dev/vdb1
```
The following figure shows the command output when the expansion is successful.
![](//mccdn.qcloud.com/static/img/57d66da9b5020324703498dbef0b12f9/image.png)
13. Run the following command to extend the XFS file system in the new partition:
```
xfs_growfs <Partition path>
```
If the partition path is `/dev/vdb1`, run the following command:
```
xfs_growfs /dev/vdb1
```
14. Run the following command to manually mount the new partition:
```
mount <Partition path> <Mounting point>
```
If the partition path is `/dev/vdb1` and the mounting point is `/data`, run the following command:
```
mount /dev/vdb1 /data
```
15. Run the following command to view the new partition:
```
df -h
```
The following figure shows the command output when the mounting is successful, that is, you can see the data disk.
![](//mccdn.qcloud.com/static/img/a2bd04c79e8383745689e19033a0daaa/image.png)

<span id="CreateANewGPTPart"></span>
### Formatting the expanded capacity into an independent new partition (GPT)

1. Run the following command as the root user to confirm changes in cloud disk capacity:
 ```
parted <Disk path> print
```
If the disk path is `/dev/vdb`, run the following command:
```
parted /dev/vdb print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the following figure, the cloud disk size is 107 GB after expansion and the size of existing partitions is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)
2. Run the following command to check whether the cloud disk has partitions mounted:
```
mount | grep '<Disk path>' 
```
If the disk path is `/dev/vdb`, run the following command:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Run the following command to unmount the data disk:
```
umount <Mounting point>
```
If the mounting point is `/data`, run the following command:
```
umount /data
```
>? Unmount the file systems from all partitions on the cloud disk, and perform the operations in [Step 4](#step4) again. You can run the following command again to confirm that the file systems have been unmounted from all partitions on the cloud disk:
```
mount | grep '/dev/vdb'
```
The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d1a9a33f0d4e3725aed677f2403c91ae.png)
<span id="Step4"></span>
4. Run the following command to enter the parted partition tool:
```
parted '<Disk path>'
```
If the disk path is `/dev/vdb`, run the following command:
```
parted '/dev/vdb'
```
5. Run the following command to view the partition information and record the `End` value of the existing partition, which will be used as the start offset value of the next partition:
```
print
```
![](//mccdn.qcloud.com/static/img/788ce125bba952f204ed6ee36dfb644d/image.png)
6. Run the following command to create a new primary partition. This partition starts from the end of the existing partition, and covers all the newly added space on the disk.
```
mkpart primary start end
```
If the `End` value is 10.7 GB, run the following command:
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
You can select a file system format such as EXT2 or EXT3.
If the file system is EXT3, run the following command: 
```
mkfs.ext3 /dev/vdb2
```

<span id="AddToTheExistingMBRPart"></span>
### Assigning the expanded capacity to an existing partition (MBR)
The fdisk/e2fsck/resize2fs automatic expansion tools are applicable for the Linux operating system. They are used to add the newly expanded disk space to the existing file system. For successful expansion, the following four requirements must be met:
- The file system is EXT2, EXT3, EXT4, or XFS.
- The current file system does not have any error.
- The disk size after expansion does not exceed 2 TB.
- The current tools only support Python version 2, not Python version 3.


1. Run the following command as the root user to unmount the partition:
```
umount <Mounting point>
```
If the mounting point is `/data`, run the following command:
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
If the disk path is `/dev/vdb` and the file system is `vdb1`, run the following command:
```
python /tmp/devresize.py /dev/vdb
```
![](//mccdn.qcloud.com/static/img/c7617b90578192d64d19f02325f00ffb/image.jpg)
 - If "The filesystem on /dev/vdb1 is now XXXXX blocks long." is output, the expansion is successful. Then, perform [Step 4](#step4MBR).
 - If the output is "[ERROR] - e2fsck failed!!", perform the following steps:
   a. Run the following command to fix the partition where the file system is located:
```
fsck -a <Partition path>
```
If the disk path is `/dev/vdb` and the file system is `vdb1`, run the following command:
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
mount <Partition path> <Mounting point>
```
The mounting point is `/data`.
 - If a partition exists before expansion and the partition path is `/dev/vdb1`, run the following ocmmand:
```
mount /dev/vdb1 /data
```
 - If no partition exists before expansion, run the following command:
```
mount /dev/vdb /data
```
5. Run the following command to view the partition capacity after expansion:
```
df -h
```
The following figure shows the command output when the mounting is successful, that is, you can see the data disk.
![](//mccdn.qcloud.com/static/img/2367f3e70cd0c3c1bef665cc47c1c3bc/image.jpg)
6. Run the following command to view the data information of the original partition after expansion and check whether the newly added storage space has been expanded into the file system.
```
ll /data
```

<span id="CreateANewMBRPart"></span>
### Formatting the expanded capacity into an independent new partition (MBR)
1. Run the following command as a root user to view the partition information of the mounted data disk:
```
df -h
```
![](//mccdn.qcloud.com/static/img/0a450dfaa9cfc7b2c7fdc04861f0e754/image.png)
2. Run the following command to view the information of the data disk without partitions after expansion:
```
fdisk -l
```
![](//mccdn.qcloud.com/static/img/594671a1215dee3036b7940892438f62/image.png)
3. Run the following command to unmount all mounted partitions:
```
umount <Mounting point>
```
If the mounting point is `/data`, run the following command:
```
umount /data
```
>? After all partitions of the cloud disk have been unmounted, perform [Step 4](#Step4MBR) again.
<span id="Step4MBR"></span>
4. Run the following command to create a new partition:
```
fdisk <Disk path>
```
If the disk path is `/dev/xvdc`, run the following command:
```
fdisk /dev/xvdc
```
According to the prompts on the page, sequentially enter `p` (to check the existing partition information), `n` (to create a partition), `p` (to create a primary partition), `2` (to create a second primary partition), press **Enter** twice (to use default configurations), enter `w` (to save the partition table), and start the partition, as shown in the following figure.
![](//mccdn.qcloud.com/static/img/8c35d6f4dfb367e74edc27ce6822c317/image.png)
>? This document takes creating one partition as an example. You can create multiple partitions according to your actual needs.
5. Run the following command to view the new partition:
```
fdisk -l
```
The following figure shows that the new partition xvdc2 has been created.
![](//mccdn.qcloud.com/static/img/e04e924d62317bc2c605c8abaac394f5/image.png)
6. Run the following command to format the new partition and create a file system:
```
mkfs.<fstype> <Partition path> 
```
You can select a file system format such as EXT2 or EXT3.
If the file system is EXT3, run the following command:
```
mkfs.ext3 /dev/xvdc2
```
![](//mccdn.qcloud.com/static/img/074e23eaa580495f96fb532b688d2d68/image.png)
7. Run the following command to create a mounting point:
```
mkdir <New mounting point>
```
If the new mounting point is `/data1`, run the following command:
```
mkdir /data1
```
8. Run the following command to manually mount the new partition:
```
mount <New partition path> <New mounting point>
```
If the new partition path is `/dev/xvdc2` and the new mounting point is `/data1`, run the following command:
```
mount /dev/xvdc2 /data1
```
9. Run the following command to view the information of the new partition:
```
df -h
```
The following figure shows the command output when the mounting is successful, that is, you can see the data disk.
![](//mccdn.qcloud.com/static/img/7b749a4bb6e7c8267c9354e1590c35d4/image.png)
> To allow the CVM to automatically mount a data disk upon restart or start, perform [Step 10](#AddNewPartINFOstep10) and [Step 11](AddNewPartINFOstep11) to add the new partition information to `/etc/fstab`.
10. <span id="AddNewPartINFOstep10"></span>Run the following command to add information:
```
echo '/dev/xvdc2 /data1 ext3 defaults 0 0' >> /etc/fstab
```
11. <span id="AddNewPartINFOstep11"></span>Run the following command to view information:
```
cat /etc/fstab
```
The following figure shows the command output when the partition information is successfully added.
![](//mccdn.qcloud.com/static/img/f0b5c14bf08fd3629ddf6d9b1ae01ffc/image.png)

## Related Actions
- [Extending partitions and file systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
