## Overview
This document describes how to troubleshoot the problem of disks being read-only.

## Troubleshooting Approaches
- Check the disk usage to see whether the disk is full.
- Check whether the inode resource of the disk is exhausted (for Linux CVM instances).
- Check whether a disk hardware component is faulty.


## Locating and Troubleshooting the Problem

### Windows CVM instances
Log in to the Windows CVM instance and perform the following operations.

#### Disk is full
1. In the disk properties dialog box, check whether the disk space is exhausted.
![](https://main.qcloudimg.com/raw/291ec4b7c1fc9363961342659d214fd5.png)
2. If the disk space is exhausted, access the disk and delete unnecessary files.
> If the disk is full or files cannot be deleted due to an increase in the business volume, we recommend that you [expand CBS cloud disks](https://intl.cloud.tencent.com/document/product/213/32377). 


#### Hardware failure
 If the failure is caused by a faulty hardware component or other problems, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Linux CVM instances
Log in to the Linux CVM instance and perform the following operations.

#### Disk is full

1. Run the following command to check the disk usage.
```plaintext
df -m
```
2. If the disk usage has reached 100%, access the directory that is already full and run the following command to check the sizes of the files in the directory.
```plaintext
du -f
```
3. Delete unnecessary files to release disk space as needed. You can run the following command to delete unnecessary files. To do this, you need to replace `file_name` with the specific file name. We recommend that you do not delete non third-party files.
 ```plaintext
 rm -rf file_name
 ```
> If the disk is full or files cannot be deleted due to an increase in the business volume, we recommend that you [expand CBS cloud disks](https://intl.cloud.tencent.com/document/product/213/32377). 


 #### The inode resource has been exhausted
 If the disk usage has not reached 100% but the inode resource has been exhausted, it is generally because the generation of many small files exhausted the inode resource.
 1. Run the following command to check the inode usage.
 ```plaintext
 df -i
 ```
![](https://main.qcloudimg.com/raw/f556dff564970157ab2db6eeeed07aa4.png)

2. In Linux, the partition for the root directory is generally small. If small files are periodically generated and not cleared in a timely manner, the inode resource will soon be exhausted. If the inode resource usage has reached 100%, complete the following steps:
i. Run the following command to identify the directory with the largest number of files.
  ```plaintext
	for i in /*; do echo $i; find $i | wc -l; done
  ```
> If the directory is known, replace `/*` with the specific directory.

 ii. More files will consume more inodes. Therefore, access the directory with many files and run the following command to delete unnecessary files. To do this, you need to replace `file_name` with the specific file name. We recommend that you do not delete non third-party files.
   ```plaintext
	 rm -rf file_name
   ```
> If the disk is full or files cannot be deleted due to an increase in the business volume, we recommend that you [expand CBS cloud disks](https://intl.cloud.tencent.com/document/product/213/32377). 


 #### Hardware failure
 If the hardware failure is caused by a faulty hardware component or other problems, [submit a ticket](https://console.cloud.tencent.com/workorder/category).





