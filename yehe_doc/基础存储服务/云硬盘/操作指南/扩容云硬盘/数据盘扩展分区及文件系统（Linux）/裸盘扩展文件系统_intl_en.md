## Overview
This document describes how to extend a file system after logging in to the CVM instance. This method is suitable for scenarios where the file system is directly created without partitioning the cloud disk.

## Directions
1. Run the following command to determine the file system type.
```
df -ihT
```
 - The following result shows an EXT file system.
![](https://main.qcloudimg.com/raw/198ad9bcb209db6ed1934e02f3234f8b.png)
 - The following result shows an XFS file system.
![](https://main.qcloudimg.com/raw/50ecea03c960daa2d04b734226ad69a0.png)
2. Use the file system-specific command to extend the file system.
>?Note the following capacity limits for an EXT file system:
> - EXT3 supports up to 16 TB, and each file cannot exceed 2 TB.
> - EXT4 supports up to 1 EB, and each file cannot exceed 16 TB.
>
 - Run the following command to extend the EXT file system `/dev/vdb`.
```
resize2fs /dev/vdb
```
If the following command output is returned, the expansion is successful.
![](https://main.qcloudimg.com/raw/9f68b0ab1e6446943da4e426df92919b.png)
 - Run the following command to extend the XFS file system `/dev/vdc`.
```
xfs_growfs /dev/vdc
```
If the following command output is returned, the expansion is successful.
![](https://main.qcloudimg.com/raw/56fac50edbb153585adb67b2eb246cf4.png)
3. Run the following command to view the disk space of the file system.
```
df -h
```
