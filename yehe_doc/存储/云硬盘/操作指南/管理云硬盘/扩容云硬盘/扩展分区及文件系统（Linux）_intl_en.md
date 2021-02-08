## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data in it.
After [expanding a cloud disk](https://intl.cloud.tencent.com/document/product/362/5747), you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition.



## Prerequisites
>!Extending the file system may affect the existing data. We strongly recommend you to manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before the operation.
To protect your existing data, you can choose to use the `umount` command to unmount existing partitions and use the `fsck` command to check file systems during the operation.

- You have [expanded the cloud disk capacity](https://cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Linux CVM and created a file system.
- You have [logged in to](https://intl.cloud.tencent.com/document/product/213/5436) the Linux CVM on which you want to extend partitions and the file system.

## Directions
### Confirming the expansion method
<span id="fdisk"></span> 
1. Run the following command as the root user to view the partition format of the cloud disk.
```plaintext
fdisk -l
```
 - If the result indicates that the device has no partition (for example, it only shows /dev/vdb), see [Extending the file system](#ExpandTheFileSystem).
 - If the result is as shown in the following two figures (which may vary according to the operating system), the GPT partition format is used.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - If the result is as shown in the following figure (which may vary according to the operating system), the MBR partition format is used.
 >! MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data. When the GPT partition is used on a Linux CVM, you have to use the parted partition tool, because fdisk will become unavailable.
 >
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2. Follow [Step 1](#fdisk) to view the cloud disk partition format, and select the corresponding operations guide.
<table>
     <tr>
         <th nowrap="nowrap">Partition format</th>  
         <th>Operations guide</th>  
         <th>Notes</th>  
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

1. Run the following command based on the operating system to extend the file system.
 - For an EXT file system, run the `resize2fs` command to extend the file system.
    Taking `/dev/vdb` as an example, run the following command to extend an EXT file system:
```plaintext
resize2fs /dev/vdb
```
 - For an XFS file system, run the `xfs_growfs` command to extend the file system.
	Taking `/dev/vdb` as an example, run the following command to extend an XFS file system:
	```plaintext
	xfs_growfs /dev/vdb
	```
2. Run the following command to view the new partition:
```plaintext
df -h
```

<span id="AddToTheExistingGPTPart"></span> 

### Assigning the expanded capacity to an existing partition (GPT)
1. Run the following command as the root user to confirm changes in cloud disk capacity.
 ```plaintext
parted <Disk path> print
 ```
	Taking the disk path `/dev/vdb` as an example, run the following command:
	```plaintext
	parted /dev/vdb print
	```
	If a message as shown in the following figure appears in the process, enter `Fix`.
	![](https://main.qcloudimg.com/raw/5f15f47bd5ef00b1387a1a93936298ea.png)
	As shown in the following figure, the cloud disk space is 107 GB after expansion and the existing partition capacity is 10.7 GB.
	![](https://main.qcloudimg.com/raw/e8a7487b284622ae617dc17bcadcd68e.png)
2. Run the following command to check whether the cloud disk has partitions mounted:
```plaintext
mount | grep '<Disk path>' 
```
 Taking the disk path `/dev/vdb` as an example, run the following command:
```plaintext
mount | grep '/dev/vdb'
```
 As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](https://mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)

3. Run the following command to unmount the data disk:
```plaintext
umount <Mount point>
```
 Taking the mount point `/data` as an example, run the following command:
```plaintext
umount /data
```
 >? Unmount the file systems from all partitions on the cloud disk, and perform the operations in [Step 4](#step4) again. You can run the following command again to confirm that the unmounting is successful:
```plaintext
mount | grep '/dev/vdb'
```
 The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9242efdec1aab382ae74f975ca68d68a.png)

4. <span id="step4"></span>Run the following command to access the parted tool.
```plaintext
parted '<Disk path>'
```
 Taking the disk path `/dev/vdb` as an example, run the following command:
```plaintext
parted '/dev/vdb'
```
5. Run the following command to change the unit from the default “GB” to “sector” for display and operation:
```plaintext
unit s
```
6. Run the following command to view partitions and record their `Start` values:
>! After a partition is deleted and a new one is created, the `Start` value must remain unchanged. Otherwise, data may be lost.
```plaintext
print
```
 This document uses the `Start` value 2048s as an example.
![](https://mccdn.qcloud.com/static/img/67ba54c1d9d63c307d4b8a157b70c722/image.png)

7. Run the following command to delete the existing partition.
```plaintext
rm <Partition Number>
```
 For example, run the following command to delete the partition “1” from the cloud disk.
```plaintext
 rm 1
```
 The following figure shows the command output.
![](https://mccdn.qcloud.com/static/img/3384eeada87ce75695e0e55125109eff/image.png)

8. Run the following command to create a new primary partition:
```plaintext
mkpart primary <Start sector of the original partition> 100%
```
 The 100% in the command indicates this partition goes to the end of the disk.
Assume that the primary partition starts from sector 2048 (it must be the same as that of the previously deleted partition, that is, the `Start` value must be 2048s), run the following command:
```plaintext
mkpart primary 2048s 100%
```
 If a status as shown in the following figure appears, enter `Ignore`.
![](https://mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)

9. Run the following command to check whether the new partition has been created successfully:
```plaintext
print
```
 If the result as shown in the following figure is returned, the new partition has been created successfully.
![](https://mccdn.qcloud.com/static/img/cb1af5adaf6c89d066077c43fd428a38/image.png)

10. Run the following command to exit the parted tool:
```plaintext
quit
```
11. Run the following command to check the extended partition:
```plaintext
e2fsck -f <Partition path>
```
 Taking the new partition “1” (its partition path is `/dev/vdb1`) as an example, run the following command:
```plaintext
e2fsck -f /dev/vdb1
```
 The following figure shows the command output.
![](https://mccdn.qcloud.com/static/img/307f7a0c98eea05ca1d4560fe4e96f57/image.png)
Extend your file system as follows:
	- For an **EXT file system**:
		1. Run the following command to extend the EXT file system in the new partition:
	```plaintext
	resize2fs <Partition path>
	```
	Taking the partition path `/dev/vdb1` as an example, run the following command:
	​```plaintext
	resize2fs /dev/vdb1
	​	```
	If the result as shown in the following figure is returned, the expansion is successful.
	![](//mccdn.qcloud.com/static/img/57d66da9b5020324703498dbef0b12f9/image.png)
		2. Run the following command to manually mount the new partition:
		```plaintext
		mount <Partition path> <Mount point>
		```
		 Taking the partition path `/dev/vdb1` and the mount point `/data` as an example, run the following command:
		```plaintext
		mount /dev/vdb1 /data
		```

 - For an **XFS file system**
	  1. Run the following command to manually mount the partition:
	```plaintext
	mount <Partition path> <Mount point>
	```
		Taking the partition path `/dev/vdb1` and the mount point `/data` as an example, run the following command:
		```plaintext
		mount /dev/vdb1 /data
		```
	  2. Run the following command to extend the XFS file system in the new partition:
	```plaintext
	xfs_growfs <Partition path>
	```
		Taking the partition path `/dev/vdb1` as an example, run the following command:
		```plaintext
		xfs_growfs /dev/vdb1
		```
12. Run the following command to view the new partition:
```plaintext
df -h
```
 If the result as shown in the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://mccdn.qcloud.com/static/img/a2bd04c79e8383745689e19033a0daaa/image.png)

<span id="CreateANewGPTPart"></span> 
### Formatting the expanded capacity into an independent new partition (GPT)

1. Run the following command as the root user to confirm changes in cloud disk capacity:
 ```plaintext
parted <Disk path> print
 ```
 Taking the disk path `/dev/vdb` as an example, run the following command:
```plaintext
parted /dev/vdb print
```
 If a message as shown in the following figure appears in the process, enter `Fix`.
![](https://mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
As shown in the following figure, the cloud disk space is 107 GB after expansion and the existing partition capacity is 10.7 GB.
![](https://mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)

2. Run the following command to check whether the cloud disk has partitions mounted:
```plaintext
mount | grep '<Disk path>' 
```
 Taking the disk path `/dev/vdb` as an example, run the following command:
```plaintext
mount | grep '/dev/vdb'
```
 As shown in the following figure, the cloud disk has one partition (vdb1) mounted to `/data`.
![](https://mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)

3. Run the following command to unmount the data disk:
```plaintext
umount <Mount point>
```
 Taking the mount point `/data` as an example, run the following command:
```plaintext
umount /data
```
 >? Unmount the file systems from all partitions on the cloud disk, and perform the operations in [Step 4](#Step4) again. You can run the following command again to confirm that the unmounting operation is successful.
```plaintext
mount | grep '/dev/vdb'
```
 The file systems are unmounted from all partitions on the cloud disk, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d1a9a33f0d4e3725aed677f2403c91ae.png)
<span id="Step4"></span> 

4. Run the following command to access the parted partition tool:
```plaintext
parted '<Disk path>'
```
 Taking the disk path `/dev/vdb` as an example, run the following command:
```plaintext
parted '/dev/vdb'
```
5. Run the following command to view partitions and record their `End` values, which will be used as the start offset of the next partition:
```plaintext
print
```
 ![](https://mccdn.qcloud.com/static/img/788ce125bba952f204ed6ee36dfb644d/image.png)
6. Run the following command to create a primary partition. This partition starts at the end of existing partitions, and covers all the new space on the disk.
```plaintext
mkpart primary start end
```
 Taking the `End` value 10.7 GB as an example, run the following command:
```plaintext
mkpart primary 10.7GB 100%
```
7. Run the following command to check whether the new partition has been created successfully:
```plaintext
print
```
 ![](https://mccdn.qcloud.com/static/img/fc54fd4c05102ee91c648526d77d1b42/image.png)
8. Run the following command to exit the parted tool:
```plaintext
quit
```
9. Run the following command to format this new partition:
```plaintext
mkfs.<fstype> <Partition path> 
```
 You can select a file system format such as EXT2 or EXT3.
If you use an EXT3 file system, run the following command: 
```plaintext
mkfs.ext3 /dev/vdb2
```

<span id="AddToTheExistingMBRPart"></span> 
### Assigning the expanded capacity to an existing partition (MBR)
You can use automatic expansion tools including fdisk, e2fsck and resize2fs to add the expanded cloud disk capacity to the existing file system on a Linux CVM. To ensure a successful expansion, the following four requirements must be met:
- The file system is EXT2, EXT3, EXT4, or XFS.
- The current file system does not have any error.
- The disk size after expansion does not exceed 2 TB.
- These tools are only compatible with Python version 2, but not Python version 3.


1. Run the following command as the root user to unmount the partition:
```plaintext
umount <Mount point>
```
 Taking the mount point `/data` as an example, run the following command:
```plaintext
umount /data
```
 ![](https://mccdn.qcloud.com/static/img/c0acc05057941681627a5fd34979d194/image.jpg)
2. Run the following command to download an expansion tool.
    This tool is recommended in the Chinese mainland:
```plaintext
wget -O /tmp/devresize.py https://tencentcloud.coding.net/p/tencentcloud/d/tencentcloud-cbs-tools/git/raw/master/devresize/devresize.py
```
 This tool is recommended in regions outside the Chinese mainland:
```plaintext
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. Run the following command to use the tool for expansion:
```plaintext
python /tmp/devresize.py <Disk path>
```
 Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
```plaintext
python /tmp/devresize.py /dev/vdb
```
 ![](https://mccdn.qcloud.com/static/img/c7617b90578192d64d19f02325f00ffb/image.jpg)
 - If "The filesystem on /dev/vdb1 is now XXXXX blocks long." is output, the expansion is successful. Then, perform [Step 4](#step4MBR).
 - If the output is "[ERROR] - e2fsck failed!!", perform the following steps:
   a. Run the following command to fix the partition where the file system resides.
	```plaintext
	fsck -a <Partition path>
	```
	Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
	```plaintext
	fsck -a /dev/vdb1
	```
    b. After the partition is fixed, run the following command again to use the tool for expansion.
	```plaintext
	python /tmp/devresize.py /dev/vdb
	```
<span id="step4MBR"></span> 
4. Run the following command to manually mount the extended partition:
```plaintext
mount <Partition path> <Mount point>
```
 This document uses the mount point `/data` as an example.
 - If a partition at the partition path `/dev/vdb1` exists before the expansion, run the following command:
```plaintext
mount /dev/vdb1 /data
```
 - If no partition exists before expansion, run the following command:
```plaintext
mount /dev/vdb /data
```
5. Run the following command to view the partition capacity after expansion:
```plaintext
df -h
```
 If the result similar to the following figure is returned, the mount is successful, and you can see the data disk.
![](https://mccdn.qcloud.com/static/img/2367f3e70cd0c3c1bef665cc47c1c3bc/image.jpg)

6. Run the following command to view the original partition data after expansion and check whether the file system is added with expanded storage space.
```plaintext
ll /data
```

<span id="CreateANewMBRPart"></span> 
### Formatting the expanded capacity into an independent new partition (MBR)
1. Run the following command as a root user to view the partition information of the mounted data disk:
```plaintext
df -h
```
 ![](https://mccdn.qcloud.com/static/img/0a450dfaa9cfc7b2c7fdc04861f0e754/image.png)
2. Run the following command to view the information of the data disk without partitions after expansion:
```plaintext
fdisk -l
```
 ![](https://mccdn.qcloud.com/static/img/594671a1215dee3036b7940892438f62/image.png)
3. Run the following command to unmount all mounted partitions:
```plaintext
umount <Mount point>
```
 Taking the mount point `/data` as an example, run the following command:
```plaintext
umount /data
```
 >? Unmount the file systems from all partitions on the cloud disk, and perform the operations in [Step 4](#Step4MBR) again. You can run the following command again to confirm that the unmounting is successful:
```plaintext
mount | grep '<Disk path>'
```
 If the return is null, then all file systems have been unmounted from partitions on the cloud disk.
4. <span id="Step4MBR"></span>Run the following command to create a partition.
```plaintext
fdisk <Disk path>
```
 Taking the disk path `/dev/xvdc` as an example, run the following command:
```plaintext
fdisk /dev/xvdc
```
 When prompted, sequentially enter `p` (to check existing partitions), `n` (to create a partition), `p` (to create a primary partition), `2` (to create the second primary partition), press `Enter` twice (to use the default configuration), enter `w` (to save the partition table), and start the partition, as shown in the following figure:
![](https://mccdn.qcloud.com/static/img/8c35d6f4dfb367e74edc27ce6822c317/image.png)

>? This document takes creating one partition as an example. You can also create multiple partitions as needed.
5. Run the following command to view the new partition:
```plaintext
fdisk -l
```
 The following figure shows that the new partition xvdc2 has been created.
![](https://mccdn.qcloud.com/static/img/e04e924d62317bc2c605c8abaac394f5/image.png)

6. Run the following command to format the new partition and create a file system:
```plaintext
mkfs.<fstype> <Partition path> 
```
 You can select a file system format such as EXT2 or EXT3.
If you use an EXT3 file system, run the following command:

```plaintext
mkfs.ext3 /dev/xvdc2
```
 ![](https://mccdn.qcloud.com/static/img/074e23eaa580495f96fb532b688d2d68/image.png)
7. Run the following command to create a mount point:
```plaintext
mkdir <New mounting point>
```
 Taking the new mount point `/data1` as an example, run the following command:
```plaintext
mkdir /data1
```
8. Run the following command to manually mount the new partition:
```plaintext
mount <New partition path> <New mount point>
```
 Taking the new partition path `/dev/xvdc2` and the new mount point `/data1` as an example, run the following command:
```plaintext
mount /dev/xvdc2 /data1
```
9. Run the following command to view the new partition:
```plaintext
df -h
```
 If the result as shown in the following figure is returned, the mounting is successful, and you can see the data disk.
 ![](https://mccdn.qcloud.com/static/img/7b749a4bb6e7c8267c9354e1590c35d4/image.png)

>? To allow the CVM to automatically mount a data disk upon restart or start, perform [Step 10](#AddNewPartINFOstep10) and [Step 11](#AddNewPartINFOstep11) to add the new partition to `/etc/fstab`.
10. <span id="AddNewPartINFOstep10"></span>Run the following command to add the partition:
```plaintext
echo '/dev/xvdc2 /data1 ext3 defaults 0 0' >> /etc/fstab
```
11. <span id="AddNewPartINFOstep11"></span>Run the following command to view the partition:
```plaintext
cat /etc/fstab
```
 If the result as shown in the following figure is returned, the partition has been successfully added.
![](https://mccdn.qcloud.com/static/img/f0b5c14bf08fd3629ddf6d9b1ae01ffc/image.png)

## Relevant Operations
[Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## FAQs
If you encounter a problem when using Tencent Cloud CBS, refer to the following documents for troubleshooting as needed:
- [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409)
- [Features FAQs](https://intl.cloud.tencent.com/document/product/362/32408)
