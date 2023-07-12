## Overview
If your cloud disk has a GPT partition that contains the file system, you can use either of the following methods to extend partitions and file systems:
- [Assigning the expanded capacity to an existing GPT partition](#Add)
- [Formatting the expanded capacity into an independent new GPT partition](#New)



## Prerequisite
You can use automatic expansion tools including e2fsck and resize2fs to add the expanded cloud disk capacity to the existing file system on a Linux CVM. To ensure a successful expansion, the following requirements must be met:
- The way to expand and partition has been confirmed. For more information, see [Determining the Expansion Method](https://intl.cloud.tencent.com/document/product/362/39995).
- The file system is EXT or XFS.
- The current file system does not have any error.


## Directions

[](id:Add)
### Assigning the expanded capacity to an existing GPT partition
1. Run the following command as the root user to confirm changes in cloud disk capacity.
```shellsession
parted <Disk path> print
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
parted /dev/vdc print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](https://main.qcloudimg.com/raw/bdc9f2fcb281e24ec5799e73c08535eb.png)
The cloud disk size is 2,040 GB after expansion and the existing partition capacity is 10.7 GB, as shown in the following figure:
![](https://main.qcloudimg.com/raw/40a1141f65ba7ac15b8dac4b94e0d6a5.png)
2. Run the following command to check whether the cloud disk has partitions mounted.
```shellsession
mount | grep '<Disk path>' 
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
mount | grep '/dev/vdc'
```
 - The following result indicates that the cloud disk has one partition (vdc1) mounted to `/data`.
![](https://main.qcloudimg.com/raw/61ae197d19c522f6ebd1e9c7bf4b4d88.png)
Run the following command to unmount **all partitions** from the cloud disk.
```shellsession
umount <Mount point>
```
Taking the mount point `/data` as an example, run the following command:
```shellsession
umount /data
```
 - The following result indicates that there is no partition mounted. Proceed to the next step.
![](https://main.qcloudimg.com/raw/4a6d070830fd0629a336836fd6b4c1fd.png)
3. Run the following command to use the parted partition tool.
```shellsession
parted <Disk path>
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
parted /dev/vdc
```
4. Run the following command to change the unit from the default "GB" to "sector" for display and operation.
```shellsession
unit s
```
5. [](id:step5)Run the following command to view partitions and record their `Start` values.
```shellsession
print
```
>! Do record `Start` values. After a partition is deleted and a new one is created, the `Start` value must remain unchanged. Otherwise, data may be lost.
>
![](https://main.qcloudimg.com/raw/a4b3b6710d2d03549c26b8efd7d844db.png)
6. Run the following command to delete the existing partition.
```shellsession
rm <Partition Number>
```
For example, run the following command to delete the partition "1" from the cloud disk.
```shellsession
rm 1
```
7. Run the following command to confirm the deletion. The returned information is as shown below:
```shellsession
print
```
![](https://main.qcloudimg.com/raw/fbac9760d06da56e3f3be3a61309cc10.png)
>!You can immediately run the `rescue` command, and enter `Start` and `End` values as prompted to restore a partition being accidentally deleted.
>
8. Run the following command to create a new primary partition.
```shellsession
mkpart primary <Start sector of the original partition> 100%
```
The 100% in the command indicates this partition goes to the end of the disk. Enter the `Start` value obtained in [step 5](#step5). In this document, the start sector of the original partition is 2048s (that is, the `Start` value is 2048s), run the following command:
```shellsession
mkpart primary 2048s 100%
```
If a status as shown in the following figure appears, enter `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
9. Run the following command to check whether the new partition has been created successfully.
```shellsession
print
```
If the result as shown in the following figure is returned, the new partition has been created successfully.
![](https://main.qcloudimg.com/raw/823646dcfd0e42ece63a37338e0d4e16.png)
10. Run the following command to close the parted tool.
```shellsession
quit
```
11. Run the following command to sync the partition table to the operating system.
```shellsession
partprobe
```
12. Run the following command to check the extended partition.
```shellsession
e2fsck -f <Partition path>
```
Taking the new partition "1" (its partition path is `/dev/vdc1`) as an example, run the following command:
```shellsession
e2fsck -f /dev/vdc1
```
The following figure shows the command output.
![](https://main.qcloudimg.com/raw/12c917c78829014cd784e3f184c01eed.png)
13. Use a file system-specific command to resize each file system on the new partition.
 - Run the following command on the **EXT file system**.
```shellsession
resize2fs <Partition path>
```
Taking the partition path `/dev/vdc1 as an example, run the following command:
```shellsession
resize2fs /dev/vdc1
```
If the result as shown in the following figure is returned, the expansion is successful.
![](https://main.qcloudimg.com/raw/7daebff27ce10c66b63c2b35c9712418.png)
 - Run the following command on the **XFS file system**.
```shellsession
xfs_growfs <Partition path>
```
Taking the partition path `/dev/vdc1` as an example, run the following command:
```shellsession
xfs_growfs /dev/vdc1
```
14. Run the following command to manually mount the new partition:
```shellsession
mount <Partition path> <Mount point>
```
Taking the partition path `/dev/vdc1` and the mount point `/data` as an example, run the following command:
```shellsession
mount /dev/vdc1 /data
```
15. Run the following command to view the new partition:
```shellsession
df -h
```
If the result as shown in the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://main.qcloudimg.com/raw/476829f5a9cb6aef62f3cace31cb2586.png)


[](id:New)
### Formatting the expanded capacity into an independent new GPT partition
1. Run the following command as the root user to confirm changes in cloud disk capacity.
```shellsession
parted <Disk path> print
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
parted /dev/vdc print
```
If a message as shown in the following figure appears in the process, enter `Fix`.
![](https://main.qcloudimg.com/raw/c69cd8b3741675f1a96715c4679ce6e6.png)
The cloud disk size is 2,147 GB after expansion and the existing partition capacity is 2,040 GB, as shown in the following figure.
![](https://main.qcloudimg.com/raw/8d8e72b1a5716443673453f67c1d798d.png)
2. Run the following command to check whether the cloud disk has partitions mounted.
```shellsession
mount | grep '<Disk path>' 
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
mount | grep '/dev/vdc'
```
 - The following result indicates that the cloud disk has one partition (vdc1) mounted to `/data`.
![](https://main.qcloudimg.com/raw/1703f6594a1fbff86dd1d1dfb2ab124d.png)
Run the following command to unmount **all partitions** from the cloud disk.
```shellsession
umount <Mount point>
```
Taking the mount point `/data` as an example, run the following command:
```shellsession
umount /data
```
 - The following result indicates that there is no partition mounted. Proceed to the next step.
![](https://main.qcloudimg.com/raw/d10d74c1fff5e8ffdb306d5acb664ae1.png)
3. Run the following command to use the parted partition tool.
```shellsession
parted '<Disk path>'
```
Taking the disk path `/dev/vdc` as an example, run the following command:
```shellsession
parted '/dev/vdc'
```
4. [](id:Step4)Run the following command to view partitions and record their `End` values, which will be used as the start offset of the next partition.
```shellsession
print
```
![](https://main.qcloudimg.com/raw/7f11b89e481035897d525fa8a93cb7e7.png)
5. Run the following command to create a primary partition. This partition starts at the end of existing partitions, and covers all the new space on the disk.
```shellsession
mkpart primary start end
```
Obtain the `End` value in [step 4](#Step4). In this example, the `End` value is 2,040 GB, run the following command:
```shellsession
mkpart primary 2040GB 100%
```
6. Run the following command to check whether the new partition has been created.
```shellsession
print
```
If the following output is returned, the partition has been created.
![](https://main.qcloudimg.com/raw/5e1418caaddf22932ac624ff906cf302.png)
7. Run the following command to close the parted tool.
```shellsession
quit
```
8. Run the following command to format the new partition into EXT2, EXT3, etc. as needed.
```shellsession
mkfs.<fstype> <Partition path> 
```
Taking EXT4 as an example, run the following command: 
```shellsession
mkfs.ext4 /dev/vdc2
```
9. Run the following command to manually mount the new partition.
```shellsession
mount <Partition path> <Mount point>
```
Taking the partition path `/dev/vdc2` and the mount point `/data` as an example, run the following command:
```shellsession
mount /dev/vdc2 /data
```
10. Run the following command to view the new partition.
```shellsession
df -h
```
If the result as shown in the following figure is returned, the mounting is successful, and you can see the data disk.
![](https://main.qcloudimg.com/raw/cd9d36d49388882f0cb898c13d565bb0.png)

## References
[Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## FAQs
If you encounter a problem when using Tencent Cloud CBS, refer to the following documents for troubleshooting as needed:
- [Usage FAQs](https://intl.cloud.tencent.com/document/product/362/32409)
- [Features FAQs](https://cloud.tencent.com/document/product/362/17818)


