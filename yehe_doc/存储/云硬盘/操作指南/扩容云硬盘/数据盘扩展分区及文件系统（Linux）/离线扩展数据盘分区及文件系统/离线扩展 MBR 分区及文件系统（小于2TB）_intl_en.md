## Overview
If your cloud disk has a MBR partition that contains the file system, with a disk size of less than 2 TB after expansion, you can use either of the following methods to extend partitions and file systems:
- [Assigning the expanded capacity to an existing MBR partition](#Add)
- [Formatting the expanded capacity into an independent new MBR partition](#New)


## Prerequisite
You can use automatic expansion tools including fdisk, e2fsck and resize2fs to add the expanded cloud disk capacity to the existing file system on a Linux CVM. To ensure a successful expansion, the following requirements must be met:
- The way to expand and partition has been confirmed. For more information, see [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).
- The file system is EXT2, EXT3, EXT4, or XFS.
- The current file system does not have any error.
- The disk size after expansion does not exceed 2 TB.
- Only use Python version 2 because of compatibility with expansion tools in this document.



## Directions

[](id:Add)
### Assigning the expanded capacity to an existing MBR partition
Run the following command as the root user to query partitions of the cloud disk.
```
lsblk
```
 - The following output indicates there is only one partition. In this case, you can perform the [automatic expansion](#AutomaticExpansion) using tools.
 ![](https://main.qcloudimg.com/raw/297d678489b57dd70171a8882c9416f4.png)
 - The following output indicates there are two partitions: `vdb1` and `vdb2`. In this case, you need to choose a partition to be extended as instructed in [manual expansion](#ManualExpansion).
![](https://main.qcloudimg.com/raw/070f2144acc543c84d4ab8ab3db25620.png)

<dx-tabs>
::: Automatic Expansion [](id:AutomaticExpansion)


<dx-alert infotype="explain" title="">
This method is only applicable to the scenario where there is only one partition. If you have two or more partitions, choose [manual expansion](#ManualExpansion).
</dx-alert>


1. Run the following command as the root user to unmount the partition.
```shellsession
umount <Mount point>
```Taking the mount point `/data` as an example, run the following command:
```shellsession
umount /data
```
2. Run the following command to download an expansion tool.
```shellsession
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. Run the following command to use the tool for expansion.
```shellsession
python /tmp/devresize.py <Disk path>
```Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
```shellsession
python /tmp/devresize.py /dev/vdb
```
 - If `The filesystem on /dev/vdb1 is now XXXXX blocks long.` is output as follows, the expansion is successful. Then, perform [step 4](#step4MBR).
![](https://main.qcloudimg.com/raw/689209e1d1f8a227274e8e65be07d2ec.png)
 - If `[ERROR] - e2fsck failed!!` is output, perform the following steps:
   a. Run the following command to fix the partition where the file system resides.
```shellsession
fsck -a <Partition path>
```Taking the disk path `/dev/vdb` and the file system `vdb1` as an example, run the following command:
```shellsession
fsck -a /dev/vdb1
```b. After the partition is fixed, run the following command again to use the tool for expansion.
```shellsession
python /tmp/devresize.py /dev/vdb
```
4. [](id:step4MBR)Run the following command to manually mount the extended partition. This document uses the mount point `/data` as an example.
```shellsession
mount <Partition path> <Mount point>
- If a partition at the partition path `/dev/vdb1` exists before expansion, run the following command:
```shellsession
mount /dev/vdb1 /data
```
5. Run the following command to view the partition capacity after expansion.
```shellsession
df -h
If the result similar to the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
6. Run the following command to view the data information of the original partition after expansion and check whether the new storage space has been added to the file system.
```shellsession
ll /data
```
:::
::: Manual Expansion[](id:ManualExpansion)
1. Run the following command as the root user to unmount the partition.
```shellsession
umount <Mount point>
```Taking the mount point `/data` as an example, run the following command:
```shellsession
umount /data
```
2. Run the following command to extend the `vdb2` partition. Replace `vdb2` with your actual partition when using the command. 
```shellsession
growpart /dev/vdb 2
```
3. Run the following command to extend the file system of the partition.
```shellsession
resize2fs /dev/vdb2
```If the following output is returned, the file system has been extended.
![](https://main.qcloudimg.com/raw/ba8d2693823a3eb0ccfc4dd097f09ed5.png)
4. [](id:step4MBR)Run the following command to manually mount the extended partition. This document uses the mount point `/data` as an example.
```shellsession
mount <Partition path> <Mount point>
```If a partition at the partition path `/dev/vdb2` exists before expansion, run the following command:
```shellsession
mount /dev/vdb2 /data
```
5. Run the following command to view the partition capacity after expansion.
```shellsession
df -h
```If the result similar to the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://main.qcloudimg.com/raw/92cd4cc0e9b1c08975603f73e922266f.png)
6. Run the following command to view the data information of the original partition after expansion and check whether the new storage space has been added to the file system.
```shellsession
ll /data
```
:::
</dx-tabs>


[](id:New)
### Formatting the expanded capacity into an independent new MBR partition
1. Run the following command as the root user to view the mounted partition of the data disk.
```shellsession
df -h
```
As shown in the following figure, the mounted partition of the data disk is 20 GB.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
2. Run the following command to view the data disk that has no partition after expansion:
```shellsession
fdisk -l
```
As shown in the following figure, the data disk has been expanded to 30 GB.
![](https://main.qcloudimg.com/raw/f21420374b4334a790022c95bac1fe0f.png)
3. Run the following command to unmount all mounted partitions.
```shellsession
umount <Mount point>
```
Taking the mount point `/data` as an example, run the following command:
```shellsession
umount /data
```
<dx-alert infotype="explain" title="">
After all the partitions of the cloud disk are unmounted, perform [step 4](#Step4MBR) again.
</dx-alert>

4. [](id:Step4MBR)Run the following command to create a partition.
```shellsession
fdisk <Disk path>
```
Taking the disk path `/dev/vdb` as an example, run the following command:
```shellsession
fdisk /dev/vdb
```
Perform the following steps in sequence when prompted.
 1. Enter **p** to check existing partitions, such as `/dev/vdb1` in this document.
 2. Enter **n** to create a partition.
 3. Enter **p** to create a primary partition.
 4. Enter **2** to create the second primary partition.
 5. Press **Enter** twice to use the default partition size.
 6. Enter **w** to save the partition table and start partitioning.
 See below:
![](https://main.qcloudimg.com/raw/894ba5a11a73d56a0a165ee7cb49e7c6.png)
<dx-alert infotype="explain" title="">
This document takes creating one partition as an example. You can also create multiple partitions as needed.
</dx-alert>



5. Run the following command to view the new partition.
```shellsession
fdisk -l
```
The following figure shows that the new partition `vdb2` has been created.
![](https://main.qcloudimg.com/raw/d604d00955d0db5f052e964ecd409cc3.png)

6. Run the following command to format the new partition and create a file system in a desired format, such as EXT2 or EXT3.
```shellsession
mkfs.<fstype> <Partition path> 
```
Taking EXT4 as an example, run the following command:
```shellsession
mkfs.ext4 /dev/vdb2
```
The following figure shows the successful creation of the EXT4 file system.
![](https://main.qcloudimg.com/raw/db15ed11252e6db8adb706f61ed14225.png)

7. Run the following command to create a mount point.
```shellsession
mkdir <New mount point>
```
Taking the new mount point `/data1` as an example, run the following command:
```shellsession
mkdir /data1
```
8. Run the following command to manually mount the new partition.
```shellsession
mount <New partition path> <New mount point>
```
Taking the new partition path `/dev/vdb2` and the new mount point `/data1` as an example, run the following command:
```shellsession
mount /dev/vdb2 /data1
```
9. Run the following command to view the new partition.
```shellsession
df -h
```
If the result as shown in the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://main.qcloudimg.com/raw/465c988014acc85957078335d776bfc3.png)
<dx-alert infotype="explain" title="">
To allow the CVM instance to automatically mount a data disk upon restart or startup, perform [step 10](#AddNewPartINFOstep10) and [step 11](#AddNewPartINFOstep11) to add the new partition information to `/etc/fstab`.
</dx-alert>

10. [](id:AddNewPartINFOstep10)Run the following command to add the partition.
```shellsession
echo '/dev/vdb2 /data1 ext4 defaults 0 0' >> /etc/fstab
```

11. [](id:AddNewPartINFOstep11)Run the following command to view the partition.
```shellsession
cat /etc/fstab
```
If the result as shown in the following figure is returned, the partition has been successfully added.
![](https://main.qcloudimg.com/raw/761a846bafe385b24dfb322a6ad2977f.png)

## References
[Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## FAQs
If you encounter a problem when using Tencent Cloud CBS, refer to the following documents for troubleshooting as needed:
- [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409)
- [Features FAQs](https://intl.cloud.tencent.com/document/product/362/32408)
