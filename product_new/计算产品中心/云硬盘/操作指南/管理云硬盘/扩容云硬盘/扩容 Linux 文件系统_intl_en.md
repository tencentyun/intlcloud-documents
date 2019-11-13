## Scenario
Cloud disks are expandable storage devices on the cloud. After you create a cloud disk, you can expand its capacity at any time to increase its storage space without losing any original data.
After [expanding cloud disks](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign the expanded capacity to an existing partition, or format it into an independent new partition.
## Notes

Extending the file system may affect existing data. We strongly recommend that you manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before performing the operation.

## Prerequisites

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
 - If the result indicates that the device has no partition (for example, it only shows /dev/vdb), see [Expanding the file system](#ExpandTheFileSystem).
 - If the result is as shown in the following two figures (which may vary according to the operating system), GPT partition format is used.
![](//mccdn.qcloud.com/static/img/972969e3db92b65311211734690fe763/image.png)
![](//mccdn.qcloud.com/static/img/2c1f4a40279d211a7b81bada7ed38280/image.png)
 - If the result is as shown in the following figure (which may vary according to the operating system), MBR partition format is used.
 > The maximum disk capacity supported by MBR partition format is 2TB. If your disk partition is in MBR format, and you need to expand its capacity to more than 2TB, we recommend you create and mount a new data disk, and copy the data to the new disk using GPT partition format. For Linux operating system, if the disk partition format is GPT, fdisk partition tool can no longer be used, and parted tool must be used.
 >
![](//mccdn.qcloud.com/static/img/4d789ec2865a2895305f47f0513d4e2b/image.png)
2. Follow [Step 1](#fdisk) to view the cloud disk partition format, and select the corresponding operations guide.
<table>
     <tr>
         <th nowrap="nowrap">Partition format</th>  
         <th>Operations guide</th>  
         <th>Description</th>  
     </tr>
		 	 <tr>      
         <td>-</td>   
	     <td nowrap="nowrap"><a href="#ExpandTheFileSystem">Expand the file system</a></td>
	     <td>Applicable to scenarios where a file system is created directly on a bare device without creating a partition.</td>
     </tr>
	 <tr>      
         <td rowspan="2">GPT</td>   
	     <td nowrap="nowrap"><a href="#AddToTheExistingGPTPart">Assign the expanded capacity to an existing partition (GPT)</a></td>
	     <td>Also applicable to scenarios of direct formatting without partitions.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewGPTPart">Format the expanded capacity as an independent new partition (GPT)</a></td> 
	     <td>Can retain the original partition without changes.</td>
     </tr> 
	 <tr>
         <td rowspan="2">MBR</td>   
	     <td><a href="#AddToTheExistingMBRPart">Assign the expanded capacity to an existing partition (MBR)</a></td> 
	     <td>Also applicable to scenarios of direct formatting without partitions.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewMBRPart">Format the expanded capacity as an independent new partition (MBR)</a></td> 
	     <td>Can retain the original partition without changes.</td>
     </tr> 
</table>

<span id="ExpandTheFileSystem"></span>
### Expanding file system

1. According to the file system type, different commands must be executed to perform expansion.
 - For EXT file system, execute the `resize2fs` command to expand the file system.
 - For XFS file system, execute the `xfs_growfs` command to expand the file system.

 Taking `/dev/vdb` as an example, the following command is executed for an EXT file system:
```
resize2fs /dev/vdb
```
Taking `/dev/vdb` as an example, the following command is executed for an XFS file system:
```
xfs_growfs /dev/vdb
```
2. Execute the following command to view the new partition.
```
df -h
```

<span id="AddToTheExistingGPTPart"></span>
### Assigning the expanded capacity to an existing partition (GPT)
1. Run the following command as the root user to confirm changes in cloud disk capacity.
 ```
parted <Disk path> print
 ```
If the disk path is `/dev/vdb`, then execute:
```
parted /dev/vdb print
```
If in the process a message appears as shown in the following image, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the figure below, cloud disk size is 107 GB after expansion and the size of existing partitions is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)

2. Run the following command to check whether the cloud disk has partitions mounted.
```
mount | grep '<Disk path>' 
```
If the disk path is `/dev/vdb`, then execute:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Execute the following command to unmount the data disk.
```
umount <Mounting point>
```
If the mounting point is `/data`, then execute:
```
umount /data
```
>Unmount the file systems of all partitions on the cloud disk, and execute the operations in [Step 4](#step4) again. You can run the following command again to confirm that the file systems of all partitions on the disk have been unmounted.
```
mount | grep '/dev/vdb'
```
![](https://main.qcloudimg.com/raw/9242efdec1aab382ae74f975ca68d68a.png)

<span id="step4"></span>
4. Execute the following command to enter the parted partition tool.
```
parted '<Disk path>'
```
If the disk path is `/dev/vdb`, then execute:
```
parted '/dev/vdb'
```
5. Execute the following command to change the display and operational unit to sector (the default is GB).
```
unit s
```
6. Enter `print` to view the partition information, and note the `Start` value of the existing partition.
> After deleting a partition and creating a new one, the `Start` value must not change. Otherwise, it may cause data loss.

 ![](//mccdn.qcloud.com/static/img/67ba54c1d9d63c307d4b8a157b70c722/image.png)
7. Execute the following command to delete the existing partition.
```
rm <Partition Number>
```
For example, from the figure above, we see that the cloud disk has one partition, with a Number of 1. In this case, execute:
```
 rm 1
```
Returned information is similar to what is shown in the following figure:
![](//mccdn.qcloud.com/static/img/3384eeada87ce75695e0e55125109eff/image.png)
5. Execute the following command to create a new primary partition.
```
mkpart primary <Start sector of the original partition> 100%
```
Here, 100% indicates this partition goes to the end of the disk.
For example, the primary partition starts from sector 2048 (it must be the same as that of the previously deleted partition, that is, the `Start` value must be 2048s). Execute:
```
mkpart primary 2048s 100%
```
If a status appears as shown in the following figure, enter `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
6. Execute the following command to view whether the new partition has been created successfully.
```
print
```
If the returned result is as shown in the following figure, it indicates that the new partition is created successfully.
![](//mccdn.qcloud.com/static/img/cb1af5adaf6c89d066077c43fd428a38/image.png)
7. Execute the following command to exit the parted tool.
```
quit
```
11. Execute the following command to examine the expanded partition.
```
e2fsck -f <Partition path>
```
If the newly created partition is 1 (that is, the partition path is `/dev/vdb1`), then execute:
```
e2fsck -f /dev/vdb1
```
The results are as shown in the following figure.
![](//mccdn.qcloud.com/static/img/307f7a0c98eea05ca1d4560fe4e96f57/image.png)
12. Execute the following command to perform expansion on the EXT file system of the new partition.
```
resize2fs <Partition path>
```
If the partition path is `/dev/vdb1`, then execute:
```
resize2fs /dev/vdb1
```
![](//mccdn.qcloud.com/static/img/57d66da9b5020324703498dbef0b12f9/image.png)
13. Execute the following command to perform expansion on the XFS file system of the new partition.
```
xfs_growfs <Partition path>
```
If the partition path is `/dev/vdb1`, then execute:
```
xfs_growfs /dev/vdb1
```
14. Execute the following command to manually mount the new partition.
```
mount <Partition path> <Mounting point>
```
If the partition path is `/dev/vdb1` and the mounting point is `/data`, then execute:
```
mount /dev/vdb1 /data
```
15. Execute the following command to view the new partition.
```
df -h
```
If the returned information is as shown in the following figure, mounting is successful and you can see the data disk.
![](//mccdn.qcloud.com/static/img/a2bd04c79e8383745689e19033a0daaa/image.png)

<span id="CreateANewGPTPart"></span>
### Formatting the expanded capacity as an independent new partition (GPT)

1. Run the following command as the root user to confirm changes in cloud disk capacity.
 ```
parted <Disk path> print
 ```
If the disk path is `/dev/vdb`, then execute:
```
parted /dev/vdb print
```
If in the process a message appears as shown in the following image, enter `Fix`.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the figure below, cloud disk size is 107 GB after expansion and the size of existing partitions is 10.7 GB.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)
2. Run the following command to check whether the cloud disk has partitions mounted.
```
mount | grep '<Disk path>' 
```
If the disk path is `/dev/vdb`, then execute:
```
mount | grep '/dev/vdb'
```
As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. Execute the following command to unmount the data disk.
```
umount <Mounting point>
```
If the mounting point is `/data`, then execute:
```
umount /data
```
>Unmount the file systems of all partitions on the cloud disk, and execute the operations in [Step 4](#Step4) again. You can run the following command again to confirm that the file systems of all partitions on the disk have been unmounted.
```
mount | grep '/dev/vdb'
```
![](https://main.qcloudimg.com/raw/d1a9a33f0d4e3725aed677f2403c91ae.png)
<span id="Step4"></span>
4. Execute the following command to enter the parted partition tool.
```
parted '<Disk path>'
```
If the disk path is `/dev/vdb`, then execute:
```
parted '/dev/vdb'
```
5. Execute the following command to view the partition information, and note the `End` value of the existing partition, which will be used as the start offset value of the next partition.
```
print
```
![](//mccdn.qcloud.com/static/img/788ce125bba952f204ed6ee36dfb644d/image.png)
6. Run the following command to create a new primary partition. This partition starts at the end of the existing partition, and covers all the newly added space on the disk.
```
mkpart primary start end
```
If the `End` value is 10.7GB, then execute:
```
mkpart primary 10.7GB 100%
```
7. Execute the following command to view whether the new partition has been created successfully.
```
print
```
![](//mccdn.qcloud.com/static/img/fc54fd4c05102ee91c648526d77d1b42/image.png)
8.  Execute the following command to exit the parted tool.
```
quit
```
9. Execute the following command to format the newly created partition.
```
mkfs.<fstype> <Partition path> 
```
You can select the file system format, for example, EXT2, EXT3, etc.
If the file system is EXT3, then execute: 
```
mkfs.ext3 /dev/vdb2
```

<span id="AddToTheExistingMBRPart"></span>
### Assigning the expanded capacity to existing partition (MBR)
The fdisk/e2fsck/resize2fs automatic expansion tools are applicable for the Linux operating system. They are used to add the newly expanded disk space to the existing file system. For expansion to succeed, the following four conditions must be met:
- File system is EXT2/EXT3/EXT4/XFS.
- Current file system does not have any error.
- Disk size after expansion does not exceed 2 TB.
- Current tools only support Python version 2, not Python version 3.


1. Execute the following command as the root user to unmount the partition.
```
umount <Mounting point>
```
If the mounting point is `/data`, then execute:
```
umount /data
```
![](//mccdn.qcloud.com/static/img/c0acc05057941681627a5fd34979d194/image.jpg)
2. Execute the following command to download the tool.
```
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. Execute the following command to use the expansion tool to perform expansion.
```
python /tmp/devresize.py <Disk path>
```
If the disk path is `/dev/vdb` and the file system is `vdb1`, then execute:
```
python /tmp/devresize.py /dev/vdb
```
![](//mccdn.qcloud.com/static/img/c7617b90578192d64d19f02325f00ffb/image.jpg)
 - If “The filesystem on /dev/vdb1 is now XXXXX blocks long.” is returned, the expansion is successful. Execute [Step 4](#step4MBR).
 - If “[ERROR] - e2fsck failed!!” is returned, execute the following steps:
   a. Execute the following command to repair the partition where the file system is located.
```
fsck -a <Partition path>
```
If the disk path is `/dev/vdb` and the file system is `vdb1`, then execute:
```
fsck -a /dev/vdb1
```
    b. After successful repair, execute the following command again to use the expansion tool to perform expansion.
```
python /tmp/devresize.py /dev/vdb
```
<span id="step4MBR"></span>
4. Execute the following command to manually mount the expanded partition.
```
mount <Partition path> <Mounting point>
```
This article takes the mounting point as `/data` as an example.
 - If there is an existing partition before expansion and the partition path is `/dev/vdb1`, then execute:
```
mount /dev/vdb1 /data
```
 - If there is no partition before expansion, execute:
```
mount /dev/vdb /data
```
5. Execute the following command to view the partition capacity after expansion.
```
df -h
```
If the returned information is as shown in the following figure, mounting is successful and you can see the data disk.
![](//mccdn.qcloud.com/static/img/2367f3e70cd0c3c1bef665cc47c1c3bc/image.jpg)
6. Execute the following command to view the data information of the original partition after expansion and confirm whether the newly added storage space has been expanded into the file system.
```
ll /data
```

<span id="CreateANewMBRPart"></span>
### Formatting the expanded capacity as an independent new partition (MBR)
1. Execute the following command as a root user to view the partition information of the mounted data disk.
```
df -h
```
![](//mccdn.qcloud.com/static/img/0a450dfaa9cfc7b2c7fdc04861f0e754/image.png)
2. Execute the following command to view the information of the data disk without partitions after expansion.
```
fdisk -l
```
![](//mccdn.qcloud.com/static/img/594671a1215dee3036b7940892438f62/image.png)
3. Execute the following command to unmount all mounted partitions.
```
umount <Mounting point>
```
If the mounting point is `/data`, then execute:
```
umount /data
```
>After all partitions of the cloud disk have been unmounted, execute [Step 4](#Step4MBR) again.
<span id="Step4MBR"></span>
4. Execute the following command to create a new partition.
```
fdisk <Disk path>
```
If the disk path is `/dev/xvdc`, then execute:
```
fdisk /dev/xvdc
```
According to the interface prompts, sequentially enter `p` (check the existing partition information), `n` (create a new partition), `p` (create a new primary partition), `2`(create a second primary partition), press **Enter** twice (use default configurations), enter `w` (save the partition table), and start the partition. This is shown in the following figure:
![](//mccdn.qcloud.com/static/img/8c35d6f4dfb367e74edc27ce6822c317/image.png)
> This article takes creating one partition as an example. You can create multiple partitions according to your actual needs.
5. Execute the following command to view the new partition.
```
fdisk -l
```
As shown in the following figure, the new partition xvdc2 has been created.
![](//mccdn.qcloud.com/static/img/e04e924d62317bc2c605c8abaac394f5/image.png)
6. Execute the following command to format the new partition and create a file system.
```
mkfs.<fstype> <Partition path> 
```
You can select the file system format, for example, EXT2, EXT3, etc.
If the file system is EXT3, then execute:
```
mkfs.ext3 /dev/xvdc2
```
![](//mccdn.qcloud.com/static/img/074e23eaa580495f96fb532b688d2d68/image.png)
7. Execute the following command to create a new mounting point.
```
mkdir <New mounting point>
```
If the new mounting point is `/data1`, then execute:
```
mkdir /data1
```
8. Execute the following command to manually mount the new partition.
```
mount <New partition path> <New mounting point>
```
If the new partition path is `/dev/xvdc2` and the new mounting point is `/data1`, then execute:
```
mount /dev/xvdc2 /data1
```
9. Execute the following command to view the information of the new partition.
```
df -h
```
If the returned information is as shown in the following figure, mounting is successful and you can see the data disk.
![](//mccdn.qcloud.com/static/img/7b749a4bb6e7c8267c9354e1590c35d4/image.png)

>If you want the cloud disk to be automatically mounted when the CVM restarts or starts up, you must execute [Step 10](#AddNewPartINFOstep10) and [Step 11](#ViewNewPartINFOstep11) to add the new partition information into `/etc/fstab`.

<span id="AddNewPartINFOstep10"></span>
10. Execute the following command to add information.
```
echo '/dev/xvdc2 /data1 ext3 defaults 0 0' >> /etc/fstab
```
<span id="ViewNewPartINFOstep11"></span>
11. Execute the following command to view the information.
```
cat /etc/fstab
```
If the returned information is as shown in the following figure, it means the partition information is added successfully.
![](//mccdn.qcloud.com/static/img/f0b5c14bf08fd3629ddf6d9b1ae01ffc/image.png)

## Related Actions
[Expanding partitions and file systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

